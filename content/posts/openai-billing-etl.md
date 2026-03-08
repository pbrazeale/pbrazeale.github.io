+++
tags = ['AI', 'LLM', 'Shell', 'SQL']
title = 'Building a Production-Ready OpenAI Billing and Usage ETL Pipeline'
date = 2026-03-08T10:00:00-06:00
draft = false
+++

_(From raw Admin API pages to reliable cost analytics; with idempotency, watermarks, retries, and a real runbook.)_

## Summary

I built a daily **ETL (Extract, Transform, Load)** pipeline that ingests **OpenAI organization** billing and usage data and turns it into analytics-ready fact tables.

### The core idea is simple:

- **Capture raw API pages** as immutable evidence (for audit/replay/debugging).
- **Normalize typed facts** for fast querying and trend analysis.
- **Upsert idempotently** so reruns are safe.
- **Advance incremental watermarks** so daily runs are quick; but still recover cleanly from partial failures.
- Wrap it all in operational guardrails: **retries, pagination correctness, scheduler integration, alerting, retention policy, and testing**.

This post walks end-to-end through the architecture, data model, reliability systems, and the migration hardening work that turned a “works on my machine” script into something that runs unattended every day in production.

---

## Why This Pipeline Exists

### The Problem Statement

I needed a repeatable **daily ingestion process** for OpenAI org-level usage and costs.

And I needed _two things at once_:

1. **Forensic fidelity**  
   Store full raw Admin API page responses (and request context) so I can replay, audit, and debug any number I report.

2. **Reporting performance**  
   Store typed, normalized facts so Business Intelligence queries don’t require re-parsing JSON blobs at read time.

Also: reruns must be safe; failures must be recoverable; and an operator (often: future-me) should be able to run it without spelunking through code.

### Goals

- Daily repeatable ingestion for OpenAI organization usage + costs.
- Raw-page evidence retained for audit/replay.
- Normalized fact tables for fast analytics.
- Idempotent upserts.
- Incremental windowing + watermarking for recovery after partial failures.
- Operator-friendly: schedules cleanly; logs cleanly; alerts reliably; documented runbook.

---

## What's Ingest

### Endpoints Ingested

#### Costs

- `/organization/costs`

#### Usage

- `/organization/usage/completions`
- `/organization/usage/embeddings`
- `/organization/usage/moderations`
- `/organization/usage/images`
- `/organization/usage/audio_speeches`
- `/organization/usage/audio_transcriptions`
- `/organization/usage/vector_stores`
- `/organization/usage/code_interpreter_sessions`

_(Yes, it’s a lot; but the whole point is organization-level coverage—so we can actually trust the totals.)_

### Metrics & Dimensions Captured

#### Measures:

- token counts, request counts
- image counts / sizes
- characters, seconds, bytes
- session counts
- monetary amounts (for costs and line items)

#### Dimensions:

- project, user, API key
- model
- batch
- service tier
- size, source
- line item

The group-by strategy is intentionally **maximal** per endpoint (_within reason_); I’d rather preserve the highest granularity available and aggregate later than throw away detail and regret it.

---

## How the Pipeline Works

### High-level Flow

#### At a 10,000-foot view:

1. Fetch from OpenAI Admin API
2. Paginate until exhaustion
3. Persist raw pages _immediately_
4. Normalize buckets/results into typed facts
5. Upsert facts using deterministic fingerprints
6. Update watermarks
7. Write run metadata (`success | partial_success | failed`)
8. Alert on the outcome (SES preferred; SMTP fallback)

### Core Components

#### API client

- Authorization headers
- Configurable timeout
- Retry policy with exponential backoff + jitter (especially for 429 and 5xx)

#### Paginator

- Driven by `has_more` and `next_page`
- Persists each page before transforming

#### Raw page sink

- Table: `etl_api_pages_raw`
- Stores request params, response payload, pagination context, timestamps

#### Transform layer

- Normalizes “bucket/result” patterns across endpoints into a consistent usage fact schema

#### Upsert layer

- Deterministic `row_fingerprint` per logical record
- `INSERT ... ON CONFLICT(row_fingerprint) DO UPDATE` behavior (or equivalent)

#### Watermark manager

- Tracks incremental cursor state per endpoint
- Supports selectable consistency mode

#### Alert manager

- `EMAIL_PROVIDER=auto|ses|smtp`
- SES (Simple Email Service) preferred; SMTP fallback for portability/testing

---

## Data Model & Storage Design

### Design principle: hybrid storage

- **Raw, immutable page-level evidence** for audit/replay
- **Typed fact rows** for fast querying and dashboards

You don’t want to choose between “auditability” and “queryability”; you want both.

### Tables Implemented

#### `etl_runs`

- Run lifecycle (start/end), status, metadata, error/warning counters, environment snapshot (sanitized)

#### `etl_api_pages_raw`

- Request/response evidence with pagination context (endpoint, window, page token, payload, timestamps)

#### `etl_watermarks`

- Incremental cursor state per endpoint (last successful `end_time`, plus mode metadata)

#### `fact_openai_usage`

- Normalized usage across all usage endpoints (measures + dimensions + bucket window)

#### `fact_openai_costs`

- Normalized costs for billing amounts and line items

### Views Implemented

#### `vw_ingestion_daily_summary`

- Daily per-endpoint row volumes (spot anomalies quickly)

#### `vw_last_etl_run`

- Latest run status snapshot (the first thing an operator checks)

### Integrity & Performance

- **Unique `row_fingerprint`** on fact tables (idempotency)
- **Check constraints** (non-negative metrics/costs; bucket time sanity; currency consistency where applicable)
- **Indexes**
  - Endpoint + bucket time (the core query pattern)
  - Common reporting dims (project/model/user where present)

---

## Idempotency Strategy

### Deterministic Fingerprints

Each logical fact row gets a deterministic fingerprint hash built from:

- endpoint name (e.g., `usage/completions`)
- bucket window (start/end time; UTC)
- dimensional keys (project, model, user, key, tier, etc.)
- any endpoint-specific grouping keys (size/source/line item)

A typical approach:

- canonicalize a dictionary of key fields
- serialize in a stable way (sorted keys; explicit null handling)
- hash (e.g., SHA-256)
- store as `row_fingerprint`

Then your upsert becomes:

- If the same logical record appears again (rerun, overlap window, late data), it updates in place.
- No duplicates; no double-counting; no “I guess we’ll delete yesterday and try again.”

**Daily overlap reprocessing is safe and expected**—I _want_ overlaps (they absorb late-arriving corrections), but only if idempotency makes overlaps harmless.

---

## Incremental Loading & Recovery

### Windowing Model

Everything is UTC-based:

- inclusive `start_time`
- exclusive `end_time`

Config knobs:

- `BACKFILL_DAYS` for initial history load
- `REPROCESS_DAYS` for daily overlap

### Watermark Modes

I support two watermark consistency modes:

1. **`endpoint` mode**
   - Each endpoint advances its watermark independently after it succeeds.
     - Pros: faster partial progress; a single flaky endpoint doesn’t block everyone else.
     - Cons: cross-endpoint comparisons can be temporarily misaligned.
2. **`run` mode**
   - Watermarks only advance when the whole run succeeds.
     - Pros: stronger global consistency.
     - Cons: a single endpoint failure stalls progress for everything.

### Partial Failure Behavior

- Endpoint failures are isolated.
- Overall run status becomes `partial_success` when some endpoints succeed and some fail.
- Failed endpoints do **not** advance their watermark.
- Raw pages for successful endpoints remain stored (even during partial runs), which is huge for recovery and debugging.

---

## Operating it Reliably

### API Robustness

Reliability here means:

- retry on **429 (rate limit)** and **5xx (server errors)**
- retry on network timeouts/transient errors
- exponential backoff + jitter
- configurable max retries and timeout

The point isn’t “never fail”; the point is “fail _predictably_ and recover cleanly.”

### Pagination

Pagination is one of those things that “kind of works” until it silently drops data.

So the pipeline does:

- fetch page
- persist raw page (with token context)
- if `has_more`, continue with `next_page`
- repeat until exhausted

Because raw persistence happens per-page _before transforms_, a mid-run crash doesn’t destroy evidence; you can replay from raw or rerun safely.

### Lessons Learned

A few real-world constraints that shaped the implementation:

- API page limits can vary by bucket width (for example: `1d` capped at 31).
- Runtime defaults + environment tuning must prevent invalid limit requests.
- Failure logs are not trash; they’re design inputs.
  - I preserved failure logs and used them to add guardrails (limit clamping, better parameter validation, clearer runbook guidance).

---

## Retention, Auditability, and Governance

### Raw Retention Policy

Raw pages can grow quickly, so retention is explicit:

- `RAW_PAGE_RETENTION_DAYS` (default 90)
- facts + run history remain long-lived (in the current design)

### Why?

- provenance (what did the API say, exactly?)
- debugging (why did costs jump; which dimension changed?)
- replay (re-derive facts with improved transforms)
- forward-compatible derivations (new metrics later; old evidence still usable)

### Why Purge Raw Pages

- database growth control
- reduced retention of potentially sensitive metadata

---

## Alerting & Notifications

### Provider Model

Alerts support:

- `EMAIL_PROVIDER=auto|ses|smtp`
- SES (Simple Email Service) is the preferred path
- SMTP fallback exists for portability

### Alert Semantics

- Alert on `partial_success` and `failed`
- Optional warning-only success alerts: `ALERT_ON_WARNING=true`
- Optional success summaries: `ALERT_ON_SUCCESS=true`

This matters because “always email on success” can become noise; but “never email unless disaster” can hide slow degradation. The config lets you choose.

### Transport hardening

- SES requires credential and identity validation
- SMTP security modes: `starttls`, `ssl`, `none`
- Logging explicitly avoids credential material

---

## Operations

### Daily Run Commands

I like a small CLI obvious intent:

- Standard daily run  
  `python -m openai_billing_etl run`
- One-day manual rerun  
  `python -m openai_billing_etl run --start 2026-02-18 --end 2026-02-19`
- Backfill  
  `python -m openai_billing_etl backfill --days 90`
- Dry-run (no writes)  
  `python -m openai_billing_etl run --dry-run`
- Endpoint isolation  
  `python -m openai_billing_etl run --only usage/completions`

### Windows Scheduler Integration

The scheduler wrapper does a few boring-but-critical things:

- activates the virtual environment
- validates required environment variables
- executes ETL
- writes timestamped logs to disk
- returns meaningful exit codes
- enforces single-instance execution

### Operator Checks

- Verify latest run status (`vw_last_etl_run`)
- Verify daily volume patterns (`vw_ingestion_daily_summary`)
- Verify alert channel health
- Spot-check costs for anomalies

---

## Data Quality Systems

### SQL Validation

Typical validations include:

- latest run status query
- daily endpoint volume checks
- duplicate fingerprint checks
- null bucket checks
- watermark freshness
- currency consistency
- raw retention age check

### Embedded Validation During ETL

During transforms/upserts:

- zero-row windows and integrity anomalies raise warnings
  - warning-only runs can optionally alert (configurable)

**The goal is “detect surprises early.”**

+++
tags = ['AI', 'LLM', 'SQL', 'Build Notes', 'Docker']
title = 'Building the AI Operations Backbone'
date = 2026-03-07T13:00:00-06:00
draft = false
+++

# Building the AI Operations Backbone

Raw agent activity is throwing darts blind, without a system to capture, normalize, and surface metrics. Here's the architecture we built at [World Parts Direct](https://worldpartsdirect.com) to turn n8n workflow completions into measurable, auditable AI performance data, and why every decision in the stack was deliberate.

## The Problem

Before building this, operating our AI agents felt like flying blind. We had multiple workflows running across different use cases, but we had no consistent way to compare how they were performing.

- Was one agent slower than another?
- Were failures clustering around a specific node type?
- Was a prompt change last Tuesday responsible for the reliability dip this week?

We couldn’t answer those questions reliably because we weren’t tracking the right data. Reporting was inconsistent, our BI (business intelligence) was shaky; management couldn’t plan investments or prioritize the right AI work.

Three problems kept surfacing:

- **Agent behavior was incomparable.** Each workflow had its own ad-hoc logging (or none at all). Spotting a regression meant manually digging through execution histories.
- **Prompt changes had no audit trail.** Someone would tweak a system prompt, redeploy, and we'd have no structured record of what changed, when, or what effect it had.
- **Management reporting was manual and inconsistent.** Every time leadership asked for an update on AI reliability or cost, someone had to stitch together numbers from different sources and hope they matched last week's version.

What we needed was better tools and operations discipline. A durable data backbone that captured every meaningful event from every agent run, and an API layer that could turn that data into consistent, trustworthy reporting. Ideally centralized on a dashboard for management to use themselves instead vibe trusting the AI department.

## The Stack

### n8n as the Execution Layer

We were already running n8n for workflow automation. Rather than building a separate orchestration layer, we extended what we had.

The key design choice was **completion-based webhook ingestion**: every workflow and every node fires a POST to our API when it finishes. This keeps the integration simple and retry-safe. If a webhook fails, n8n retries it without us needing custom retry logic on every workflow.

As we continue to develop, the n8n layer will more and more become the frontend interface for the agent node, but the true logic and functionally will migrate more and more to the backend.

### Flask as the System Boundary

We built a Flask API as the single entry point for all ingestion and reporting. This wasn't just an architectural preference, it was a governance decision.

A dedicated API layer means:

- Auth and validation happen in one place.
- Internal and admin surfaces are protected behind API keys.
- The data contract between n8n and the database is explicit and versioned.

The only public endpoint is `GET /health`. Everything else requires an API key, the best practice for production AI operations.

### Postgres as the Observability Store

Postgres was hands down the right call for three reasons:

1. We needed **normalized lifecycle tables**: workflow runs and node runs are separate concerns, and they needed to be queryable independently.
2. JSONB support lets us capture flexible payload data (inputs, outputs, errors) as our workflows evolve without requiring schema migrations every time a workflow changes shape.
3. Strong constraints and indexes give us dashboard-grade query performance on the analytics endpoints without needing a separate OLAP layer.

The more I've used Postgres and explored the native functionality, the more I've grown enamored, and can't imagine picking another default database. (Unless the use case allows me to get away with SQLite)

### Dokploy + Docker for Delivery

Reproducible production deployments matter when you're building internal infrastructure. Docker keeps the environment consistent across dev and prod, and Dokploy gives us a controlled rollout model with environment-driven configuration.

No surprises on deploy day.

Dokploy also helps manage the networking via native integration with Traefik. Built-in reverse proxy and domain redirects to the container applications; all encrypted over HTTPS via Let's Encrypt.

If you want simple and reliable dev ops that anyone on the team can manage, Dokploy is a perfect solution for small and midsize projects.

### Apitally for API Telemetry

We added Apitally for request-level operational insight on the API; built in tracking fro latency, error rates, endpoint usage.

This is separate from our agent observability data.

## Architecture Overview

### Ingestion Model

Two endpoints handle all agent event data:

```
POST /api/n8n/workflow-complete
POST /api/n8n/node-complete
```

Both use **deterministic event IDs** derived from the workflow execution context.

This gives us idempotent writes; if n8n retries a webhook, we don't double-count the run. Safe retries are non-negotiable in any production ingestion pipeline, _per the papers I've read_.

### Data Model

The schema is built around four core table groups:

**Lifecycle tables:**

- `workflow_runs`
  - workflow-level outcomes, timing, and status
- `node_runs`
  - node-level detail including agent name, tool name, and traceability fields

**Cost and telemetry:**

- `usage_events` — token and cost data, currently scoped to model-level, designed for expansion
  - (_We've since migrated to use the OpenRouter; and I'll rework this entire system to tie directly into the tracking system I'm building there. See: [# Building a Production-Ready OpenAI Billing and Usage ETL Pipeline](https://pbrazeale.github.io/posts/openai-billing-etl/) for an idea of what that tracking system will be and do, but only for OpenRouter instead of OpenAI_)

**Tool governance:**

- `ai_tools`, `ai_tool_versions`, `tool_runs`
  - versioned tool definitions with an "one active version" constraint

By treating tool definitions as versioned entities, we create the data foundation for a controlled prompt improvement loop. (_Which was the core goal behind pitching this project for me. Though offering a clean reporting dashboard for business intelligence will help free up time and gain trust for my department throughout the company._)

### Analytics API Surface

The analytics layer exposes four endpoint groups:

- **Admin overview:** aggregate reliability and throughput
- **Workflow drill-down:** per-workflow performance trends
- **Node detail:** node-level failure analysis and duration distributions
- **Agent summaries:** per-agent run counts, fail rates, and tool usage

These endpoints serve both executive dashboards and operator-level debugging without anyone needing direct database access.

## Systematic Agent Review

The core value here is **full execution traceability**.

Every workflow completion and node completion event is persisted with its timing, status, and payload. That means:

- Failures can be traced by workflow, node type, agent name, or tool name.
- Duration distributions are queryable across time, so you can spot when p95 latency degrades before users notice. A real issue when constantly changes models, and using fallback models. (_Though I hope to have solved this particular issue with the use of OpenRouter._)
- Run counts and fail rates are comparable across agents and workflows.

Before this system, debugging an agent issue meant manually replaying executions or asking the person who last touched the workflow. Now it means running a query, and reading outputs.

Teams move from anecdotal debugging ("it felt slow last week") to evidence-based review ("fail rate on workflow X increased 12% after the deploy on Tuesday").

## Prompt Improvement Loop

The `ai_tool_versions` table is the linchpin here. Every prompt change creates a new version record. The "one active version" constraint means rollout is controlled and rollback is a single update.

Node-level payload capture gives us the other half of the picture. Input, output, and error data is retained at the node level, which means you can inspect how a specific prompt version behaved in context of real workflow executions. (_Also allows for testing my hypothesis about using different baseline models depending on the core node functionality; regardless of the workflow._)

The current state gives us the data foundation. The next phase closes the loop: correlating prompt versions with **reliability, latency**, and **cost changes** across the same time window.

When that's wired up, version promotion stops being a judgment call and becomes a measured outcome, with universal reporting that can be analyzed and understood at ever level within the organization regardless of expertise.

## Standardized Reporting

This was one of the original requirements, and it's worth being direct about why it matters. Without a central reporting API, everyone generates their own numbers. Definitions drift. Denominators change. Leadership meetings turn into debates about whose spreadsheet is right.

The analytics API solves this by being the single source of truth:

- **Workflow success/failure trends:** consistent definitions, consistent denominators
- **Agent and tool performance breakdowns:** attributable to specific agents and tool versions
- **Cost trends:** scoped to model and provider via the usage events expansion

When every report pulls from the same API, reporting logic becomes reusable and auditable. Leadership gets consistent operational signals without anyone manually stitching data together.

## Security

A few decisions here that aren't optional:

- Public exposure is limited to `GET /health`.
  - Everything operational is behind API key auth.
- Ingest contracts enforce strict schema and timestamp semantics.
  - Malformed payloads are rejected at the boundary, not silently written to the DB.
- Idempotency constraints protect against duplicate ingest from retries.

These aren't over-engineering. They're the minimum viable governance for a system that management is going to rely on for operational decisions.

## What Comes Next

The foundation is stable. The next phase is depth and surface:

- **Expanded usage telemetry:** model-level and provider-level cost reporting
- **UI layers:** a user-facing report generation interface and an internal admin operations dashboard
- **Quality scoring and alerting:** automated regression detection when prompt or agent performance degrades (_Given the increase in foundation model development this might need to become a 4-6 week timeline instead of 13_)

The dashboard and alerting work is what turns this from a data system into an operations system.

## Takeaways

AI value isn't just model selection. It's operational discipline.

Choosing the right model in only half the job. Being able to measure what's happening, trace failures to their source, and improve prompts based on evidence rather than intuition is just as important.

The architecture we built isn't exotic: n8n, Flask, and Postgres. All running on a Dokploy server. It doesn't get much simpiler.

The value is in the discipline: standardized ingestion, strict validation, normalized observability, and a reporting layer that the whole organization can trust.

If your AI operations are still held together by manual log reviews and pre-meeting spreadsheets, the problem isn't your models and prompts.

---

[**World Parts Direct**](https://www.worldpartsdirect.com/): guaranteed lowest prices OEM parts for GM and Mopar parts, with next day delivery options for over 100k items. Preowned parts for almost any make and model are also available, with identical warranties to new.

+++
tags = ['NovelFoundry', 'SaaS', 'Build Notes']
title = 'Fixing a Production Queue Bug in NovelFoundry: How I Stopped Stale Analysis Jobs from Locking the App'
date = 2026-03-10T20:00:00-06:00
draft = false
+++

What looked, on the surface, like a simple “job stuck in `queued`” issue inside NovelFoundry turned out to be a wider systems problem: the backend had no authoritative recovery path for queued jobs that never actually started, the deployment model was missing the scheduler needed to reconcile stale work, and the application trusted stale job state long enough to lock users out of the dashboard.

---

## User-Facing Failure

NovelFoundry’s manuscript workflow depends on a reliable handoff between the application, the backend, and the worker process that performs analysis. When a user uploads a manuscript and starts analysis, the system creates a job row and the application begins reflecting that state in the dashboard.

The failure mode was this:

- the backend created a `jobs` row with `status = queued`
- under certain failure conditions, the worker never advanced that row into a running state
- the application continued to interpret that queued job as active work
- the dashboard lockout logic kept the manuscript screen blocked

So while the technical symptom was “stuck queued jobs,” the operational consequence was that users could be trapped behind a permanent processing state.

---

## Architecture Trace

To fix the issue safely, I first had to map the exact runtime path the analysis job followed through the stack.

Three systems were involved:

1. **`nf-application`** starts jobs and renders job state in the dashboard.
2. **`nf-backend`** creates job records, exposes the API, and runs the Celery worker.
3. **Supabase** persists the `jobs`, `manuscripts`, and `analysis_reports` data that both sides depend on.

The runtime model itself is straightforward on paper:

- a **Flask API**
- a **Celery worker**
- **Redis** as the broker/backend
- a **Dokploy** deployment configuration

The key paths in this investigation were:

- `nf-backend/app/api/jobs.py`
- `nf-backend/app/tasks/worker.py`
- `nf-backend/app/services/db.py`
- `nf-application/src/hooks/dashboard/useManuscripts.ts`
- `nf-application/src/hooks/dashboard/useTimerLockout.ts`

That was the chain I needed to inspect end-to-end: where the job was created, when it was expected to move forward, how stale rows were read back, and how the application interpreted those states once they came over the wire.

---

## Investigation

Once the code path was traced, the bug stopped looking mysterious.

The backend API created `jobs.status = queued` immediately when a manuscript analysis was launched. That part was correct.

The problem was what happened next.

The worker only moved the job forward after it had already completed several startup steps.

That meant there was a timing window where the job existed as `queued`, but no durable signal yet indicated that a worker had truly picked it up. If something failed in that gap, the row could remain `queued` indefinitely.

That alone would have been bad enough. But three more issues amplified it:

### 1. There was no backend reconciliation for stale queued jobs

If a job stayed queued far longer than it reasonably should have, nothing on the backend periodically cleaned it up.

No scheduler was failing old queued rows.

No API read path was correcting stale data.

The database could simply retain a stale `queued` row forever.

### 2. The frontend stopped polling too early

The application did not continue refetching manuscript data long enough to reliably detect backend correction, especially in edge cases where the worker never properly transitioned the state.

That meant even if the backend later changed something, the dashboard could remain visually stale.

### 3. Timer-wrapped terminal states were still treated as active

The dashboard included timer/status semantics that wrapped stages in strings like `timer|...|failed`.

The trouble was that terminal timer-wrapped states could still leak into lockout behavior.

In other words, even when the meaning of the state was effectively “this is over,” the UI logic could continue treating it like “this is still active.”

Taken together, the bug crossed four boundaries at once:

- backend job creation
- worker state progression
- deployment scheduling
- application polling and lockout logic

---

## Backend Fix

The backend fix had several parts, and each one solved a different failure mode.

### Configurable timeout settings

The first improvement was adding configurable timeout behavior in `nf-backend/app/config.py`.

Two defaults were introduced:

- **queue timeout:** 5 minutes
- **sweep interval:** 60 seconds

That sounds small, but it is one of those changes that turns “magic behavior” into explicit operational policy. A queue should not be allowed to imply activity forever.

If a job has remained queued beyond a reasonable threshold, the system needs a shared definition of stale. Putting those values in configuration makes that policy clear, reviewable, and adjustable as production behavior evolves.

### Stale queued-job reconciliation helpers

Next, I added reconciliation helpers in `nf-backend/app/services/db.py`.

These helpers detect queued jobs whose age exceeds the configured threshold, then transition them to `failed` with an explanatory error. The message makes the failure mode explicit: the job timed out while waiting to start.

First, it gives the system an authoritative backend recovery path.

Second, it makes the failure visible. Silent staleness is poisonous in production; visible failure is recoverable.

### Read-time self-healing in the API

A defensive system should not rely on only one repair path.

So in addition to the periodic sweeper, both the single-job endpoint and the manuscript list endpoint now reconcile stale queued jobs before returning data.

That work landed in:

- `nf-backend/app/api/jobs.py`
- `nf-backend/app/api/manuscripts.py`

Even if the periodic scheduler is unavailable, delayed, or temporarily misconfigured, the API can still self-heal stale queued rows at read time.

That means the app does not have to wait for a background process to clean things up; ordinary reads can surface corrected truth.

In practice, this turns stale rows from “permanent poison” into “repairable on contact.”

### Worker hardening

The worker also needed to become more authoritative about job pickup.

In `nf-backend/app/tasks/worker.py`, the worker now moves a job out of `queued` immediately upon pickup by writing `running_initializing` as soon as the job has actually been claimed.

That closes the ambiguous window where a job existed as queued but the worker had not yet written a non-queued state.

Just as importantly, terminal statuses are now written as plain terminal values: `completed` and `failed`.

They are no longer preserved in timer-wrapped terminal strings that can confuse downstream UI logic.

### Periodic sweep for stale jobs

Finally, the durable production mechanism was added: a Celery task that periodically fails stale queued jobs.

This is the long-running enforcement layer that keeps queue truth healthy over time. Even if no user refreshes the page, even if no read-time endpoint is hit, and even if a job quietly goes stale in the background, the system now has a recurring process whose sole purpose is to reconcile that bad state.

---

## Dokploy / Infrastructure Fix

One of the most important findings in this effort was that the original production deployment did not include everything required for the code-level fix to actually run.

The Dokploy deployment had:

- `web`
- `worker`
- `redis`

But it did **not** have a `beat` service.

That meant any periodic Celery reconciliation task could exist perfectly in code and still never execute in production.

So `nf-backend/docker-compose.prod.yml` was updated to add a **beat** service. That change matters every bit as much as the code changes themselves.

This is a classic production lesson: infrastructure omissions often masquerade as application bugs. The backend can be correct on paper and still fail operationally if the process model that makes it work is missing from the deployment shape.

---

## Application Fix

The backend now had a way to tell the truth. The application needed to notice it, reflect it, and stop over-locking the UI.

### Active manuscript refetching\

In `nf-application/src/hooks/dashboard/useManuscripts.ts`, the application now continues refetching manuscripts while any job is genuinely active.

If the backend flips a stale queued job to `failed`, the application has to keep listening long enough to observe that correction. Brief polling windows are fine for optimistic flows; they are not enough for resilient queue state handling.

### Timer/status handling cleanup

Next, the timer and lockout semantics were cleaned up in:

- `nf-application/src/pages/dashboard/status/timerUtils.ts`
- `nf-application/src/hooks/dashboard/useTimerLockout.ts`

The core rule is simple: terminal timer-wrapped states are terminal. They should not count as active lock states.

That sounds obvious, but UI state machines often grow by accumulation.

A wrapper format that once helped render countdown behavior can later leak into business logic in ways that keep old assumptions alive. This cleanup reasserted a clearer contract between status rendering and lockout behavior.

### Better dashboard rendering

The dashboard itself was also updated in `nf-application/src/pages/Dashboard.tsx` so terminal timer-wrapped states render as normal status badges rather than countdown-style badges.

Good rendering helps communicate the true lifecycle of the job. A terminal failure should look finished, not “still timing.”

When the visual language matches the state model, users trust the product more—and maintainers debug it faster.

---

## Before and After

The cleanest way to understand the fix is to compare the system’s behavior before and after.

### Before

- job created as `queued`
- worker might never move it forward
- no stale-job sweeper existed
- frontend stopped polling too soon
- timer-wrapped terminal states could still lock the UI
- users could remain stuck indefinitely

### After

- worker exits `queued` immediately on pickup
- stale queued jobs are marked `failed`
- API endpoints reconcile stale rows on read
- Celery beat runs the periodic sweep in production
- application keeps refetching while jobs are active
- terminal timer states no longer lock the dashboard
- users see a visible failure instead of a permanent stall

---

## Final Outcome

At the end of this work, the queue pipeline is materially healthier.

Stale queued jobs no longer remain in limbo forever. The backend can detect and fail them automatically. The API can self-heal stale reads even if the periodic path is unavailable.

The application now keeps listening long enough to observe those corrections. And the production deployment includes the scheduler process required for periodic reconciliation to actually run.

Just as important, terminal statuses are now treated as truly terminal—both in backend truth and in dashboard behavior.

It was a coordination failure between:

- backend truth
- worker lifecycle semantics
- deployment process shape
- frontend refresh and lockout logic

Treating it as a narrow status-field bug would have produced a narrow patch. Treating it as a systems problem produced a durable fix.

That is usually the right instinct in queue-backed applications. When user-facing state depends on asynchronous workers, the system needs all of the following:

- authoritative transitions
- stale-state recovery
- deployment support for periodic cleanup
- client behavior that notices corrected truth
- clear distinction between active and terminal states

Miss one of those, and stale state starts acting like product logic.

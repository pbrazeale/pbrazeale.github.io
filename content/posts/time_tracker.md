+++
tags = ['Build Notes', 'Python', 'Open Source']
title = 'Time Tracker Release'
date = 2025-09-26T19:30:07+01:00
draft = false
+++

## Local Hosted Database: built for the real workday

### [Time Tracker Repo](https://github.com/pbrazeale/Time-Tracker)

This is a personal project ready for public use. Released under the MIT license, feel free to adjust as you see fit. I'm actively updating the application as I find new features I want/need. If you want to contribute the repo's README explains how.

![Time Tracker Logo](https://pbrazeale.github.io/images/time_tracker_logo_300.jpg)

## TL;DR

I built this for work after I couldn't find a solution that wasn't a subscription web app. First to track my hours on the clock; then to track **project-level timeframes** so I can hand upper management better estimates (fewer guesses; more receipts). It’s _local-first_ (SQLite), set to **America/Chicago** (CST/CDT), and optimized for easy time tracking.

---

## Why I built it

- I needed **one source of truth** for time, not a mix of my developer blog and memory.
- I needed **project tracking**. Hours by category and project, so future estimates stop being vibes and start being numbers.
- I needed it **offline and private**.
- And I needed **a fast UX,** not 10 settings and 3 screens. One click to start/stop. No overlapping sessions.

---

## What you get

- **One-click timers**; prevents overlaps; Central Time as system of record.
- **Project-level entries** with category, elapsed hours, and **manual HH:MM** corrections (because real days are messy).
- **Reports that matter**: toggle Plotly charts ↔ raw tables; daily totals and category breakdowns; quick ranges that match how managers ask.
- **Admin workspace**: fix typos, manage categories, backfill entries—without leaving the app.
- **Local-only storage**: everything in `time_tracker.db` (portable; offline; yours).

---

## Setup

- Create a venv; `pip install -r requirements.txt` (`streamlit`, `pandas`, `plotly`).
- Run `streamlit run app.py`.
- First launch seeds `time_tracker.db` (schema + starter categories).
- Lean deps → faster cold starts; runs anywhere Python runs.

---

## Data layer

**`db.py`** defines:

- `WorkSession` and `ProjectEntry` (dataclasses).
- Schema + **timezone-aware** connection.
- `init_db()` migrates safely (adds columns like `total_hours` when missing) and preloads defaults.
- `get_conn()` wraps connections; enforces foreign keys; commits reliably.

All timestamps are **ISO (International Organization for Standardization) strings** tagged with Central Time.

---

## Services

**`services.py`** translates UI → DB and back:

- Normalizes inputs with `parse_time_text()` + `combine_date_time()`; **HH:MM** → TZ-aware ISO.
- Computes durations on demand; returns **pandas** DataFrames for the UI.
- Shapes chart-ready data so Streamlit components stay declarative (and thin).

Net effect: validation/aggregation/formatting lives in one place; easier to test → fewer surprises.

---

## Streamlit UI

- **`render_tracker()`**: manages the active day; blocks multiple open sessions; uses `st.toast()` + `st.rerun()` for instant feedback.
- **`render_reports()`**: chart/table toggle sticks in `st.session_state`; date pickers with sane defaults; charts or tables (same numbers either way).
- **`render_admin()`**: edit sessions/entries; create manual entries; uses the same parse/validate path as live tracking (one truth).

---

## Reporting

- Aggregations: `fetch_daily_hours_summary()` and `fetch_category_breakdown()` keep fidelity (no rounding oopsies).
- Visuals: `build_daily_hours_chart()` and `build_category_pie()` pull the palette from `constants.py`.
- **Same summary frames** power charts **and** tables → no “which is right?” moments.

This helps me submit project estimates to stakeholders.

---

## Admin

- Forms enforce required fields and valid times.
- Running sessions can stay open (no forced stop/start gymnastics).
- Manual additions follow the **same pipeline** as live tracking (fewer edge cases, cleaner DB).

---

## Roadmap (pragmatic; no heroics)

- **Multi-time-zone** support/selection.
- **Richer analytics** (streaks; utilization; parent project tracking).
- **Automated backups** of `time_tracker.db`.

+++
tags = ['Build Notes', 'Python', 'Open Source']
title = 'Music Meta Tagger'
date = 2025-09-21T19:30:07+01:00
draft = true
+++

## Simple Music Metadata Updater

### [Music Meta Tagger](https://github.com/pbrazeale/music_meta_tagger)

I needed a fast way to fix metadata for my Jellyfin music library, especially for indie albums that arrived with inconsistent tags. Jellyfin couldn’t reliably group or identify some of these releases because fields like Album Artist, Year, or Track numbers weren’t standardized. This tool let me normalize those tags in bulk so Jellyfin “understood” my indie albums and organized them correctly.

If you want to contribute the repo's README explains how.

![Music Meta Tagger Logo](https://pbrazeale.github.io/images/music_meta_tagger_logo_300.jpg)

---

## TL;DR

Fix messy tags fast so Jellyfin stops guessing. **Music Meta Tagger** is a small Streamlit app for **bulk edits** across MP3/MP4/FLAC/WMA (Windows-friendly fields, including **0–5 star ratings**; works with local drives and UNC paths). You get a **200-row preview**, sane parsers/validators (only writes what you fill in), a progress bar, and per-file error reporting. Run it with Python 3.12 → `pip install -r requirements.txt` → `streamlit run app.py`. Want to help? PRs welcome—see the README.

---

## What You Get as a Listener

- Bulk updates in one go: Point the app at a folder (local, mapped drive, or UNC path) and apply the same metadata across every supported audio file. Optionally include subfolders for full‑album or library‑level edits.
- Windows‑friendly tagging: Fields map to what you actually see in Windows Explorer (Title, Album, Contributing artists, Album artist, Year, Genre, Comments, and 0–5 star Ratings).
- Wide file support: MP3, MP4/M4A/M4B/M4R/M4V, FLAC, WMA/ASF — with format‑appropriate tag handling under the hood.
- Clear preview and feedback: A 200‑row preview table shows what’s in the folder; post‑update summaries call out successes and per‑file errors.
- Simple, modern UI: Streamlit‑based, with a clean dark theme and a two‑column form that’s quick to scan and fill.
- Network‑share aware: Works with `\\\\server\\share` UNC paths as well as local drives.

---

## Project Overview

Music Metadata Tagger is a small, focused desktop‑friendly web app (Streamlit) for bulk‑editing audio tags with Mutagen. The goal is rapid, confident cleanup of common fields that downstream players (Windows, Jellyfin, etc.) rely on for grouping, sorting, and display.

- Entry point: `app.py`
- Core logic: `metadata_logic.py` (tag parsing, validation, write handlers)
- Folder workflow: `folder_logic.py` (UNC normalization, caching, selection)
- UI helpers: `ui.py` (sidebar, preview table, form fields, results)
- Theme: `style.py` (dark, brand‑colored CSS injected via Streamlit)
- Deps: `streamlit`, `mutagen`, `pandas` (see `requirements.txt`)

---

## Build Process: From Idea to Working App

1. Define the “must‑fix” fields

   - I listed the minimum set that fixes 80% of library issues: Title, Subtitle, Contributing artists, Album artist, Album, Year, Track number (with optional total), Genre, Comments, and a 0–5 star Rating.
   - Each field has a small parser/validator (e.g., YYYY or YYYY‑MM‑DD for Year; “1/10” for Track number).

2. Normalize tags across formats

   - Mutagen is the engine, but every container stores fields differently:
     - MP3: ID3 frames like `TIT2` (Title), `TPE1` (Artists), `TPE2` (Album Artist), `TRCK` (Track), `TDRC` (Year), `POPM` (Rating).
     - MP4/M4A: iTunes‑style atoms like `\xa9nam` (Title), `aART` (Album Artist), `trkn` (Track), `rate` (Rating).
     - FLAC: Vorbis comments (`title`, `artist`, `album`, `date`, `genre`, plus `tracknumber`/`tracktotal`).
     - WMA/ASF: `WM/*` fields (e.g., `WM/AlbumTitle`, `WM/SharedUserRating`).
   - Ratings are converted to what each format expects (e.g., MP3’s `POPM`, MP4’s `rate`, ASF’s `WM/SharedUserRating`).

3. Make bulk edits safe and repeatable

   - Field parsers live in `metadata_logic.py` and only write fields the user actually fills in. Leaving a field blank means “don’t touch it.”
   - A progress bar surfaces long runs; per‑file errors are captured and shown in a results grid.

4. Fast, readable UI

   - The two‑column form mirrors how you think about albums: textual fields left/right, rating as a simple dropdown, comments as a textarea.
   - The preview table shows a slice (up to 200 files) for quick visual checks before committing changes.

5. Respect Windows and networks

   - `folder_logic.py` normalizes UNC paths and caches folder listings. The sidebar provides a native folder picker (via Tkinter) and a text field for power users.

6. Add a touch of polish
   - `style.py` injects a light custom theme so it feels like a tool, not a prototype.

---

## How to Run

- Requirements
  - Python 3.12
  - `pip install -r requirements.txt`
- Launch
  - `streamlit run app.py`
- Open the browser at `http://localhost:8501` if a tab doesn’t auto‑open.

---

## Implementation Highlights

- Field parsing and validation
  - `parse_year` enforces `YYYY` or `YYYY‑MM‑DD` to keep libraries consistent.
  - `parse_track_number` accepts `N` or `N/T` and guards against bad values.
  - `parse_people` splits contributing artists on commas/semicolons, trimming whitespace.
- Format‑specific handlers
  - Dedicated classes per container (`MP3TagHandler`, `MP4TagHandler`, `FLACTagHandler`, `ASFTagHandler`) map semantic fields to correct low‑level tags.
- Preview path
  - A quick “easy mode” read with Mutagen populates the folder preview; WMA/ASF gets a direct read fallback for better coverage.
- Session and caching
  - Session state tracks the selected folder and toggles; changing the folder resets form inputs to avoid accidental carryover.

---

## Limitations and Future Work

- No online metadata lookup (yet). For now, this is a “you provide the truth” tool. Wishlist items:
  - MusicBrainz/Discogs lookup to prefill fields.
  - Per‑field dry‑run preview to show the “before → after” diff for a sample file.
  - More fields (composer, disc number/total, album sort, artwork) and ID3 v2.4 options.
- Internal cleanups
  - Centralize constants and user‑tunable options (see `constants.py` and `settings.py` TODOs).

---

## Practical Tips

- Back up unique files before bulk edits.
- Start with a small folder to validate your choices, then expand.
- Keep “Album artist” consistent across tracks to help any media server, not just Jellyfin.

---

## Closing Thoughts

This project was born from a real need: get Jellyfin to understand my indie albums by fixing the basics quickly and correctly. By focusing on a tight set of well‑mapped fields and a pragmatic UI, Music Metadata Tagger makes bulk cleanup fast, predictable, and friendly.

+++
tags = ['Sarah AI Line Editor', 'AI', 'Build Notes', 'Python', 'SaaS']
title = 'Sarah MVP Launch'
date = 2025-07-08T10:50:07+01:00
draft = false
+++

![Sarah Hero](https://pbrazeale.github.io/images/sarah_hero.jpg)

🚀 Just shipped my first personal project from the [Boot.dev](https://Boot.dev) curriculum — and what started as a simple idea quickly evolved into a full-fledged SaaS concept.

🔗 GitHub: [github.com/pbrazeale/sarah](https://github.com/pbrazeale/sarah)

Meet Sarah — an AI-powered editing assistant for fiction authors. She helps break down manuscripts into chapters, analyze beat structure, perform line edits, and deliver developmental feedback — all tailored to your genre, tense, and point of view.

## Along the way, I learned a ton:

- 🧠 AI can (and should) be your code review partner — Gemini saved me more than once from invisible bugs and variable mismatches.
- ⏳ Handling long API calls? I used `threading` + `itertools.cycle()` to add a CLI loading spinner — no more checking web dashboards or racking up surprise bills.
- 🔄 Starting over isn’t failure. It’s a natural part of development. Rewriting code with hard-earned clarity is worth it.
- ☕ Oh — and plan for twice the time and three times the caffeine. **Always!**

Now I'm diving into web design and interfaces using **FastAPI**, **Jinja**, and **Tailwind CSS** to take this idea even further. Excited to keep building and sharing!

---

## ✨ Key Features

### ✅ Manuscript Upload & Processing

- Accepts .docx files.
- Extracts title and creates project directories for organized outputs.
- Splits manuscripts into chapters based on Heading 1 structure.
- Preserves rich text formatting (bold, italics, underline).

### 📝 Editing Options

- Line Editing tailored to:
  - Genre & subgenre
  - Tense (past/present)
  - Point of View (1st, 3rd limited, 3rd omniscient)
- Developmental Editing providing deep, actionable feedback:
  - Full novel analysis
  - Beat sheet creation
  - Act-level and chapter-level developmental edits

### ⚡ Output & Downloads

- Generates clean .md files for each chapter.
- Saves Beat Sheets, Manuscript Developmental Edits, and Chapter Edits.
- Designed for easy conversion back to .docx, .epub, or print-ready formats.

## 🚧 Project Status

Sarah is under active development with core functionality in place:

- ✅ .docx upload and chapter splitting
- ✅ Beat Sheet generation
- ✅ Manuscript Developmental Editing
- ✅ Chapter Developmental Editing
- 🛠️ CLI-based workflow (GUI planned for future)
- 📦 Export features to organized directories

### ⚠️ Note on Prompts & Guidelines

This project uses a modular prompting system. You must provide your own:

- guidelines.py This file defines your editing guidelines and examples to guide the LLM according to your editorial style or genre expectations.

## 🛠️ Project Structure

```bash
Sarah/
├── main.py
├── requirements.txt
├── functions/
│   ├── process_chapter.py
│   └── openrouter_call.py
├── prompts/
│   └── prompt.py
│   └── guidelines.py*
├── working_dir/
│   ├── import/
│   ├── export/
│   └── markdown/
└── .env
└── README.md
```

## 📅 Roadmap

- GUI-based interface for easier usage
- EPUB export integration
- Enhanced error handling and validation
- Author-focused SaaS deployment

## 📄 License

This project is currently proprietary to Aconite Cafe for internal author tooling. Licensing terms for external use are pending.

## 💡 Credits

Sarah is developed by Aconite Cafe, combining AI editing expertise with indie author publishing experience to create tools that empower storytellers.

“Helping authors tell better stories, one AI edit at a time.”

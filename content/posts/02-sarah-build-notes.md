+++
tags = ['SARAH: Story Analysis & Revision AI Helper', 'AI', 'Build Notes', 'Python', 'PyQt']
title = 'Sarah MVP Development Roadmap'
date = 2025-06-06T10:50:07+01:00
draft = false
+++

This will be my first project where I build it entirely myself with no AI coding assistance. After I have an MVP I built, and understand the mistakes I make, then I'll reconsider using AI to maintain and expand upon my project.

Based on the roadmap and [boot.dev](https://www.boot.dev/courses/build-personal-project-1) assignment to spend 20-40 hours coding and implementing the software, the MVP might take the full timeframe. Once I have the core logic working, and everything behaves as indented (_I'll need to test several file versions_), I'd like to focus on making the software a standalone application and polishing the UI.

UI has never been my focus before now, but this might be the right project to start. _Might us AI to make the GUI after the fact. Not sure if I'd count that as cheating myself, as I'm not trying to learn/master front-end._

---

## 🧱 Phase 1: Core Architecture

1. **Frontend (PyQt6)**
   - File upload field
   - Multi-select checkboxes (e.g., grammar, tone, conciseness)
   - Text field: "Briefly describe what you're aiming for"
   - Submit button
   - Status updates + file download link
2. **Backend**
   - Parse uploaded file
     - Use `python-docx` for `.docx`
     - Plain text reader for `.txt`, `.md`, etc.
   - Construct a prompt based on user input
   - Send prompt + file content to OpenAI API
   - Receive and write edited file to disk
   - Return download path to PyQt UI

### 🧰 Required Libraries

##

**Frontend:**

- `PyQt6`
- `PyQt6.QtWidgets` for the GUI elements

**Backend:**

- `openai` (API access)
- `python-docx` (for `.docx` reading/writing)
- `mammoth` (optional, for converting `.doc` to HTML/text)
- `markdown` (optional, if you want to clean up `.md` formatting)

### 🔧 Design Decisions

| Feature            | Approach                                        |
| ------------------ | ----------------------------------------------- |
| File Storage       | Temp folder (`tempfile`) or `app_data/edited/`  |
| AI Editing         | Summarize user options into a prompt            |
| File Output Format | Match original format (e.g., `.docx` → `.docx`) |
| Prompt Control     | Templates to build robust, reusable prompts     |

---

## 🚀 Initial Deliverables

- ✅ Basic PyQt6 app with file picker, options, and "submit"
- ✅ Backend script that:
  - Accepts a `.txt` or `.docx`
  - Accepts user options + brief
  - Sends content to OpenAI with a pre-written prompt
  - Returns a new file

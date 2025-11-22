+++
tags = ['NovelFoundry', 'AI', 'Build Notes', 'Python', 'PyQt']
title = '01 Build Notes Sarah - AI Line Editor'
date = 2025-06-06T10:40:07+01:00
draft = false
+++

I used GPT to assist in analyzing the cost benefits for building an AI editor with PyQt6 (_software I'm familiar with_) vs using Word's track changes for inline edits. Likewise debated between trying to encapsulate an AI model into the software to prevent API calls; however, I'm unsure that models have been distilled down enough to make it feasible for mass adoption.

Based upon the quick analysis, I've decided to move forward with a PyQt6 MVP an rely on OpenAI API. Given my past experience this should likewise make the build process smoother and allow me to focus my hours on making a viable MVP, rather than bashing my head on coding bugs, and learning new frameworks.

---

## GPT Prompt

> I want to build
> Sarah: Your AI Line Editor
>
> I'm familiar with Python, so I'd like to stick with it where possible.
>
> I'd like to explore the difference between creating a PyQt6 interface that accepts a file upload (.md, .docx, .doc, .txt) and returns an edited file based on multiple selection options and quick description written by the user. (This will tie into prompts I write on the backend.)
>
> The other option would be built around uploading a .docx file and the AI does inline edits using Word's track line changes.
>
> Please explain the complexity issues of using word in that way vs upload and download a file?
>
> Also, what are the requirements to create a locally hosted AI embedded into the software, versus using an AI subscription. Give me a time complexity for designing an embedded AI system.

---

## ⚖️ Option Comparison: PyQt6 Editor vs Word Inline Edits

### 🔹 Option 1: PyQt6 App with Upload/Return

- **File Types**: Accepts `.md`, `.txt`, `.doc`, `.docx`
- **Flow**: User uploads → selects style goals/options → enters brief → backend edits file → returns new version
- **Complexity Level**: Medium
  - Parsing `.md` and `.txt` is straightforward.
  - `.docx` and `.doc` require `python-docx` and potentially `mammoth` or `pywin32` (Windows-only).
  - You’re not manipulating tracked changes—just replacing or modifying text.
- **Pros**:
  - Platform-agnostic (Linux/Mac/Windows)
  - Easier to design a consistent editing logic
  - Flexible styling options via PyQt UI
- **Cons**:
  - You lose native Word features like tracked changes
  - Harder for users who expect Microsoft Word-style edits

### 🔹 Option 2: `.docx` with Tracked Changes (Word Integration)

- **Flow**: Upload `.docx` → AI edits it inline using Word’s tracked changes → return `.docx`
- **Complexity Level**: High
  - Word's tracked changes aren't fully supported in `python-docx`
  - You’ll likely need `win32com.client` (Windows-only, needs Word installed) or Aspose (expensive license)
- **Pros**:
  - Produces native-looking output for professional editing workflows
  - Familiar to users (especially editors, publishers)
- **Cons**:
  - Hard to test cross-platform
  - Difficult automation (esp. on Linux/macOS)
  - May require commercial libraries or subscriptions

---

## 🧠 Embedded AI vs Subscription (Cloud API)

### 🔸 Embedded AI (Locally Hosted)

- **Options**: Use models like LLaMA 3, Mistral, GPT4All
- **Requirements**:
  - A decent GPU (at least 6–12 GB VRAM for useful models)
  - Quantized models (GGUF or GPTQ) to reduce load
  - Use libraries like `llama-cpp-python` or `ctransformers` for integration
- **Pros**:
  - No API costs or internet requirement
  - Full data privacy
- **Cons**:
  - Slower response time (especially on CPU-only systems)
  - Limited model size (can’t run GPT-4 locally without massive resources)
  - More dev time to tune prompts, memory mgmt, token handling

**⏱️ Time Complexity Estimate:**

- **Research + Setup**: 1–2 weeks
- **Integration with UI and preprocessing logic**: 2–3 weeks
- **Prompt tuning + testing**: 1–2 weeks
- **Total**: ~5–7 weeks for a usable local AI tool (part-time)

### 🔸 API Subscription (e.g., OpenAI, Anthropic, Mistral Cloud)

- **Requirements**: API key, internet access
- **Pros**:
  - State-of-the-art models (GPT-4, Claude, Mistral)
  - Fast, scalable
  - Easier multi-platform deployment
- **Cons**:
  - Usage costs ($)
  - Latency for large documents
  - Data privacy concerns for sensitive content

**⏱️ Time Complexity Estimate:**

- **Prompt design + API integration**: 2–4 days
- **Testing and file handling**: 1 week
- **Total**: ~1–2 weeks for MVP

---

## 🧩 Summary Table

| Feature           | PyQt Upload/Return | Word Tracked Changes         | Embedded AI             | API AI        |
| ----------------- | ------------------ | ---------------------------- | ----------------------- | ------------- |
| Platform          | Cross-platform     | Windows-only (realistically) | Linux/Windows/Mac (GPU) | Any           |
| User Experience   | Custom UI          | Native Word experience       | Variable (CLI/UI)       | Consistent UX |
| Dev Complexity    | Moderate           | High                         | High                    | Low           |
| Cost              | Low (free libs)    | Medium–High (Word license)   | High (hardware, time)   | Pay per use   |
| Data Privacy      | Good               | Good                         | Excellent               | Weak–Moderate |
| Total Time to MVP | ~2–3 weeks         | ~4–5 weeks                   | ~5–7 weeks              | ~1–2 weeks    |
|                   |                    |                              |                         |               |

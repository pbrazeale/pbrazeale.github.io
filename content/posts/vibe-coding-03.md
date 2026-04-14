+++
tags = ['AI', 'Vibe Coding by Kim and Yegge', 'Learning', 'Articles', 'OpenClaw', 'Book Reviews']
title = 'Vibe Coding: The Human Loop Still Matters'
date = 2026-04-14T09:05:07+01:00
draft = true
+++

Main Source: [_Vibe Coding: Building Production-Grade Software With GenAI, Chat, Agents, and Beyond_](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

## AI Collaborators

### Vibe Coding Loop

1. Frame your objective
2. Decompose the tasks
3. Start the conversation
4. Review with care
5. Test and verify
6. Refine and iterate
7. Automate your own workflow

![Vibe Coding Loop](https://itrevolution.com/wp-content/uploads/2025/08/Screenshot-2025-08-12-at-12.10.08-PM-1024x472.png.webp)
[(Kim and Yegge 87)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> The OODA loop (observe, orient, decide, act loop) is a decision-making model developed by United States Air Force Colonel John Boyd in the early 1970s. [Source](https://en.wikipedia.org/wiki/OODA_loop)

> By breaking down a complex task, collaborating with AI through conversation, and iteratively building a solution, Gene accomplished in under an hour what might never have happened otherwise. [(Kim and Yegge 94)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> What might be a 50–100% speedup with chat-based vibe coding can become a 5–10x speedup with agentic coding. [(Kim and Yegge 96)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

### MCP

> Almost every tool will eventually have an MCP (Model Context Protocol) server sitting in front of it, to enable AI to manipulate it like a human user. [(Kim and Yegge 96)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

For almost all of this book, I found myself nodding along, mostly agreeing with aspects of my own workflow that I was already doing, and have now refined to align more with their setup. However, on this point, I think it’s wrong. Not just because I’ve avoided MCP this whole time, but because it’s the wrong approach for the model’s use case. (_Now, this could change with time as MCP evolves, but as of April 2026, no._)

##### Leaky Abstractions

> This is what I call a leaky abstraction. TCP attempts to provide a complete abstraction of an underlying unreliable network, but sometimes, the network leaks through the abstraction and you feel the things that the abstraction can’t quite protect you from. [Source](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)

Don’t take my word for it; here’s Onur Solmaz from OpenClaw talking about it too:

> The MCP versus CLI argument should be reframed as Computer vs No-computer argument. ... A key factor was that giving a CLI to a model also means you are giving it an entire COMPUTER ... One is a Turing machine, and the other one is basically a REST API. ... So MCPs win in restricted/local environments, whereas CLIs/shell access win in unrestricted/remote ones. [Source](https://solmaz.io/x/2036538477269934562/)

> Steve got the best results by removing himself from the loop through MCP. By using Puppeteer, the agent could finally “see” the front-end client UI for itself and could identify and fix problems that had previously required multiple frustrating and time-consuming rounds of slinging to address. This closed the feedback loop, enabling his AI collaborator to make its own corrections. [(Kim and Yegge 98)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

This is the one use case I’ve found for MCP: when an actual browser must be used. So when an application suite must be used, such as Chrome, MCP is perfect.

### Coding Agent Tools

> Coding agents solve problems semi-autonomously, checking in occasionally with you—just the way you’d want a collaborator to work. [(Kim and Yegge 98)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> We’ll frequently “downgrade” from an agent to chat programming. [(Kim and Yegge 99)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

The tooling built around ChatGPT and other such platforms has meant that, aside from specific research tasks where I’ve gathered enough domain expertise to know what to consider—and more importantly, what to avoid—it’s best to use their agent framework for searching the web for the right research notes. And even where I do have custom research prompts, now with extended thinking, unless I have a precise sequence to follow, it’s just as good, and easier, to let the platform handle it. However, like all skills, it’s vital to practice often and keep it fresh—unless you’re prepared to lose it and grow rusty.

#### Future of Coding Agents

- Asynchronous, remote agents
- Clusters of agents
- Supervisor agents
- Agent meshes

[(Kim and Yegge 101)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

Kim and Yegge’s predictions have manifested in [OpenClaw](https://openclaw.ai/), with the integration of OpenShell. Keep your eye out; I’ll soon release the book _OpenClaw on Proxmox_, which will explain, step-by-step, how to leverage the framework to create an agent swarm suitable for enterprise use.

##### Conway's law

> Organizations which design systems (in the broad sense used here) are constrained to produce designs which are copies of the communication structures of these organizations. [Source](https://en.wikipedia.org/wiki/Conway%27s_law)

### Key Vibe Coding Principles

> In contrast, prompt engineering is more like emailing a lawyer who is suing you—everything in that email is fraught with consequence, requiring precision and care. [(Kim and Yegge 102)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

- AI mistakes are both common and okay.
- AI is endlessly tolerant of your typos and occasionally sloppy grammar.
- Don’t spend too much time, if any, correcting your prompts.
  - _Absolutely true, if you’re maintaining human-in-the-loop control._
- Embrace the messy, productive joy of having problem-solving conversations.

> Human-in-the-loop allows the user to change the outcome of an event or process. The immersion effectively contributes to a positive transfer of acquired skills into the real world. This can be demonstrated by trainees utilizing flight simulators in preparation to become pilots. [Source](https://en.wikipedia.org/wiki/Human-in-the-loop)

#### Letting Errors Speak for Themselves

##### Rubber Duck

> Rubber duck debugging (or rubberducking) is a debugging technique in software engineering, wherein a programmer explains their code, step by step, in natural language—either aloud or in writing—to reveal mistakes and misunderstandings. [Source](https://en.wikipedia.org/wiki/Rubber_duck_debugging)

I learned this when taking Harvard's [CS50X](https://pll.harvard.edu/course/cs50-introduction-computer-science) and CS50P [Clip](https://www.youtube.com/shorts/r6hY_MMxhy8) _Thank you again to David J. Malan, Ph.D. and the team behind the program.Especially Carter's supplementary videos!_

> These act as the feedback your AI partner needs to course-correct.

- **For compilation errors:** Copy/paste the build output.
- **For runtime errors:** Share the stack trace.
- **For unexpected behavior and failing tests:** Provide the actual versus expected output.
- **For IDE issues:** Share a screenshot of the relevant window.
- **For UI issues:** Use a screen-grab server like Puppeteer.

[(Kim and Yegge 103)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> Properly configured, coding agents will automatically see all these error messages: They can access your browser console, your terminal shell, your logs, and your test suites, and usually require little to no action from you. [(Kim and Yegge 104)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

## AI Context and Conversations

> You’ll develop an intuition for when to select parts of the available context or go all-in and dump everything you have into the window. [(Kim and Yegge 111)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> ... approximately 80% of Git repositories worldwide can fit within a 500,000 token context window. [(Kim and Yegge 111)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> ... your conversation is a JSON structure that grows gradually until it’s too big for the context window. [(Kim and Yegge 115)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> AI chat interfaces increasingly have functionality, such as OpenAI’s ChatGPT Memory, which is information that is put into every conversation. Examples of items in Gene’s ChatGPT Memory include his preferred programming language (Clojure) and interests, including DevOps, functional programming, etc. [(Kim and Yegge 115)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

Depending on the use case, OpenAI cache has helped reduce the context burden; modern Codex is refined to the point that auto-compaction is also trustworthy enough with the right branching and commit system in place. _Though I still use `/compact` myself between feature checkpoints. See notes on [[Spec Driven Development Phases]]._

> Most coding agents now provide a “save game” checkpointing feature—use it liberally to remove unwanted context from wrong turns. Your future self (and wallet) will thank you. [(Kim and Yegge 116)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> AI performance doesn’t degrade gradually as context fills up; it falls off a cliff. Research from 2024 shows why this is the case. Most models show degraded reasoning at 3,000 tokens—far below their advertised limits. This is called _context saturation_, where AI begins to:
>
> - Generate less coherent responses.
> - Forget key details from thirty seconds earlier.
> - Provide inconsistent answers, leading you in circles.
> - Ignore explicit instructions, even those given in CAPITAL LETTERS.

[(Kim and Yegge 117)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

As of April 2026, when compiling these notes, I’ve found this to be largely solved; and again, when combined with proper agentic hygiene, it becomes an odd fluke.

> “Context is king” remains a fundamental rule in countless fields, from marketing to historical interpretation. It applies to vibe coding as much as any of them. As Simon Willison, a prominent figure in web development, open-source software, and data journalism, astutely notes, “Context is king. Most of the craft of getting good results out of an LLM comes down to managing its context.” [(Kim and Yegge 118)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> At larger scales, retrieval-augmented generation (RAG) becomes your best friend. RAG works like a specialized search engine for your AI, letting it pull in the relevant pieces when needed. [(Kim and Yegge 121)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> So, giving a coding agent access to your RAG system, perhaps via MCP, will make it converge on correct answers faster. ... Boris Cherny, technical lead for Claude Code, said, “Agentic search outperformed [RAG] by a lot. This was surprising.” [(Kim and Yegge 122)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

### Key Practices

- Keep an eye on your AI’s context window.
- Recognize context saturation early.
- Use focused or comprehensive context.
- Explore tooling support.
- Trust your instincts.
  - _In the age of AI, I think more people need to hear this and embody it. As we stand up agents across the planet in all domains, the human spirit and good taste will be what stand between us and the machine._

[(Kim and Yegge 123)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

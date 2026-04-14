+++
tags = ['AI', 'Vibe Coding by Kim and Yegge', 'Learning', 'Articles', 'OpenClaw', 'Book Reviews']
title = 'Vibe Coding: Reward Function Trap'
date = 2026-04-14T17:35:07+01:00
draft = false
+++

Main Source: [_Vibe Coding: Building Production-Grade Software With GenAI, Chat, Agents, and Beyond_](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

## Hijacking the Reward Function

**TL;DR:** FAAFO makes vibe coding more addictive than any video game ever created. No longer is the question, “Can I do this?” It becomes, “Am I the best person to do it?” When we’re all builders, the humility to know when we should build versus when we should use someone else’s software becomes vital. I’m sure we all attempted to build our own agent framework, but now that we have OpenClaw, it’s time to build together. Embrace the Agent OS moment and ship our pieces.

> Baby-counting involves obvious omissions, whereas the cardboard muffin problem involves AI actively disguising incomplete or fake work as genuine completion. ... When facing constraints—limited context windows, complex requirements, or approaching output token limits—AI goes into crisis mode. [(Kim and Yegge 128)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> (AI model providers are working hard to reduce this problem. At the time of this writing, Anthropic released their Claude 4 models, which demonstrated a 65% reduction in these behaviors. That’s a promising improvement, but as the numbers show, reward hijacking still happens.) [(Kim and Yegge 129)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

**Goodhard's Law**

> "When a measure becomes a target, it ceases to be a good measure" [Source](https://en.wikipedia.org/wiki/Goodhart%27s_law)

My personal experience is that this is all but gone as of April 2026. My stack is Codex (always the latest OpenAI model), shell scripts, a few custom subagents (prompts with highly specific skills), and a few limited skills (I often modify and make a new skill per major repo I manage). Outside my environment, I’m unaware of the current state, but most of my gains over the past three months have been due to model improvements and Codex updates. _I’m currently exploring Pi and might have a new setup within two to three weeks based on present tests as of writing this._

> The TL;DR is that Google engineering appears to have the same AI adoption footprint as John Deere, the tractor company. Most of the industry has the same internal adoption curve: 20% agentic power users, 20% outright refusers, 60% still using Cursor or equivalent chat tool. It turns out Google has this curve too. [Source](https://simonwillison.net/2026/Apr/13/steve-yegge/#atom-everything)

> AI has seen the best practices, the most elegant patterns, and the most sophisticated implementations to solve problems. Yet when left to its own devices, it regularly ignores the right patterns and conventions, choosing instead to write tangled, unmaintainable code that “gets the job done.” [(Kim and Yegge 129)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> The problem is that LLMs inherently **lack the virtue of laziness**. Work costs nothing to an LLM. LLMs do not feel a need to optimize for their own (or anyone’s) future time, and will happily dump more and more onto a layercake of garbage. Left unchecked, LLMs will make systems larger, not better — appealing to perverse vanity metrics, perhaps, but at the cost of everything that matters. As such, LLMs highlight how essential our human laziness is: our finite time **forces** us to develop crisp abstractions in part because we don’t want to waste our (human!) time on the consequences of clunky ones. The best engineering is always borne of constraints, and the constraint of our time places limits on the cognitive load of the system that we’re willing to accept. This is what drives us to make the system _simpler_, despite its essential complexity. [Source](https://bcantrill.dtrace.org/2026/04/12/the-peril-of-laziness-lost/)

**Specification Gaming**

> One interesting type of unintended behavior is finding a way to game the specified objective... [Source](https://vkrakovna.wordpress.com/2018/04/02/specification-gaming-examples-in-ai)

This is why the engineer is not going away. Nor the human, for that matter, in most lines of work.

## Head Chef Mindset

Critical thinking, and the wisdom to know when we should delegate to agents and when we must maintain complete control, will be the determining factor moving forward.

> But once you understand AI’s inherent nondeterminism, with its unique strengths and weaknesses—like human assistants—you can adapt your approach accordingly. [(Kim and Yegge 136)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> The rewards are real and available today. But it does require putting in a bit of time and effort to unlock them. It’s not like taking a university-level technical course; vibe coding is nowhere near that difficult to learn if you’re already a programmer. But it will take some practice. [(Kim and Yegge 138)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> The AI is an _assistant_, not a driver, at least not with 2025 models. [(Kim and Yegge 139)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

Still true, and maybe more so. As we all deal with the code hangover, it becomes apparent who among us use agents as tools to supercharge our abilities, and who have merely supercharged shoddy thinking. When building can move 10x faster, it’s more important than ever to understand each logical assumption baked into the code. Technologies are easier than ever to use, but wisdom and sound thinking are arguably harder than ever with the [siren call](<https://en.wikipedia.org/wiki/Siren_(mythology)>) from agents. The risk is not that the broom can carry water; it’s that the apprentice doesn’t know how to stop it. Vibe coding has a real [Sorcerer’s Apprentice](https://en.wikipedia.org/wiki/The_Sorcerer%27s_Apprentice) problem.

> Blaming AI also won’t result in any organizational learnings, or address the root cause, which is that, when it breaks things, engineers aren’t using it correctly. ... Practically, this means reviewing, validating, and testing that code more than usual—especially for code that is security-sensitive, performance-critical, or where absolute correctness is required. [(Kim and Yegge 140)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> But great software has never been built by dumping vague goals onto someone and walking away. It comes from creating clear specifications that decompose big problems into manageable pieces. [(Kim and Yegge 140)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

With the power of agents, both for coding and research, the path from junior to senior has never been clearer; while at the exact same time, it has become perilous, as the temptation to use coding agents as a crutch (_not unlike Stack Overflow copy-pasting was_) has become all too easy to fall for. The opportunity for self-education (_if there was ever an alternative_) has never been easier, but it means going deeper. I personally discover new patterns and possible functionality built into Python (my main language) on a weekly basis by exploring the problem space with my agents. Use them as a tutor, and then verify their assertions with primary documentation. It’s a Google search away; or your agent can provide a link. Primary source referencing has never been easier. Make it the required standard.

> Every time AI modality shifts—completions, chats, chat agents, clusters of agents—we all reset our speed gauges back to “who knows.” ... AI-assisted development may be significantly faster, but the exact speedup varies. Calibrate conservatively and multiply your optimistic estimate by five. [(Kim and Yegge 148)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> When you vibe code with coding agents, you’re no longer a solo developer. You and your coding agents are now a development _team_. [(Kim and Yegge 150)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

The core point is that the human shipping the code owns the outcomes and responsibilities when it goes wrong. Don’t spam Enter and commit without understanding what you’ve made.

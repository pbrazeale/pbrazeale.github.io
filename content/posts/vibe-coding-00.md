+++
tags = ['AI', 'Vibe Coding by Kim and Yegge', 'Learning', 'Articles', 'OpenClaw', 'Book Reviews']
title = 'Vibe Coding Changes the Economics of Building'
date = 2026-03-28T09:05:07+01:00
draft = false
+++

Main Source: [Vibe Coding: Building Production-Grade Software With GenAI, Chat, Agents, and Beyond](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

**Vibe coding** is more than “using AI to write code faster.” It's a shift in the economics, responsibilities, and creative scope of software work.

It increases what an individual can attempt. The developer’s role is morphing from line-by-line implementer to director/operator, creating new possibilities _provided it is approached with discipline_.

> **Gene Kim** is a multiple award-winning CTO, Tripwire founder, Visible Ops co-author, IT Ops/Security Researcher, Theory of Constraints Jonah, a certified IS auditor and a rabid UX fan. [source](https://www.goodreads.com/author/show/328437.Gene_Kim)

> **Steve Yegge** is ex-Geoworks, ex-Amazon, ex-Google, ex-Grab, and ex-Sourcegraph, with over 30 years of tech industry experience, 40 years coding total. [source](https://steve-yegge.medium.com/)

Together, the two have captured the zeitgeist and distilled the core essence of **vibe coding**, providing a clear, structured path to embrace the new style of work on a spectrum from **embrace the exponentials** to **head chef**.

> Here’s what it means to embrace the exponentials, again from Mat Velloso: “This year, very likely AI will surpass human ability in coding. It’s happening. Just like it crossed the bar in many other things before (playing Chess, Go, etc.).” [(Kim and Yegge 51)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

## Forward

Offers exceptional insight on the transition by Dario Amodei, CEO and Co-founder of Anthropic (July 2025).

> At my company, we train the models (like Claude) and the coding agents (like Claude Code), and then use them to improve future versions of themselves. It’s all part of what we’ve seen for a few years now: a smooth exponential of accelerating AI progress, where things become unrecognizable rather quickly, even compared to a few months beforehand. The sudden arrival of vibe coding is a qualitative shift in how we work, but it’s also part of a relentless upward spiral of AI capabilities that shows no sign of slowing down. [(Amodei XV)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

At the time of writing this, it's March 2026, and the flywheel Amodei and his teams within Anthropic saw a year ago is now at the fingertips of any software engineer, and most people, if they embrace the new paradigm and learn to use the tools as we once learned to use IDEs.

> Old-style coding by hand seems pointless. [(Kim and Yegge 24)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

No longer are engineers limited by the economics of potential failure. Experimentation and ideation are merging. We're approaching the point where the cost of shipping code will approach the cost of electricity and storage. This will result in an explosion of software that will make the 2010s boom seem quaint. [See: Jevons Paradox](https://en.wikipedia.org/wiki/Jevons_paradox)

> Vibe coding is a whole new way of working: We should expect to see entirely new, economy-boosting advances in software and engineering as a result.[(Amodei XV)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> Take it from someone who employs many of the best coders in the world: The “vibe coding” way of working is here to stay. [(Amodei XV)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

## Preface

> In short, we believe vibe coding may be the best thing that happened to developers since…well, ever.
>
> It reminds us of what happened in the 1990s. Early adopters who recognized the importance of the internet became unstoppable and turned into companies like the legendary FAANGs (Facebook, Amazon, Apple, Netflix, Google), while skeptics dismissed the transformation as hype. [(Kim and Yegge xix)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

I've been arguing that this new opportunity is the same kind of moment as the '94 internet revolution; and now, with NemoClaw's drop, I'm using Jensen Huang's explanation that it's a new operating system moment. [NVIDIA GTC Keynote 2026](https://www.youtube.com/live/jw_o0xr8MWU?si=9XeOgol1D7IFY4a7)

The way I see it, we're all moving from the days of command-line OS interfaces to the Windows 3.1 moment. Likewise, our interface with agents is evolving from chat and CLI to full-fledged OS interfacing. The future is here. We will soon speak to "Computer" like Star Trek and watch as drudgery is handled for us.

But to get there will require thousands of developer-years, and this book will help us all get there faster.

> While some of the finer details may be outdated by the time you read this—that’s the price of exponential change—the core principles we share have remained consistent even as we’ve evolved from chat-based coding to autonomous agents to coordinating groups of agents. [(Kim and Yegge xxi)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

## Introduction

>  in 2024, Dr. Meijer gleefully made this striking and startling declaration: "The days of writing code by hand are coming to an end." [(Kim and Yegge xxiii)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

How true. This prophetic declaration is nearly complete. As for my own work, I find myself writing 1–3% of shipped production code. And this is for full systems used for real business needs, not prototypes or demos.

> At Adidas, seven hundred developers using AI coding tools reported a 50% increase in what they call “Happy Time”—hours spent on creative work they enjoy, rather than wrestling with brittle tests or debugging trivial errors. High-performing teams now spend 70% of their time directly coding, compared to 30% for teams using traditional methods. [(Kim and Yegge xxiii)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

This is the core concept behind Kim and Yegge's coined term **FAAFO**. The ability to stay in the "Happy Time" turns programming into a more addictive feedback loop than any video game I've played (_unless we're counting chess.com, despite my abysmal ELO_).

> _vibe coding_. It was coined by the legendary Dr. Andrej Karpathy [(Kim and Yegge xxiv)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

It's one of those perfect terms where, the moment you hear it, you wonder how any other term could be used. Not unlike Shakespeare creating “eyeball.” _What did our ancestors call it? Flesh orb of sight? LOL_

Approaching it again from the video game view, it's a process by which we can enter pure flow, even when failing, and come out the other side with days of work condensed into a single session. _Though Kim and Yegge will cover the dark side of what happens when we stay in that addictive flow state too long, without the proper guardrails for ourselves and the agents._

> In 2021, we saw AI-generated *code completions*, where the IDE (integrated developer environment) would auto-complete code based on what you had typed [(Kim and Yegge xxiv)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> *Agentic coding* (where AI autonomously generates, refines, and manages code) appeared in early 2025 [(Kim and Yegge xxv)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> We and many others have felt that, at times, you can be 10x more productive with vibe coding compared to manual coding. [(Kim and Yegge xxvi)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

While I was not there for the 2021 days, I can attest that by Nov. 2025 I was using agentic coding at all times, and by Jan. 2026, I reached the point where 97%+ of code was being written by agents. If, by some chance, you've not tried to embrace the exponentials and let an agent build you a module or even a full side project, stop reading this now and go try. _Or read the book, and then try with the right skill set to avoid the pitfalls._

### FAAFO

> Vibe coding lets you build things *faster*, be more *ambitious* about what you can build, build things more *autonomously*, have more *fun*, and explore more *options*. This is what we’re calling FAAFO [(Kim and Yegge xxvii)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> FAAFO framework—fast, ambitious, autonomous, fun, and optionality—the five superpowers vibe coding bestows upon you. [(Kim and Yegge 2)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

By embracing the agentic method of coding—"vibe coding"—you'll unlock more than increased enjoyment. You'll literally produce faster and better code, provided you follow a structured framework. At the end of the day, it's a technology for exponentially increasing the processes you run. _Be that technological or mental._ If you have bad habits, especially in your codebase, agents will expand upon them. The good news is that you, and your agents, can learn best practices, and it has never been easier to adhere to them. No longer are testing and documentation bureaucratic bottlenecks to shipping. Instead, they've morphed into the tools that help you reach 10x and beyond productivity.

### Steve's Journey

> I’ve been in the industry for over thirty years, including almost twenty years at Amazon and Google. ... At Google, I took productivity head-on by leading the creation of Kythe, a rich knowledge base for understanding source code. ... But by early 2024, I had started to worry that I could no longer make good decisions as a technology leader unless I deeply understood the radical technology change that was transpiring. [(Kim and Yegge xxi)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

> He coded in Java without an IDE until 2011 and refused to learn Git until 2021. Steve is a bona fide late adopter.[(Kim and Yegge xl)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

Steve's journey is beyond impressive, and him sharing his journey from skeptic to believer throughout this book will, I hope, put to rest the doubts I still hear thrown around by industry veterans—and worse, by those no longer in the industry at all. The revolution is here. It's gaining speed as every engineer throws proverbial coal into the furnace, and those who miss out now will be left behind. There is no longer the option to wait and see. **Wait and watch the future of software development leave you behind.**

### Gene's Journey

> My journey with software began when I created a UNIX security tool during an independent study project at Purdue University in 1992, which was later commercialized as Tripwire. ... Throughout the development of this book, I vibe coded tools to help in the writing process. [(Kim and Yegge xxxiii-xxiv)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

Throughout this book, there are pertinent points about the new revolution and how it will reshape the meaning of work as the workplace itself is forced to adapt. I kept finding myself nodding along, or thinking, "_I've literally argued that point!_" Pure brilliance permeates this text.

It wasn't until nearly the end of the book that I found out Gene co-authored [Wiring the Winning Organization](https://www.goodreads.com/book/show/125164532-wiring-the-winning-organization), and I suspect this was a huge influence—and one reason behind _Vibe Coding_ making such poignant insights on how the workplace will change. How I will make the time, I don't know, but I will read his other book.

### Everyone's Journey

> The coding revolution is still in its early days.[(Kim and Yegge xxxv)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

The book was published October 21, 2025; assuming the standard six-month editing window, that would place the writing of this statement at the beginning of 2025. In that year, the revolution happened, built steam, and unified into a cohesive vision _now known as OpenClaw_.

If you read this book and walk away thinking you've got time, we're in complete disagreement. Those who've let the vibe coding moment slip past them are playing catch-up as we transition into full-fledged agentification.

> The dirty secret of programming has always been that implementation details and busywork consume most of our time, leaving precious little for creation and problem-solving. [(Kim and Yegge xxxv)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

#### Hype Train

> Steve is not someone who yields readily to hype. Most of his favorite tech is from the mid-to-late 1990s. ... New technologies often have a lot of bugs, and Steve, who has seen many frameworks come and go, prefers to spend his time solving user problems rather than debugging new tech. ... The skills that made developers valuable yesterday are not the same ones that will matter tomorrow. And we both believe one thing with absolute certainty: If you don’t adapt to this shift, you may become irrelevant. [(Kim and Yegge xl)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

I hope I've made my biases known. I'm fully onboard with the vision of the future: that we can achieve Star Trek, at least where the laws of physics aren't broken without some as-yet-unknown technology. So maybe not teleporters, but we will get computers that handle all the drudgery and unlock rapidly increasing economic growth because of it, leading to rapid distribution of abundance.

The future is change. And that change is upon you, whether you embrace it or not.

> "May you live in interesting times" [source](https://en.wikipedia.org/wiki/May_you_live_in_interesting_times)

Is in fact not a curse, but rather an opportunity to embrace the transition and flourish.

To see that the hype and fear cycle is cyclical, and the underlying needs haven't changed, you can read this Forbes article from May 31, 1999: [Dig more coal -- the PCs are coming](https://www.forbes.com/forbes/1999/0531/6311070a.html)

## The Plan

I intend to continue this series in a structured format following Kim and Yegge's four-part layout, and then beyond that as I formulate my personal experience and insights into actionable articles.

In no way, shape, or form should these articles be taken as the endpoint. My hope is that by reading these, and getting my point of view on the matter, you'll be encouraged to buy a copy for yourself, read it, and write your own notes. [Vibe Coding: Building Production-Grade Software With GenAI, Chat, Agents, and Beyond](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

When writing my notes, I skipped over chunks of this book that I felt weren't relevant to my needs or that didn't resonate.

As we'll all start using these practices for thousands of hours over the next few years, it seems an obvious tradeoff to buy the book and learn directly from brighter minds than me. **Gene Kim** and **Steve Yegge** have condensed hundreds of hours of research and experimentation into an easily digestible format.

### Continued Articles

[Vibe Coding Changes the Economics of Building](https://pbrazeale.github.io/posts/vibe-coding-00/)

+++
tags = ['AI', 'LLM']
title = 'Promotion Update: AI Engineering Lead at World Parts Direct'
date = 2026-02-16T10:00:00-06:00
draft = false
+++

Today I’m stepping into a new role at [**World Parts Direct**](https://www.worldpartsdirect.com/) as **AI Engineering Lead**; same mission as before (make customer support faster, cheaper, and less painful); more ownership now (architecture, roadmap, and making sure the whole system holds together under real production pressure).

If you’ve followed any of my recent work, you already know the theme: **ship practical automation that actually works**, then measure it, harden it, and scale it.

---

## New Role

Being an “AI Engineer” can mean a lot of things; in my case it’s not “let’s duct tape a chatbot onto a helpdesk” (_no thanks_); it’s building an **end-to-end automation system** that can reliably handle real customer conversations, integrate with the tooling we already use, and escalate cleanly when the AI shouldn’t be the one answering.

As AI Engineering Lead, I’m accountable for:

- **System design & architecture**
- **Quality and reliability**.
- **Instrumentation & reporting**
- **Mentoring and execution velocity**
- **Cross-team alignment** (because AI work without stakeholder trust just becomes “the thing nobody wants to touch”).

---

## Core Focus

The next phase is less about “can we automate this?” and more about “can we **operate** this?”

**Meaning**:

### 1) Observability

I want a system where we can answer, instantly:

- What nodes ran?
- What model was called?
- What did it decide, and with what confidence?
  - Feedback loops from observational agents.
- What data did it see?
- What response was sent?
- Did the human override it (and why)?

If we can’t trace behavior, we can’t fix behavior; and we can’t scale.

### 2) Stronger feedback loops

Not just “the customer was mad”; but _what rule failed_; _what category was misfired_; _what policy boundary got crossed_; and _how do we prevent this exact failure class from happening again?_

That means structured labeling, bug taxonomy, and a review workflow that’s actually sustainable. And most importantly, provide metric driving reports to stakeholders to make informed decisions for the company.

### 3) More automation coverage

Coverage matters; but bad automation is worse than no automation.

The goal is to push coverage higher while keeping handoffs clean and intentional. With two core metrics to measure against, there's no reason the systems can't achieve our objectives within 120 days.

### 4) Team leverage

If I’m doing everything myself, we’re capped.

The lead role is about building systems that other engineers (and non-engineers) can extend safely; with Standard Operating Procedures (SOPs), tests, dashboards, and rules that keep the whole thing coherent.

---

## Driving Principles

A few rules I’ve learned the hard way:

- **Reliability beats novelty** (a boring system that works wins).
- **Measure everything** (or you’re just debating opinions).
- **Make failures legible** (fast diagnosis is half the battle).
- **Human handoff isn’t failure** (it’s a feature; the goal is the right answer, not AI vanity metrics).
- **Build components, not blobs** (small agents with clear contracts scale; mega-prompts rot).

---

## Appreciation

I’m grateful for the trust from leadership and the team; this is a real step up in responsibility, and I’m taking it seriously.

Also: I’m writing this down because it’s easy to get lost in the churn of tickets, metrics, and “just one more fix”; the point is to build something durable; something that keeps working even when volume spikes, edge cases show up, and priorities shift.

More updates soon; I’ll share what I can. Especially the stuff that’s generally useful to anyone building production automation with LLMs.

---

[**World Parts Direct**](https://www.worldpartsdirect.com/): guaranteed lowest prices OEM parts for GM and Mopar parts, with next day delivery options for over 100k items. Preowned parts for almost any make and model are also available, with identical warranties to new.

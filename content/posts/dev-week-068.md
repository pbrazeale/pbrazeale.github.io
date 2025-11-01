+++
tags = ['Developer Log', 'Learning', 'AI']
title = 'Developer Week 068'
date = 2025-11-01T15:14:27+01:00
draft = false
+++

## Books

[AI Engineering by Chip Huyen](https://www.oreilly.com/library/view/ai-engineering/9781098166298/) **Done**

[Courage is Calling by Ryan Holiday](https://www.goodreads.com/book/show/58145670-courage-is-calling) **DONE**
[Book Review: Courage is Calling by Ryan Holiday](https://pbrazeale.github.io/posts/book-review-courage-is-calling/)

[Prompt Engineering for LLMs by Berryman and Ziegler](https://www.goodreads.com/book/show/221244015-prompt-engineering-for-llms) (50/280) **~18%**

[Fluent Python by Luciano Ramalho](https://www.goodreads.com/book/show/54330869-fluent-python) (21/983) **~2%**

[Wisdom Takes Work by Ryan Holiday](https://www.goodreads.com/book/show/230422186-wisdom-takes-work) (260/400) **~52%**

[Discipline is Destiny by Ryan Holiday](https://www.goodreads.com/book/show/60018575-discipline-is-destiny) (116/312) **~37%~**

## Work Log

Received my 90-day review last week and presented my impact report, showcasing what I managed to build in 10 weeks (_3 weeks of my first 90-days was spent on marketing efforts and not AI_). Overall it went well; my title has been updated to `AI Automation Engineer I`.

My CEO and COO also provided a clear checklist of AI systems to build and minimum performance metrics to meet to earn a promotion to `AI Automation Engineer II`. All of which are achievable and fell within my 6 to 9 month roadmap in my impact report.

The past two weeks have been spent building the foundational backend requirements for the new SMS agent system, along with fleshing out the performance requirements with the stakeholders. I've now read the API documentation for webhooks, events, and SMS at least three times. The original design was to modify the existing webhook. However, Monday I'll need to present my case clearly for the advantages to building a new webhook, given the event subscription design.

There were several bugs related to our current AI system's received JSON. With assistance from my CTO and insightful guidance, I'm back on track and was able to patch all the bugs while also creating a more elegant system for preventing the bugs moving forward.

Database broke due to an emjoi encoding error. Was able to resolve the bug, after my CTO found the root cause in 30 seconds while I was still looking to the db LOL. _I have much to learn!_

Stackoverflow helped solve my issue quick:
[Difference between utf8mb4_unicode_ci and utf8mb4_unicode_520_ci collations in MariaDB/MySQL?](https://stackoverflow.com/questions/37307146/difference-between-utf8mb4-unicode-ci-and-utf8mb4-unicode-520-ci-collations-in-m)

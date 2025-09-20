+++
tags = ['Developer Log', 'AI', 'Python', 'Learning']
title = 'Developer Week 062'
date = 2025-09-19T20:45:07+01:00
draft = true
+++

## Projects

### SARAH: Story Analysis & Revision AI Helper

**New Site Design**
![Sarah Hero](https://pbrazeale.github.io/images/SARAH_hero_page.jpg)

Wrote a full article ([SARAH UI Redesign](https://pbrazeale.github.io/posts/04-sarah-build-notes/)) about the process and objective for the SaaS launch in mid October.

## Books

[AI Engineering by Chip Huyen](https://www.oreilly.com/library/view/ai-engineering/9781098166298/) (113/521) **~22%**

- [NOTES: AI Engineering by Chip Huyen: Chapter 1](https://pbrazeale.github.io/posts/01-ai-engineering/)
- [NOTES: AI Engineering by Chip Huyen: Chapter 2](https://pbrazeale.github.io/posts/02-ai-engineering/)
- I'm really enjoying this book, and look forward to finishing it. However, I'll go on pause as I start a new book for work.

[Designing Software Architectures: A Practical Approach by Cervantes and Kazman](https://www.goodreads.com/book/show/27283384-designing-software-architectures) **0%**

- It should be here Sunday and I'm going to tare into it. As usual I'll post my notes and major takeaways here.

## Work Log

I ended up in the ER on 9/6 with walking pneumonia. My O₂ levels were in the low 80s, and it was nearly impossible to keep my eyes open. The brain fog was so severe that I struggled to answer the most basic questions: name, address, date of birth. Thankfully, the staff immediately jumped into action and started pushing IV fluids and antibiotics. By Tuesday morning, 9/9, I was cleared to leave the hospital with a full round of antibiotics and an Albuterol inhaler to keep my airway clear.

All told, I coughed up over 400 ml of mucus from my lungs while in the hospital. Even as I write this, I’m still dealing with random coughing spells that produce more mucus. I’ve coughed so hard that I’ve strained the muscles around my solar plexus.

_“That which does not kill us makes us stronger.”_ ― Friedrich Nietzsche

To help make up for the missed days, I put in solid 10 hour days this week, and will likely do the same next week. Though of course I've already been putting in over time since day one when I started. Regardless, I think it's the honorable thing to try and close the gap and get the projects back on track. I've never worked so feverously as I did Tuesday to get my agents back online. Call it pride or honor, but I took it as a personal failure to know they had to take them offline whilst I was out. (Even if my absence was fully justified, and unavoidable.)

---

### Tue 9/9

- Left the hospital around 10:15 and started organizing discussions to get my agents back online by 11:30.
- Updated the AI agent server to the latest stable version.
- Submitted a PR for the counteroffer API.
  - Approved, and agents turned back on!
  - Fixed a JSON bug in the CS Orchestration Agent.
- Fixed an Amazon bug for v2.0 Returns Agent counteroffers.

### Wed 9/10

- Updated the Warranty Agent to handle highly detailed denial messages with quoted reasoning from the warranty manual.
- Created an agent to convert HTML → inline plain text format.
  - This will be useful in many workflows.
- Submitted v2 Return Agent for final approval.
- Submitted a proposal to leverage vapi.ai to build a blue-ocean warm lead sales associate.
- Launched v2 Return Agent.
- Fixed the Amazon Order Number bug (again).
- Drafted the v2 Returns Agent announcement.
- Started a Vapi project to handle abandoned carts.

### Thu 9/11

- Fixed a counteroffer bug with the help of our CTO.
- Reran the failed execution from overnight.
  - Still maintaining a sub-2% failure rate.
  - Not sure I can get below 1% given the APIs I’m hitting and the occasional LLM hallucinations.
- Submitted a report to the CEO and COO outlining a new abandoned cart policy expansion, and proposed using Vapi to move leads from “warm” to “hot” for CS Reps to close.
- Pair-coded with our CTO, who identified the root cause of the Amazon Order Number message queue issue by tracing the DB calls and finding where a misformatted email address caused the conflict.
  - My bug fix had been a step in the right direction but didn’t resolve the root problem.
  - Learned a valuable lesson about testing full workflows. Had I done so the first time, I would have at least seen there was still an underlying issue. (Even our CTO admitted it was a tricky one, and he’s a brilliant engineer.)
- Met with our Shipping Manager to get buy-in on the Vapi AI agent for converting abandoned carts into hot leads.
- Figured out how to force custom CSS and HTML on RevParts custom pages so our Marketer can create more content-rich “blog post” style articles.
  - Built tools so he can write posts and easily copy them in HTML format to post directly into the site’s special framework.
- Tested the first steps of Vapi and got the first agent version running.
  - Still need to build out the DB table and access the API endpoint via a cron job (M–F, 9–16).
  - First phone call went well and proved the concept, though there are still plenty of kinks to iron out (_like teaching the AI to identify the customer name—LOL_).

### Fri 9/12

- Explained my Vapi decisions to the COO and walked through my decision-making process to maximize impact with limited time and resources.
  - Upper management seems to be embracing the idea of giving me more autonomy to pursue projects I believe have the best ROI relative to dev time. We keep using the phrase “low-hanging fruit” as we target the 80/20 projects first. There’s so much room for automation and efficiency gains.
  - Toward this end, I’ve begun compiling a report for my 90-day review, tracking the bottom-line revenue and profit impact of my work. My goal is to quantify my ROI to the company and (hopefully) prove my worth enough to earn a promotion to full-fledged AI Engineer.
- Began the image project for the WPD site. Looked into the database structure.
  - Pulled down a CSV metadata representation of the S3 buckets.
  - Ran initial tests and saw <10% success.
  - Planning an AI Agent to process and validate the 382,000+ images.
- Built out three VIN Check APIs:
  - Create the initial queue check.
  - Pull the updated queue for completed VIN Checks.
  - Upsert when completed to prevent duplicate Replyco messaging.
- Built the AI Agent framework to leverage the new APIs.
  - Still needs extensive testing before rollout to production. And of course, our CTO must sign off on the PRs I’ll submit Monday morning. (_Never push on Fridays—LOL_).

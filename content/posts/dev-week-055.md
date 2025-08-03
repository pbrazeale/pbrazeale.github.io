+++
tags = ['Developer Log', 'AI']
title = 'Developer Week 055'
date = 2025-08-03T07:05:07+01:00
draft = false
+++

![Developer Week 055](https://pbrazeale.github.io/images/devweek055.jpg)

## Books

[AI Engineering by Chip Huyen](https://www.oreilly.com/library/view/ai-engineering/9781098166298/) (20/521) **~4%**

[NOTES: AI Engineering by Chip Huyen: Preface](https://pbrazeale.github.io/posts/00-ai-engineering/)

![3 Key Levers](https://pbrazeale.github.io/images/model_three_keys.jpg)

## Work Log

[World Parts Direct](https://www.worldpartsdirect.com/)

Designed and implemented a new Customer Service Agent Orchestration Workflow, reducing average response times by 47% from ~17 seconds to ~9 seconds, while increasing message coverage by over 10X, and reducing LLM costs by optimizing prompts and proper model selection.

### Mon 7/28

- Learned Jira basics and planned out my first two week sprint
- Redesigned the AI Agent Orchestration workflow
- Began the process of prompt refinement

### Tue 7/29

- Learned Postman basics for API testing
- Restructured JSON objects for Agent data processing
- Reflowed to allow for sub-agent orchestration.
  - Checked data flow to test/verify JSON objects arrive as expected throughout pipeline.
- Created a sku Availability agent

### Wed 7/30

- Identified a `thread_ID` bug and fixed
- Implemented the new API for calling o4-mini from our own backend.
- Reflowed the Availability Agent and reached functional state.
  - Will be ready to turn on and ship within 3 days!
- Finished Postman course and setup tests for our internal APIs
  ![YouYube Tutorial](https://img.youtube.com/vi/zp5Jh2FIpF0/maxresdefault.jpg)

### Thu 7/31

- Finalized `order_status_update` Agent workflow
- Launched the full workflow (superior to past version)
  - Went live with only one minor bug.
- Created a new `kill_request` flow to prevent spam and system messages
- Modified prompt to stop `other` as a category
- Updating categories based on the historical data provided to me by Matt

### Fri 8/1

- Created the order `cancellation_request` agent scaffolding
  - Received MVP diagram approval from Chris
- Proactively monitoring the live agent, and modifying orchestrator agent to tweak outcomes as needed. (e.g. `kill_request` for FB notifications)
- Created `order_complaint` category
- Stayed late to fix `order_status` agent bug that I discovered.

### Sat 8/2

- logged errors and prepared testing to first thing Monday morning.

## Courses

### Boot.Dev Back-end Developer Career Path (~73.83%) (📈 +0.59%)

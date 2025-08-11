+++
tags = ['Developer Log', 'AI', 'API', 'Litestar']
title = 'Developer Week 056'
date = 2025-08-11T07:05:07+01:00
draft = false
+++

![Developer Week 056](https://pbrazeale.github.io/images/devweek056.jpg)

## Courses

### Litestar

[Litestar Docs](https://docs.litestar.dev/latest/usage/index.html)
This what we use at work, and I'm holding up projects by not being able to build out APIs by myself. For the foreseeable future this is my main learning focus per day.

I'm about 25% done with the tutorial section.
[Litestar Tutorial](https://docs.litestar.dev/latest/tutorials/index.html)

## Work Log

[World Parts Direct](https://www.worldpartsdirect.com/)

### Mon 8/4

- Two `order_status_update` errors occurred over the weekend.
  - I proactively identified the root cause in the pipeline.
    - Tested through the pipeline to verify.
  - Wrote new rule sets, and pushed to production.
    - Tested Solution, and passed!

### Tue 8/5

- Pair-coded with Matt (_my CTO_) most of the day. He's a beast!
- Dug deeper into [Litetar documentation](https://docs.litestar.dev/2/).
  - Plan to build out a few tutorials to get more accustomed to API design.

### Wed 8/6

- Began building out an AI script to process product data and turn it into a finalized product description.
  - Forced AI to follow [Schema.org](https://schema.org/) format inside a JSON output HTML wrapped description field.

### Thu 8/7

- Got approve for product description output from all stake holders ands tarted the batch runs. ETA ~40 hours of compute time
  - gpt-5 dropped!!!!
    - Spent a solid hour playing with the API.
    - Dropped the ETA to ~28 hours, and increased the quality of the outputs for a negligible increase in cost.

### Fri 8/8

- Updated the Product Description script to run asynchronously
  - Finished out first group of ~28,000
- Began work on next AI agent workflow.
  - Got the bird's-eye view rundown from Cameron our Director of Administration, to understand how it'll assist the teams under him.
- Modified prompt to address new product line and Utilize .pdf reference tables

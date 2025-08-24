+++
tags = ['Developer Log', 'AI']
title = 'Developer Week 058'
date = 2025-08-24T09:05:07+01:00
draft = false
+++

## Work Log

It took about 30 days, but I finally feel comfortable in my role. That's not to say there isn't plenty left to learn, but I'm confident that my impact on the company is going to show up on the bottom line presently. By my calculations the agents I've built should be addressing ~12% of total Customer Service requests received company wide.

While I'm obviously biased, I am impressed and pleased with the quality of responses produced by the agents. And aside from a few growing pains at first, the agents respond in such a helpful and polite manner that customers are satisfied; often sending "thank you" replies. For my personal metric of subjective value, that's the gold mark.

Monday I'll know if I've improved enough on building APIs. I'm not sure my bottleneck is Litestar anymore, but more so the technologies we're using the bring together all the dbs. Hopefully my PR feedback will illuminate the unknown unknowns and I'll make another leap forward.

Overall love my job, and the puzzles I get to solve every day are highly engaging. I'm at the right difficulty level where I can easily fall into the flow state most days.

### Mon 8/18

- Upgraded all Agents to change API calls from WPD -> OpenAI, to OpenAI's API directly.
- BUG: Return Agent double responding, lacking Replyco thread context.
- Built an API endpoint.
  - PR rejected.
    - Solution was to change the order object at the source of the initial message queue.

### Tue 8/19

- Updated C.S. Agent Discord notifications per co-worker's request
- Modified JSON
- Submitted PR for filtered_orders()
  - Rejected. CTO had a far better approach to solving this issue!

### Wed 8/20

- Identified order JSON bug and began testing.
- Met with CEO to discuss Agent progress and identify the next steps.
- Submitted PR for fetch_all_order()
  - First PR failed to meet standards; submitted 2nd PR, a refactored version.
    - Second PR was partially accepted, CTO saved my butt by changing where I handled the db call to minimize the number of rows returned. Else my version would have bogged down the server and slowed everyone's requests.
- Updated all agents to use the new order data structure
- Updated Discord notifications

### Thu 8/21

- Addressed failed API calls, updated server, and reset.
- Built an Order Status Update Agent v2.0 to make refined decisions with far more context provided by the new order data and shipping data structures.
  - Met with C.S. Management to go over the design.
    - Redesigned agent response windows
  - Create new flows to allow the agent more autonomy
  - Updated Notification Channels
  - Launched before Friday!

### Fri 8/22

- Order Status Update Agent's first batch of live data worked well.
  - Fixed a few small subpar performances around message formatting.
- Submitted PR for first ever API endpoint built 100% by myself. (_fingers crossed_) To be reviewed/implemented Monday obviously LOL
- Began the counteroffer agent to reduce returns and increase overall profit margins.

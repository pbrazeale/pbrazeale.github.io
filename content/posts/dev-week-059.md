+++
tags = ['Developer Log', 'AI']
title = 'Developer Week 059'
date = 2025-09-10T09:05:07+01:00
draft = false
+++

## Work Log

My most productive week yet. I've finally learned enough about the company that I can move with a quickness between all the department meetings I'm having and the feedback from coworkers is that they're thrilled with the amount of questions I ask to proactively learn all the departments and policies; which in turn translates to more efficient agents. They can only do what I understand.

Will continue to keep my nose to the grindstone, but I feel that I've fully "on-boarded" and am able to move through my sections of the codebase with ease. The amount of progress I make each day compared to what I was making in the first weeks is a night and day difference.

### Sun 8/24

- Checked in on the new Agent's alerts. Found an urgent request with a flagged 48 hour time limit and forwarded it along to the correct managers.

### Mon 8/25

- Closed two bug tickets clustered around the agents responding too quickly.
- Updated Return Agent to move forward the counteroffer options.
- Began designing the VIN Check Agent
- Modified Supervisor alerts to prevent false positives. Was an issue around lack of context in the messages, and the agent perceived that to mean a Supervisor was needed.
- Met with Admin Direcotor and Shipping Manager about the agent Customer Serivice notification system on delayed forged packages. Turned out to be an error with Customer Service team not communicating with the shipping team. Adding in a new field for the agents to use and notify the CS team more.
- Met with CTO and went over my PRs. 1 denied and fully rewritten/redesigned to use a new model for the API. The 2nd was fully approved for the replyco message queue (only feedback was to change single quotes to double quotes).

### Tue 8/26

- Address Amazon order number not coming through to the agent via API JSON
  - Pair programmed with CTO who fixed it.
- Meeting with Admin Director about GM OVN and other Agent needs
  - He'll confer with COO about VIP list
  - Possible Task level breakdown notifications
- Fixed bug Part Eval sending dead-end messages.
- Created Shipping Address Update Agent
- Meeting with Admin Director to assist with Aqua/Shelly doorbell setup.
  - Appears to be an issue with the network, or the physical device is not setup properly (can't test remotely)
- Meeting with CEO to address the agent status.
  - Backburnered the Discord bot expansion
  - Confirmed Returns Agent expansion
  - Verified I should ignore Discord server reorganization

### Wed 8/27

- Aqua doorbell/Shelly closed out. Admin Director figured it out intigration with Amazon Alexa.
- Built out the counteroffer agent with the Returns Agent
  - COO's Feedback sent the counteroffer design back to square one for the logic and algorithmic dollar amount. However, most of the Agent Response chain is salvageable.
- Built out new Formulas for counteroffer
- Meeting with Markerting for SEO and CSS page posts
  - Limitations of the website make blog posts not possible (actually doing site pages)
    - Need to compile the Aconite Cafe tools for him to use to boost SEO and Articles
- Reflowed P&L calculations for returns

### Thu 8/28

- Reran failed API calls. Our server seems to be hitting bumps.
- Submitted 3rd version of counter offer algorithm.
- Redesigned the entire Discord Notification system to land in new Forum Threads instead of the general Customer Service channel.
- Updated server to latest stable version.
- Made a new counteroffer agent workflow in accordance to COO's feedback.
- Updated the counteroffer API algorithms in accordance to COO's feedback.
- Feedback form COO & CEO means that the Returns Agent must start over.
  - Began the diagram and decision process for v2 Reruns Agent
  - Wrote the first new line.
- Logged in after hours to fix a JS error that caused an AI Agent run to fail.
  - Simple JS issue of not using ? to access object property.

### Fri 8/29

- Updated Discord notifications to use fallback to replyco thread id where the order number is not available for the title of the new Discord Thread.
- Finalized a Warranty Claims agent that's able to identify if the part in question is covered under the manufacture warranty, and how best assist the customer, including automatic denials where needed.
- BUG: Amazon Double response fixed, turned off a conflicting auto responder.
- Tested v2 Returns Agent and discovered underlining bugs related to Amazon order. Will have to hammer those out first before I can procced further.

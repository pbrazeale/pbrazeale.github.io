+++
tags = ['Developer Log', 'AI', 'Python', 'Learning']
title = 'Developer Week 063'
date = 2025-09-28T09:14:07+01:00
draft = false
+++

## Projects

### Time Tracker

[Time Tracker Repo](https://github.com/pbrazeale/Time-Tracker)

I built this for work after I couldn’t find a solution that wasn’t a subscription web app. First to track my hours on the clock; then to track **project-level timeframes** so I can hand upper management better estimates (fewer guesses; more receipts). It’s *local-first* (SQLite), set to **America/Chicago** (CST/CDT), and optimized for easy time tracking.

![Time Tracker Logo](https://pbrazeale.github.io/images/time_tracker_logo_300.jpg)

### Music Meta Tagger

[Music Meta Tagger Repo](https://github.com/pbrazeale/music_meta_tagger)

I needed a fast way to fix metadata for my Jellyfin music library, especially for indie albums that arrived with inconsistent tags. Jellyfin couldn’t reliably group or identify some of these releases because fields like Album Artist, Year, or Track numbers weren’t standardized. This tool let me normalize those tags in bulk so Jellyfin “understood” my indie albums and organized them correctly.

![Music Meta Tagger Logo](https://pbrazeale.github.io/images/music_meta_tagger_logo_300.jpg)

#### Description

Fix messy tags fast so media players stops guessing. **Music Meta Tagger** is a small Streamlit app for **bulk edits** across MP3/MP4/FLAC/WMA (Windows-friendly fields, including **0–5 star ratings**; works with local drives and UNC paths). You get a **200-row preview**, sane parsers/validators (only writes what you fill in), a progress bar, and per-file error reporting. Run it with Python 3.12 → `pip install -r requirements.txt` → `streamlit run app.py`. Want to help? PRs welcome—see the README.

---

## Books

[Designing Software Architectures: A Practical Approach by Cervantes and Kazman](https://www.goodreads.com/book/show/27283384-designing-software-architectures) (75/210) **~36%**

I started this book after a long code feedback session from my CTO where he provided brilliant insights into software architecture; specifically with how small to go with our modules.

And then literally the next day Stephen Samuelsen posted about how important it is for software engineers to start studying software architecture the moment they get their first position; just as DSA is vital for the first job, software architecture is vital for promotions and career advancement.

Checkout Stephen's: [The Most Exhaustive List of Software Engineering Books on YouTube](https://www.youtube.com/watch?v=nWaWE6Fibzg) for a curated list of books to read.

---

## Work Log

Brutal week. I clocked out Friday mentally fried.

Balancing my responsibilities for the AI Agents and trying to build out our full marketing strategy ASAP, while simultaneously training our marketer, has proven to be a few more spinning plates than I initially thought. I'm moving as fast as I can, but there's so much to get lined up in 15-20 days.

Typically a marketing strategy is designed, tested, and validated over six months. However, I don't have that kind of time.

I'm not going to put aside AI Engineering for that long.

Given my decade plus experience as a publisher (which is mostly a marketing and advertising role) I'm highly confident I've already identified our two target audiences for our marketing efforts. While I've not been able to validate with our own statistics as of yet; I've demonstrated our competitors efforts and backward engineered what I believe to be their strategy.

If all goes well, we'll be on track within 30 days. By 90 days we should have enough traction and stats for me to present that direct advertising is our next major opportunity.

I've already submitted my 15-day and 30-day plan of action. I'm fleshing out the 30-day, 60-day, and 90-day benchmarks for our marketer.

I’m writing up an exhaustive step-by-step operations manual for another team member to take over the oversight of the day-to-day marketing metrics and ensure we stay on track.

Still not 100% sure how to address the article edits and feedback for our marketer, as this is the only path forward (just as code reviews advance engineers). Wish I'd launched SARAH already, as converting her to offer feedback for articles and posts ought to be straight forward.

_Famous last words I know._

While I'm inching to get back to the engineering, I know how vital this project is to the long-term success of the organization, and I've already modeled what I expect the ROI to be at 6 months, 12 months, and 36 months; assuming growth matches what I've seen in publishing. Also, I hope that showing how effective I can be in 20 days on a project where I have deep expertise, will help articulate where I can grow to as a software engineer. Especially with AI, as the job requires creative writing and empathy skills, same as marketing, when understanding the models. _I think it's the number one reason my prompting skills are so sharp._

### Sun 9/21

- Submitted a brief memo to upper management about switching our standard model to Grok-4 Fast to save us about 66% on API costs. While maintaining the same quality customer support.

### Mon 9/22

- Had a personal event to handle in the morning, but managed to stay in message contact with the teams, and kept the new marketing project moving forward while I was out.
- Handled a critical bug with the VIN Check anent ending up in a circular loop when the customer was actually wanting a person to find a part on his behalf. New modified update fixed it, and should handle far more edge cases that don't fall into an actual VIN Check.
- Part of the VIN Check fix, was the way agent process replyco threads, so I updated every agent in the company to also use the new format. Only downside is it also meant manually updating every single prompt, and we're up to over 30 total agents.
  - Really kind of impressive when I step back and realize what I've built in such a short period of time. _Yet the bugs never end LOL_.
- Started my new marketing project.
  - Identified the core issues as I see them, as to why our marketing effort are lacking.
  - Found a solution to our indexing issue with google.
  - Submitted my 30-day action report on how I can oversee the reshaping of our marketing efforts and a step-by-step breakdown of how best to utilize our resources.

### Tue 9/23

- Rerunning failed executions and glitches for the agents.
  - Total failure rate is up to 1.9% this week, and I had gotten it down to 1.2%. I suppose that's the cost to pay for expanding into new agents.
    - Overall I consider this entire project to still be in Beta mode, as I've yet to finalize all the agents required for the orchestration agent to do it's job correctly.
      - Also once the agents are all created, I'll need to conduct another data analysis of the categories being hit, and reflow the entire orchestration to address the new design. Likewise, I'll have so much more real data by then, where as of now I've been using synthetic data for testing.
      - I think by the end of November I'll have a complete picture of the agent(s) and will be able to redesign the system with the hard won lessons. Meaning before the start of 2026, I'll have a true Version 1.0.0 live and leave the beta behind.
        - Excellent milestone, but also a huge step forward as I'll have to take radical ownership of all errors and glitches moving forward. (_Though even now I take ownership, even when it's outside of my control, since it's my responsibility to fix, patch, and repair anything that happens. Often under time crunch, which I'm sort of addicted to the adrenaline rush._)
  - This was a bit piled up, since I was out Monday morning, and didn't check when I got back in the afternoon, as I address a critical bug, and then had to switch to marketing.
  - Discovered VIN Check Bugs.
    1. Stellantis instead of Mopar
    2. List issue with part numbers
    3. Data pulled from wrong database, not most up to date, so a data check process was being skipped.
    - Took about 30 minutes to hunt down all the issues, but managed to fix them all.
- Digging deeper into the marketing project.
  - Got screaming frog to address our indexing issue.
    - Researching the full nuanced settings to get best results.
- BUG: Returns Agent entered an odd loop where it wouldn't accept a return request because it believed the human to be deceptive.
  - Probably correct flag, but the messaging lacks nuance, as we've hard guard railed the reply parameters, so it looks like an on repeat template email with slight tweaks.
  - Solution is the build out a counteroffer loop, where after a return response, there's an evaluation agent, and where the offer is being denied, despite deception on part of the customer, we just pass it to human CS Rep to finalize/deny.
  - _I love emergent behavior, it's like watching a toddler start to explore everything in sight! You never know what's going to happen next._
- Running first Screaming Frog index/report. ETA 28 hours.
  - LOL, software was running slow, despite having resources. Switched all my work to my PC and reduced ETA by 25%
- Submitted an updated report on our current marketing stats, and awaiting approval to fix what I see.
  - Received full approval, running forward with it.
- Error check 15:07
- Began the process of converting our baseline foundation model to Grok 4 Fast!
- Got back on late 9:00 - 10:00 PM, to check no the new site indexing software.
  - Running into issue with RAM limitations and I have 32GB! I've never seen a desktop application eat through memory like this. Presented a hardware solution, based on my RAM to page index calculation, but we'll see if they go for it.

### Wed 9/24

- Couldn't sleep, so I got on early today before 6:00 AM to check on the indexing software.
  - The tweaks I made last night allowed it to keep building the index, but the computer is screaming, running hot, and the CPU is pressing 80%, while the RAM is showing only 2GB left. Not sure if the crash will crash just the application, or my whole system, as I over allocated resources. Not advised, but I needed to test, and get more data for system requirements calculations.
- Only 1 execution failure overnight.
- Testing Grok 4 Fast as our new default foundation model. Showing promise, but still need to gather more data and test every single agents output to be sure.
  - Overall testing is showing a cost reduction of 68.4%
  - I can't identify any issue with the outputs, but there is a clear difference in the use of more periods for Grok where GPT uses more em dashes.
- BUG: VIN Check part number mistaken as VIN fixed by expanding out the message parsing and made the regex more strict.
- BUG: Missing part mistaken as an Order Status Update. Change the Orchestration Agent to send directly to the CS Team.
- Handled marketing related tasks for the majority of the day, as I assisted the Marketer in the use of the new software, and provided the 15-day, 30-day, and 60-day roadmap for the new marketing strategy I designed.
- Marketing strategy is moving forward full speed, and I'll have solid metrics by Monday.
  - As for the ROI outcomes that'll take 90+ days.

### Thu 9/25

- Marketing. Will the be majority of my work for the next few weeks.

### Fri 9/26

- Marketing.
  - Submitted updated report on site indexing. Current ETA is 13 more days `-_-` _I'm impatient._ I know what this is about to do for our company though, so I'm making myself relax and sitting on my hands.
    - With the forward momentum on my other strategies I expect to increase our organic sales by ~15% within 90 days, and ~70% within 365. Those are conservative numbers if they'll authorize direct advertising based around my target customer base that I'm actively proving.
  - Our COO requested an update, and I provided a partial update with the feedback that I'll submit a full report in two weeks when I have enough data, but made sure to provide enough details to keep him in the loop. Will do a better job keeping upper management looped in as I sprint forward on the marketing project.
    - Going to send a daily morning report that summarizes the prior day.

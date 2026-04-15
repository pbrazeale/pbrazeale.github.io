+++
tags = ['AI', 'Vibe Coding by Kim and Yegge', 'Learning', 'Articles', 'OpenClaw', 'Book Reviews']
title = 'Silent System-Boundary Failure in a Multi-Service Message Pipeline'
date = 2026-04-15T09:35:07+01:00
draft = true
+++

# Silent System-Boundary Failure in a Multi-Service Message Pipeline

It took me the better part of 10 days, but I solved a multi system bug, where the interplay between the systems exposed a critical bug that was failing silently as none of the dashboards indicated a drop in performance. i.e. charts kept growing, so the assumption was all systems were working.

This was a lie!

It was a system-boundary failure: a centralized email dashboard, an internal Python intake service, an automation workflow layer, and a phone/callback provider all appeared to be operating, while customer messages were silently falling through the gaps.

And all of this was discovered as I attempted to roll out a new message channel. Good thing too; else this might not have been found and solved.

## Initial Sign

I had been brought back due to the overall system not performing as well as when I'd left. Upon my first week back, before I'd had time to really get my head around the code base drift since I'd left, Operations reported rising workload.

I'd wrongfully assumed this was due to two key factors: automated system I'd built degrading, and business improvements.

The automation metrics did not show the same increase, due to multiple factors, and once the system was repaired, I'd written off the original concern.

#### First Key Lesson

> Listen to outside departments. They're almost always correct that there's smoke. When you think you've put the fire out, get confirmation.

While I got confirmation that workloads returned to manageable levels, I should have taken it upon myself to measure with quantifiable metrics the ratio before and after. Had I, this bug would have surfaced sooner.

## Scope

The system had five functional layers.

1. The centralized email dashboard & API server
2. The Python backend; which pulled threads and messages from that dashboard.
3. The form intake and phone callback provider handled special routing for callback requests and structured customer submissions.
4. The agent automation workflows platform classified those messages and automated most responses.
5. The internal database was supposed to be the durable source of truth beneath it all.

The weak point was the boundary between the external dashboard and the ingestion service.

#### Second Key Lesson

> Dashboards can report activity without reporting truth.

_Not going to lie, at times in this process I felt like [Jim Hawkins](https://en.wikipedia.org/wiki/Treasure_Planet) surfing the aether with no guarantee I'd find solid earth._

The queue assumed the dashboard API exposed new customer activity in the same shape the business needed to process it. In practice, the API behavior was: thread creation dates instead of activity updates.

That small assumption had large consequences.

The database was supposed to make the system observable. But when ingestion was incomplete, every downstream layer inherited the blind spot.

#### Third Key Lesson

> When ingestion is wrong, every downstream metric becomes suspect.

And because of how the systems interact; all systems appeared healthy.

The automation layer was failing loudly; the intake layer was failing quietly.

#### Fourth Key Lesson

> Always approach a system bug from first principles. Never trust what someone did before, nor the shared understanding of an outside system. API docs can lie!

## Logging

At that point, broad debugging stopped being useful.

The dashboards said the system was alive. The queues were running. The charts were still moving up and to the right. From the outside, nothing looked broken enough to explain what Operations was seeing.

So I changed the question.

I stopped asking, “Did the job run?”

I started asking, “Where did this specific message disappear?”

> At its core, observability is about these unknown-unknowns. [Source](https://charity.wtf/2020/03/03/observability-is-a-many-splendored-thing/)

That required a different kind of logging. Not more noise; better evidence.

Python’s logging system was the right tool because it gave me hierarchical loggers, severity levels, handlers, and separate output paths. In practice, that meant I could create focused logs for each subsystem without flooding the main process with every successful event.

I knew happy paths were working. I logged every possible failed path, and moved from them.

I added message lifecycle logs to prove when messages were seen.

I added drop-focused logs to capture when a message exited the normal path. I added route-specific logs for form intake, normal email flow, and phone callback handling. I expanded exception logs so provider failures included the actual response instead of a vague “something failed.”

_Keep in mind, at this point I had no idea that the issue was external. By all documentation it was supposed to be a bug on our end. And likely one I had made. High velocity comes with the drawbacks of fixing bugs._

I also split logs by subsystem, because one giant log file was annoying to read, as I used each file to represent a different segment point for where in the process the data was.

![Who disturbs my slumber](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fwww.quickmeme.com%2Fimg%2Fd5%2Fd5098f675369255409d119a975dfb5be3115ef5d0d00483d50c51ef5e5000673.jpg&f=1&nofb=1&ipt=5ee1dc73e09a69db37df04bc715e86ad0bda09c3496db223ca13e3f7f55e27ad)

One I built the API endpoints to see the logs in real-time; the whole system opened up to me. _It was as if I'd been driving in a tunnel with my headlights out and emerged into a bright valley floor._

#### Fifth Key Lesson

> Logging should be built alongside tests to track data as it moves though the system. Happy paths can be turned off, or consolidated into final counts, but gaps and failures can be seen faster.

## Falsifiable Test

> A scientific hypothesis must be based on observations and make a testable and reproducible prediction about reality, in a process beginning with an educated guess. If a hypothesis is repeatedly independently demonstrated by experiment to be true, it becomes a scientific theory [Source](https://en.wikipedia.org/wiki/Hypothesis)

Hypothesis:

- If the thread appeared in the intake logs, the internal system dropped it.
- If the thread never appeared, the third-party API was not returning data according to our assumption.

![Yeah Science!](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fmedia4.giphy.com%2Fmedia%2FQC7UQbxq89MnL9r6AN%2Fgiphy.gif&f=1&nofb=1&ipt=6fa272aee6cd3a6509413b3ed330917dbb5da28e8141363cca24bfcdab6cd203)

_Now I get it's a bit grandiose to discuss the systems test this way, but I was an author for a decode before switching to AI Engineering. This is the closest I've come to using the scientific method since college. And when it worked, I suddenly didn't feel so bad about the money I spent to have other tell me what books to read._

There was more that went into setting up the test; but the above is the gist of my hypothesis, and it worked.

Though testing to prove, and solving the problem, are two completely different problems!

The system treated thread freshness as message freshness. The API appeared to expose recently changed threads, when in fact it showed newly created threads. _And don't get me started on the fact that new threads aren't being created, but I can only write my code base._

### Backfill Verification

With my log evidence in hand; I presenting my findings to the top brass, along with a plan to verify _and at least temporarily_ patch it.

Enter the nifty little backfill script. Only draw back; it hammered the shit out of the API for over 14 hours (_before you scream; I was cognizant that main processes were still running. Backfill script batched small, 100 threads, 25 messages, 1 second sleep between steps, and 5 second delays between batches_); had to run it on a spare server away from my own network.

By systemically checking all thread for the past 365 days, I found tens of thousands of messages that had never reached the automation layer at all. _The log file is 51MB! So greping around to find an insight was out of the question._

That made the issue concrete. This was not a theoretical edge case, or a one-off integration glitch. Real customer messages had been sitting outside of system and not logged into the database.

That discovery also changed how the automation metrics had to be read. _At present my back of a napkin math indicates a 100X+ improvement in message cover for automation, and theoretically 100% coverage for database logging._ Missed messages created misleading queue metrics, which made the team underestimate inbound volume and overestimate automation coverage.

#### Sixth Key Lesson

> Spend more time designing tests when the bug is beyond a single module; and especially when it's entwined with multiple systems.

## Redesign

Broadened our pulling window to capture past 30 days of threads by default, rather than one day; as the API doesn't in fact fetch threads with new activity. Tested around this to balance out highest coverage without overwhelming the API server. Settled on 15 days as a happy medium.

#### Seventh Key Lesson

> First own the data; then automate against it.

Refined the API back offs and sleep cycles to match what I observed from the API sever. This is to create the system we must have, whilst being respectful of their server's resources.

Tested delays of messages at origin to hitting their server. Proved that the centralized email API server doesn't timestamp their messages upon received, but rather passes along timestamp from origin. _Yet another oddity uncovered, and assumption built into our code._ This too was dropping messages, due to our hashmap, but easy fix by modifying the hashmap and backtracking window.

#### Eighth Key Lesson

> Zero trust is not just for Security. Test and verify all system design claims.

Upgraded the hashmap to save itself as a sqlite3 file. This will prevent long start ups, as each new start was forced to build a new hashmap into memory. Still must be verified and rebuilt, but reduced build times from >84 minutes to <24 minutes (_When tested on my machine_). Still ill advised to restart the task unless needed, but none the less.

When tested on my machine, I saw CPU usage drop by >14% when running and ram demands drop by >300MB. _And with RAM prices where they are, each MB counts again!_

> Vibe coding increases your ability to explore options and mitigate risks before committing to decisions. [(Kim and Yegge 29)](https://www.goodreads.com/en/book/show/228438060-vibe-coding)

_Full article:_ [Vibe Coding: From Line Cook to Head Chef](https://pbrazeale.github.io/posts/vibe-coding-01/)

This entire redesign was actually my 3rd one, and I dare say the optimal one. Had I not taken the time to explore options, I wouldn't have found all the small fixes that lead to an optimal solution.

#### Ninth Key Lesson

> Explore the problem, and use multiple approaches before settling. Coding agents make it easier than every to build and test multiple approaches before having to settle on one.

#### Tenth Key Lesson

> In distributed systems, the boundary is often the bug.

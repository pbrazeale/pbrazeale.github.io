+++
tags = ['Developer Log', 'AI', 'Go', 'Sarah AI Line Editor']
title = 'Developer Week 051'
date = 2025-07-07T06:05:07+01:00
draft = false
+++

![Developer Week 051](https://pbrazeale.github.io/images/devweek051.jpg)

## Projects

### Sarah (AI Developmental Editor)

Finished my first personal project for Boot.dev. In the making it grew into a full fledged SaaS idea; so now I'm in the middle of learning basic web design and interfaces with FastAPI, Jinja, and Tailwind.css.

[https://github.com/pbrazeale/sarah](https://github.com/pbrazeale/sarah)

> Sarah is an **AI-powered editing assistant** designed to help fiction authors refine their manuscripts with professional-grade insights. It automates chapter parsing, beat sheet analysis, line editing, and developmental feedback to support your storytelling and publishing goals.

#### Key Learning Points

1. Us AI sooner as a review partner for code that's working as expected. _I can't count the number of typos Gemini caught for me that I overlooked. In large part due to renaming a variable and not updating it everywhere._
2. Learned about asynchronous processing and using `threading` to allow for an API call that will take too long to sit in a loop for.
   1. Paired with `itertools` and I was able to update my CLI interface with a loading screen.
   2. `spinner = itertools.cycle(['-', '/', '|', '\\'])`
   3. Far superior solution to waiting around and checking my API web portal to see if the call went through. Also can help cut down surprise bills.
3. There is no shame in setting aside the code base and starting over from the ground up with the knowledge gained from dead ends.
4. A project will take twice as long and 3 times as much coffee to accomplish compared to initial estimates.

## Courses

### Boot.Dev Back-end Developer Career Path (~66.45%) (📈 +3.76%)

#### 13. Learn Go (153/188)

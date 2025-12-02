+++
tags = ['Developer Log', 'AI', 'NovelFoundry']
title = 'Developer Week 072'
date = 2025-11-30T11:14:27+01:00
draft = false
+++

## NovelFoundry

Finalized my architectural decisions around how to divide up my SaaS hosting, and one big choice was to go with supabase for a managed postgreSQL. You can read a full breakdown of my research and decision process here: [NovelFoundry Database Structured For Day 0 and Day 1000](https://pbrazeale.github.io/posts/novelfoundry-build-log-01/)

The only part I have left to finalize on the database side is designing the actual table layouts to allow for the right scalability. I need to balance between user speed and file storage. Which means not everything goes into the database, and then other parts will be logged on the database for my own use and not shared with the user. By far the most complex data relationship I've designed yet.

Spent the rest of the week working on the backend design and making sure that what I build today will allows us to grow to over 1,000 users without an issue. [NovelFoundry Backend: NGINX, Celery, Redis](https://pbrazeale.github.io/posts/novelfoundry-build-log-02/) If you read the linked article about the backend choices I've made and the technologies I've decided to use, you'll see the design should accommodate thousands of users without major changes. At most I should need to scale my servers.

The website should be live at time of posting this: [NovelFoundry.com](https://novelfoundry.com/) (_Please don't signup for the early release if you're not an active author._)

Though the entire application is not ready, the front end is done, and built to allow for automatic article posting; important for SEO and building out our site authority. Later on I'll post a whole write up on the marketing strategies I use and how you can implement versions yourself.

Next week is all about building out the backend and database, with a serious focus on security. Ensuring that the data uploaded by the users are segregated properly, and encrypted to prevent data leaks. Likewise, double and triple checking that I'm using the best practices possible to harden the backend to prevent breaches.

The deeper I get into this project, the more I realize there is to learn. Obviously when I stated, I knew I'd have to learn and I was aware of the unknown unknowns. However, as some of those unknowns become known, the sheer scale of knowledge required to orchestrate and build an entire SaaS reveals itself. It's no wonder that companies are actively seeking to hire those developers who've launched a SaaS and managed real users. I'm starting to understand the selection process from the position hirer's point-of-view.

## Books

[The United States of Anonymous by Jeff Kozzeff](https://www.goodreads.com/book/show/57926932-the-united-states-of-anonymous) **DONE** 4/5 Stars

[Prompt Engineering for LLMs by Berryman and Ziegler](https://www.goodreads.com/book/show/221244015-prompt-engineering-for-llms) **DONE** 3/5 Stars

[The NGINX Handbook by Farhan Hasin Chowdhury](https://www.freecodecamp.org/news/the-nginx-handbook/) **~25%**

+++
tags = ['Developer Log', 'Azure', 'Python', 'Linux']
title = 'Developer Week 038'
date = 2025-04-06T08:01:07+01:00
draft = false
+++

## Projects

### 100 Days of Code: The Complete Python Pro Bootcamp (44/100)

### `AuthorLedger` v2.0.0 ~65%

Revisiting my `CS50P` final project and upgrading it to a useable software state for other authors/publishers.

- Currently on v1.15.1

As it presently stands that software does everything the original did, but better.

#### Requirements.txt

```python
PyQt6>=6.4.0       # For the GUI
pandas>=1.5.0      # For reading and manipulating CSV/data
matplotlib>=3.6.0  # For plotting charts
fpdf2>=2.7.0       # For generating PDF reports
```

#### Currently Solved

1. **Rebuilt GUI** with `PyQt6` upgraded from PyQt5
2. Built **upload functionality** using `os` and `re`, `data_importer.py`
	1. Expanded functionality to include `KDP Payments` and `KDP Royalties`
		1. fixed bug so that it doesn't matter which order the files are uploaded.
		2. This upgrade fixed currency conversion issue. (currently set to USD default)
		3. created verification rules to prevent double uploading of same monthly report, even if file is renamed.
3. Built **database functionality** using `sqlite3`, and `pandas`
	1. Refactored `database.py` into `db_schema.py`, `royalty_manager.py`, and `expense_manager.py` (*for future expansion*)
	2. currently `royalties.db` will expand to multiple databases and software functionality expands.
4. Redesigned **graphs** using `matplotlib` to automatically produces a multicolor histogram x=time y=royalties based upon book titles.
	1. Expanded options to include `author` level selection instead of just publisher level which is how the report is generated from Amazon.
	2. User built `series` selection to save time when comparing earnings.
	3. Adjusted date range to default as `YYYY-MM` and dropped `DD` as reports are monthly.

#### TODO

1. finalize series build function
2. Create author adding to book titles for multi-author books
3. **Future Expansions**
	1. Expand reports to include *Draft 2 Digital, Nook, iBooks, Google Play*, possibly more.
	2. *Facebook* Ad tracker to calculate title level ROI and series level ROI using inhouse algorithms.
		1. (*Need to identify how best to minimize user manual input*)
	3. Cash flow tracker
		1. Create a ledger for users to log their expenses
		2. Automatically include royalties from database
		3. Allow for other income sources to be entered
		4. Produce an easy P&L report
		5. Produce a category pie chart to show expenses by weight, and income by weight.

#### Monetization

- With the Amazon Royalties functionality finalized, I can launch a beta version to our Patreon community for free.
	- Upon feedback, I can expand the beta to our Discord and Facebook community (1,000+ authors)
	- This feedback should finalize the report functions by identifying the unforeseen bugs.

1. Can launch `AuthorLedger` with just Amazon royalties for $0 to gain user base.
2. When the expansion is done, can sell AuthorLedger full version for $20 to $50.
	- Need to research user licensee agreements
	- Would need a separate LLC for personal protection
	- Need to research registration options 
		- Identify upgrade options
		- Might require a server to solve both, but I want that software to run locally with no internet connection requirement, and to be a one-time purchase software.
3. Could drop mandatory purchase entirely, and rely strictly on donations/pay-what-you-want model.
	- Could seek corporate support/donations from *Amazon, Draft 2 Digital, Barnes & Noble*, and *Google*. 
		- (*not likely, but possible*)

## Courses

### Boot.Dev Learn Python (7.1/14.8) **~48%**

- Learned more about Unit Testing to the point I can write small tests now.
- Learned Bitwise operations and how/when they're applicable

## Application Process

- Worked with a Senior Software Developer to redesign my entire resume and LinkedIn profile.
	- Still need to improve:
		1. **`AuthorLedger`** (Royalty, Marketing, and Expense tracker for small publishers) Based upon Alpha feedback, I'm aiming for a Beta launch within the next 45 days.
		2. **`Proxmox` Homelab** needs to be upgraded and documented. Should follow [Misha van den Burg's](https://github.com/mischavandenburg) example and document my homelab on GitHub.
			- He could be right that the homelab needs to be built with `Kubernetes`. If so, that's a few month away before I could consider rebuilding it.
		3. **Community Networking**: Join a meetup group and start discussing my progress publicly to receive vial feedback.    

### Applications (38+/1,000) **~3.8%**

- Tracking applications I apply for on company websites, but not the LinkedIn easy apply ones.
- Tailoring my resume based on the job listing, to highlight my skills that are relevant to the position.
- Writing a cover letter for each position that provides the option. For those that don't I'm connecting with a relevant employee on LinkedIn and providing my cover letter that way.
	- Thus far zero feedback on this approach.
- Splitting my time 80% continuing skill improvement and 20% applying (*though I spent all day Tuesday revamping my Resume, LinkedIn, Cover Letter template, and applying to new positions.*)
- At my present rate, it should take 30-40 weeks to hit 1,000 applications.
	- Will reassess approach at 200 based on feedback/lack there of.


#### Chances of Landing a Job				

##### Variables

- Individual Application odds 1/120
- Cumulative odds of acceptance (P=1−(1−p) ^n)
- 5 applications/day
- 5 day/week

##### Chart

| Application | Chance | Odds of Acceptance | Days | Weeks |
| ----------- | ------ | ------------------ | ---- | ----- |
| 5           | 0.83%  | 4.10%              | 2    | 1     |
| 20          | 0.83%  | 15.41%             | 5    | 2     |
| 60          | 0.83%  | 39.47%             | 13   | 3     |
| 120         | 0.83%  | 63.37%             | 25   | 6     |
| 200         | 0.83%  | 81.24%             | 41   | 9     |
| 358         | 0.83%  | 95.00%             | 72   | 15    |
| 820         | 0.83%  | 99.90%             | 165  | 34    |
| 1053        | 0.83%  | 99.99%             | 211  | 43    |

##### Breakdown

1. After  **60 applications** I have a **39.47%** chance
	1. When I play Texas Hold'em live those odds are often high enough to justify calling an all-in for 100 big blinds, so I like my chances.
2. After **120 applications** the odds are only **63.37%**
3. After **200 applications** the odds are only **81.24%**
	1. Basically the same odds as AA vs KK, and I'll take that bet all day and twice on Sunday.
4. After **358 applications** the odds are only **95%**
	1. That's pushing triple the expected 120.
	2. Better odds than flopping top set against an over pair!
5. After **820 applications** the odds are still only **99.9%**
	1. 1 in 1,000 chance of no job offer
6. After **1053 applications** finally hit **99.99%**
	1. 1 in 10,000 chance of no job offer

##### Takeaways

I'm confident in my ability to land a job before I hit the 1,000 applications, but of course there are no guarantees, as anyone who's played Texas Hold'em can attest to.
- This is also assuming pessimistic numbers. 
- Assums that the market won't improve within the next 6-12 months
- And asusms that I don't find a interview/offer via a network connection between now and 1,000 applications.

The whole thing can look daunting, but if I **evaluate the odds**, accept them for what they are, and **plan accordingly**, there's **no reason I can't** find my way into the industry within 30-40 weeks.
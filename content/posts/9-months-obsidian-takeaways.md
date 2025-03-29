+++
tags = ['Articles']
title = '9 Months Obsidian Takeaways'
date = 2025-03-29T10:34:07+01:00
draft = false
+++

My only regret is that I didn't stick with Obsidian the first time I downloaded it.

## Mind Map

![202050327_obsidan_mind_map.png](https://pbrazeale.github.io/images/202050327_obsidan_mind_map.png)

I thought it would take much longer to get a node cluster this size. But an odd thing happened three months into using Obsidian as my sole note taking source: I found myself compelled to take **more** notes.

The node view was the first thing that caught my eye when I saw others using Obsidian. Once mine stopped looking like a sad cluster of stars--like the night sky in the midst of downtown--and began to resemble the sea of stars from the camp grounds in a desert, I was addicted.

## Organization

### Color Tags

Each color represents a tag for the 100 folder system, staring with 00, 10, 20, etc. each parent folder gets a tag, and is then color coordinated onto the graph.

As it stands I have three empty parent folders, and one that's one sub folder away from being completely full.

### Single Vault

I don't separate my notes into multiple vaults. I prefer to maintain an entangled web of personal and professional. While I compartmentalize my personal life away from my professional, I don't stop reflecting on my professional life during my personal; I'm not convinced it would be healthy to ignore what I spend 1/3 plus of my life on.

While [Zettelkasten](https://en.wikipedia.org/wiki/Zettelkasten) appears all the rage in the community, it failed to solve the objectives I sought:

- Deep thinking via the process of communicating with myself via writing
- Organized notes that are capable of being shared (article style)
- Clear hierarchy of folder structure

Instead I chose to maintain the more traditional method of essay writing with a mix of journal like thoughts embedded directly into the notes. My [blog](https://pbrazeale.github.io) is a prime example of how I take notes.

### Hierarchy

As mentioned, I use the 10 folder system, but since I love folders, I made each folder then have it's own 9 folders, giving me a grand total of 100.

_00 Notes_ to _90 Meta_

Each folder then gets a meta article that looks like this:

```md
TITLE
___
**Folder:** #90_Meta
{{date}}
**Source:**
**Progress:**
___
## Table of Contents
%% Waypoint%%


## Tags
[[00 Notes]]
```

This gives me an easy way to view every post within a folder in one convenient location, and also allows me to "tag" my articles by linking to it in the **Tags** section, which is how I control the note links in the above graph.

The actual built in tag function `#00_Notes` is only ever used for the 10 parent categories to colorize the notes on the graph.

_If anyone knows how to add `#00_notes` to uploaded files: images, pdfs, etc... please let me know!_

`00.9` becomes a catch all folder for quick notes, before I begin the organization process of identifying the best home for the note. I cheat this way to keep my folder view clear. I only ever want to see the one 00_Notes file and sub folders inside the parent folder.

### Links

Example for _Developer Week 037_ article:

```md
## Tags
[[50 IT]] [[51 Programing]] [[52 Developer Log]] [[54 Hardware]] [[55 Linux]] [[pbrazeale.github.io]] [[python]] [[tkinter]] [[smtplib]] [[Requests, HTTP for Humans]] [[LPIC-1]] [[CompTIA Security+]]
```

This gives a realistic example of what my tag section looks like for a complex note that's a full blown article. And my dev logs are fairly tame.

When writing a note, I almost always find a way to link to another note that I find relevant. If I don't/can't that's a good sign it's time to make a new folder or subfolder. Though I try to use the four note rule.

#### 4 Note Rule

When I find four notes that link to one another well, but don't all link to another folder, that's usually a good sign it's time to refactor and think of a new category to organize under.

This was time consuming and happened often at first, but I think it's been over three months since I last made a folder, and I still have 3 parent folders open.

## Extensions

- [Excel to Markdown Table](https://github.com/ganesshkumar/obsidian-excel-to-markdown-table) Made importing cleanly formatted tables as simple as ctl+c ctl+v
- [Paste Image Rename](https://github.com/reorx/obsidian-paste-image-rename) This has has made images as easy as ctl+c ctl+v
- [Shortcuts Extender](https://github.com/ryjjin/Obsidian-shortcuts-extender) This reflowed my writing process so that I can use ctl+2 to instantly get a heading. There's much more it does, and most of my articles go to at least H4, so this saves me serious effort over time.
- [Tag Wrangler](https://github.com/pjeby/tag-wrangler) One of the few I consider a **must have** for any Obsidian setup. It automatically renames my links if I decided later on a better title. _Literally updated a 30+ link change for me once_.
- [Waypoint](https://github.com/IdreesInc/Waypoint) is the backbone of my folder hierarchy system. This auto populates a parent article _name matched to the folder_ with a list of every article and folder within.

### Waypoint "52 Developer Log" Example

```md
%% Begin Waypoint %%
- **[[100 Days of Code]]**
- **[[Articles]]**
- **CS50P**
	- [[CS50P Certificate]]
	- [[CS50P Final Project Readme]]
	- [[CS50P Week 6 Lecture Notes]]
	- [[CS50P Week 7 Lecture Notes]]
	- [[CS50P Week 8 Lecture Notes]]
	- [[CS50P Week 9 Lecture Notes]]
- **CS50W**
	- [[CS50W 0]]
- **CS50X**
	- [[CS50X 4]]
	- [[CS50X Week 5 Lecture Notes_02]]
	- [[CS50X Week 5 Lecture Notes]]
	- [[CS50X Week 6 Lecture Notes]]
	- [[CS50X Week 6.5 Lecture Notes]]
	- [[CS50X Week 7 Lecture Notes]]
	- [[CS50X WEEK 8 Lecture Notes]]
	- [[CS50X Week 9 Lecture Notes_02]]
	- [[CS50X Week 9 Lecture Notes]]
	- [[CS50X Week 10 Lecture Notes]]
- **[[Eloquent JavaScript]]**
- **Github Profile Readme**
	- [[pbrazeale]]
- **[[NeetCode]]**
- **[[pbrazeale.github.io]]**
- **Published Notes**
	- [[Writing Readable Code Notes]]

%% End Waypoint %%
```

Where it finds another Waypoint, such as `pbrazeale.github.io` it links to that waypoint and stops. This is **extremely** helpful in some of my folders, else the Waypoint would be a mile long.

### Appearance

I'm running the "Tokyo Night" theme, and do so anywhere I can.

I think add in this snippet extension to get the folders the way I want:
[github.com/pbrazeale/Obsidian-Colored-Sidebar/tree/main](https://github.com/pbrazeale/Obsidian-Colored-Sidebar/tree/main) It's a fork of CyanVoxel's project. I use the "_Colored Sidebar Items_10s Version.css_"

When opened, I run with a sidebar always open for folder navigation, and bottom left corner has a constant mind map graph display. Usually I keep 4-5 tabs open at once, and **rarely** do I use split view. Only if I need a PDF or personal article open to read from as I take notes.

## Writing Process

Coming to IT from being a professional author, long-form content is my default, so the short snippet notes that are all the rage in the community don't work for me. Instead I think and write in full article format. When I sit down to write or take notes on a lesson, I'm more inclined to build out my notes in a longer form with multiple H2s, _such as this article_.

### Course Notes

For course notes taking, I approach my notes format as a condensed version of the lecture with a few personal notes. Upon a second read I layer in all my thoughts on the lecture, with the advantage of hindsight.

When the course is a hands-on lab I'll often copy and paste most of the provided instructions or notes, and trim up any fluff I find, but otherwise leave it as is with a reference to the project folder where I'm building the lab.

### Book Notes

For books, especially technical materials _such as [Security+ Study Guide](https://pbrazeale.github.io/posts/security+-04-social-engineering-and-password-attacks/)_ I use the approach of synthesizing each section as I go through it. I always title my headings the same as in the book, but I try to rewrite most of the information in my own words. Occasionally, I'll copy verbatim when I feel the author captured a key point better than I can write myself.

The act of engaging with the material and streamlining it into a concise and useable format such as the link above, is the **key** to knowledge acquisition. _Though that chapter's test score would indicate I need further review._

### Journaling

I'm not a daily journaler, but usually twice a week I'll take a moment to brain dump all my thoughts into a long a note. Sometimes when I feel the need to rant or need to bust out several thousand words worth of notes, I'll switch to MS Word and use their built-in dictation function to write it out.

## Final Review

Obsidian has proven to be an invaluable tool for knowledge retention, and quick reference lookup. My only regret is that I failed to use it sooner and stick with it. By the 90 day mark of using it daily as my sole method of note taking, I realized it's value.

The first time I was able to search for a note I knew I wrote, and find it instantly, I was hooked. Add in the ability to link notes together, creating an enriched experience for reviewing notes, I'm not sure there's a better way to learn and master any subject domain.

And of course the mind map is like a modern art project that I create as I continue to work. At first watching it grow offered a positive feedback loop that kept me coming back and encouraged me to take more notes than I usually would. Now I'm intrinsically motivated by the knowledge acquisition itself.

Armed with the trust that if I take a note, the information will be available to me 24/7 within moments, I wake up every morning eager to compound my knowledge and write another 5+ notes. I'm thrilled at the prospect of evaluating my mind map at the 18 month mark.

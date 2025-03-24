+++
tags = ['CS50', 'Python', 'Developer Log', 'SQL']
title = 'Developer Week 011'
date = 2024-09-29T16:34:07+01:00
draft = false
+++

## CS50P Final Project (Progress 100%)

It's hard to place an exact progress report as there's no clear cut milestones toward the final product. Likewise, the final product I plan to release to the public will be a bit more polished than what I turn in as my course project. I'll use this as my beta MVP and then tweak based on feedback.

### Python Desktop App with PyQt

Thanks to [Code With Josh](https://www.youtube.com/watch?v=4y9BWBkj9Bo) I was able to learn the basics of how to make the desktop application I envisioned to track and display book royalties using a SQL database.

### Day 02 Progress

Put together the basic layout of the application.

Lost two hours due to Ubuntu bricking on my laptop. Placed learning more on Linux on hold. For now I'll stick with Windows and focus on finishing the courses in front of me. PH125.5X (Data Science: Productivity Tools) starts next month, and I'll see if Linux is a need then.

#### TODO

- Learn how to build an import function that will take a .xlsx and then automatically put the data into the SQL database.
- Convert the "Books" section into an interactive table where it reads the unique "Titles" from the database and turns them into selectable buttons for the SQL query.
- Fix Bugs
  - Fix the "start date" to actually pull the current date and then convert to 1/1/YYYY.
  - Fix the "end date" to actually pull the correct current date.
- Implement the graphs in the main section based on the SQL query parameters.
  - Units sold (Bar Graph)
    - Multicolor stack if multiple books selected
    - side-by-side multicolor stack if KENP and book format selected at same time.
  - Earnings (Line graph)
- Implement an "Export" button that saves a PDF with the charts and an option to include the selected database rows on pages 2+.

### Day 04 Finalized

Accomplished all the TODOs except for the "Export" function. Will revisit this when I rebuild the application using Electron.

While I was able to create a functional application for my own personal use, the current version is not suitable for distribution to other authors/publishers.

Video demo of the application can be found here: [https://youtu.be/0qZjCObs3eU](https://youtu.be/0qZjCObs3eU)

[Final Project README](https://pbrazeale.github.io/cs50p-Final-Project/)
"If I circle back around to this program for further development, I think starting over from scratch and building it in Electron is my best move. The options I’ve discovered for converting Python programs into .exe applications leave a lot to be desired. Election offers the ability to use the program on all three desktop environments, at the cost of learning JavaScript (which is a recommended language anyways).

Given the community around JS, I’m confident I would discover similar libraries to handle the charting and file importing/exporting; which are the core functions of the application."

## CS50X Final Project (Progress ~5%)

### Day None

Still in the conceptional phase and planning out the best method to implement the software. Originally I thought I'd use electron to build the software, but now I'm debating if I should build it with PyQt.

Starting with the KDPtracker was an excellent idea, as it's far less complex and easier to define the steps required to achieve a working prototype.

Creating an ePub creator is still a bit more ambitious than I'm prepared to take on, because there are serious gaps in my knowledge as to how I would even start approaching the core problem of taking a .doc/.docx file and converting the text format into corresponding html. I'm looking at markdown converts as inspiration. And then there's the matter of how I go about building all the text fields to be a rich text editor, etc...

For the purposes of the course, I'm thinking it might be best to scale back my ambition and implement a streamlines MVP protype of my main idea and then rebuild it once I have a working protype.

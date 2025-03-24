+++
tags = ['CS50', 'Python', 'PyQt', 'SQL']
title = 'CS50P Final Project'
date = 2024-09-25T10:34:07+01:00
+++

## KDP Tracker

#### Video Demo:  [https://youtu.be/0qZjCObs3eU](https://youtu.be/0qZjCObs3eU)

#### Description:

An easy to use Python program for managing KDP reports by uploading them to a SQL database and then allowing the user to visualize a Sales/Earnings chart.

## Features

- Import KDP Reports (.xlsx)
- Create SQL database from KDP Reports
- Track unit sales over time:
  - eBook
  - KENP
  - Free
  - Paperback
  - Hardback
  - Audio Book
- Track Royalties over time
- Display in easy to read chart
- Filter by:
  - Start Date range
  - End Date range
  - Book title
  - Publication Format

## How to Use

### Library Requirements

- PyQt5
- pandas
- sqlalchemy
- matplotlib

### KDP Reports/KDPTracker database

1. Run the program from within a python environment.
   1. It will initialize the KDPtracker database (if one does not already exist).
2. Upload all the KDP Reports you want to store in the database (bottom right button)
   1. "Books" section on the left panel will automatically populate based on the unique titles within the database.

### KDPTracker Filters

1. **"Start Date:"** will automatically default to 1/1/YYYY (current year).
   1. Change this to whichever month you want to filter by
2. **"End Date:"** will automatically default to (current day).
   1. Change this to whichever month you want to filter by
   2. The KDPTracker database stores records by YYYYMM (as that's how it come from KDP Reports), so leave the day of the month as the 1st.
3. **"Books:"** section is selectable one-by-one or `ctl + a` to select all titles.
4. **"Format:"** section is selectable one-by-one or `ctl + a` to select all formats.
5. **"Run"** when you've selected the books you want to look up, and the formats you want to check, push "Run" and the Sales/Earnings chart will automatically populate.

### KDPTracker Chart

1. **X-axis** is by months/year (it's recommended to view 12 months max, but there's no limit)
2. **Left Y-axis** is "net units sold/KENP reads" and corresponds to the height of the blue bar graph.
3. **Right Y-axis** is "royalties" and corresponds to the dots of the orange line graph.

## Design Breakdown

KDP Tracker opperates as two files: project.py and kdptracker.db.

Upon first running project.py the program will use PyQT5 to create the GUI.

```python
class KDPTracker(QWidget):

    def __init__(self):

        super().__init__()

        self.settings()

        self.initUI()
```

I chose PyQt5 as a result of stumbling upon [Code With Josh](https://www.youtube.com/watch?v=4y9BWBkj9Bo) as he built a fitness tracker, which used a SQL database and matplotlib to track data and then display a chart. Going into this project, I knew the basics of what I wanted to accomplish (import xlsx, create database, display charts similar to KDP user dashboard), but only after seeing what Josh did, did I understand the libraries I needed.

### Why make this program?

The KDP Reports dashboard only allows filtering by past 90 days and lifetime, which this program aims to solve. Compiling all the KDP reports into a single SQL database also makes it easier to save and backup moving forward.

My main objective was to get hands on experience creating a functional piece of software that solved a real world issue, and was not just a carbon copy of an already existing application. I'm confident this checks that box, though it's not in a "commercially" viable state, it's built well enough for my personal use moving forward.

### Future Features

1. Create an export function to save reports as PDFs.
2. Create a conditional function that filters for KENP and splits it into it's own bar graph.
3. Integrate an API to convert foreign currencies into USD.
4. Create a pi graph function that breaks down royalties by format type.
5. Create an "author" filter to change the "books" section to only populate based on the selected author.

### Electron

If I circle back around to this program for further development, I think starting over from scratch and building it in Electron is my best move. The options I've discovered for converting Python programs into .exe applications leave a lot to be desired. Election offers the ability to use the program on all three desktop environments, at the cost of learning JavaScript (which is a recommended language anyways).

Given the community around JS, I'm confident I would discover similar libraries to handle the charting and file importing/exporting; which are the core functions of the application.

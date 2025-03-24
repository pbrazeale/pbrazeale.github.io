+++
tags = ['CS50', 'Python', 'SQL', 'Data Structures']
title = 'CS50X Week 07 Lecture Notes'
date = 2024-08-10T06:34:07+01:00
draft = false
+++

## SQL

Database-centric language.

## flat-file database

CSV

### Language Poll of Class

```python
import csv

#'r' is default for open
#using 'with' will automatically close the file.
with open("favorites.csv", "r") as file:
	reader = csv.reader(file)
	#next will skip the header
	next(reader)
	for row in reader:
		print(row[1])
```

Continue with DictReader

```python
import csv

#'r' is default for open
#using 'with' will automatically close the file.
with open("favorites.csv", "r") as file:
	reader = csv.DcitReader(file)
	for row in reader:
		#this now prevents issues if columns move
		#favorite = row["language"]

```

More elegant way to iterate

```python
import csv

with open("favorites.csv") as file:
	reader = csv.DcitReader(file)
	#naming the variables, setting the counters
	scratch, c, python = 0, 0, 0

	for row in reader:
		#serach by key
		favorite = row["language"]
		#check key value
		if favorite == "Scratch":
			scratch += 1
		elif favorite == "C":
			c += 1
		elif favorite == "Python":
			python += 1

print(f"Scratch: {scratch}")
print(f"C: {c}")
print(f"Python: {python}")
```

Refactored to be more pythonic

```python
import csv

with open("favorites.csv") as file:
	reader = csv.DcitReader(file)
	#empty dic created
	counts = {}

	#smae loop
	for row in reader:
		favorite = row["language"]
		#catch expceted condition and add to count
		if favorite in counts:
			counts[favorite] =+ 1
		#create count to begin
		else:
			counts[favorite] = 1

for favorite in counts:
	print(f"{favorite}: {counts[favorite]}")
```

You can sort the dictionary easily with sorted()

```python
for favorite in sorted(counts):
	print(f"{favorite}: {counts[favorite]}")
```

Sort by key's value _in this case numerically_

```python
for favorite in sorted(counts, key=counts.get):
	print(f"{favorite}: {counts[favorite]}")
```

To change it to descending order use reverse

```python
for favorite in sorted(counts, key=counts.get, reverse=True):
	print(f"{favorite}: {counts[favorite]}")
```

### Collections Library

```python
import csv

from collections import Counter

with open("favorites.csv") as file:
	reader = csv.DcitReader(file)
	#objcet with built in counting functionality
	counts = Counter()

	for row in reader:
		favorite = row["language"]
		counts[favorite] += 1

#comes with built in ability to return pairs key value
for favorite, count in counts.most_common():
	print(f"{favorite}: {counts}")
```

can change to "problem" easily

```python
import csv

from collections import Counter

with open("favorites.csv") as file:
	reader = csv.DcitReader(file)
	#objcet with built in counting functionality
	counts = Counter()

	for row in reader:
		#this is all that changes since the program is written so modularly.
		favorite = row["problem"]
		counts[favorite] += 1

#comes with built in ability to return pairs key value
for favorite, count in counts.most_common():
	print(f"{favorite}: {counts}")
```

## Relational Database

### C.R.U.D.

- Create, insert
- Select
- Update
- Delete, drop

CREATE TABLE table (column type, ...);

### Sqlite3

Popular database option for smaller programs.

`$ sqllite3 favorites.db`

`sqlite>`

```SQL
.mdoe csv
.import favorites.csv favorites
.quit
```

```SQL
#shows the database information
.schema
# '*' is a whildcard (meaning it stands in for the column key)
SELECT * FROM favorites;

#makes sure that only 10 resutls come back.
SELECT language FROM favorites LIMIT 10;
```

#### Built in phrases

- AVG
- COUNT
- DISTINCT
- LOWER
- MAX
- MIN
- UPPER
- ...

returns the number of rows

```SQL
SELECT COUNT(\*) FROM favorites;

```

returns every value in column languages

```SQL
SELECT DISTINCT(language) FROM favorites;
```

returns the number of DISTINCT values in column languages

```SQL
SELECT COUNT(DISTINCT(language)) FROM favorites;

```

#### More keywords

- WHERE
- LIKE
- ORDER BY
- LIMIT
- GROUP BY

returns the count of only C within coloumn language

```SQL
SELECT COUNT(*) FROM favorites WHERE language = 'C';
```

returns the count of only C within coloumn language AND also match Hello, World within coloumn problem

```SQL
SELECT COUNT(\*) FROM favorites WHERE language = 'C' AND problem = 'Hello, World';

```

returns a table of languages and their associated count

```SQL
SELECT language, COUNT(*) FROM favorites GROUP BY language;
```

returns a table of languages and their associated count; now ordered by accending order.

```SQL
SELECT language, COUNT(_) FROM favorites GROUP BY language ORDER BY COUNT(_);

```

returns a table of languages and their associated count; now ordered by descending order.

```SQL
SELECT language, COUNT(*) FROM favorites GROUP BY language ORDER BY COUNT(*) DESC;
```

Can name a condition to save repeats

```SQL
SELECT language, COUNT(\*) AS n FROM favorites GROUP BY language ORDER BY n DESC;

```

Add data into the database

```SQL
INSERT INTO table (column, ...) VALUES(value, ...);
```

NULL == lack of data for field.

### IMDb

Movie/TV Show database with a GUI as the website

#### Best Practice

when storing data associate a string _header_ with an id number. That way ids can be associated across multiple pieces of data and not risk a string being misspelled.

### Data Types

- BLOB
  - Binary Large Object
- INTEGER
- NUMBERIC
  - dates and times
- REAL
  - floats or decimal points
- TEXT
  - strings

PRIMARY KEY = unique id
FOREIGN KEY = use of PRIMARY KEY in a new database table.

Search data matched between two tables

```SQL
SELECT \* FROM shows WHERE id IN
(SELECT show_id FROM ratings WHERE rating >= 6.0);
```

#### JOIN

This will combine the two tables by defining the shared value "shows.id" and then outputs the first 10 options with a rating >= 6.0, and only show the title and rating.

```SQL
SELECT title, rating FROM shows JOIN ratings ON shows.id = ratings.show.id WHERE rating >= 6.0 LIMIT 10;
```

#### Many to Many

requires a 3rd table to link the unique data tables "Person" "Shows"

#### INDEX

INDEX will create a B-Tree; and while it takes time to process the table the first time; there after it will result in far faster searches between tables.

```SQL
CREATE INDEX person_index on stars (person_id);

```

**Tradeoffs:** will cost more memory, and has to be updated anytime the table is modified.

### Python to use SQL

```python
form cs50 import SQL
db = SQL("sqlite:///favorites.db")

favorite = input("Favorite: ")

rows = db.execute("SELECT COUNT(*) AS n FROM favorites WHERE problem = ?", favorite)
row = rows[0]

print(row["n"])
```

#### Race Conditions

where you attempt to update a database multiple times within a short period of time, and there is a conflict.

- BEGIN TRANSACTION
- COMMIT
- ROLLBACK

These help control and prevent conflicts where race conditions are a known possibility.

```python
db.execute("BEGIN TRANSACTION")
rows = db.execute("SELECT likes FROM posts WHERE id = ?", id);
likes = rows[0]["likes"]
db.execute("UPDATE posts SET likes = ? WHERE id = ?", likes + 1, id);
db.execute("COMMIT")
```

### SQL Injection ATTACK

Safe solution is to use '?' as a placeholder when a variable needs to be entered.

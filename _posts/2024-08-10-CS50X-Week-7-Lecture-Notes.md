## SQL
Database-centric language.

## flat-file database
CSV

### Language Poll of Class
{% highlight py linenos %}
import csv

#'r' is default for open
#using 'with' will automatically close the file.
with open("favorites.csv", "r") as file:
	reader = csv.reader(file)
	#next will skip the header
	next(reader)
	for row in reader:
		print(row[1])

{% endhighlight %}

Continue with DictReader
{% highlight py linenos %}
import csv

#'r' is default for open
#using 'with' will automatically close the file.
with open("favorites.csv", "r") as file:
	reader = csv.DcitReader(file)
	for row in reader:
		#this now prevents issues if columns move
		#favorite = row["language"]

{% endhighlight %}

More elegant way to iterate
{% highlight py linenos %}
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
{% endhighlight %}

Refactored to be more pythonic
{% highlight py linenos %}
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
{% endhighlight %}

You can sort the dictionary easily with sorted()
{% highlight py linenos %}
for favorite in sorted(counts):
	print(f"{favorite}: {counts[favorite]}")
{% endhighlight %}

Sort by key's value *in this case numerically*
{% highlight py linenos %}
for favorite in sorted(counts, key=counts.get):
	print(f"{favorite}: {counts[favorite]}")
{% endhighlight %}

To change it to descending order use reverse
{% highlight py linenos %}
for favorite in sorted(counts, key=counts.get, reverse=True):
	print(f"{favorite}: {counts[favorite]}")
{% endhighlight %}

### Collections Library
{% highlight py linenos %}
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
{% endhighlight %}

can change to "problem" easily
{% highlight py linenos %}
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
{% endhighlight %}

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

{% highlight sqlite linenos %}
.mdoe csv
.import favorites.csv favorites
.quit
{% endhighlight %}

{% highlight sqlite linenos %}
#shows the database information
.schema
# '*' is a whildcard (meaning it stands in for the column key)
SELECT * FROM favorites;

#makes sure that only 10 resutls come back.
SELECT language FROM favorites LIMIT 10;
{% endhighlight %}

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
{% highlight sqlite linenos %}
SELECT COUNT(*) FROM favorites;
{% endhighlight %}

returns every value in column languages
{% highlight sqlite linenos %}
SELECT DISTINCT(language) FROM favorites;
{% endhighlight %}

returns the number of DISTINCT values in column languages
{% highlight sqlite linenos %}
SELECT COUNT(DISTINCT(language)) FROM favorites;
{% endhighlight %}

#### More keywords
- WHERE
- LIKE
- ORDER BY
- LIMIT
- GROUP BY

returns the count of only C within coloumn language
{% highlight sqlite linenos %}
SELECT COUNT(*) FROM favorites WHERE language = 'C';
{% endhighlight %}

returns the count of only C within coloumn language AND also match Hello, World within coloumn problem
{% highlight sqlite linenos %}
SELECT COUNT(*) FROM favorites WHERE language = 'C' AND problem = 'Hello, World';
{% endhighlight %}

returns a table of languages and their associated count
{% highlight sqlite linenos %}
SELECT language, COUNT(*) FROM favorites GROUP BY language;
{% endhighlight %}

returns a table of languages and their associated count; now ordered by accending order.
{% highlight sqlite linenos %}
SELECT language, COUNT(*) FROM favorites GROUP BY language ORDER BY COUNT(*);
{% endhighlight %}

returns a table of languages and their associated count; now ordered by descending order.
{% highlight sqlite linenos %}
SELECT language, COUNT(*) FROM favorites GROUP BY language ORDER BY COUNT(*) DESC;
{% endhighlight %}

Can name a condition to save repeats
{% highlight sqlite linenos %}
SELECT language, COUNT(*) AS n FROM favorites GROUP BY language ORDER BY n DESC;
{% endhighlight %}

Add data into the database
{% highlight sqlite linenos %}
INSERT INTO table (column, ...) VALUES(value, ...);
{% endhighlight %}

NULL == lack of data for field.

### IMDb
Movie/TV Show database with a GUI as the website

#### Best Practice
when storing data associate a string *header* with an id number. That way ids can be associated across multiple pieces of data and not risk a string being misspelled. 

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
{% highlight sqlite linenos %}
SELECT * FROM shows WHERE id IN 
	(SELECT show_id FROM ratings WHERE rating >= 6.0);
{% endhighlight %}

#### JOIN
This will combine the two tables by defining the shared value "shows.id" and then outputs the first 10 options with a rating >= 6.0, and only show the title and rating.
{% highlight sqlite linenos %}
SELECT title, rating FROM shows JOIN ratings ON shows.id = ratings.show.id WHERE rating >= 6.0 LIMIT 10;
{% endhighlight %}

#### Many to Many
requires a 3rd table to link the unique data tables "Person" "Shows"

#### INDEX
INDEX will create a B-Tree; and while it takes time to process the table the first time; there after it will result in far faster searches between tables.

{% highlight sqlite linenos %}
CREATE INDEX person_index on stars (person_id);
{% endhighlight %}

**Tradeoffs:** will cost more memory, and has to be updated anytime the table is modified.


### Python to use SQL
{% highlight py linenos %}
form cs50 import SQL
db = SQL("sqlite:///favorites.db")

favorite = input("Favorite: ")

rows = db.execute("SELECT COUNT(*) AS n FROM favorites WHERE problem = ?", favorite)
row = rows[0]

print(row["n"])
{% endhighlight %}


#### Race Conditions
where you attempt to update a database multiple times within a short period of time, and there is a conflict.

- BEGIN TRANSACTION
- COMMIT
- ROLLBACK

These help control and prevent conflicts where race conditions are a known possibility.

{% highlight py linenos %}
db.execute("BEGIN TRANSACTION")
rows = db.execute("SELECT likes FROM posts WHERE id = ?", id);
likes = rows[0]["likes"]
db.execute("UPDATE posts SET likes = ? WHERE id = ?", likes + 1, id);
db.execute("COMMIT")
{% endhighlight %}


### SQL Injection ATTACK
Safe solution is to use '?' as a placeholder when a variable needs to be entered.
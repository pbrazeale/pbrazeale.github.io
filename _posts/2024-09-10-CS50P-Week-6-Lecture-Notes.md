## File I/O
List can store multiple values, but they're still saved in the computer memory; so nor permanent after the program closes. 

{% highlight python linenos %}
names = []

for _ in range(3):
	names.append(input("What;s your name?"))

for name in sorted(names):
	print(f"hello, {name}")
{% endhighlight %}

### Open
allows you to access a file 

{% highlight python linenos %}
name = input("What's your name?")

file = open("names.txt", "a")
file.write(f"{name}\n")
file.close()
{% endhighlight %}

"w" is for write to the file, and if the file doesn't exist, **open** will create the file automatically for me.
This will also overwrite the file each time.

"a" is append and will add the entry to the document, but smashed together. Be sure to add a new line.

{% highlight python linenos %}
name = input("What's your name?")

with open("names.txt", "a") as file:
	file.write(f"{name}\n")
{% endhighlight %}

The above code will do the same as before, only now it opens and closes the file automatically.

{% highlight python linenos %}
with open ("names.txt", "r") as file:
	for line in file:
		print("hello,", line.rstrip())
{% endhighlight %}

Using a CSV file I can store data and then iterate over the file to create multiple variables at the same time.

{% highlight python linenos %}
with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		print(f"{name} is in {house}")
{% endhighlight %}

create a dictionary and then sort it by name

{% highlight python linenos %}
with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		student = {}
		sudent["name"] = name
		student["house"] = house
		students.append(student)

def get_name(student):
	return student["name"]

for student in storted(students, key=get_name):
	print(f"{student['name']} is in {student['house']})
{% endhighlight %}

can be condensed further with lambda function

{% highlight python linenos %}
with open("students.csv") as file:
	for line in file:
		name, house = line.rstrip().split(",")
		student = {}
		sudent["name"] = name
		student["house"] = house
		students.append(student)

for student in storted(students, key=lambda student: student["name"]):
	print(f"{student['name']} is in {student['house']})
{% endhighlight %}

You can learn more in Python’s documentation of [CSV](https://docs.python.org/3/library/csv.html).
### CSV reader
{% highlight python linenos %}
import csv

students = []

with open("students.csv") as file:
	reader = csv.reader(file)
	for row in reader:
		students.sppend({"name": name, "home": home})

for student in storted(students, key=lambda student: student["name"]):
	print(f"{student['name']} is in {student['house']})
{% endhighlight %}

Best practice to use first row as the column headers
{% highlight python linenos %}
import csv

students = []

with open("students.csv") as file:
	reader = csv.DictReader(file)
	for row in reader:
		students.sppend({"name": row["name"], "home": row["home"]})

for student in storted(students, key=lambda student: student["name"]):
	print(f"{student['name']} is in {student['house']})
{% endhighlight %}

Write to a CSV

{% highlight python linenos %}
import csv

name = input("What's your namne? ")
home = input("What's your home? ")

with open("students.csv", "a") as file:
	writer = csv.DicWriter(file, fieldnames=["name", "home"])
	writer.writerow({"name": name, "home": home})
{% endhighlight %}

### Binary Files
You can learn more in Pillow’s documentation of [PIL](https://pillow.readthedocs.io/).

{% highlight python linenos %}
import sys

from PIL import Image

images = []

for arg in sys.argv[1:]:
	image = Image.open(arg)
	images.append(image)

images[0].save(
	"cosumes.gif", save_all=True, append_images=[images[1]], duration=200, loop=0
)
{% endhighlight %}
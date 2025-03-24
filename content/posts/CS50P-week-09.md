+++
tags = ['CS50', 'Python']
title = 'CS50P Week 9 Lecture Notes'
date = 2024-09-20T10:34:07+01:00
draft = false
+++

## Et Cetera

### Set

```python
students = [
    {"name": "Hermione", "house": "Gryffindor"},
    {"name": "Harry", "house": "Gryffindor"},
    {"name": "Ron", "house": "Gryffindor"},
    {"name": "Draco", "house": "Slytherin"},
    {"name": "Padma", "house": "Ravenclaw"},
]

houses = set()
for student in students:
    houses.add(student["house"])

for house in sorted(houses):
    print(house)
```

Use .add instead of .append for set, and it will automatically filter out duplicates.

### Global

You can set a variable outside of the main function that allows all functions to modify or use the variable.

```python
balance = 0


def main():
    print("Balance:", balance)
    deposit(100)
    withdraw(50)
    print("Balance:", balance)


def deposit(n):
    global balance
    balance += n


def withdraw(n):
    global balance
    balance -= n


if __name__ == "__main__":
    main()
```

This runs into an issue though where the balance becomes a local variable when called and modified inside main. This is where using a class of Account becomes valuable.

```python
class Account:
    def __init__(self):
        self._balance = 0

    @property
    def balance(self):
        return self._balance

    def deposit(self, n):
        self._balance += n

    def withdraw(self, n):
        self._balance -= n


def main():
    account = Account()
    print("Balance:", account.balance)
    account.deposit(100)
    account.withdraw(50)
    print("Balance:", account.balance)


if __name__ == "__main__":
    main()
```

### Type Hints

#### mypy

```python
# by using : int, we're creating a hint to the funciton for what should be passed in.
def meow(n: int):
    for _ in range(n):
        print("meow")


number = input("Number: ")
meow(number)
```

`mypy meows.py`
`meows.py:7: error: Argument 1 to "meow" has incompatible type "str"; expected "int"  [arg-type]`
`Found 1 error in 1 file (checked 1 source file)`

**Type hints** are best practice to help decrease the probability of bugs, and one reason other languages are preferred for Python. (\*Note to self: think **TypeScript\***)

### Docstrings

Standard practice is to document within the function, not above it, and to use `"""`

```python
def meow(n):
    """
    Meow n times.

    :param n: Number of times to meow
    :type n: int
    :raise TypeError: If n is not an int
    :return: A string of n meows, one per line
    :rtype: str
    """
    return "meow\n" * n


number = int(input("Number: "))
meows = meow(number)
print(meows, end="")
```

- _Established tools, such as [Sphinx](https://www.sphinx-doc.org/en/master/index.html), can be used to parse docstrings and automatically create documentation for us in the form of web pages and PDF files such that you can publish and share with others._
- _You can learn more in Python’s documentation of [docstrings](https://peps.python.org/pep-0257/)._

### Command Line Argument Program

```python
import sys

if len(sys.argv) == 1:
    print("meow")
elif len(sys.argv) == 3 and sys.argv[1] == "-n":
    n = int(sys.argv[2])
    for _ in range(n):
        print("meow")
else:
    print("usage: meows.py [-n NUMBER]")
```

This allows the user to specify at the command line how many times they wish to execute the program.

`python meows.py -n 3`
would then print "meow" three times.

#### Argparse

This library will handle the command line arguments for you so that you can focus on writing the core functionality of the program.

```python
import argparse

parser = argparse.ArgumentParser(description="Meow like a cat")
# set default to precent breaking if ran alone, set help to explain the argument, set type to ensure an int is passed through.
parser.add_argument("-n", default=1, help="number of times to meow", type=int)
args = parser.parse_args()

for _ in range(args.n):
    print("meow")
```

### Unpacking

```python
def total(galleons, sickles, knuts):
    return (galleons * 17 + sickles) * 29 + knuts


coins = [100, 50, 25]

print(total(coins[0], coins[1], coins[2]), "Knuts")

# using *coins below handles the unpacking for us.

def total(galleons, sickles, knuts):
    return (galleons * 17 + sickles) * 29 + knuts


coins = [100, 50, 25]

print(total(*coins), "Knuts")

# us ** allows to unpack the dictiony coins twice, thus passing in the key:value pair.

def total(galleons, sickles, knuts):
    return (galleons * 17 + sickles) * 29 + knuts


coins = {"galleons": 100, "sickles": 50, "knuts": 25}

print(total(**coins), "Knuts")
```

### Map

```python
def main():
    yell("This", "is", "CS50")


def yell(*words):
    uppercased = map(str.upper, words)
    print(*uppercased)


if __name__ == "__main__":
    main()
```

### List Comprehensions

```python
def main():
    yell("This", "is", "CS50")


def yell(*words):
    uppercased = [arg.upper() for arg in words]
    print(*uppercased)


if __name__ == "__main__":
    main()

```

We can use the list comprehension to sort a previous list and build a new list based on a condition.

```python
students = [
    {"name": "Hermione", "house": "Gryffindor"},
    {"name": "Harry", "house": "Gryffindor"},
    {"name": "Ron", "house": "Gryffindor"},
    {"name": "Draco", "house": "Slytherin"},
]

gryffindors = []
for student in students:
    if student["house"] == "Gryffindor":
        gryffindors.append(student["name"])

for gryffindor in sorted(gryffindors):
    print(gryffindor)
```

### Filter

You can also use filter to pass in a conditional argument and the list to be filtered.

```python
students = [
    {"name": "Hermione", "house": "Gryffindor"},
    {"name": "Harry", "house": "Gryffindor"},
    {"name": "Ron", "house": "Gryffindor"},
    {"name": "Draco", "house": "Slytherin"},
]


def is_gryffindor(s):
    return s["house"] == "Gryffindor"


gryffindors = filter(is_gryffindor, students)

#the lamda s allows us to sort on the "name" key
for gryffindor in sorted(gryffindors, key=lambda s: s["name"]):
    print(gryffindor["name"])
```

### Dictionary Comprehension

Similar in spirit to list comprehension, but creates a dictionary object

```python
students = ["Hermione", "Harry", "Ron"]

gryffindors = {student: "Gryffindor" for student in students}

print(gryffindors)
```

### Enumerate

Returns the index and value

```python
students = ["Hermione", "Harry", "Ron"]

for i, student in enumerate(students):
    print(i + 1, student)
```

- _You can learn more in Python’s documentation of [`enumerate`](https://docs.python.org/3/library/functions.html#enumerate)._

### Generators

By using `yeild` instead of `return` I'm able to crunch much larger sets of data without crashing the program.

```python
def main():
    n = int(input("What's n? "))
    for s in sheep(n):
        print(s)


def sheep(n):
    for i in range(n):
        yield "🐑" * i


if __name__ == "__main__":
    main()

```

This will allow the program to actually print out 1,000,000 sheep instead of bricking the computer.

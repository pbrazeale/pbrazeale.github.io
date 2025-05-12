+++
tags = ['Developer Log', 'Python', 'SQL', 'Data Structures', 'Algorithms']
title = 'Developer Week 030'
date = 2025-02-09T06:34:07+01:00
draft = false
+++

## NeetCode Algorithms and Data Structures for Beginners (progress 28/35)

### NeetCode 150 (progress 26/150)

## Projects

[I Learned Python By Building These Projects - Tutorial for Beginners](https://www.youtube.com/watch?v=ehD6tdxmjDU) followed along with these and tried to stay one step ahead whilst going through it to see just how well I understood python. Project 1, learned to use `for idx, quesiton in enumerate(selected_questions):` as a way to step through the dictionary which if far more elegant than my loop approach.

[Python Enumerate](https://docs.python.org/3/library/functions.html#enumerate)
"Return an enumerate object. *iterable* must be a sequence, an [iterator](https://docs.python.org/3/glossary.html#term-iterator), or some other object which supports iteration. The [`__next__()`](https://docs.python.org/3/library/stdtypes.html#iterator.__next__ "iterator.__next__") method of the iterator returned by [`enumerate()`](https://docs.python.org/3/library/functions.html#enumerate "enumerate") returns a tuple containing a count (from *start* which defaults to 0) and the values obtained from iterating over *iterable*."

## IT Specialist Position

I applied for an IT Specialist role at a medium sized organization, and once I heard back that they were interested dropped everything to double-down on brushing up. Toward that end I jumped into NeetCode's System Design for Beginners.

### NeetCode System Design for Beginners (21/21)

This was a good surface level refresher, and then dug a bit deeper into architectural design principles I've not encountered before. I know have note with references to further reading to dig into.

This year I'll need to read 6-12 academic IT books to advance faster than what I can find fragmentally online.

### NeetCode SQL for Beginners (20/75)

Excellent refresher and it's going deeper than the CS50 course module did, which is insightful. This course is using PostgreSQL, whereas CS50 used SQLite, and I've just reached the portion that highlights the unique functions of PostgreSQL such as ENUM and IDENTITY.

ENUM offers a way to hard code an array of options for the column value to then be enumerated over when inserting data, and reduces data errors.

IDENTITY auto-increments the column number, helping to maintain UNIQUE PRIMARY KEYs.

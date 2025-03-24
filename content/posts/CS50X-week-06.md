+++
tags = ['CS50', 'Data Structures', 'Python']
title = 'CS50X Week 06 Lecture Notes'
date = 2024-08-10T04:34:07+01:00
draft = false
+++

## Python

Transitioning to Python, which offers the advantage of abstractions, a vast catalogue of libraries, and an ease of readability.

**Python manages the memory for us, thus reducing the time requirements to code.**

The tradeoff is that Python is slower and takes up more space than C, but the tradeoff for faster coding speed is often worth it.

### Edges Filter

This was one of the harder C assignments for Week 4, and in Python it's quite simple.

```python
from PIL import Image, ImageFilter

before = Image.open("bridge.bmp")
after = before.filter(ImageFilter.FIND_EDGES)
after.save("out.bmp")
```

### Face Recognition

There's an open library built in Python that offers the ability to recognize faces from an inputted image.

### Import

```python
import cs50
//or only import what's needed.
from cs50 import get_string
	//this recuded the memory space required if you don't need the entire library.

answer = get_string("What's your name? ")
//input == get_string
answer = input("What's your name? ")
//formatted string
print(f"hello, {answer}")
```

### Types

- bool
- float
- int
- str
- range
- list
- tuple
- dict
- set

### Truncation

Python will convert int to floats when dividing.
Though floating point precision still exits.

```python
x = int(input("x: "))
y = int(input("y: "))

z = x + y

print(f{z:50f})
```

This will output more digits than can be calculated.

### Exceptions

A way to catch expected errors.

```python
try:
	...
except ValueError:
	...
	//to ignore
	pass
```

### List

is essentially a linked list, without having to handle the pointers ourselves.

#### for loops

come with the ability to associate an else clause.

## OOP

Object Oriented Programing
Types come with functions

+++
tags = ['Developer Log', 'C']
title = 'Developer Week 047'
date = 2025-06-08T14:05:07+01:00
draft = false
+++

![Developer Week 047](https://pbrazeale.github.io/images/devweek047.jpg)

## Courses

### Boot.Dev Back-end Developer Career Path (~53.04%) (📈 +1.36%)

#### ~~10. Build a Maze Solver~~ DONE

##### 10.4.0 Drawing Some Lines

Learned the difference between `self.variable` and `self.__variable`

**GPT**

> The choice between `self.__variable` and `self.variable` in Python class design reflects **intentions around visibility, encapsulation, and internal use**.

- `self.variable` – **Public attribute**
- `self._variable` – **Protected (by convention only)**
- `self.__variable` – **Private (name-mangled)**

I think I was supposed to know this already, but clearly forgot.

![Build a Maze Solver in Python](https://qvault-webapp-dynamic-assets.storage.googleapis.com/certificates/0f47bba5-cd28-4599-b216-7a6067d42387.jpeg?1749216242239)

#### 11. Learn Memory Management (26/101 modules)

##### 11.2.3

In C, splitting code into files like `coord.c`, `coord.h`, and `main.c` is a practice called **modular programming**. Here’s how each file serves a distinct purpose:

###### `coord.h` (Header file):

This file declares the structures and function prototypes (signatures) of your coordinate utilities. By including it in other files, the compiler knows about your types and functions—even if their actual implementation is somewhere else.  
_For example, it tells the compiler “there’s a function called `scale_coordinate` that returns a `struct Coordinate`."_

###### `coord.c` (Implementation file):

This implements (defines) the functions declared in `coord.h`. All the logic—the instructions for struct manipulation and coordinate math—lives here.  
By separating this from the header, you can change how functions work without breaking code that calls them, as long as you keep the interface the same.

###### `main.c` (Driver/test file):\*\*

This is the entry point: it contains the `main()` function and any code to run your program or tests. It relies on the declarations in `coord.h` and the real code in `coord.c`.

###### Why does C do this?

- It keeps code organized and easier to maintain.
- It allows teams to work on different parts independently.
- It helps prevent "duplicate symbols" and other compilation errors.

###### In summary:

- Header files declare *what* exists,
- Implementation files define *how* things work,
- Main (or other) files use these pieces to create the program's behavior.

#### 12. Personal Project 1 (3/4)

[01 Build Notes Sarah - AI Line Editor](https://pbrazeale.github.io/posts/01-sarah-build-notes/)

[Sarah MVP Development Roadmap](https://pbrazeale.github.io/posts/02-sarah-build-notes/)

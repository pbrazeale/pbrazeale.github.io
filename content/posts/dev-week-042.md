+++
tags = ['Developer Log', 'Python', 'Git']
title = 'Developer Week 042'
date = 2025-05-05T07:35:07+01:00
draft = false
+++

![Developer Week 042](https://pbrazeale.github.io/images/devweek042.jpg)

## Courses

### Boot.Dev Back-end Developer Career Path (~32.22%) (📈 +6.66%)

#### 7. ~~Functional Programming (9/9)~~ Done

##### 7.2.5 Learned how/why functional programming can be more resource efficient.

By using map() to feed the newly split document into convert_line(), I can then "\n".join() the list of modified lines, and thus return an entirely new document.

```python
def change_bullet_style(document):
    return "\n".join(map(convert_line, document.split("\n")))
    # lines_list = document.split("\n")
    # new_line_list = []
    # for line in lines_list:
    #     new_line_list.append(convert_line(line))
    # rejoined_doc = "\n".join(new_line_list)
    # return rejoined_doc


# Don't edit below this line


def convert_line(line):
    old_bullet = "-"
    new_bullet = "*"
    if len(line) > 0 and line[0] == old_bullet:
        return new_bullet + line[1:]
    return line

```

###### BOOTS

1. **Functionality:**  
   Both snippets apply `convert_line` to every line and join them back together. So, the *output* will be the same.
2. **How `map` works:**  
   In Python 3, `map()` is what's called a "lazy iterator." That means it doesn't immediately create a list in memory—it produces each transformed line one at a time, only as needed by the `.join()` function.
3. **For-loop approach:**  
   Your version with the `for` loop and `new_line_list.append(...)` **explicitly** builds a new list in memory before joining.
4. **Resource use:**  
   So, which is more memory efficient?
   - `map`: Uses less memory because it produces lines one at a time; only a small amount is kept in memory.
   - `for` loop: Builds the full list of converted lines up front.

##### 7.3.1 Pure Functions

In computer programming, a pure function is a function that has the following properties:

1. the function **return values** are **identical** for **identical arguments** (no variation with local static variables, non-local variables, mutable reference arguments or input streams, i.e., referential transparency), and
2. the function has **no side effects** (no mutation of local static variables, non-local variables, mutable reference arguments or input/output streams).
   [source](https://en.wikipedia.org/wiki/Pure_function)

**Example:**

```python
def find_max(nums):
    max_val = float("-inf")
    for num in nums:
        if max_val < num:
            max_val = num
    return max_val
```

##### 7.3.5 Reference vs. Value

[copy](https://docs.python.org/3/library/copy.html) allows us to make a new object for use in local scope, without altering the original.

##### 7.3.12 Memoization

In computing, [memoization](https://en.wikipedia.org/wiki/Memoization) or memoisation is an **optimization technique** used primarily to **speed up computer programs** by storing the results of expensive function calls to pure functions and **returning the cached result** when the same inputs occur again.

###### Etymology

> The term **memoization** was coined by Donald Michie in 1968 and is derived from the Latin word memorandum ('to be remembered'), usually truncated as memo in American English, and thus carries the meaning of 'turning the results of a function into something to be remembered'. While memoization might be confused with memorization (because they are etymological cognates), memoization has a specialized meaning in computing.

##### 7.8.7 lru_cache

Solved the problem "technically" as a simple two pointer problem, but it undermined the lesson, because I failed to build a cache.

The correct solution was recursively cleaner.

#### 8. Build a Static Site Generator (3/5 modules)

#### 9. Learn Data Structures and Algorithms (3/16 modules)

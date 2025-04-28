+++
tags = ['Developer Log', 'Python', 'Git']
title = 'Developer Week 041'
date = 2025-04-28T07:35:07+01:00
draft = false
+++

## Courses

### Boot.Dev Back-end Developer Career Path (~25.56%) (📈 +7.78%)

#### 5. Learn Object Oriented Programming (100%)

While I've been using Python Classes, I'm not sure I understood them nearly as well as I do now. Especially how to pass back up/override using super(). Excellent course!

#### 6. Build Asteroids (100%)

[https://github.com/pbrazeale/asteroid](https://github.com/pbrazeale/asteroid)

#### 7. Functional Programming (~22.22%)

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

##### BOOTS

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

#### 9. Learn Data Structures and Algorithms (~12.5%)

#### 16. Learn SQL (~18.18%)

##### Notes

- Learned about ALTER for use on modifying an existing table.
- Best practice of up migrating in order to allow for down migrating.

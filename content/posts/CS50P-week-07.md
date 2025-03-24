+++
tags = ['CS50', 'Python']
title = 'CS50P Week 7 Lecture Notes'
date = 2024-09-12T10:34:07+01:00
+++

## Regular Expressions

Really just a pattern. **REGEX**

```python
email = input("What's your email? ").strip()

if "@" in email and "." in email:
	print("Valid")
else:
	print("Invalid")
```

```python
email = input("What's your email? ").strip()

username, domain = email.split("@")

#if username and "." in domain:
if username and domain.endswhith(".edu"):
	print("Valid")
else:
	print("Invalid")
```

### Regular Expression (RE)

[Python Documentation](https://docs.python.org/3/library/re.html)

re.serach

```python
import re

email = input("What's your email? ").strip()

if re.serach("@", email):
	print("Valid")
else:
	print("Invalid")
```

Validation characters

```
.   any character except a new line
*   0 or more repetitions
+   1 or more repetitions
?   0 or 1 repetition
{m} m repetitions
{m,n} m-n repetitions

^   matches the start of the string
$   matches the end of the string or just before the newline at the end of the string

[]    set of characters
[^]   complementing the set

\d    decimal digit
\D    not a decimal digit
\s    whitespace characters
\S    not a whitespace character
\w    word character, as well as numbers and the underscore
\W    not a word character

A|B     either A or B
(...)   a group
(?:...) non-capturing version
```

r can be used to create a raw string

```python
import re

email = input("What's your email? ").strip()

if re.search(r".+@.+\.edu", email):
    print("Valid")
else:
    print("Invalid")
```

Flags

```python
re.IGNORECASE
re.MULTILINE
re.DOTALL
```

Format.py

```python
name = input("What's your name? ").strip()
print(f"hello, {name}")


```

Using re instead of split

```python
import re

name = input("What's your name? ").strip()
if matches := re.search(r"^(.+), *(.+)$", name):
    name = matches.group(2) + " " + matches.group(1)
print(f"hello, {name}")
```

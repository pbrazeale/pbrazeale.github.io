+++
tags = ['CS50', 'Python', 'Developer Log']
title = 'Developer Week 010'
date = 2024-09-22T16:34:07+01:00
draft = false
+++

## CS50P (Progress 90%)

### Week 7 Regular Expressions

#### Working 9 to 5

Not sure what was wrong with the program, but after nearly two hours of trying to fix my test_working.py file I submitted for a 16/18 score. For the life of me I can't understand what the issue was with testing for a SystemExit("ValueError"), but regardless, the assignment is done and I'm moving forward.

### Week 8 OOP

A review of what I learned in CS50X, but always good to refresh, and I learned the technical definition of a tuple which will be useful moving forward.

The second half of the lecture was packed full of information, and this week's lecture notes, might be the longest I've taken thus far.

## Pytest

Unit testing is finally starting to click for me, an I've learned how to use pytest to raise errors and verify that my programs are correctly catching and handling errors, along with of course asserting correct functionality.

```python
import pytest
from cookie import Cookie

def test_init():
cookie = Cookie(8)
assert cookie.\_capacity == 8

    with pytest.raises(ValueError):
        Cookie(-2)
```

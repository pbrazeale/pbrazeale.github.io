+++
tags = ['Developer Log', 'Data Structures', 'Alorithms']
title = 'Developer Week 013'
date = 2024-10-06T16:34:07+01:00
draft = false
+++

## Day Job

I'm up against deadlines and have to focus on them as my priority before returning to courses.

Data Science: Productivity Tools (PH125.5X) starts on the 16th, and I'll need to jump straight into it. Likewise I still need to finalize the rebuilt of my KDP tracking software using Electron to submit for the CS50X final project.

## LeetCode (progress 10/3313)

### LeetCode 347

Used NeetCode video to solve, and then studied the solution, and solved on LeetCode with one reference to fix `freq = [[] for i in range(len(nums) + 1)]`

I suspect I understand the reasoning behind this solution at about 65%. Need to focus more deeply on easy array solutions on LeetCode before continuing with the NeetCode 150.

### LeetCode 35

Solution I wrote

```python
class Solution(object):
def searchInsert(self, nums, target):

        index = len(nums) - 1
        for i in range(len(nums) -1, 0, -1):
            if target > int(nums[i]):
                return (index + 1)
            index -= 1
```

Runtime Error I'm receiving

```python
TypeError: None is not valid value for the expected return type integer
raise TypeError(str(ret) + " is not valid value for the expected return type integer");
Line 36 in \_driver (Solution.py)
\_driver()
Line 42 in <module> (Solution.py)
```

I'll have to use NeetCode to figure out a proper solution. Looking at it, I think my solution is O(n) time and memory, which the requirements call for "You must write an algorithm with `O(log n)` runtime complexity." But I'm unsure if I'd receive an Runtime Error because of it.

When I tested the code locally it ran fine.

```python
def main():
nums = [1,3,5,6]
target = 5

    index = len(nums) - 1

    for i in range(len(nums) -1, 0, -1):
        if target > int(nums[i]):
            print(index + 1)
            return (index + 1)
        index -= 1

if **name**=="**main**":
main()
```

## NeetCode 150 (progress 7/150)

## NeetCode Algorithms and Data Structures for Beginners (progress 5/35)

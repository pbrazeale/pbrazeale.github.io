+++
tags = ['Developer Log', 'Data Structures','Algorithms', 'Git', 'C']
title = 'Developer Week 044'
date = 2025-05-19T09:05:07+01:00
draft = false
+++

![Developer Week 044](https://pbrazeale.github.io/images/devweek044.jpg)

## Courses

### Boot.Dev Back-end Developer Career Path (~51.68%) (📈 +14.35%)

##### NOTE:

_I changed the tracking from **modules to lessons**, so that's in part a reason for the jump in percent complete. I made more progress than I did last week, but not double the progress._

#### 9. ~~Learn Data Structures and Algorithms~~ DONE

##### 9.10.8 Delete

```python
class BSTNode:
    def delete(self, val):
        if self.val is None:
            return None
        if val < self.val:
            if self.left is not None:
                self.left = self.left.delete(val)
                return self
        if val > self.val:
            if self.right is not None:
                self.right = self.right.delete(val)
                return self
        if val == self.val:
            if self.right is None:
                return self.left
            if self.left is None:
                return self.right
        #If there are both left and right children, we need to find the new "successor":
        #the smallest node in the right subtree, which is the value next largest after the current node's value.
        # Finding the successor (smallest value in right subtree)
        min_larger_node = self.right
        # Find the smallest node in the right subtree by walking down the current right child's left branches until reaching a node with no left child.
        while min_larger_node.left:
            min_larger_node = min_larger_node.left

        # Replace current node's value with successor's value
        self.val = min_larger_node.val

        # Delete the successor from the right subtree
        # This recusion fixes the tree structure right, bring the vlaue up?
        self.right = self.right.delete(min_larger_node.val)

        # Return the current node (which now has the successor's value)
        return self

    # don't touch below this line

    def __init__(self, val=None):
        self.left = None
        self.right = None
        self.val = val

    def insert(self, val):
        if not self.val:
            self.val = val
            return

        if self.val == val:
            return

        if val < self.val:
            if self.left:
                self.left.insert(val)
                return
            self.left = BSTNode(val)
            return

        if self.right:
            self.right.insert(val)
            return
        self.right = BSTNode(val)


```

##### 9.10.14 Node Exists

```python
    def exists(self, val):
        if self.val ==  val:
            return True

        if val < self.val:
            if self.left:
                return self.left.exists(val)
            else:
                return False

        if self.right:
            return self.right.exists(val)
        else:
            return False
```

This is cleaner than my solution. It's designed to only check one half if needed, and directly returns value instead of creating a new variable.

##### 9.13.2 Tries Exist

```python
class Trie:
    def exists(self, word):
        current = self.root
        for c in word:
            if c not in current:
                return False
            current = current[c]
        return self.end_symbol in current
```

Much cleaner solution compared to my try, except. Learned I can search directly for the c within the dictionary.

##### Review

![Algos 1 done](https://qvault-webapp-dynamic-assets.storage.googleapis.com/certificates/05ece783-8b5d-4a68-827f-4f186b3679d1.jpeg?1747236911723)

Absolute hardest course I've taken, but that's a failure on my part. I need to practice more. Will 100% be retaking this course! Along with studying [[NeetCode]] for more practice visualizing what's happening to the data.

#### 10. Build a Maze Solver (6/13)

##### 10.4.0 Drawing Some Lines

Learned the difference between `self.variable` and `self.__variable`

**GPT**

> The choice between `self.__variable` and `self.variable` in Python class design reflects **intentions around visibility, encapsulation, and internal use**.

- `self.variable` – **Public attribute**
- `self._variable` – **Protected (by convention only)**
- `self.__variable` – **Private (name-mangled)**

I think I was supposed to know this already, but clearly forgot.

#### 11. Learn Memory Management (25/101)

##### NOTE:

_Deeper Learning section doesn't count toward the course completion; though I intent to take all the courses once I've finished the final project._

#### Deeper Learning: Learn Git 2 (27/73)

## Summer Break

With the summer upon us, my progress will likely slow down with my daughter out of school. We're going to visit Hurricane Harbor weekly; though I'll take a laptop and attempt to knock out a few lessons to maintain the daily streak.

Alongside spending time with her, Summers are a major crunch season for the day job, which may also slow me down. Though thus far I've managed to keep them in balance.

My trajectory had me completing the final project by early August, but now I'm going to revise my projection to mid September. If I'm able to maintain my current pace, all the better, but if not September will still be excellent.

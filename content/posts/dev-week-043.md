+++
tags = ['Developer Log', 'Data Structures','Algorithms', 'Git', 'Proxmox', 'Home Lab', 'TrueNAS']
title = 'Developer Week 043'
date = 2025-05-11T19:35:07+01:00
draft = false
+++

![Developer Week 043](https://pbrazeale.github.io/images/devweek043.jpg)

## Projects

### Home Lab

#### Proxmox -> LVM Networking Issue

For the past few weeks I've experienced a network issue with my proxmox server where it would randomly lock up and I would not be able to reach it over the network unless I unplugged the ethernet and plugged it back in.

I finally realized it all stemmed from my initial setup of the TrueNAS LVM. I had originally created the LVM using VirtIO as the model for the network device. Now that I've redeployed using Intel E1000 I'm no longer running into an issue. _fingers crossed_ that was the root cause and not a random coincidence.

##### Main Takeaway

When setting up my LVMs I'll pass through the exact hardware for the network devices moving forward.

And likely I should buy a dedicated network card and create a virtualized router. But for now I'll revel in the server working as expected.

## Courses

### Boot.Dev Back-end Developer Career Path (~37.22%) (📈 +5.00%)

#### 8. ~~Build a Static Site Generator~~ Done

[GitHub Repo](https://github.com/pbrazeale/static_site_gen)
[Deployed Site](https://pbrazeale.github.io/static_site_gen/)

##### 8.4.3 Block to HTML

Had to look at the solution to fix my code. Turns out, despite passing tests along the way, I had failed to isolate the scope of the functions and they were in fact doing too much processing. Furthermore, I had structured my code in such a way as to create to many modules.

Once I tried to put the whole thing together and run tests that required each step to work in unison, it failed. I finally understand what engineers mean when they talk about test coverage not being a guarantee.

Of all the lessons I've taken: here, including CS50P, and 100 Days of Code, this lessons has been the most important and impactful. Building this project was the right size that forced me to reach my level of incompetency and thus learn the most while discovering unknown territory.

Before building **12.1.1 First Personal Project**, I want to rebuild this project using the design principles I've learned. If I do so without looking at my existing code, I'll know I'm prepared.

![Static Site Generator](https://qvault-webapp-dynamic-assets.storage.googleapis.com/certificates/2d94e45a-510d-487f-b6e6-0e3312c76016.jpeg?1746495792872)

#### 9. Learn Data Structures and Algorithms (10/16 modules)

##### 9.5.3 Reduction to P

This is a brilliant example of how to reduce a complex sequence.

Solve for n iterations of the Fibonacci sequence and return the value.

```python
def fib(n):
    if n == 0:
        return 0
    if n == 1:
        return 1
    grandparent = 0
    parent = 1
    current = 0
    for i in range(n -1):
        current = parent + grandparent
        grandparent = parent
        parent = current
    return current
```

##### 9.6.1 Introduction to Data Structures

Data structures are just organizational tools that allow for more advanced algorithms. Some examples:

- **Stacks**: Last in, first out.
- **Queues**: First in, first out.
- **Linked Lists**: A chain of nodes, efficient for inserts and deletes.
- **Binary Trees**: A tree where each node has up to two children.
- **Red Black Trees**: A self-balancing binary tree using colors.
- **Hashmaps**: A data structure that maps keys to values.
- **Tries**: A tree used for storing and searching words efficiently.
- **Graphs**: A collection of nodes connected by edges.

#### Deeper Learning: Learn Git 2 (2/11)

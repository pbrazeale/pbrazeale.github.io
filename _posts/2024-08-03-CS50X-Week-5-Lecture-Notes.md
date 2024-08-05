[data structures]
[Data Science]
[CS50]

## Queues

### FIFO

First In First Out
enqueue
dequeue
[Push]
Arrays store the data structure

### Stacks

#### LIFO

last in first out
[Pop]

## [Array]

Moving an array by copy pasting, will result in O N+1 as it grows.

### Memory Allocation

`int *list = malloc(3 * sizeof(int));`
Malloc allocates memory, and I can treat it as an array.

Dynamically allocate more memory.
increase the [magic number]
free(list); [memory leak] avoidance.

## Data Structure

Solution to the array issue of memory allocation

```
struct
.
*
-> is . * used together.

```

### Linked List

pointers to link the data together.
Time and Space are the tradeoff
linking requires a 2nd space to point to the next.
or 0x0 as the NULL end of the linked list.
Plus one extra pointer to start the list just like the array starter.

```
typedef struct node
{
	int number;
	struct node *next;
} node;
```

`node *list == NULL;`
Begins the linked list

```
node *n = malloc(sizeof(node));

(n).number = 1;
n->next = NULL;

```

Order of operation means updating the next node field before pointing the list

```
#incldue <stdio.h>
#include <stdlib.h>

typedef struct node
{
	int number;
	struct node *next;
}


int main(int argc, char *argv[])
{
	node *list = NULL;

	for (int i = 1; i < argc; i++)
	{
		int number = atoi(argv[i]);

		node *n = malloc(sizeof(node));
		if (n == NULL)
		{
			//FREE memory thus far
			return 1;
		}
		n->number = number;
		n->next = list;
		lsit = n;
	}

	//print list backwards of entrace
	//prepend is O(1), so fastest possible
		//binary serach not possible.
		//O(n) for search
	node *ptr = list;
	while (ptr != NULL)
	{
		printf("%i\n", ptr->number);
		ptr = ptr->next;
	}
}

```

Appending to the list will place at end O(n) time.

```
//If list has numbers
else
{
	//Iterate over nodes in list
	for (node *ptr = lsit; ptr != NULL; ptr = ptr->next)
	{
		//if at end of list
		if (ptr->next == NULL)
		{
			//Append node
			ptr->next = n;
			break;
		}
	}
}
```

Append into list to create sorted by default

```
	for (node *ptr = lsit; ptr != NULL; ptr = ptr->next)
	{
		//if at end of list
		if (ptr->next == NULL)
		{
			//Append node
			ptr->next = n;
			break;
		}

		//if middle
		if (n->next M ptr->next->number)
		{
			n->next = ptr->next;
			ptr->next = n;
			break;
		}
	}
```

### Trees

data branching
[Binary Search Tree]
Offers the best balance of storage speed and searching speed at the cost of tripling the data by requiring the left and right node pointer.
O(log n)

```
bool serach(node #tree, int number)
	if (tree == NULL)
	{
		return false;
	}
	else if (number < tree->number)
	{
		return search(tree->left, number);
	}
	else if (number > tree->right, number);
	{
		return serach(tree->right, number);
	}
	else
	{
		return true;
	}
```

### Dictionaries

store Keys with Values

### Hashing

takes infinite inputs and maps to a finite
Cards break into 4 buckets of suites

[Hash Function]
[Hash Table]

For Contacts
Array 0 - 25 for A - Z
maps to the first name, creating 26 buckets.
maps to link list of the names starting with the letter.
O(n) is worst case but best case O(1)
can increase the array by taking more starter letters. increasing chance of O(1)

`node *table[26]`

[const] is best practice when passing a string you don't want to allow adjusting on.

### Tries

is a tree of arrays
O(1)
Major downside is the memory due to unused array nodes

+++
tags = ['CS50', 'Data Structures', 'C']
title = 'CS50X Week 05 Lecture Notes 02'
date = 2025-08-09T04:34:07+01:00
+++

## Nodes

```c
typedef struct node
{
	string phrase;
	struct node *next;
}
node;
```

Hex memory address stored in next, string phrase stored as an array.

### Creating linked list

```c
//list pointer to nothing
node *list = NULL;

//new node
node *n = malloc(sizeof(node));
n->phrase = "hi!";
n->next = NULL;

list = n;
```

### Inserting Node

```c
n = malloc(sizeof(node));
n->phrase = "HEY!";
n-> = list;
list = n;

//This is a mistake becuase it doens't addres the other allocated node
free(list);

//correct solution
node *ptr = list->next;
list = ptr;
ptr = list->next;

//now free list
free(list);

list = ptr;
//ptr is NULL which is good as it means all memory has been freed.
```

## Valgrid

An exceptionally helpful testing program to identify if and where memory leaks are occurring in the compiled [[C]] program.

> "Valgrind is an instrumentation framework for building dynamic analysis tools. There are Valgrind tools that can automatically detect many memory management and threading bugs, and profile your programs in detail."

[Valgrind User Manual](https://valgrind.org/docs/manual/manual.html)

## Hash Tables

Hash table == Dictionary

Hash function determines the efficiency.

```c
//the 26 would be the first letter
node *table[26];

int hash(string phrase);
```

Hash Function implementation

```c
int hash(string phrase)
{
	 //roating words to upper and indexes 0-25 the ASCII value
	 return toupper(phrase[0]) - 'A';
}
```

## The Trie Data Structure

Source is a video from [Jacob Sorber](https://www.youtube.com/watch?v=3CbFFVHQrk4)

```c
#include <stdio.h>
#include <stdlib.h>
#incldue <stdbool.h>
#include <string.h>

#define NUM_CHARS 256

typedef struct trinode
{
	strucut triendoe *children[NUM_CHAR];
	bool terminal;
} tridenode;

trienode #createnode()
{
	trienode *newnode = malloc(sizeof *newnode);

	for (int i=0; i<NUM_CHARS; i++)
	{
		newnode->children[i] = NULL;
	}
	newnode->terminal = false;
	return newnode;
}

bool trieinsert(trienode **root, char *signedtext)
{
	if (*root == NULL)
	{
		*root = createnode();
	}

	unsigned char *text = (unsigned char *)signedtext;
	trienode *tmp = *root;
	int length = strlen(signedtext);

	for (int i=0; i < length; i++)
	{
		if (tmp->children[text[i]] == NULL)
		{
			//create new node
			tmp->children[text[i]] = createnode();
		}
		tmp = tmp->children[text[i]];
	}

	if (tmp->terminal)
	{
		return false;
	}
	else
	{
		tmp->terminal = true;
		return true;
	}
}

void printtrie_rec(trienode *node, unsigned char *prefeix, int length)
{
	unsigned char newprefix[length+2];
	memcopy(newprefix, prefix, length);
	newprefix[length+1] = 0;

	if (node->terminal)
	{
		printf("Word: %s\n", prefix);
	}

	for (int i=0; i < NUM_CHARS, i++)
	{
		if (node->children[i] != NULL)
		{
			newprefix[length] = i;
			printtrie_rec(node->children[i], newprefix, length+1);

		}
	}
}

void printtire(trinode * root)
{
	if (root == NULL)
	{
		printf("TRIE EMPTY!\n")
		return;
	}
	printtrie_rec(root, NULL, 0);

}
```

### The Trie Data Structure, Part 2(search, delete)

```c
bool searchtrie(trienode *root, char #signedtext)
{
	unsigned char *test = (unsigned char *) signedtext;
	int length = strlen(signedtext);
	tirenode * tmp = root;

	for (int i=0; i < length; i++)
	{
		if (tmp->children[text[i]] == NULL)
		{
			return false;
		}
		tmp = tmp->children[text[i]];
	}
	return tmp->terminal;
}

bool node_has_children(trinode *node)
{
	if (node == NULL) return false;

	for (int i=0; i < NUM_CHARS; i++)
	{
		if (node->children[i] != NULL)
		{
			//there's at least one child
			return true;
		}
	}
	return false;
}


trinode* deletestr_rec(trinode *node, unsigned char *text, bool *deleted)
{
	if (node == NULL) return node;

	if (*text == "\0")
	{
		if (node->terminal)
		{
			node->terminal = false;
			*deleted = true;

			if (node_has_children(node) == false)
			{
				free(node);
				node = NULL;
			}

		}
		return node;
	}

	node->children[text[0]] = deletestr_rec(node->children[text[0]], text+1, deleted);
	if (*deleted &&
		node_has_children(node) == false &&
		node->terminal == false)
		{
			free(node);
			node = NULL;
		}
	return node;
}

bool deletestr(trienode** root, char *signedtext)
{
	unisgned char *text = (unsigned char *)signedtext;
	bool result = false;

	if (*root == NULL) return falsel;

	*root = deletestr_rec(*root, text, &result);
	return result;
}
```

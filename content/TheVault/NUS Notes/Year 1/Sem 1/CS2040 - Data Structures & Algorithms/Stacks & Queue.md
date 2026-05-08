---
title: Stacks & Queue
Date Created: 2023-06-27
tags:
  - CS2040
  - Stack
  - Queue
  - DataStructures
---
# Table of Contents
---
- [[#Stacks|Stacks]]
	- [[#Stacks#Stack Visualization|Stack Visualization]]
	- [[#Stacks#Stack Usages|Stack Usages]]
- [[#Queue|Queue]]
	- [[#Queue#Queue Visualization|Queue Visualization]]
	- [[#Queue#Implementation|Implementation]]
		- [[#Implementation#Array|Array]]
			- [[#Array#Expending the array|Expending the array]]
		- [[#Implementation#Linked List|Linked List]]
---
# Stacks
---

Stacks uses the **last in first out** concept.
> The last item that was pushed into the stack will be removed first

It can be represented using a linked list.

## Stack Visualization
---

| Item | Position |
| ---- | -------- |
| 1    |   Last Item, first to leave       |
| 2    |          |
| 3    |     First Item     |

Every time an item is added or removed from the stack, it will take <b><mark class="hltr-red">O(1)</mark></b> time.

## Stack Usages
---
1. Bracket Matching

Given an equation with many brackets, a stack can be used to see if its valid.

It matches the nearest unmatched bracket type on the left. 

Thus all open brackets should be placed in the stack, the close backet will be checked with the first item in the stack.

2. Postfix Calculator

Using a stack, a general equation can be calculated

Example: 2 3 + 4 * , this is a postfix version of (2 + 3) * 4.

**Infix**
>An equation where it looks like, 1 + 2

**Prefix**
>An equation where it looks like + 1 2

**Postfix**
> An equation where it looks like 1 2 +

# Queue
---

Queues uses the *first in first out* concept.
> The first item that is placed into the queue will be the first to be dequeued

Queues <span style='color:#fa8231'>maintains</span> the order the items are kept.

## Queue Visualization
---

| Item | Position |
| ---- | -------- |
| 1    |   First Item, first to leave       |
| 2    |          |
| 3    |     Last Item     |

## Implementation
---
### Array

Using an array, for a queue the algorithm needs to keep track of 2 indexes, the <b><mark class="hltr-orange">front</mark></b> and the <b><mark class="hltr-orange">back</mark></b>.

However one <span style='color:#eb3b5a'>main problem</span>, is that the array size is fixed. One way we can go around this is to simulate a <b><mark class="hltr-orange">"circular array"</mark></b>.

To know if the array is full:
1. A <span style='color:#0fb9b1'>queue size</span> can be maintain
2. A <span style='color:#20bf6b'>1 empty spot</span> can be used to determine a full array, `Full array = ((Back + 1) % maxsize == Front)`

#### Expending the array

When expanding the array, the existing <mark class="hltr-red">items cannot be transferred based on indexing</mark>. 

| Original Array |     |     | B   | F   |     |
|:--------------:| --- | --- | --- | --- | --- |
|       1        | 2   | 3   |     | 4   | 5   |

| Temp Array |     |     | B   | F   |     |     |     |     |     |     |
|:----------:| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     1      | 2   | 3   |     | 4   | 5   |     |     |     |     |     |

From the visualization above, the empty spaces are not continuous. And thus the concept of the queue will be broken.

Thus to reassign the items to the new array, `temp[j] = arr[(front+j) % maxSize]` is used to bring the <mark style='background:#fa8231'>front element to index 0</mark> of the new array.


### Linked List

The variant of the linked list to use for a queue is a <mark style='background:#3867d6'>tail linked list</mark>. As tail will keep track of the last item.

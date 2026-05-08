---
title: List ADT
Date Created: 2023-06-27
tags:
  - CS2040
  - DataStructures
  - Lists
---
# Table of Contents
---
- [[#What's a List|What's a List]]
- [[#Implementations|Implementations]]
	- [[#Implementations#Java Array|Java Array]]
		- [[#Java Array#Issues with Java Array|Issues with Java Array]]
		- [[#Java Array#Analysis with Java Array|Analysis with Java Array]]
	- [[#Implementations#Linked List|Linked List]]
		- [[#Linked List#Concept of Linked List|Concept of Linked List]]
		- [[#Linked List#Variants|Variants]]
			- [[#Variants#Tailed Linked List|Tailed Linked List]]
			- [[#Variants#Circular Linked List|Circular Linked List]]
			- [[#Variants#Doubly Linked List|Doubly Linked List]]
---

# What's a List
---

It is used in general to <span style='color:#f7b731'>manage data</span>.

A list should have 3 basic functionalities:
1. <span style='color:#f7b731'>Add</span> Data
2. <span style='color:#f7b731'>Remove</span> Data
3. <span style='color:#f7b731'>Query</span> Data

Using an List ADT, different implementations can be used to create a List.

# Implementations
---

## Java Array
---
Using the a Java array as a way of implementing a list is doable with additional functionality.

Array creation with a size of n, i.e. `int[] arr = new arr[n];`, will take <b><mark class="hltr-red">O(n)</mark></b> time.

<span style='color:#3867d6'>ListUsingArray.java</span> to see the full implementation using Java Arrays.

### Issues with Java Array

Java's arrays are <mark class="hltr-blue">static</mark>, once created it cannot be changed. Thus when the list is filled it need to be recreated with a larger size. This makes the array <mark class="hltr-blue">dynamic</mark> instead of static.

```Java
import java.util.*; 
class ListUsingArray implements ListInterface { 
	public int capacity = 1000; // size of the array 
	public int num_items; // number of items in the array 
	public int[] arr = new int[capacity];
	
	// helper non-interface methods
	 
	public void insert(int index, int item) { 
	if (num_items+1 > capacity) // array is full, enlarge it 
		enlargeArr(); 
	for (int i=num_items-1; i >= index; i--) // create gap 
		arr[i+1] = arr[i]; 
	arr[index] = item; // insert item in gap 
	num_items++; 
	}
	// Extend the array size
	public void enlargeArr() { 
		int newSize = capacity * 2; // double the size 
		int[] temp = new int[newSize]; if (temp == null) { // not enough memory 
		System.out.println("run out of memory!"); 
		System.exit(1); 
		} 
		// copy the original array to the new array 
		for (int j=0; j < num_items; j++) 
			temp[j] = arr[j]; 
		arr = temp; // point arr to the new array 
		capacity = newSize; 
		} 
	}
}
```

### Analysis with Java Array

It will take <b><mark class="hltr-red">O(n)</mark></b> time to insert an item, if it is at the start or if there is no space.

The <span style='color:#0fb9b1'>Amortized case</span> for insertion is at most <b><mark class="hltr-red">O(1)</mark></b>. Why is that so, with our implementation of the list, the array will double in size for every 2<sup>n</sup> items. Thus for the majority of our incretions will be of O(1), time and occasionally O(n) when the array is filled.   

## Linked List
---

### Concept of Linked List

Each item will represent a node, containing the <span style='color:#f7b731'>value</span> and the <span style='color:#f7b731'>reference to the next node</span>.

The end of the link will have no neighbors, thus it will be `NULL`.

The <span style='color:#f7b731'>Head</span> is a variable that points to the first node. If the head is removed (points to null). The whole list will be reclaimed.

The sequence to insert and delete items is important. If incorrect the link list will be broken or incorrect.


### Variants
---

#### Tailed Linked List

It is the same as a linked list but it has an extra attribute called `tail`, which points to the last node in the list.

It takes <b><mark class="hltr-red">O(n)</mark></b> for deletion of last item as we need to get the 2nd last item before deletion, but for incretion is <b><mark class="hltr-red">O(1)</mark></b>.

#### Circular Linked List

The last node in the list will have a reference back to the first node of the list.

It has a tail reference

<span style='color:#3867d6'>CircularLinkedList.java</span> to learn more about the circular linked list.

#### Doubly Linked List

Instead of a node having a pointer to the next node. It will additionally have a pointer to the previous node as well.

It has a tail reference

<span style='color:#3867d6'>DListNode.java</span> to learn more about doubly linked list.
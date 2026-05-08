---
title: Binary Heap
Date Created: 2023-04-07
tags:
  - CS2040
  - Heap
  - DataStructures
---

# Priority Queue ADT
---
# Table of Contents
---
- [[#Idea|Idea]]
- [[#What is a Binary Heap|What is a Binary Heap]]
	- [[#What is a Binary Heap#Height of a Tree|Height of a Tree]]
	- [[#What is a Binary Heap#Properties of a Binary Heap|Properties of a Binary Heap]]
	- [[#What is a Binary Heap#Storing a Binary Heap|Storing a Binary Heap]]
	- [[#What is a Binary Heap#Inserting in a Binary Heap|Inserting in a Binary Heap]]
	- [[#What is a Binary Heap#Extraction in a Complete Binary Heap|Extraction in a Complete Binary Heap]]
	- [[#What is a Binary Heap#Creation of a Binary Heap|Creation of a Binary Heap]]
		- [[#Creation of a Binary Heap#Slow Version|Slow Version]]
		- [[#Creation of a Binary Heap#Fast Version|Fast Version]]
	- [[#What is a Binary Heap#Sorting with Binary Heap|Sorting with Binary Heap]]
---

# Idea

A queue where its values are stored based on the items <b><span style='color:#f7b731'>priority value</span></b> and also follows the first in last out method.

The ADT will need to store items based on priority value as well as the time of when the item is added.

# What is a Binary Heap
---

A binary heap has a similar data structure as a <span style='color:#20bf6b'>tree</span>.
> A tree is a node, with a left and right child

<b><span style='color:#2d98da'>Complete Tree</span></b> : Every level, is completely filled except the last level where the nodes must be far left as possible.
<b><span style='color:#2d98da'>Perfect Tree</span></b> : Every level, including the last is completely filled

## Height of a Tree

The height of a tree is approximately : <b><mark class="hltr-red">O(Log N)</mark></b>

**Proving height is O(Log N)**
1) Number of leaves = $(n+1) / 2 ≈ n / 2$ 
2)  Size of the tree (n) = $1 + 2^h$
3)  Log on both sides : $log n = log 1 + log 2^h$
4)  Simplifying it and removing constants : $h = log n$

Nodes at a height of h = <b><mark class="hltr-red">Ceiling( N / 2<sup>h +1</sup> )</mark></b>

## Properties of a Binary Heap

1) **Max Heap**
A max heap is where the children of the parent node must be <b><span style='color:#f7b731'>smaller</span></b> and the root stores the largest number

2) **Min Heap**
A min heap is where the children of the parent node must be <b><span style='color:#f7b731'>bigger</span></b> and the root stores the smallest number

## Storing a Binary Heap

To store a heap, use a <span style='color:#0fb9b1'>1-based array</span>, where using a 0-based array will cause issues with navigation.

`parent(i) = floor (i/2)`, where I cannot be 1 because its the root
`left(i) = 2 * i`, where the value is smaller than heap size
`right(i) = 2 * i + 1*`, where the value is smaller than heap size

## Inserting in a Binary Heap

Inserting an item will, start at the <b><span style='color:#f7b731'>back</span></b> of the array to, maintain a <b><span style='color:#f7b731'>perfect binary tree</span></b>.

After inserting, check if the heap is still valid, if not execute a <b><span style='color:#2d98da'>shift-up function</span></b> until the tree is fixed or the root has been reached.

The time complexity of <b><span style='color:#2d98da'>shift-up function</span></b> : <b><mark class="hltr-red">O(log n)</mark></b>, or <b><mark class="hltr-red">Height(i)</mark></b>.

```Java
// Pesudocode for insert
insert(v){ // O(log n)
	heapsize += 1 // Increment size by 1 as a new item is being added
	A[heapsize] = v
	shiftUp(heapsize)
}

// Pesudocode for shift up
shiftUp(i){ // O(log n)
	// Worst case, shift from leaf to root which is the height of tree.
	while i > 1 and A[parent(i)] < A[i] // swap and we are not at the root
	swap(A[i], A[parent(i)]) 
	i = parent(i)
}
```

## Extraction in a Complete Binary Heap

Extraction will retrieve the <b><span style='color:#f7b731'>root node</span></b> and the <b><span style='color:#f7b731'>last leaf</span></b> will become the new root.

Afterwards do a <b><span style='color:#2d98da'>shift-down function</span></b>, until there is no bigger child node or the leaf is reached.

For deletion/updating of a heap, replace the node with the last leaf then call either <b><span style='color:#2d98da'>shift-up function</span></b> or <b><span style='color:#2d98da'>shift-down function</span></b>.

The time complexity of  <b><span style='color:#2d98da'>shift-down function</span></b> : <b><mark class="hltr-red">O(log n)</mark></b> 

```Java
// Pesudocode for shift down
shiftDown(i){
	// This while loop will run at most from the root to a leaf, thus the height of the tree
	while i <= heapsize 
		maxV = A[i]; 
		max_id = i;
		// If the left is the bigger number
		if left(i) <= heapsize and maxV < A[left(i)];
			maxV = A[left(i)];
			max_id = left(i) ;
		// If right is the bigger number
		if right(i) <= heapsize and maxV < A[right(i)] 
			maxV = A[right(i)]; 
			max_id = right(i) // be careful with the implementation
		// If there is a larger number do a swap else break the while loop	 
		if (max_id != i) 
			swap(A[i], A[max_id]) 
			i = max_id; 
		else 
			break;
}

// Pesudocode for extract max
ExtractMax(){
	maxV = A[1];
	A[1] = a[heapsize]; // Last leaf becomese the root
	heapsize -= 1;
	shiftDown(1)
	return maxV
}
```

## Creation of a Binary Heap

### Slow Version

Time complexity : <b><mark class="hltr-red">O(n log n)</mark></b>

```Java
// Pesudocode to create a binary heap
CreateHeapSlow(arr) {
	N = arr.length();
	A[0] = 0 // Dummy entry, as we are using a 1 indexed array
	for (int i = 0; i < N; i++){ // O(n)
		Insert(arr[i]) // O(log n)
	}
}
```

**Proving time complexity is N log N**

1)  For loop will iterate N times, O(N)
2)  Each iteration Insert function is called, O(log n)
3)  Time = $log 1 + log 2 + log 3 + ... + log n$ , why 1 as tree is empty, afterwards inserting 2nd item and so on
4)  Simplifying it, $log n! = n log n$

### Fast Version

Time complexity : <b><mark class="hltr-red">O(n)</mark></b>

```Java
// Pesudocode to create a binary heap
CreateHeap(arr){
	heapsize = arr.length();
	A[0] = 0 // Dummy entry
	for (int i = 1; i < heapsize; i++){ // O(n)
		A[i] = arr[i-1]
	}
	
	// O(n/2) because we need to check for half of the tree and not the leaves
	for (int i = parent(heapsize); i >= 1; i--){
		shiftDown(i);
	}
}
```

This works, as it builds valid smaller heaps (sub heaps) in the binary heap.

Why this is faster is because, every children of the parent node will be compared with each other to check if its in the correct spot, it not the parent will have to shift down with the child node.

## Sorting with Binary Heap

Time complexity: <b><mark class="hltr-red">O(n log n)</mark></b>

```Java
HeapSort(Arr){
	Createheap(arr) // O(n) if you use the fast version
	int n = array.length();
	int[] A = new int[array.length]
	for (int i = 0; i < n; i++){ // O(n)
		A[N-i] = ExtractMax(Heap) // O(log n), add to the back if its a Max Heap
	return a;
	}
}
```

It can can be <b><span style='color:#f7b731'>in-place</span></b>. When an item is extracted, the last index in the array will be available as it will be replaced as a root (index 1). Thus the extracted value can be placed at the back

However is <b><span style='color:#eb3b5a'>not cache friendly</span></b>. As when a computer reads an array, it will also read those that are near by. However the children nodes are far apart from the parent node based on the index; (2n +1).
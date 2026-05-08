---
title: Heaps
Date Created: 2024-09-27
Last Updated: 2025-10-20
tags:
  - CS2040S
  - DataStructures/Heaps
  - Sorting/HeapSort
---
# Priority Queue
---
A <span style='color:#0fb9b1'>priority queue</span> is something like a <span style='color:#8854d0'>binary tree</span> but with a special property where
- All nodes in each sub tree are **smaller** (<span style='color:#0fb9b1'>Max Heap</span>)
- All nodes in each sub tree are **bigger** (<span style='color:#0fb9b1'>Min Heap</span>)  

Thus the <span style='color:#f7b731'>height</span> of a heap is <span style='color:#f7b731'>log n</span>, to be more accurate it will be $\color {#f7b731} {\lfloor log(n) \rfloor}$.

It also has additional functions called `increaseKey` and `decreaseKey` which <span style='color:#f7b731'>changes the priority</span> of the given key. This priority value determines where this node is stored in the heap.

At every instance, this heap **must** be a <span style='color:#8854d0'>complete binary tree</span>. To achieve this every <span style='color:#f7b731'>insert will be the left most possible leaf in the lowest height</span> node and then <span style='color:#2d98da'>bubble up</span>. 

Bring a <span style='color:#8854d0'>complete binary tree</span> <span style='color:#f7b731'>allows a heap to be stored in an array</span>, where the root is at index 0 while its children are in index 1 and 2 and so on.

**In general :**
- `parent(i) = floor ((i-1)/2)`
- `left(i) = 2 * i + 1`
- `right(i) = 2 * i + 2`

Storing a heap as an <span style='color:#8854d0'>AVL tree</span>, can be <span style='color:#eb3b5a'>costly due to ensuring rotations</span> as well as <span style='color:#eb3b5a'>ensuring heap ordering property</span> and the complete binary tree structure.
## Inserting into a Heap

When <span style='color:#fa8231'>inserting</span> into a <span style='color:#0fb9b1'>heap</span> :
- <span style='color:#f7b731'>Add</span> the new item <span style='color:#f7b731'>to the leaf</span> of the heap (Lets give this new node a priority value of $x$)
- Then this node needs to <span style='color:#2d98da'>bubble up</span> to the correct position

**Why need to bubble up**
>This function is used to <span style='color:#f7b731'>reposition</span> the newly added node to <span style='color:#f7b731'>not violate the heap ordering property</span>
<div style="break-after: page;"></div>

When <span style='color:#2d98da'>bubbling up</span> :
- <span style='color:#f7b731'>Compare</span> itself <span style='color:#f7b731'>with the parent</span> node until the root node is reached which can have 2 outcomes
	1) The parent node <span style='color:#eb3b5a'>violates</span> the heap ordering property, then <span style='color:#f7b731'>swap position</span> with the parent node and itself
	2) The parent node <span style='color:#20bf6b'>does not violate</span> the heap ordering property, then <span style='color:#f7b731'>terminate</span> from the function

This `bubbleUp` function <span style='color:#fa8231'>does not do</span> the following
- Violate the heap ordering property since it knows if it is bigger/smaller before swapping
- It does not break the structure of the tree

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>
## Changing Priority Value

The 2 operations to do this are `increaseKey` & `decreaseKey` and to <span style='color:#fa8231'>efficiently find the node</span> to be changed a [[quartz/content/Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Hashing#Symbol Table|hash table]] can be used along side the heap.

The problem is **after updating** the node, it <span style='color:#eb3b5a'>might not be in the correct position</span>, thus after updating, it needs to be <span style='color:#2d98da'>bubbled up</span> again to the correct position, but this only works for `increaseKey`.

For `decreaseKey`, it should <span style='color:#2d98da'>bubble down</span> instead.

When <span style='color:#2d98da'>bubbling down</span> :
- <span style='color:#f7b731'>Compare</span> itself <span style='color:#f7b731'>with the 2 child</span> node until the leaf is reached which can have 2 outcomes
	1) The parent node <span style='color:#eb3b5a'>violates</span> the heap ordering property, then <span style='color:#f7b731'>swap position</span> with the <span style='color:#f7b731'>bigger priority child</span>
	2) The parent node <span style='color:#20bf6b'>does not violate</span> the heap ordering property, then <span style='color:#f7b731'>terminate</span> from the function

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>, this is **with the help of the hash table**
## Removing from the Heap

There are some helper functions needed before <span style='color:#2d98da'>removing</span> an item one is `swap` the other is `last`.

The `last` function just gets the <span style='color:#f7b731'>right most leaf in the lowest height</span> in the heap while `swap` just <span style='color:#f7b731'>swaps the 2 </span>nodes around.
<div style="break-after: page;"></div>

Thus for <span style='color:#2d98da'>deletion</span>, it will execute as follows :
- `Node lastNode = last()`
- `swap(key, lastNode`
- `remove(lastNode)`
- `bubbleDown(lastNode)`
### Removing Max / Min

These are similar to the <span style='color:#2d98da'>deletion</span> of a node. However with heaps the minimum or maximum <span style='color:#f7b731'>value will be in the root</span>.

Then when <span style='color:#fa8231'>removing</span> just do the following :
- `Node root = root`
- `delete(root)`

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>

# Heap Sort
---
It is possible to get a <span style='color:#fa8231'>sorted list from a heap</span> :
- Just keep on calling `extractMax` or `extractMin` depending on the type of heap
- If the value is a maximum value then put at the back of the array, and if its a minimum value put at the front

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(n log n)</span></b>, which is no different than the other [[quartz/content/Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Sorting|sorting algorithms]]

## Building a Heap

Now to build a heap there are <span style='color:#fa8231'>2 ways to build a heap</span> :
1) Unsorted List $\to$ Heap
2) Sorted List $\to$ Heap

The general idea of <span style='color:#fa8231'>building a heap</span> from an array is the following :
- Iterate through the whole array
- For each element just use the `insert(key)` function

**Time complexity :** <b><span style='color: var(--mk-color-red)'>O(n log n)</span></b>, which is ok but there is a better solution
<div style="break-after: page;"></div>

There is a way to construct a heap in <span style='color:#20bf6b'>linear time</span> and this is called `heapify`, which uses recursion. 1 observation is that now all nodes must be shifted in particularly the <span style='color:#f7b731'>leaves don't need to be checked</span>. 

Even though the leaves might be in the wrong order but after <span style='color:#2d98da'>bubbling</span> from the nodes above it will be in its correct place. And the <span style='color:#f7b731'>cost</span> of <span style='color:#2d98da'>bubbling down</span> <span style='color:#f7b731'>depends on the height</span> thus starting at the bottom will be faster.

How to <span style='color:#fa8231'>carry out</span> `heapify`
- Let the given array be the final heap shape
- Start with the <span style='color:#f7b731'>smallest subtree </span>with whose <span style='color:#f7b731'>node is not a leaf node</span>
- Then call <span style='color:#3867d6'>bubble down</span> from that node
- Repeat the process by going towards `index - 1`, where index is the node of the smallest subtree

In general, just start from the parent $n$ where $n$ is the size of the array, `parent(n) = floor ((n-1)/2)`. This will be the first non leaf node and just move towards index 0.

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(n)</span></b>

---
title: Binary Tree
Date Created: 2022-06-06
tags:
  - CS2040
  - Trees
  - DataStructures
---
# Table of Contents
---
- [[#Binary Search Tree|Binary Search Tree]]
	- [[#Binary Search Tree#Ordered Map|Ordered Map]]
	- [[#Binary Search Tree#Finding Successor / Predecessor|Finding Successor / Predecessor]]
		- [[#Finding Successor / Predecessor#Predecessor|Predecessor]]
			- [[#Predecessor#Steps to Find Predecessor|Steps to Find Predecessor]]
		- [[#Finding Successor / Predecessor#Successor|Successor]]
			- [[#Successor#Steps to Find Successor:|Steps to Find Successor:]]
	- [[#Binary Search Tree#Inserting / Searching in a Binary Search Tree|Inserting / Searching in a Binary Search Tree]]
	- [[#Binary Search Tree#Find Minimum / Maximum|Find Minimum / Maximum]]
	- [[#Binary Search Tree#Deletion in a Binary Search Tree|Deletion in a Binary Search Tree]]
	- [[#Binary Search Tree#Traversing a Binary Search Tree|Traversing a Binary Search Tree]]
		- [[#Traversing a Binary Search Tree#In-order|In-order]]
		- [[#Traversing a Binary Search Tree#Pre-order|Pre-order]]
		- [[#Traversing a Binary Search Tree#Post-order|Post-order]]
- [[#AVL Tree|AVL Tree]]
	- [[#AVL Tree#Why Use an AVL Tree|Why Use an AVL Tree]]
	- [[#AVL Tree#Additional Attributes for AVL Tree|Additional Attributes for AVL Tree]]
		- [[#Additional Attributes for AVL Tree#Height|Height]]
		- [[#Additional Attributes for AVL Tree#Size|Size]]
	- [[#AVL Tree#Implementing the AVL Tree|Implementing the AVL Tree]]
		- [[#Implementing the AVL Tree#Augment the BST|Augment the BST]]
		- [[#Implementing the AVL Tree#Define a Balance Factor|Define a Balance Factor]]
	- [[#AVL Tree#Balancing the AVL Tree|Balancing the AVL Tree]]
		- [[#Balancing the AVL Tree#Right Rotation|Right Rotation]]
		- [[#Balancing the AVL Tree#Left Rotation|Left Rotation]]
		- [[#Balancing the AVL Tree#Rebalancing Cases|Rebalancing Cases]]
			- [[#Rebalancing Cases#Left Left Case|Left Left Case]]
			- [[#Rebalancing Cases#Left Right Case|Left Right Case]]
			- [[#Rebalancing Cases#Right Right Case|Right Right Case]]
			- [[#Rebalancing Cases#Left Right Case|Left Right Case]]
	- [[#AVL Tree#Get Rank in a AVL Tree|Get Rank in a AVL Tree]]
	- [[#AVL Tree#Selecting in a AVL Tree|Selecting in a AVL Tree]]
---

# Binary Search Tree
---

## Ordered Map

A BST is a ordered map, items placed have some ordering.

In a BST, the <span style='color:#f7b731'>smaller item is placed on the left</span> while the <span style='color:#f7b731'>larger or similar item is placed on the right</span>.

A perfect binary tree, is arranged just like a binary search. Where going left or right will equality partition N items. Therefore, our time complexity is <b><mark class="hltr-red">O(log n)</mark></b>.

## Finding Successor / Predecessor

Time complexity for both functions : <b><mark class="hltr-red">O(log n) / O(h)</mark></b>

### Predecessor

A predecessor of a vertex is the <span style='color:#f7b731'>largest number in the tree that is smaller than the vertex</span>.

#### Steps to Find Predecessor
1) <span style='color:#3867d6'>Search</span> vertex in the BST
2) Check if there is a <span style='color:#0fb9b1'>left child</span>, if true call `FindMax(T.left)`
3) Else, start from the parent and go up until there is a <mark class="hltr-cyan">left turn</mark> , `T.parent.right = T`
4) If the <span style='color:#0fb9b1'>root node</span> is hit and there is <mark class="hltr-cyan">no left child</mark>, there is no predecessor

### Successor

A successor of a vertex is the <span style='color:#f7b731'>smallest number in the tree that is greater than the vertex</span>.

#### Steps to Find Successor:
1) <span style='color:#3867d6'>Search</span> vertex in the BST
2) Check if there is a <span style='color:#0fb9b1'>right child</span>, if true call `FindMin(T.left)`
3) Else, start from the parent up until there is a <mark class="hltr-cyan">right turn</mark> , `T.parent.left = T`
4) If the <span style='color:#0fb9b1'>root node</span> is hit and there is <mark class="hltr-cyan">no right child</mark>, there is no successor

## Inserting / Searching in a Binary Search Tree

For both searching and inserting of a node it will start from the <span style='color:#0fb9b1'>root node</span>. If the value of the node is smaller, move to the right, else move to the left.

For <span style='color:#3867d6'>Inserting</span>, once a node with no child is found, insert it.

For <span style='color:#3867d6'>Searching</span>, once a node with the same value is found, return the node. If null is reached, return false.

Time complexity for both functions : <b><mark class="hltr-red">O(log n) / O(h)</mark></b>

## Find Minimum / Maximum

The smallest / largest node in a BST is the <mark class="hltr-cyan">most left / right node that has no left / right child</mark> respectively.

To get it, modify the <span style='color:#3867d6'>Search</span> function, to always go to the left / right child, until it cannot. 

Time complexity for both functions : <b><mark class="hltr-red">O(log n) / O(h)</mark></b>

## Deletion in a Binary Search Tree

For any deletion, a search function is called to find the vertex.

If the vertex is a <span style='color:#0fb9b1'>leaf</span>, then set the parent's left or right to null.

If the vertex has <span style='color:#0fb9b1'>one sub-tree</span>, bypass the sub-tree under the parent, `T.parent = T.left/T.right`

If the vertex has <span style='color:#0fb9b1'>two sub-tree</span>, replace the node with the <span style='color:#3867d6'>successor</span> and afterwards, <span style='color:#3867d6'>delete</span> successor.

Time complexity for deletion : <b><mark class="hltr-red">O(log n) / O(h)</mark></b>

## Traversing a Binary Search Tree

In general to print out every item in a BST, it will use the following code:
```Java
public static void printtree(Vertex T){
	if (T == null){
		return;
	}
	else{
		printtree(T.left);
		System.out.println(T.key);
		printtree(T.right);
	}
}
```

Time complexity for <span style='color:#f7b731'>any</span> traversing function is: <b><mark class="hltr-red">O(n)</mark></b>, where n is the number of vertices.

Why is the time **O(n)**:
1) For each node, it will <span style='color:#f7b731'>recursively call the left and right</span> subtree of that node.
2) Once a node is processed it will not be revisited
3) Each node will be returned at <span style='color:#f7b731'>most 3 times</span>
	1) First time to visit that node
	2) Second time after processing the left subtree
	3) Third time after processing the right subtree
4)  Thus in total it will be <span style='color:#eb3b5a'>O(3n) = O(n)</span>

### In-order

The code above shows a <span style='color:#3867d6'>in-order</span> traversal where;
1)  The vertices on the left will be processed first
2)  The parent vertex will be processed second
3)  The vertices on the right will be processed last

This is the only traversal which results in a <span style='color:#f7b731'>ordered sequence in ascending order</span>.

### Pre-order

A <span style='color:#3867d6'>pre-order</span> traversal is where the parent node will be processed <mark class="hltr-cyan">first</mark>;
1) The parent vertex will be processed first
2)  The vertices on the left will be processed second
3)  The vertices on the right will be processed last

### Post-order

A <span style='color:#3867d6'>post-order</span> traversal is where the parent node will be processed <mark class="hltr-cyan">last</mark>;
1)  The vertices on the left will be processed first
2)  The vertices on the right will be processed second
3)  The parent vertex will be processed last

# AVL Tree
---

## Why Use an AVL Tree

The runtime for BST operations can only be achieved if the BST is <span style='color:#f7b731'>not heavily skewed to one side</span>, height = number of nodes, <b><mark class="hltr-red">O(n)</mark></b>.

To prevent this the tree must be <span style='color:#f7b731'>balanced</span> and the AVL tree is one such methods to balance it.

Thus a AVL Tree is just a <span style='color:#3867d6'>perfect binary tree</span>, where h >= `floor( log(n) )` and operations take <b><mark class="hltr-red">O(log n)</mark></b>.

## Additional Attributes for AVL Tree

### Height

It is the <span style='color:#f7b731'>number of edges</span> from this <span style='color:#0fb9b1'>vertex</span> to the <span style='color:#0fb9b1'>deepest leaf</span>.

For an <span style='color:#f7b731'>empty tree / null</span>, height = - 1
For <span style='color:#f7b731'>all</span> other cases, height = `Max(x.left.height, x.right.height) + 1`

A minimum number of nodes with a specific height = N(h-1) + N(h-2) + 1

![[Height Example of a AVL Tree.png|center]]

### Size

The number of <span style='color:#0fb9b1'>vertices</span> of the <span style='color:#f7b731'>subtree rooted at this vertex</span>.

For an <span style='color:#f7b731'>empty tree / null</span>, height = - 1
For <span style='color:#f7b731'>all</span> other cases, height = `x.left.size + x.right.size) + 1`

![[Size Example of a AVL Tree.png|center]]

## Implementing the AVL Tree

### Augment the BST

In the BST, for every vertex include a <span style='color:#0fb9b1'>height</span> and <span style='color:#0fb9b1'>size</span> attribute.

And during any <span style='color:#3867d6'>insertion</span> and <span style='color:#3867d6'>deletion</span>, the height of the node must be updated using:
`x.height = max(x.left.height, x.right.height) + 1`

### Define a Balance Factor

A <span style='color:#0fb9b1'>balance factor</span>, is a threshold to indicate if the tree is imbalanced or not. This a tree to be <span style='color:#f7b731'>height balanced</span> if every vertex is also height balanced.

Balance Factor = `x.left.height - x.right.height`

The value in this case is usually **1**, however 0 can be used if a perfect binary tree is needed.

## Balancing the AVL Tree

Using the formula for balance factor `bf(x) = x.left.height - x.right.height`, if the value is <span style='color:#f7b731'>greater than 2 or smaller than -2</span>, the tree is imbalanced. Thus a <span style='color:#3867d6'>tree rotation</span> is needed

Example of a rotation:
```Java
public BSTVertex rotateLeft(BSTVertex T){ // For rotate right just reverse the code
	BSTVertex w = T.right; // Get the right child
	
	w.parent = T.parent; // Set w parent to be T parent, as we are swaping T with w
	T.parent = w; // Set the parent of T to be w
	T.right = w.left; // Set the left node of w to be the right of T
	
	if(w.left != null){ // If its not null. then parent of w left is T.
		w.left.parent = T;
	}
	
	w.left = T; // Lastly assign w.left to T
	
	update_height(T);
	update_size(T);
	
	update_height(w);
	update_size(w);
	
	return w; // Returning w will allow the caller, w.parent to update accordingly to set w as its child
}
```

### Right Rotation

Before a right rotation can be executed, the vertex V <mark class="hltr-cyan">must have a left child</mark>

Let the left child be W, make V the right child of W, and make the right child of W be the left child of V

### Left Rotation

Before a right rotation can be executed, the vertex V <mark class="hltr-cyan">must have a right child</mark>

Let the right child be W, make V the left child of W, and make the left child of W be the right child of V


### Rebalancing Cases

#### Left Left Case

This happens when the <span style='color:#0fb9b1'>balance factor</span> is <span style='color:#f7b731'>2</span> and the balance factor of the <span style='color:#f7b731'>left node is 0 or 1</span>

If this happens, then just call `rightRotate(x)`

#### Left Right Case

This happens when the <span style='color:#0fb9b1'>balance factor</span> is <span style='color:#f7b731'>2</span> and the balance factor of the <span style='color:#f7b731'>left node is -1</span>

If this happens, then call;
1) `leftRotate(x.left)` 
2) `rightRotate(x)`

#### Right Right Case

This happens when the This happens when the <span style='color:#0fb9b1'>balance factor</span> is <span style='color:#f7b731'>-2</span> and the balance factor of the <span style='color:#f7b731'>right node is -1 or 0</span>

If this happens, then just call `leftRotate(x)`

#### Left Right Case

This happens when the <span style='color:#0fb9b1'>balance factor</span> is <span style='color:#f7b731'>-2</span> and the balance factor of the <span style='color:#f7b731'>right node is 1</span>

If this happens, then call;
1) `rightRotate(x.right)` 
2) `leftRotate(x)`

## Get Rank in a AVL Tree

A rank of a vertex is the <span style='color:#f7b731'>numbered ordering</span> for that particular vertex <span style='color:#f7b731'>in ascending order</span> based on all the items in the BST. It can be used to check how many items are in a range.

The rank involves the <span style='color:#0fb9b1'>size</span> attribute of a vertex.

How to get a rank of a vertex:
1) <span style='color:#0fb9b1'>Search</span> for the vertex
2)  A rank of a vertex that is either the <span style='color:#f7b731'>root or the left subtree</span> is, `v.left.size + 1`
3)  For the <span style='color:#f7b731'>right subtree</span> is, `Rank(v.right) + v.left.size + 1`

Time complexity for rank : <b><mark class="hltr-red">O(log n) / O(h)</mark></b>

Code for Rank Function:
```Java
public static int rank(Vertex T, int v){
	if (T.key == v){
		return T.left.size + 1;
	}
	else if (T.key > v){
		return rank(T.left,v);
	}
	else{
		return rank(T.right,v) + T.left.size + 1;
	}
}
```

## Selecting in a AVL Tree

Similar to searching, selecting retrieved the vertex based on the <span style='color:#0fb9b1'>rank</span>.

It is used to get the Kth biggest / smallest element in a BST.

To get a vertex with a specific rank:
1) Check the <span style='color:#3867d6'>rank</span> of the <span style='color:#0fb9b1'>root node</span>
2) If the vertex rank is smaller go to the right subtree, else the left subtree
3) If the rank is the same return the vertex

Time complexity for select : <b><mark class="hltr-red">O(log n) / O(h)</mark></b>

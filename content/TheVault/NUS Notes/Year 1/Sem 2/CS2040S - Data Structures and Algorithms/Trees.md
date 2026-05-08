---
title: Trees
Date Created: 2024-04-29
Last Updated: 2025-10-16
tags:
  - CS2040S
  - DataStructures/Tree
---
# Dictionary
---
It is a essentially a <span style='color:#f7b731'>collection of key, value pairs</span>, where it supports the following functionality :

|   Function    |             What does it do?             |
| :-----------: | :--------------------------------------: |
|   `insert`    |        Insert a (Key, Value) pair        |
|   `search`    |       Find the value given the key       |
|  `successor`  |   Find the next largest key given $k$    |
| `predecessor` |   Find the next smallest key given $k$   |
|   `delete`    |      Remove the key from the table       |
|  `contains`   | Check if the key $k$ is inside the table |
|    `size`     |  How many (Key, Value) pairs are there   |
Take note that the <span style='color:#fa8231'>key</span>, is <span style='color:#f7b731'>unique</span>. Any new insert with the <span style='color:#f7b731'>same key will just override the value</span>.

There are many ways to <span style='color:#fa8231'>implement a dictonary</span> with standard <span style='color:#8854d0'>Java</span> data structures :
- **Sorted Array**
- **Unsorted Array**
- **Linked List**
- **Java library dictionary**
<div style="break-after: page;"></div>

# Tree
---
Think of a <span style='color:#0fb9b1'>tree</span> as a node where it branches off to other nodes which also branches of to other nodes.

Some <span style='color:#fa8231'>key components in a tree</span> are :
- **Nodes**
- **Edges**
- **Root**
- **Children**
- **Siblings** (Nodes in the same height)
- **No Cycles** (Main property)

## Binary Search Tree

Also known as <span style='color:#0fb9b1'>BST</span>, is a type of tree structure where it has this neat <span style='color:#fa8231'>property</span> where the <span style='color:#f7b731'>left sub-tree is smaller than the parent node</span> (key), and the <span style='color:#f7b731'>right sub-tree is bigger </span>than the parent node.

### Calculate Height

Number of edges on the <span style='color:#f7b731'>longest path</span> from the node to a leaf. <span style='color:#f7b731'>Leaf nodes are of height 0</span> and any other node will have a height of `max(node.left.height, node.right.height) + 1`

**A simple recursive function to calculate the height**
```Java
int get_height(Node root) {
	if(root == null) {
		return -1; // Anything below leef node is of height -1
	} else {
		if (root.height == null) { // Need to compute
			root.height = max(get_height(root.left), get_height(root.right)) + 1;
		}	
		return root.height;
	}
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>
>Update nodes above, only for deletion and inserting
<div style="break-after: page;"></div>

**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-red)'>O(n)</span></b> 
>Calculate height of every node
### Finding Max or Min key

Now knowing the property of a <span style='color:#0fb9b1'>BST</span>. the <span style='color:#f7b731'>smallest will be on the left most node</span> and the <span style='color:#f7b731'>largest is at the right most node</span>.

**A simple recursive function to get smallest item**
```Java
int get_min(Node root) { // If it is the largest element then go to the right
	if(root.left == null) {
		return root;
	} else {
		return get_min(root.left);
	}
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>
> If it is **balanced**, then only

**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-red)'>O(n)</span></b>
> If it is **heavily skewed to left or right**, basically all the nodes are on the left or right

### Searching for Something

The main goal of <span style='color:#3867d6'>searching</span> is to know <span style='color:#fa8231'>which sub-tree to head to</span> and the same concept for <span style='color:#f7b731'>binary search can be used</span>
<div style="break-after: page;"></div>

**A simple recursive function for search**
```Java
Node search(int target, Node root) {
	if (root == null) {
		return null;
	} else {
		if(root.key == target) {
			return target
		}
		if( root.key < target) {
			return search(root.left, target);
		} else {
			return search(root.right, target);
		}
	}
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>
> If it is **balanced**, then only

**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-red)'>O(n)</span></b>
> If it is **heavily skewed to left or right**, basically all the nodes are on the left or right

### Adding new keys / items

<span style='color:#3867d6'>Inserting</span> new keys into the <span style='color:#0fb9b1'>BST</span>, a <span style='color:#f7b731'>traversal</span> is needed to find the correct spot.

Does every order of <span style='color:#fa8231'>insert yield a unique shape</span>? Well <span style='color:#eb3b5a'>no</span> it follows the <span style='color:#0fb9b1'>Catalan number system</span> which is, $1, 2, 5, 14, 42, 132, 429, 1430, \dots$, when with $n!$ ways to insert.
<div style="break-after: page;"></div>

**A simple recursive function to insert**
```Java
void insert(Node root, Node key) {
	if (root < key) { // If the key is smaller than node value check the left
		if(root.left != null) {
			insert(root.left, key);
		} else {
			root.left = key;
		}
	} else if (root > key) { // If the key is bigger than node value check the right
		if(root.right != null) {
			insert(root.right, key);
		} else {
			root.right = key;
		}
	} else {
		return; // Key is in the BST, meaning node == key
	}
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>
> If it is **balanced**, then only

**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-red)'>O(n)</span></b>
> If it is **heavily skewed to left or right**, basically all the nodes are on the left or right

### Traversal

This <span style='color:#3867d6'>traversal</span> is a method to <span style='color:#f7b731'>view all nodes in the tree</span>. There are a few orders to tis traversal :
1) **In-order** (Left sub-tree, Root node, Right sub-tree)
2) **Pre-order** (Root node, Left sub-tree,  Right sub-tree)
3) **Post-order** (Left sub-tree, Right sub-tree, Root node)
4) **Level-order** (Breath first search!!, use a <span style='color:#8854d0'>queue</span> data structure)
<div style="break-after: page;"></div>

**A simple recursive function for traversal**
```Java
public void inorderTraversal(TreeNode node) {
	// Base case is when node null means there is nothing to add into the array
	if (node == null) {
		return;
	} else {
		inorderTraversal(node.left, arr, ptr); // Go left subtree
        System.out.println(node.value); // Print the node
        inorderTraversal(node.right, arr, ptr); // Go right subtree
    }
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(n)</span></b>

**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-green)'>O(n)</span></b>
> Both are the same since all the nodes will visited once

### Successor / Predecessor

This operation is to find the <span style='color:#f7b731'>next smallest or biggest</span> item based on the key given. Now there are 2 scenarios :
1) The key is **not in the tree** (Find using the next smallest element)
2) The key is **in the tree**

**Code to find successor**
```Java
public Node successor(Node node) {
	if(node.right != null) {
		return node.right.getMin(); // Use the get minimum function on the right subtree
	} else { // No right child, then go up the tree until a right turn is made
		Node child = node;
		Node parent = node.parent;
		while(parent != null && child == parent.right) {
			child = parent;
			parent = child.parent;
		}
		return parent;
	}
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(n)</span></b>

**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-green)'>O(n)</span></b>
> Both are the same since all the nodes will visited once

The main idea for <span style='color:#3867d6'>successor</span> is that :
- If there is a right sub-tree, then the <span style='color:#f7b731'>next biggest element is the smallest element in that tree</span>
- If there is no right sub-tree then go up the tree, as long as the <span style='color:#f7b731'>current node is the right child </span>of the parent, means the <span style='color:#f7b731'>parent is smaller</span>. If it becomes a <span style='color:#f7b731'>left child</span>, then the <span style='color:#f7b731'>parent is bigger</span> than the current node
- If it reaches the root node and there is nothing? Then return `null` since there is no successor.

For <span style='color:#3867d6'>predecessor</span> is the complete opposite of <span style='color:#3867d6'>successor</span> where :
- Find the <span style='color:#f7b731'>largest element in the left sub-tree</span>
- No left sub-tree, then <span style='color:#f7b731'>go up until the node is the the right child</span> instead, if it is the left child then continue upwards
### Deletion

When removing a node from a tree there are <span style='color:#fa8231'>3 cases</span> to consider :
- **No Children** (Leaf)
- **1 Child**
- **2 Children**
<div style="break-after: page;"></div>

**Code to delete a node**
```Java
public Node delete (Node root, int v) {
	if (root == null) root; // cannot find the item to be deleted

    if (root.key < v) // search to the right
      node.right = delete(T.right, v);
    else if (T.key > v)// search to the left
      node.left = delete(node.left, v);
    else { // this is the node to be deleted
      if (node.left == null && node.right == null) // this is a leaf
        node = null; // simply erase this node
      else if (node.left == null && node.right != null) { // only one child at right        
        node.right.parent = node.parent; // Set the right sub-tree to be the partent of node's parent
        node = node.right;  // bypass node such that when this node is returned it will update the parents sub tree       
      }
      else if (node.left != null && node.right == null) { // only one child at left        
        node.left.parent = node.parent;
        node = node.left; // bypass T        
      }
      else {                                 // has two children, find successor
        int successorV = successor(v);
        node.key = successorV;         // replace this key with the successor's key
        node.right = delete(T.right, successorV);      // delete the old successorV
      }
    }
    
    return node;                                          // return the updated BST
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>

**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>

There is something called <span style='color:#0fb9b1'>logical deletion</span>, where it is like a lazy delete where the <span style='color:#f7b731'>node is marked as deleted</span> and the structure is untouched. This can <span style='color:#eb3b5a'>compromise performance later on</span> when there is a lot of deleted items.
<div style="break-after: page;"></div>

# Balanced Tree
---
The <span style='color:#fa8231'>main benefit</span> for a tree being balanced is to <span style='color:#f7b731'>minimise the height</span> since most operations are $O(h)$ and thus most operations will be <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>.

At any given height, the <span style='color:#fa8231'>maximum number of nodes that can be stored at height</span> $h$ is $2^{h}$.

What does it mean to be <span style='color:#0fb9b1'>balanced</span>, a tree is balanced if if <span style='color:#f7b731'>height of the left and right differs no more than</span> $\color {#f7b731} {\pm 1}$. If this restriction is 0, it will be a perfectly balanced tree but this will <span style='color:#eb3b5a'>make operations more coastally to maintain</span> it.

This property makes the tree <b><span style='color: var(--mk-color-turquoise)'>height balanced</span></b>, where the balancing factor is the height. There is also something called <b><span style='color: var(--mk-color-turquoise)'>weight balanced</span></b>, where the balancing factor is the number of nodes in the sub-trees.

## Maintaining the Balance

Now the 2 operations that affects the shape of the tree is only <span style='color:#3867d6'>insert</span> and <span style='color:#3867d6'>deletion</span>. And to maintain the balancing factor, the usage of <span style='color:#f7b731'>tree rotations is needed</span>.

After these 2 operations, just <span style='color:#f7b731'>traverse back up the tree to see if any node violates the balancing property</span> or not. And there is <span style='color:#20bf6b'>only a need to do at most 2 rotations</span> except for <span style='color:#3867d6'>deletion</span> which can take up to <span style='color:#eb3b5a'>O(log n) rotations</span>.

Rotations work is because when rotating, the side with the <span style='color:#f7b731'>larger height will be reduced by 1</span> and the side with the <span style='color:#f7b731'>smaller height will be increased by 1</span>.
### Left / Right Rotations

```Java
public Node rotateLeft(Node T){
	BSTVertex w = T.right;
	
	w.parent = T.parent;
	T.parent = w;
	T.right = w.left;
	if(w.left != null){
			w.left.parent = T;
	}
	
	w.left = T;
	update_height(T); // Update the height again
	update_size(T);
	
	update_height(w);
	update_size(w);

	return w;
}

public Node rotateright(Node T){
    BSTVertex w = T.left; // Go to the left node
    
    w.parent = T.parent; // Since rotating right, the left node will become the new parent
    T.parent = w;
    T.left = w.right;
    
    if(w.right != null){
	    w.right.parent = T;
	}
	
	w.right = T; // Point back to the node 
	
	update_height(T); // Update the height
	update_size(T); // Update the weight which is just take the left and right weight + 1
	
	update_height(w);
	update_size(w);
	
	return w;
}
```

The above is the basis of the 2 rotations, <span style='color:#3867d6'>left</span> and<span style='color:#3867d6'> right rotation</span>, and both of them cost <b><span style='color: var(--mk-color-green)'>O(1)</span></b>

**Conditions**
- To use <span style='color:#3867d6'>rotate right</span>, there <b>must be a left child</b>
- To use <span style='color:#3867d6'>rotate left</span>, there <b>must be a right child</b>

#### Rebalancing Cases

<b><span style='color: var(--mk-color-turquoise)'>Balance factor</span></b>  = `left.height - right.height`
##### Left Left Case

This happens when the <span style='color:#0fb9b1'>balance factor</span> is <span style='color:#f7b731'>2</span> and the balance factor of the <span style='color:#f7b731'>left node is 0 or 1</span> (**Left Heavy**).
If this happens, then just call `rightRotate(x)`.
##### Left Right Case

This happens when the <span style='color:#0fb9b1'>balance factor</span> is <span style='color:#f7b731'>2</span> and the balance factor of the <span style='color:#f7b731'>left node is -1</span> (**Right Heavy**).
<div style="break-after: page;"></div>

If this happens, then call;
1) `leftRotate(x.left)` 
2) `rightRotate(x)`

##### Right Right Case

This happens when the This happens when the <span style='color:#0fb9b1'>balance factor</span> is <span style='color:#f7b731'>-2</span> and the balance factor of the <span style='color:#f7b731'>right node is -1 or 0</span> (**Right Heavy**).

If this happens, then just call `leftRotate(x)`.

##### Right Left Case

This happens when the <span style='color:#0fb9b1'>balance factor</span> is <span style='color:#f7b731'>-2</span> and the balance factor of the <span style='color:#f7b731'>right node is 1</span> (**Left Heavy**).

If this happens, then call;
1) `rightRotate(x.right)` 
2) `leftRotate(x)`

## Augmentation a BBST

Now A BBST is quite basic and can it be <span style='color:#f7b731'>modified</span> such that it can <span style='color:#f7b731'>solve other problems</span>.
### Finding the $k$-th Element

Now intrusively, its good to <span style='color:#fa8231'>store the relative ordering</span>, <span style='color:#0fb9b1'>rank</span> in each node, however that is not efficient since when inserting, <span style='color:#f7b731'>every single node must be updated</span> which will be <b><span style='color: var(--mk-color-red)'>O(n)</span></b>, making insert less efficient.

Why not store the <span style='color:#0fb9b1'>weight</span> in the tree. This <span style='color:#0fb9b1'>weight</span> is the <span style='color:#f7b731'>size of the tree</span> rooted at that node, and it is calculated by `root.left.weight + root.right.weight + 1`.

But remember, when <span style='color:#f7b731'>rotating the weights must be updated.</span>
<div style="break-after: page;"></div>

**Simple recursive function to select kth item**
```Java
public Node select(int k, Node root) {
	int rank = root.left.weight + 1;
	if (rank == k) {
		return root;
	} else if (rank < k) { // We are at some item whos order is smaller than k so go right
		return select(k - rank, root.right); // Minus rank since the left tree is disreguarded
	} else { // We are at some item whos order is bigger than k so go left
		return select(k, root.left);
	}
}
```

How about <span style='color:#fa8231'>finding what rank</span> this element is.

**Simple recursive function to find rank**
```Java
public Node getRank(int key, Node root) {
	Node result = search(root, key);
	if(result == null) {
		return -1;
	} else {
		int rank = result.left.weight + 1; 
		while (result != null) {
			Node parent = result.parent;
			if (parent.right == result) {
				rank += parent.left.weight + 1;
			}
			result = parent
		}
		return rank;
	}
}
```
### Interval Tree

Instead of one value in each node, now <span style='color:#f7b731'>each node is a range or interval</span>. Usually, the tree will sort by the <span style='color:#f7b731'>start point</span> of the interval.

How about searching if a range covers a number, how to traverse. Now the <span style='color:#eb3b5a'>start point can't be reliable</span> as it is <span style='color:#f7b731'>possible that the left or right sub tree does not cover</span> up till that number.

One additional augmentation is to <span style='color:#f7b731'>store the maximum range</span> in a given tree. 
- If the search goes right, then the left subtree has no interval
- If it goes left then the right subtree will not have this interval

This is true if <b><span style='color:#f7b731'>no interval overlaps one another</span></b>. If it does, it is possible that it might be in the other sub-tree at the end of the search.

Thus to search for a number covered by an interval is <b><span style='color: var(--mk-color-green)'>O(log n)</span></b> while finding all intervals will be <b><span style='color: var(--mk-color-green)'>O(k log n)</span></b> where k is the <span style='color:#f7b731'>number of overlapping intervals</span>.

### Orthogonal Range Searching

Given some plane (1D or 2D) with points, determine if a <span style='color:#fa8231'>box</span> (range) <span style='color:#fa8231'>contains at least 1 point</span>.

To store this, all the <span style='color:#f7b731'>data will represent leaves</span> of the tree, and the internal nodes will store the maximum value int he left tree.

Now how to <span style='color:#fa8231'>get all values within a range</span> :
- First traverse through the tree and find the <span style='color:#0fb9b1'>spilt node</span> (Node within the range)
- Afterwards go left first, if the node is greater than `low`, then get all the leaves in the right and go left, else go right
- Once the left sub-tree is done, then go right. If the node is smaller than `low`, then get all the leaves in the left and go right, else go left

The running time is <b><span style='color: var(--mk-color-green)'>O(k + log n)</span></b> where k, is the number of items found (leaves).

What about knowing how many point are in the range :
- Then it is as simple as <span style='color:#fa8231'>augmenting</span> how <span style='color:#f7b731'>many leaves in a given subtree</span>
# Trie
---
What if instead of storing integers, it now stores strings? Well it is still possible but now <span style='color:#fa8231'>comparing strings</span> is costly which takes <b><span style='color: var(--mk-color-red)'>O(L)</span></b> time and thus most operations are now <b><span style='color: var(--mk-color-red)'>O(hL)</span></b> time.

To counter this, our tree now <span style='color:#f7b731'>stores each letter as a linked list</span>.
- The tree has a **start point** and is has edges to all the starting characters of the string
- Any <span style='color:#fa8231'>letter not present</span> when traversing downwards, a <span style='color:#f7b731'>new branch</span> will be made <span style='color:#f7b731'>with that latter and the rest of the letters</span> remaining in that word
- All words will have a <span style='color:#f7b731'>terminating character</span> inside the <span style='color:#0fb9b1'>Trie</span>

Now what is the cost of <span style='color:#3867d6'>searching strings</span>, well it is now just <b><span style='color: var(--mk-color-green)'>O(L)</span></b>. Since the traversal is the length of the text. The <span style='color:#fa8231'>size</span> of a <span style='color:#0fb9b1'>Trie</span>, is at worst <b><span style='color: var(--mk-color-red)'>O(size of text * overhead)</span></b> which is just the length of all the strings.
<div style="break-after: page;"></div>

**Things Tries can do better than BST**
- **Prefix Queries** (Finding words starting with some characters)
- **Long prefix**
- **Wildcards** (Finding words that fits this requirement, "pi??le")




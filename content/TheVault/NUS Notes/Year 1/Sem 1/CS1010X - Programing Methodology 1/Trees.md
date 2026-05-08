---
Title: Trees
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - DataStructures/Tree
---
## Table of Content
- [[#What are Trees|What are Trees]]
	- [[#What are Trees#Functions for the Tree|Functions for the Tree]]
- [[#Binary Tree|Binary Tree]]
- [[#Balanced Tree|Balanced Tree]]
---
## What are Trees
---
They are usually a nested sequence either a tuple or a list.


![[Binary Tree Example.png | center]]

An example of a tree:
```Python
tree = ((1,3),(2,4),5)

# Where 5 is the root and the numbers in the tuples are leaves.
```
<div style="page-break-after: always;"></div>

### Functions for the Tree

**Counting leaves**

We can use recursion to count the number of leaves in a tree
```Python
def count_leaves(tree):
	if not tree:
		return 0
	elif type(tree) != tuple: # Its a leave
		return 1
	else:
		return count_leaves(tree[0]) + count_leaves)(tree[1:])
```

**Flatten tree**

We can use the same recursion method to flatten the tree into a sequence.
```Python
def flatten_tree(tree):
	if not tree:
		return ()
	elif not isinstance(tree,tuple):
		return (tree,)
	else:
		return flatten_tree(tree[0]) + flatten_tree)(tree[1:])
```

**Scaling**

Just like the map function, the elements in the tree can be operated on.

```Python
def tree_scale(tree, factor):
	if not tree:
		return ()
	elif not isinstance(tree,tuple):
		return (tree * factor,)
	else:
		return tree_scale(tree[0],factor) + tree_scale)(tree[1:], factor)
# OR #
def tree_scale(tree, factor):
	def helper(subtree)
		if not isinstance(tree,tuple):
			return tree * factor
		else:
			return tree_scale(subtree,factor)
	return map(helper, tree)
```
<div style="page-break-after: always;"></div>

**Copying the tree**

To copy the tree we cannot just return the tree as it will just give us a **shadow copy of the tree**. Any changes to the tree it will affect other instances of the same tree as they are identical.

```Python
def copy_tree(tree, factor):
	def helper(subtree)
		if not isinstance(tree,tuple):
			return tree * factor
		else:
			return tree_scale(subtree,factor)
	return map(helper, tree)

# Factor will be 1.
```

## Binary Tree
---

Its a ordered tree , where every node will have at most 2 children. where the left node is smaller than the parent and the right node is bigger.

This serves as a foundation for binary search and sorting.

Below shows the functions needed to use the binary tree for sorting and searching. There are many other ways to build and flatten a tree.

Example:
```Python
def make_set():
	return []

def build_tree(entry, left, right):
    tree = (entry,left,right)
    return tree

def is_empty_tree(tree):
    if not tree:
        return True
    else:
        return False

def entry(tree):
	return tree[0]

def left_branch(tree):
	return tree[1]

def right_branch(tree):
	return tree[2]

def contains(x, tree):
    if (is_empty_tree(tree)):
        return False
    else:
        if (entry(tree) == x):
            return True
        elif (x <= entry(tree)):
            
            return contains(x, left_branch(tree))
        else:
            
            return contains(x, right_branch(tree))

def flatten(tree):
    sorted_lst = []
    if (not tree):
        return sorted_lst
    else:
        left = flatten(left_branch(tree))
        right = flatten(right_branch(tree))
        for l in left:
            sorted_lst.append(l)
        
        sorted_lst.append(entry(tree))
        for r in right:
            sorted_lst.append(r)
    
        return sorted_lst

# Insert an element into the binary tree
def insert_tree(x, tree):
    if (is_empty_tree(tree)):
		    return build_tree(x,make_empty_tree(),make_empty_tree())
    elif (x <= entry(tree)):
	    tree = build_tree(entry(tree),/ 
	    insert_tree(x,left_branch(tree)), right_branch(tree))
    else:
	    tree = build_tree(entry(tree),/
	    left_branch(tree), insert_tree(x,right_branch(tree)))
	    
    return (tree)

def sort_it(lst):

    tree = make_empty_tree()
    for item in lst: # O(n) for looping through every item in list
        tree = insert_tree(item, tree) #O(n**2)
    sorted_lst = flatten(tree)
    return (sorted_lst)
```

Time (average): O(logn) to insert a element into a balanced tree.  
Time (worst): O(n) to insert an element for completely unbalanced tree.  
Space (average): O(logn) this should be the depth of tree since the solution is recursive  
Space (worst): O(n) for completely unbalanced tree to insert a item as it will take n calls

## Balanced Tree
---

A balanced tree will have roughly the same number of elements the subtrees of all its nodes. The height of the left and right subtree of any node will differ not more than 1.

```Python
# Convert a tree into a balanced tree
def balance_tree(tree):

    def helper(lst):
        if lst == []:
            return None
        middle = len(lst)//2 # The middle value will be the root node as this will make the left and right even
        return make_node(lst[middle], helper(lst[:middle]),helper(lst[middle+1:]))

    sorted_list = flatten(tree)
    tmp = helper(sorted_list)
    tree.clear()
    tree.extend(tmp)
```
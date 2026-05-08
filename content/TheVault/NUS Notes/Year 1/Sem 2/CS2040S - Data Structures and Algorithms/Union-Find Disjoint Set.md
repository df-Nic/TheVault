---
title: Union-Find Disjoint Set
Date Created: 2024-04-21
Last Updated: 2025-10-20
tags:
  - CS2040S
  - DataStructures/UnionFindDisjointSet
---
# Idea of UFDS
---
As the name suggests, this data structures <span style='color:var(--mk-color-yellow)'>maintains a collections of sets</span> and these <span style='color:var(--mk-color-yellow)'>sets can merge with one another</span> to form 1 bigger set.

**Dynamic Connectivity**
>Given a set of objects, are 2 of these objects in the same set

A <span style='color:var(--mk-color-turquoise)'>UFDS</span> must support 2 operations, `find` and `union`.
# Quick Find UFDS
---
The idea is to use a basic <span style='color:var(--mk-color-purple)'>integer array</span> where :
- Its **index** represents a **object**, which is pre-defined by the user
- The **value** represents the **component** or **set** the object is in

For **example** given this array `[0, 1, 2, 1, 0, 2, 3]`, object 3 is in component 1 and object 5 is in component 2. <span style='color:var(--mk-color-orange)'>Originally</span> each object (index) will be <span style='color:var(--mk-color-yellow)'>in its own set</span>.

What if the <span style='color:var(--mk-color-orange)'>objects are strings</span>, then an array will not be viable, but instead <span style='color:var(--mk-color-yellow)'>use a hash function</span> with or without open addressing.

Now to <span style='color:var(--mk-color-teal)'>find</span> if 2 objects are in the same component, it is suffice to just <span style='color:var(--mk-color-yellow)'>check at the index if their values are the same</span>.

But for <span style='color:var(--mk-color-teal)'>unionning</span> 2 sets, it will be <span style='color:var(--mk-color-red)'>costly</span>. Given `union(x, y)` :
1) First find what component $y$ is in
2) Then <span style='color:var(--mk-color-yellow)'>search for every value</span> inside the array or hash table and find values with the same component and change it to $x$. By <span style='color:var(--mk-color-orange)'>convention</span>, it will<span style='color:var(--mk-color-yellow)'> union the right item with the left item</span>.

**Time complexity :** `find(x, y)` is <b><span style='color: var(--mk-color-green)'>O(1)</span></b> while `union(x,y)` is <b><span style='color: var(--mk-color-red)'>O(n)</span></b>
<div style="break-after: page;"></div>

# Quick Union UFDS
---
In the previous implementation, our <span style='color:var(--mk-color-teal)'>union</span> takes a very long time, so to solve this, instead of updating everything, the <span style='color:var(--mk-color-yellow)'>values will now represent the parent node</span> (Like a <span style='color:var(--mk-color-purple)'>tree</span> data structure).

Now <span style='color:var(--mk-color-teal)'>unionning</span> given `union(x, y)`, <span style='color:var(--mk-color-yellow)'>find the root</span> of $x$ and change the value of $y$ to the root.

But what about <span style='color:var(--mk-color-teal)'>find</span>, now it is not so simple, for 2 items to be in the <span style='color:var(--mk-color-orange)'>same component</span>, it has to <span style='color:var(--mk-color-yellow)'>be in the same tree</span>. This means the <span style='color:var(--mk-color-yellow)'>root must be the same</span>.
1) For the 2 items, **traverse up** the tree until `value == index` (This means the root has been reached).
2) If the <span style='color:var(--mk-color-yellow)'>2 roots are the same</span> then they are in the <span style='color:var(--mk-color-yellow)'>same component</span>

Now the issue is that this <span style='color:var(--mk-color-purple)'>tree</span> is <span style='color:var(--mk-color-red)'>not guaranteed to be balanced</span> and is not binary.

**Time complexity :** `find(x, y)` is <b><span style='color: var(--mk-color-red)'>O(n)</span></b> while `union(x,y)` is <b><span style='color: var(--mk-color-red)'>O(n)</span></b>

Hmm not so quick now.

# Optimisations
---
## Weighted Union

The reason why fast union is slow overall is because, the <span style='color:var(--mk-color-yellow)'>tree can be skewed to one side</span>. The idea of weighted union, is to union in such a way that the <span style='color:var(--mk-color-yellow)'>height</span> of the tree can be <span style='color:var(--mk-color-yellow)'>minimised</span> to achieve a <span style='color:var(--mk-color-yellow)'>O(log n) search time</span>.

What to do is during <span style='color:var(--mk-color-teal)'>union</span>, compare the <span style='color:var(--mk-color-yellow)'>number of nodes of both components</span> and if they are not in the same component, <span style='color:var(--mk-color-yellow)'>merge</span> the <span style='color:var(--mk-color-yellow)'>smaller tree with the bigger tree</span> using the quick union method.

So now the **size** will need to be keep tracked and stored. Thus the <span style='color:var(--mk-color-yellow)'>height will be at most log n</span>.
- This can be done with **height** it is the same idea

Important <span style='color:var(--mk-color-orange)'>properties</span> to take note of :
- Only the height/wright/rank/size of the <b>root will change</b> and not the subtree
- And the height/wright/rank/size will **only increase** if the tree <span style='color:var(--mk-color-yellow)'>size doubles</span> (When 2 tree of same height are combined together)

**Time complexity :** `find(x, y)` is <b><span style='color: var(--mk-color-green)'>O(Log n)</span></b> while `union(x,y)` is <b><span style='color: var(--mk-color-green)'>O(Log n)</span></b>
## Path Compression

The idea of <span style='color:var(--mk-color-teal)'>path compression</span> is that, when the root is found during <span style='color:var(--mk-color-teal)'>find</span> operation, <span style='color:var(--mk-color-yellow)'>set the parent for each of the traversed node to the root</span>.

**Path compression visualisation**
![[Path Compression Example.png|center|500]]

Some key observation is that <span style='color:var(--mk-color-yellow)'>path compression will alter the height</span>, thus weighted union by size is better since size does not change in path compression.

As long as the <span style='color:var(--mk-color-orange)'>root needs to be search</span>, <span style='color:var(--mk-color-teal)'>path compression</span> can be **executed**.

**Example code for path compression**
```Java
public int findRoot(int node) {
	int root = p;
	// Just recurse up until the root is found, bcause the parent[root] = root
	while (parent[root] != root) {
		root = parent[root];
	}
	compressPath(node, root);
	
	return root;
}

// Setting parent to the root
public void compressPath(int node, int root) {
	while(parent[node] != node) {
		// Remember the next node to go to
		temp = parent[p];
		// Path compression by editing the parent to the root
		parent[p] = root;
		node = temp;
	}
}

// Setting parent to the grandparent which works as well and only needs 1 pass/walk
public int findRoot(int node) {
	int root = p;
	// Just recurse up until the root is found, bcause the parent[root] = root
	while (parent[root] != root) {
		parent[root] = parent[parent[root]];
		root = parent[root];
	}	
	return root;
}
```

<span style='color:var(--mk-color-teal)'>Path compression</span> makes a significant improvement, where a sequence of $m$ <span style='color:var(--mk-color-teal)'>union/find</span> on $n$ objects the time complexity will be <b><span style='color: var(--mk-color-green)'>O(n + mα(m,n))</span></b>. This is a amortized running time. 
> α(n,m) is called <span style='color:#8854d0'>inverse Ackermann</span> function which grows very slowly, but it is <span style='color:var(--mk-color-red)'>not O(1)</span>. It will always be less than 5 in this universe

# UFDS Time Complexity Summary
---
![[UFDS Time Complexity Table.png|center]]
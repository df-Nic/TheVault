---
title: UFDS
Date Created: 2023-07-06
tags:
  - CS2040
  - UnionFind
  - DataStructures
---
# Table of Contents
---
- [[#Union-Find Disjoint Sets|Union-Find Disjoint Sets]]
	- [[#Union-Find Disjoint Sets#What is a UFDS|What is a UFDS]]
	- [[#Union-Find Disjoint Sets#Idea|Idea]]
	- [[#Union-Find Disjoint Sets#Data Structure to store the UFDS|Data Structure to store the UFDS]]
		- [[#Data Structure to store the UFDS#Constructor|Constructor]]
		- [[#Data Structure to store the UFDS#Finding a Set|Finding a Set]]
		- [[#Data Structure to store the UFDS#Union a set|Union a set]]
---
# Union-Find Disjoint Sets
---

## What is a UFDS

A union-find disjoint (UFSD) set is a collection of <span style='color:#20bf6b'>disjoint sets</span>.

It should be able to:
1. Union 2 disjoint sets
2. Find which set an item belongs to
3. Check if 2 items belong to the same set

## Idea

- Each set is modeled as a tree, thus disjoint sets is a collection of trees
- Each set is represented by a <span style='color:#f7b731'>representative item</span>

Using strings as node values, can be <span style='color:#f7b731'>mapped into a integer</span>.

All UFDS operations runs in <b><mark class="hltr-red">O(α(N))</mark></b> implemented with both <span style='color:#0fb9b1'>“union-by-rank” and “path-compression” heuristics</span>.
> α(N) is called <span style='color:#8854d0'>inverse Ackermann</span> function which grows very slowly. It can be assumed as <b><mark class="hltr-red">O(1)</mark></b> for practical values N <= 1 Million

## Data Structure to store the UFDS

The collection of trees can be stored in a 1D array **P**, where;
- `P[i]` records the parent of item i
- If `P[i] = i`, then i is the root

| Integer Value: | 2   | 3   | 3   | 3   | 3   | 6   | 6   | 6   | 8   |
|:--------------:| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     Index:     | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |

### Constructor

When initializing a UFDS, <mark class="hltr-orange">all items from 0 to n-1 are disjoint and each of their rank is 0</mark>.

**Example**
```Java
class UnionFind {
	public int[] p;
	public int[] rank;
	
	public UnionFind(int N){ // Where N is the number of disjoint sets
		p = new int[N];
		rank = new int[N];
		for (int i = 0 ; i < N; i++){
			p[i] = i; // Each item is its own set.
			rank[i] = 0; // Rank will always be 0 at the start
		}
	}
}
```

### Finding a Set

To find an item, a recursive function can be made visiting `p[i]` until, `p[i] = i` thus we hit the root.

In addition, the <span style='color:#f7b731'>path it took will be compressed</span>, placing the child at the root. This makes future operations very fast, <b><mark class="hltr-red">O(1)</mark></b>.

**Example:**
```Java
public int findSet(int i) { 
	if (p[i] == i) return i; 
	else { 
		p[i] = findSet(p[i]); // Recursively call p[i] and set it to the root node value
		return p[i]; 
	} 
}
```

Thus to check, if 2 items are in the same set, just check if <span style='color:#f7b731'>both their root nodes are the same</span> using `findset(i)`.

### Union a set

When union 2 sets, the <span style='color:#f7b731'>shorter set will union with the taller tree</span>.

If both have the same rank, then the standard convention is to <span style='color:#f7b731'>union the left with the right one</span>.

<span style='color:#0fb9b1'>Rank</span>, will be stored in an array **R**, where it stores the <span style='color:#f7b731'>upper bound</span> of the set because the tree will be compressed. 

To form a tree of height **h**, union subsets with similar height from 1 to h and the representative node to avoid path compression.

**Example:**
```Java
public void unionSet(int i, int j) { 
	if (!isSameSet(i, j)) { // Cannot union the same set together!
		int x = findSet(i), y = findSet(j); 
		// rank is used to keep the tree short
		if (rank[x] > rank[y]) 
			p[y] = x; 
		else { // initially have the same rank 
			p[x] = y; 
			if (rank[x] == rank[y]) // rank increases 
				rank[y] = rank[y]+1; // only if both trees 
		}
	} 
}
```
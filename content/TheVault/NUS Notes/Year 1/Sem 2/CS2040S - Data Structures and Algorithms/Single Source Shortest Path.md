---
title: Single Source Shortest Path
Date Created: 2024-04-24
Last Updated: 2025-10-20
tags:
  - CS2040S
  - Algorithms/ShortestPath
  - DataStructures/Graphs
---
# SSSP Problems
---
[[quartz/content/Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Breadth-First Search|BFS]] itself can find the shortest path from one node to another. But that <span style='color:#f7b731'>applies to un-weighted graphs</span> since it minimised the numbed of edges used. With weighted graph it is not that simple.

<span style='color:#0fb9b1'>Weighted Graphs</span>
>It is a graph where its <span style='color:#f7b731'>edges have a specific value</span> tied to it and this value is called a <span style='color:#0fb9b1'>weight</span>

What if <span style='color:#fa8231'>all edges have the same weight</span>, then just use [[quartz/content/Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Breadth-First Search|BFS]].

The key idea for all SSSP algorithms is the <b>triangular inequality</b>. Let $\delta(S,D)$ be the distance from start to destination :
- $\delta(S,C) \le \delta(S,A) + \delta(A,C)$

At the start of the shortest path search there is some <span style='color:#fa8231'>processing</span> that needs to be done
- A source will be given and the weight for the source to itself will be 0
- While the rest of the nodes will be set to a very big number like infinity or `MAX_INTEGER`

To find the shortest path, the <span style='color:#f7b731'>objective is to maintain a good estimate for each distance to a particular node</span>. To do this a <span style='color:#2d98da'>relax</span> function is used.
```Java
public void relax (int node, int parentNode, int edgeWeight){
	// This is the triangular inequality	
	if (weight[node] > weight[parentNode] + edgeWeight) {
		weight[node] = weight[parentNode] + edgeWeight
	}
}
```
<span style='color:#eb3b5a'>Relaxing all edges once will not work</span>.

Another <span style='color:#fa8231'>key property</span> is that if $\delta(S,D)$ passes through node $X$ then $\delta(S,X)$ and $\delta(X,D)$ shortest paths has been found.

Most algorithms will not work on negative cycles, how about <span style='color:#fa8231'>re weighting the graph</span> :
1) **Adding by a constant number** will <span style='color:#eb3b5a'>not work</span> as it will <span style='color:#f7b731'>change the shortest path</span>
2) **Multiplying by a constant** <span style='color:#20bf6b'>will work</span>

A **longest path problem** is harder since positive cycles will make it infinite. But on a **DAG** is is possible with the [[quartz/content/Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Directed Acyclic Graph|topological ordering]].
# Bellman Ford
---
Now, looping through all edges will not work but what if it was done $V - 1$ times. This is the idea behind <span style='color:#2d98da'>bellman ford</span>.

**How does Bellman Ford work**
- For each $\color {#f7b731} {v - 1}$ vertices (nodes) in the graph
- Iterate through <span style='color:#f7b731'>all edges in the graph</span>
- Then <span style='color:#2d98da'>relax</span> the 2 nodes connected by this edge

**Invariant :** After 1 iteration for all edges, then the <span style='color:#f7b731'>node along the shortest path</span> to the destination that is <span style='color:#f7b731'>1 edge away has the correct estimate</span>.

```Java
public void BellmanFord() {
	// Iterate through n - 1 vertices
	for (int i = 0; i < n; i++) {
		// Iterate through all edges in the graph
		for (Edge e : graph) {
			// An edge will have a parent node and a destination/child node
			relax(e)
		}
	}
}
```

It however does not need to go through all $V - 1$ iterations, it can <span style='color:#fa8231'>terminate early</span> if after iterating through <span style='color:#f7b731'>every edge, there is no relaxing done</span>. But after $\color {#f7b731} {V - 1}$ <span style='color:#f7b731'>it guarantees the shortest path</span> even if more edges are added midway.

If <span style='color:#2d98da'>Bellman Ford</span>, fails to converge after $V - 1$ passes, that means there is a <span style='color:#eb3b5a'>negative cycle</span>. Thus it can also detect negative cycles as well, just execute one more pass of <span style='color:#2d98da'>Bellman Ford</span> and if there is still <span style='color:#2d98da'>relaxes</span> then a negative cycle is in the graph.

However this does not mean that <span style='color:#2d98da'>bellman ford</span> cannot have negative edges, <span style='color:#f7b731'>it can handle negative edges just not cycles</span>.

Is it possible to do <span style='color:#fa8231'>bellman within 1 pass</span> (iteration). Yes and will only work if the graph is a <b><span style='color: var(--mk-color-teal)'>DAG</span></b>.
- Does not have any cycles and a <span style='color:#f7b731'>good ordering</span> of the edges can be imposed by using topological ordering. 

Using any <span style='color:#2d98da'>topological algorithm</span> The <span style='color:#f7b731'>first item of the topo order is the starting vertex</span> and then iterate through the order and <span style='color:#f7b731'>relax all of each vertex's neighbors</span>. This works because, in a topological order, before reaching a vertex, it will have found its shortest path as <span style='color:#f7b731'>only vertices to the left (incoming edges) can only affect its shortest path</span>.

Time complexity : <b><span style='color: var(--mk-color-green)'>O(V + E)</span></b>

**Time complexity** is based on the **graph** for **normal bellman ford**:

**Dense Graph :** <b><span style='color: var(--mk-color-red)'>O(V<sup>3</sup>)</span></b>
> E = V<sup>2</sup> thus O(V * V<sup>2</sup>), or using a adjacency matrix

**Sparse Graph :** <b><span style='color: var(--mk-color-green)'>O(VE)</span></b>
> It will iterate through every edge for v number of vertices

# Dijkstra's Algorithm
---
Instead of going through all edges $V - 1$ times, <span style='color:#2d98da'>Dijkstra's algorithm</span> <span style='color:#f7b731'>relaxes each node at most 1 time</span> and visits each edge at most once as well. This <span style='color:#f7b731'>as it runs, it builds the shortest path tree</span>.

**How does Dijkstra's algorithm work**
- Firstly add the source vertex in a [[Heaps#Priority Queue|priority queue]] and with it pair it with weight 0
- Retrieve the node with the <span style='color:#f7b731'>smallest estimated weight</span> (`extractMin()`) in the priority queue
- <span style='color:#2d98da'>Relax</span> all outgoing edges from the node
	1) If the neighbouring nodes are **not in the priority queue** then add them
	2) If **they are in** either update with the new estimate or just add in but keep track if they have been visited
- Repeat until the <span style='color:#f7b731'>priority queue is empty</span> or <span style='color:#f7b731'>all nodes have been visited</span>

Why does removing a node from the priority queue <b>ensures that it is the correct estimate</b>
- Assume not that node $A$ extracted from the priority queue is **not a good estimate**
- Then there is **another shorter path** from the source to the node that was extracted
- Lets say this path passes through node $B$ which is still in the priority queue
- Then by the shortest path property, the path from source to $B$ is <span style='color:#f7b731'>shorter</span> than to $A$
- Then by following the path from $B$ to $A$, the <span style='color:#f7b731'>distance will only be the same or bigger</span> as more nodes are traversed
- This contradicts point one since $A$ is extracted first meaning $\delta(A) \le \delta(B)$

Because of this, <span style='color:#f7b731'>once the destination has been dequeued</span> from the priority queue, the <span style='color:#f7b731'>program can be terminated early</span>.

And also because of this property, it <span style='color:#eb3b5a'>cannot handle negative weights</span>. But can it be <span style='color:#fa8231'>modified</span> :
- The simplest way is to check if the new weight is smaller
- And if the node has already been removed, just <span style='color:#f7b731'>add it back into the priority queue</span> and continue
- This will not work for <span style='color:#eb3b5a'>negative cycles</span>
- This will be of **time complexity**, <b><span style='color: var(--mk-color-red)'>O(E log E)</span></b>

**Time complexity** : <b><span style='color: var(--mk-color-green)'>O(E log V)</span></b>
- O(V log V) + O(E log V) = O((E+V) log V), whichever is bigger V or E

However the time complexity also <b>depends on the priority queue implementation</b>.

| PQ Implementation |      `Insert`      |    `deleteMin`     |   `decreaseKey`    |            Total            |
| :---------------: | :----------------: | :----------------: | :----------------: | :-------------------------: |
|       Array       |         1          |         V          |         1          |    **O(V<sup>2</sup>)**     |
|     AVL Tree      |       Log V        |       Log V        |       Log V        |       **O(E Log V)**        |
|    d-way Heap     | d Log<sub>d</sub>V | d Log<sub>d</sub>V | d Log<sub>d</sub>V | **O(E Log<sub>E/V</sub>V)** |
|  Fibonacci Heap   |         1          |       Log V        |         1          |     **O(E + V log V)**      |


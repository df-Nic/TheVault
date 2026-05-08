---
title: Graphs
Date Created: 2024-04-17
Last Updated: 2025-10-20
tags:
  - CS2040S
  - DataStructures/Graphs
  - Algorithms/GraphTraversal
---
# What is a Graph
---
For something to <span style='color:#fa8231'>constitute</span> as a graph :
- It contains **0 to some number** of <span style='color:#0fb9b1'>nodes</span> or <span style='color:#0fb9b1'>vertices</span>
- And **between 2 nodes** it can have an <span style='color:#0fb9b1'>edge</span> which connects the 2 together and <span style='color:#f7b731'>each edge is unique</span>

<span style='color:#0fb9b1'>Multi graph</span>
>If there are <span style='color:#f7b731'>more than 1 edge connected</span> to the same nodes.

<span style='color:#0fb9b1'>Hyper graph</span>.
>If <span style='color:#f7b731'>1 edge connects to more than 2 nodes</span> then the graph.

From here on :
- A graph will be denoted as $G = <V, E>$
- $V$ is the set of nodes and $\vert V \vert \ge 1$
- $E$ is the set of edges, where $E \subseteq \{(v,w) : (v \in V) \land (w \in V)\}$
- This set $E$ will **not have duplicate similar edges**
## Graph Terminologies

**(Simple) Path**
>Set of edges connecting two nodes and a path <span style='color:#f7b731'>intersects each node at most once</span>

**Connected**
>**Every pair of nodes** is <span style='color:#f7b731'>connected by a path</span>

**Disconnected**
>**Some pair of nodes** is <span style='color:#f7b731'>not connected by a path</span>

**Connected Components**
>**Some pair** of nodes is <span style='color:#f7b731'>not connected by a path</span>. In a **connected graph** however, there is **1 connected component**. Or another words there is a path from $a$ to $b$ and $b$ to $a$ as well.
<div style="break-after: page;"></div>

**Cycle**
>A path where the <span style='color:#f7b731'>start and end </span>nodes are the <span style='color:#f7b731'>same</span>. Preferably the edges are **distinct**

**Unrooted Tree**
>A <span style='color:#f7b731'>connected</span> graph with <span style='color:#f7b731'>no cycles</span>

**Forest**
>A graph with <span style='color:#f7b731'>no cycles</span>. Basically a collection of trees which are disconnected

**Degree of a Node**
>Number of **adjacent edges** on a particular node

**Degree of a Graph**
><span style='color:#f7b731'>Maximum number</span> of **adjacent edges** of a particular node in the graph

**Diameter**
>**Maximum** distance between two nodes, <b><span style='color: var(--mk-color-yellow)'>following the shortest path</span></b>

**Dense / Sparse Graphs**
>It is **how many nodes a graph has**, a dense graph has many nodes while a sparse graph has very little nodes

**Planner Graph**
>A graph where <span style='color:#f7b731'>no edges overlap one another</span>

**Directed Graph**
>Same as a normal graph but an <span style='color:#f7b731'>edge has a direction</span>. An edge can we <span style='color:#0fb9b1'>ingoing</span> or <span style='color:#0fb9b1'>outgoing</span>, where one is edges pointing to the node while the other is edges pointing to other nodes

Note that a <span style='color:#fa8231'>undirected graph can be transformed into a directed graph</span> by adding 2 edges of opposite directions to each node.
<div style="break-after: page;"></div>

## Special Graphs
![[Special Graphs.png|center|550]]

# Graph Representation
---
## Adjacency List

It is an <span style='color:#f7b731'>array of V lists</span>, one <span style='color:#f7b731'>list for each vertex</span>. Each element in the array list is neighbors of the vertex.

For <span style='color:#f7b731'>weighted graphs</span> it stores a pair of <<span style='color:#f7b731'>neighbor, weight</span>>.

Space Complexity : <b><span style='color: var(--mk-color-red)'>max(V, E)</span></b> or <b><span style='color: var(--mk-color-red)'>O(V + E)</span></b>, where E is the number of edges. In the worse case it will be <b><span style='color: var(--mk-color-red)'>O(V<sup>2</sup>)</span></b> for a <span style='color:#f7b731'>complete graph</span>.
## Adjacency Matrix

It is a <span style='color:#f7b731'>2D array of size V by V</span>, where V is the number of vertices in the graph.

If a node from I -> J exist then `AdjMatrix[i][j]` contains value 1 else 0. For <span style='color:#f7b731'>weighted graphs</span>, store the weight of the edge instead.

Space Complexity : <b><span style='color: var(--mk-color-red)'>O(V<sup>2</sup>)</span></b>, but matrix is <span style='color:#f7b731'>better for speed</span> since index lookup is <b><span style='color: var(--mk-color-green)'>O(1)</span></b>
<div style="break-after: page;"></div>

## Edge List

It is an <span style='color:#f7b731'>array of E edges</span>.

In the list,  `EdgeList` contains a triple <<span style='color:#f7b731'>U, V, W(U, V)</span>>.
V : Source Vertex
U : Destination Vertex
W : Weight

For <span style='color:#f7b731'>unweighted graph </span>then weight can be stored as 0 or 1 or a pair.

Space Complexity : <b><span style='color: var(--mk-color-red)'>O(E)</span></b> In the worse case it will be <b><span style='color: var(--mk-color-red)'>O(V<sup>2</sup>)</span></b> for a <span style='color:#f7b731'>complete graph</span>
> E can be = V<sup>2</sup> for a clique

# Graph Traversal
---
There are <span style='color:#fa8231'>2 basic graph traversal</span> methods
1) <span style='color:#2d98da'>BFS</span>
2) <span style='color:#2d98da'>DFS</span>

Some characteristics of it is that **visits every node and edge** <b>but not every path</b>. And to explore every path, the **time taken will be exponential**.
## Breadth-First Search

A <span style='color:#2d98da'>BFS</span> starts from some source vertex $S$ and traverse in a <span style='color:#f7b731'>level order manner</span>, meaning it traverses to all nodes that are accessible with 1 hop, then 2 and so on until the whole graph is visited.

**Hop**
>A hop is the <span style='color:#f7b731'>precise number of edges</span> needed to get from 1 vertex to another vertex

**How does BFS work**
-  Have a <span style='color:#8854d0'>queue</span>, which initially contains $S$, the starting vertex.
-  <span style='color:#2d98da'>Poll</span> a vertex V from queue and <span style='color:#2d98da'>enqueue</span> all of its <span style='color:#f7b731'>neighbors</span> into the queue.
-  <span style='color:#f7b731'>Mark the polled vertex as visited</span> which can be simply done with an array of length $V$. This <span style='color:#f7b731'>prevents cycles</span>
-  Set the <span style='color:#f7b731'>predecessor of all its neighbors to V</span>, which denotes the path taken, which can be simply done with an array of length $V$

By running <span style='color:#2d98da'>BFS</span> on an <span style='color:#f7b731'>unweighted graph</span> it will give the <b>shortest path</b> from the source to all other nodes.

And this shortest path to all other nodes from the source will <span style='color:#f7b731'>form a tree</span>. It <span style='color:#f7b731'>cannot have a cycle</span> because if there is, then there are 2 paths to a particular node but one is longer than the other.

One downfall of <span style='color:#2d98da'>BFS</span> is that it <span style='color:#eb3b5a'>does not guarantee that it will visit every single node</span>. For <span style='color:#f7b731'>disconnected graphs</span> it will not visit one of the components. 

To fix this, <span style='color:#2d98da'>BFS</span> must <span style='color:#f7b731'>start from every single vertex</span> and this is <span style='color:#eb3b5a'>not good at computing distance</span>.

**Time complexity** of <span style='color:#2d98da'>BFS</span> based on **storing method**:

**Adjacency Matrix :** <b><span style='color: var(--mk-color-red)'>O(V<sup>2</sup>)</span></b>
> Need to loop through every item in the matrix

**Adjacency List :** <b><span style='color: var(--mk-color-green)'>O(V + E)</span></b>
> As long as it is <span style='color:#f7b731'>not a clique</span>, not all vertices will have $n-1$ edged. Else if it is then it will still be <b><span style='color: var(--mk-color-red)'>O(V<sup>2</sup>)</span></b>. Also each edge is called upon at most 2 times. **It also visits every edge and node**
## Depth-First Search

A <span style='color:#2d98da'>DFS</span> starts from some source vertex $S$ and traverse in a <span style='color:#f7b731'>as deep as possible</span> before backtracking. Once a dead end has been found it will <span style='color:#f7b731'>go back</span> from the path it took and <span style='color:#f7b731'>find alternative nodes which has not been visited</span> and continue its search.

**How does DFS work**
-  Have a <span style='color:#8854d0'>stack /  recursion</span>, which initially contains $S$, the starting vertex.
-  <span style='color:#2d98da'>Pop</span> a vertex V from stack and <span style='color:#2d98da'>push</span> all of its <span style='color:#f7b731'>neighbors</span> into the queue.
-  <span style='color:#f7b731'>Mark the polled vertex as visited</span>
-  Set the <span style='color:#f7b731'>predecessor of all its neighbors to V</span>, which denotes the path taken

This <span style='color:#eb3b5a'>will not give the shortest path</span>, however the discovered path to all other nodes from the source will <span style='color:#f7b731'>form a tree</span>. It <span style='color:#f7b731'>cannot have a cycle</span>.

**Time complexity** of <span style='color:#2d98da'>DFS</span> based on **storing method**:

**Adjacency Matrix :** <b><span style='color: var(--mk-color-red)'>O(V<sup>2</sup>)</span></b>
> Need to loop through every item in the matrix

**Adjacency List :** <b><span style='color: var(--mk-color-green)'>O(V + E)</span></b>
> As long as it is <span style='color:#f7b731'>not a clique</span>, not all vertices will have $n-1$ edged. Else if it is then it will still be <b><span style='color: var(--mk-color-red)'>O(V<sup>2</sup>)</span></b>. Also each edge is called upon at most 2 times. **It also visits every edge and node**
# Directed Acyclic Graph
---
As the name suggests, a <span style='color:#0fb9b1'>DAG</span> is a <span style='color:#f7b731'>directed graph with no cycles</span>. And a DAG has a special ordering called a <span style='color:#0fb9b1'>topological ordering</span>.

<span style='color:#0fb9b1'>Topological Order</span>
>It is a sequential <span style='color:#f7b731'>total ordering</span> of every node such that the <span style='color:#f7b731'>edges only point forward</span>. In other terms, a node can only be visited if all of the ingoing edges are visited already

It **must have no cycles** because if there is, then it will break one rule as there will be <span style='color:#f7b731'>1 edge pointing backwards</span>.

How to find a <span style='color:#0fb9b1'>topological order</span>, use the <span style='color:#2d98da'>DFS</span> algorithm, however when adding a node into the ordering, ensure that the <b>node is added in a post-order manner</b> (After the recursive call). This is because the usual <span style='color:#eb3b5a'>pre-order DFS will not give a valid topological ordering</span>.

And with a <span style='color:#2d98da'>post-order DFS</span>, the node will be <span style='color:#f7b731'>added to the back</span> of the topological ordering. And for a [[Single Source Shortest Path|single source shortest path problem]], the order to relax should be in <span style='color:#f7b731'>reverse DFS post-order</span>.
## Kahn's Algorithm

Another alternative is to use <span style='color:#2d98da'>khan's algorithm</span> instead of <span style='color:#2d98da'>DFS</span>. The idea is to use the property that <span style='color:#f7b731'>nodes with no incoming edges are next in the order</span>.

**How does Khan's algorithm work :**
- For all nodes in $G$, find all those with <span style='color:#f7b731'>no incoming edges</span>, which can already be added into the topological ordering
- **Remove** all edges connected to the nodes above
- Remove the nodes added into the ordering from the graph $G$
- Repeat until all edges are added

**Time Complexity :** <b><span style='color: var(--mk-color-green)'>O(V + E)</span></b>


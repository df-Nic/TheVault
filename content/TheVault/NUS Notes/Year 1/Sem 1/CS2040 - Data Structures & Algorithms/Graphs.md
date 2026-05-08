---
title: Graphs
Date Created: 2023-07-12
tags:
  - CS2040
  - Graphs
  - DataStructures
---
# Table of Contents
---
- [[#What is a Graph|What is a Graph]]
	- [[#What is a Graph#Types of edges|Types of edges]]
	- [[#What is a Graph#Terminologies|Terminologies]]
- [[#Data Structure to Store Graphs|Data Structure to Store Graphs]]
	- [[#Data Structure to Store Graphs#Adjacency Matrix|Adjacency Matrix]]
	- [[#Data Structure to Store Graphs#Adjacency List|Adjacency List]]
	- [[#Data Structure to Store Graphs#Edge List|Edge List]]
	- [[#Data Structure to Store Graphs#Pros and Cons on Storing Methods|Pros and Cons on Storing Methods]]
- [[#Graph Traversal|Graph Traversal]]
	- [[#Graph Traversal#Path Traversal Methods|Path Traversal Methods]]
		- [[#Path Traversal Methods#Breadth First Search|Breadth First Search]]
		- [[#Path Traversal Methods#Depth First Search|Depth First Search]]
	- [[#Graph Traversal#Path Reconstruction|Path Reconstruction]]
- [[#Graph Traversal Applications|Graph Traversal Applications]]
	- [[#Graph Traversal Applications#Reachability Test|Reachability Test]]
	- [[#Graph Traversal Applications#Shortest Unweighted Path|Shortest Unweighted Path]]
	- [[#Graph Traversal Applications#Counting Components|Counting Components]]
	- [[#Graph Traversal Applications#Topological Sort|Topological Sort]]
		- [[#Topological Sort#Kahn's Algorithm|Kahn's Algorithm]]
		- [[#Topological Sort#DFS Variant|DFS Variant]]
	- [[#Graph Traversal Applications#Counting Strongly Connected Components|Counting Strongly Connected Components]]
		- [[#Counting Strongly Connected Components#Kosaraju's Algorithm|Kosaraju's Algorithm]]
---

# What is a Graph
---

A <span style='color:#0fb9b1'>simple graph</span>, is a set of N vertices where some (0 to $nC2$) pairs of the vertices are connected by <span style='color:#0fb9b1'>edges</span>.

A <span style='color:#0fb9b1'>multi graph</span>, is a graph where a 2 vertices can have <span style='color:#f7b731'>2 or more similar edge types</span>.

A <span style='color:#0fb9b1'>mixed graph</span>, is a graph with <span style='color:#f7b731'>multiple combinations of edge types</span> in a graph

## Types of edges

An edge is just a connection between 2 vertices and each edge can be given a <span style='color:#0fb9b1'>weightage</span>.

1) Undirected Edges
There is <span style='color:#f7b731'>no direction</span> between the 2 vertices, thus the 2 vertices are <span style='color:#0fb9b1'>neighbors</span>.

2) Directed Edges
The edge has <span style='color:#f7b731'>a direction</span> between 2 vertices. One vertex is a neighbor of the other vertex <span style='color:#f7b731'>but not vise versa</span>.

3) Bi-directed Edges
Between 2 vertices, it has <span style='color:#f7b731'>a directed edge pointing back and forth</span>.

## Terminologies

**Sparse**
> A graph with not so many edges, O(V) or less, where v is the number of <span style='color:#0fb9b1'>vertices</span>.

**Dense**
> A graph with many edges, O(V<sup>2</sup>) where v is the number of <span style='color:#0fb9b1'>vertices</span>.

**Complete**
> A <span style='color:#0fb9b1'>simple graph</span> with N vertices and $nC2$ edges. Every vertex has <span style='color:#f7b731'>edges to all other vertices</span>.

**In Degree**
> Number of <span style='color:#f7b731'>incoming edges</span> to the vertex.

**Out Degree** 
> Number of <span style='color:#f7b731'>outcoming edges</span> from the vertex.

**Simple Path**
> Sequence of <span style='color:#f7b731'>unique vertices connected by undirected edges</span>. A path with 1 vertex and no edge is a <span style='color:#0fb9b1'>empty path</span>

**Simple Directed Path**
> Same as simple path, but the <span style='color:#f7b731'>edges are directed</span> and is in the <span style='color:#f7b731'>same direction</span>

**Path Length / Cost**
> Number of edges or sum of the weightages in the paths.

**Simple Cycle**
> Path that starts and ends with the same vertices, with a <span style='color:#f7b731'>minimum of 3 vertices</span> and it has to be unique.

**Acyclic**
> A graph with no cycles.

**Simple Directed Cycle**
> A cycle where the <span style='color:#f7b731'>edges are directed</span> and it must be in the <span style='color:#f7b731'>same direction</span>. It involves <span style='color:#f7b731'>2 or more unique vertices</span>.

**Component**
> The <span style='color:#f7b731'>maximum</span> group of vertices in a <mark class="hltr-orange">undirected graph</mark> that can visit each other with some path

**Connected Graph**
> <mark class="hltr-orange">Undirected graph</mark> with <span style='color:#f7b731'>1 component</span>. All vertices are reachable via some path.

**Reachable / Unreachable**
> Weather a vertex can reach to another vertex via some path.

**Sub Graph**
> Subset of vertices (and their edges) of the original graph

**Directed Acyclic Graph (DAG)**
> It is a <mark class="hltr-orange">directed graph</mark> that has <span style='color:#f7b731'>no cycles</span>.

**Tree**
> Is a <mark class="hltr-orange">connected undirected graph</mark> where, `Edges = Vertices - 1`. There is <span style='color:#f7b731'>only one unique path</span> for any pair of vertices

**Bipartite Graph**
> Is a <mark class="hltr-orange">undirected graph</mark> where a partition into 2 sets has <span style='color:#f7b731'>no edges between members of the same set</span>. <span style='color:#f7b731'>2-colorable</span>, no cycles with <span style='color:#f7b731'>odd edges</span> and it can be <span style='color:#0fb9b1'>disconnected</span>.

# Data Structure to Store Graphs
---

## Adjacency Matrix

It is a <span style='color:#f7b731'>2D array of size V by V</span>, where V is the number of vertices in the graph.

If a node from I -> J exist then `AdjMatrix[i][j]` contains value 1 else 0.

For <span style='color:#0fb9b1'>weighted graphs</span>, store the weight of the edge.

Space Complexity : <b><mark class="hltr-red">O(V<sup>2</sup>)</mark></b>

## Adjacency List

It is an <span style='color:#f7b731'>array of V lists</span>, once <span style='color:#0fb9b1'>array list</span> for each vertex. Each element in the array list is neighbors of the vertex.

For <span style='color:#0fb9b1'>weighted graphs</span> it stores a pair of <<span style='color:#f7b731'>neighbor, weight</span>>.

Space Complexity : <b><mark class="hltr-red">max(V, E)</mark></b>, where E is the number of edges. In the worse case it will be <b><mark class="hltr-red">O(V<sup>2</sup>)</mark></b> for a <span style='color:#0fb9b1'>complete graph</span>

## Edge List

It is an <span style='color:#f7b731'>array of E edges</span>.

In the list,  `EdgeList` contains a triple <<span style='color:#f7b731'>U, V, W(U, V)</span>>.
V : Source Vertex
U : Destination Vertex
W : Weight

For <span style='color:#0fb9b1'>unweighted graph </span>then weight can be stored as 0 or 1 or a pair.

Space Complexity : <b><mark class="hltr-red">O(E)</mark></b>, In the worse case it will be <b><mark class="hltr-red">O(V<sup>2</sup>)</mark></b> for a <span style='color:#0fb9b1'>complete graph</span>
> E can be = V<sup>2</sup>

## Pros and Cons on Storing Methods

![[Pros & Cons on Graph Storage Types.png|center]]


# Graph Traversal
---

Unlike a binary tree, the <span style='color:#f7b731'>start point for a graph is self defined</span>, in addition it needs to avoid running in a cycle.

Some vertex S can reach vertex D, then <mark class="hltr-orange">all the neighbors of D is reachable from S</mark>.

## Path Traversal Methods

### Breadth First Search

A <span style='color:#3867d6'>BFS</span> starts from S and traverse in a <span style='color:#f7b731'>level order manner</span>, meaning it traverses edge by edge.

To prevent cycles have a <span style='color:#f7b731'>array of size V, to track if a vertex is visited</span>.

To memories the path have a <span style='color:#f7b731'>array of size V</span>, and the value in each spot <span style='color:#f7b731'>denotes the predecessor</span>, `p[2] = 1` means 2 is reachable from 1.

-  Have a <span style='color:#0fb9b1'>queue</span>, which initially contains S, the starting vertex.
-  <span style='color:#3867d6'>Poll</span> a vertex V from queue and <span style='color:#3867d6'>enqueue</span> all of its <span style='color:#0fb9b1'>neighbors</span> into the queue.
-  <span style='color:#f7b731'>Mark the polled vertex as visited</span>
-  Set the <span style='color:#f7b731'>predecessor of all its neighbors to V</span>, which denotes the path taken

<span style='color:#3867d6'>BFS</span> will form a <span style='color:#0fb9b1'>spanning tree</span>, which is a <span style='color:#f7b731'>subset of edges which connects the whole graph</span>.

**Pseudocode for BFS**
```Java
public static BFS (int start){		
	Q = {start} // start from s and Q = queue
	visited[start] = 1
	
	while Q is not empty // O(V) will run one for all vertices
		u = Q.dequeue
		
		//O(2E) for undirected graph as an edge can be stored both ways
		for all v adjacent to u // order of neighbor, 
		if visited[v] = 0 // influences BFS
			visited[v]  = true // visitation sequence
			p[v] = u
			Q.enqueue(v)
}

public static main (String[] args){
	// Initialization phase, in addition to this we need to use a DS to store the graph
	
	for all v in V //O(V)
		visited[v] = 0; // 0 means not visited yet
		p[v] = -1; // Path memorization, -1 means there is no in degree

	BFS(s); // Start the recursive call from s
}
```

Time complexity on BFS based on **storing method**:

Adjacency Matrix : <b><mark class="hltr-red">O(V<sup>2</sup>)</mark></b>
> No matter what, it will need to loop through V times for each vertex.

Adjacency List : <b><mark class="hltr-red">O(V + E)</mark></b>
> Why not O(VE) as not all vertices have edges and not all have fixed number edges.

**Best case** is <b><mark class="hltr-red">O(1)</mark></b> using <span style='color:#0fb9b1'>Adjacency List</span> where the <span style='color:#f7b731'>starting point has no neighbors</span>.

### Depth First Search

A <span style='color:#3867d6'>DFS</span> starts from S and traverse in a <span style='color:#f7b731'>depth first manner</span>, meaning it traverses until it hits a dead end.

-  Have a <span style='color:#0fb9b1'>stack /  recursion</span>, which initially contains S, the starting vertex.
-  <span style='color:#3867d6'>Pop</span> a vertex V from stack and <span style='color:#3867d6'>push</span> all of its <span style='color:#0fb9b1'>neighbors</span> into the queue.
-  <span style='color:#f7b731'>Mark the polled vertex as visited</span>
-  Set the <span style='color:#f7b731'>predecessor of all its neighbors to V</span>, which denotes the path taken

**Pseudocode for DFS**
```Java
public static void DFSrec(int s) {
	visited[s] = 1; // to avoid cycle
	for all v adjacent to s // order of neighbor O(E)
		if visited[v] == 0; // influences DFS
		p[v] = s; // visitation sequence
		DFSrec(v); // recursive (implicit stack)
}

public static void main(String[] args){
	// Initialization phase, in addition to this we need to use a DS to store the graph
	for all v in V // O(V)
		visited[v] = 0;
		p[v] = -1;
	}
	DFSrec(s) // start the recursive call from s, it will be called O(V) calls
}
```

Time complexity on DFS based on **storing method**:

Adjacency Matrix : <b><mark class="hltr-red">O(V<sup>2</sup>)</mark></b>
> No matter what, it will need to loop through V times for each vertex.

Adjacency List : <b><mark class="hltr-red">O(V + E)</mark></b>
> Why not O(VE) as not all vertices have edges and not all have fixed number edges.

**Best case** is <b><mark class="hltr-red">O(1)</mark></b> using <span style='color:#0fb9b1'>Adjacency List</span> where the <span style='color:#f7b731'>starting point has no neighbors</span>.

## Path Reconstruction

```Java
void backtrack(u){
	if (u == -1) // recall: predecessor of s is -1)
		break
	backtrack(p[u])
	// go back to predecessor of u
	Output u // recursion like this reverses the order
}
// in main method
// recursive version (normal path)
Output "Path:"
backtrack(t); // start from end of path (vertex
// try it on this array p, t = 4
// p = {-1, 0, 1, 2, 3, -1, -1, -1} => 0 1 2 3 4
```

# Graph Traversal Applications
---

## Reachability Test

Weather a <span style='color:#f7b731'>2 vertices can reach one another</span> via some path. 

Use either <span style='color:#3867d6'>BFS</span> / <span style='color:#3867d6'>DFS</span> on a starting vertex S, and if `visited[S] = 1` then its reachable. As both methods will eventually scan through the entire graph.

## Shortest Unweighted Path

Since an <span style='color:#0fb9b1'>unweighted graph</span> has the same weight, the shortest path between 2 vertices is finding the <span style='color:#f7b731'>least number of edges</span> from one vertex to another.

Using <span style='color:#3867d6'>BFS</span> will get that path. Because it goes level by level, meaning from the start vertex, it will visit all n+1 nodes, afterwards n + 2 and so on.

## Counting Components

Counting the <span style='color:#f7b731'>number of groups</span> where the vertices are all reachable from one another.

Loop through every vertex, if its not visited call <span style='color:#3867d6'>BFS</span> / <span style='color:#3867d6'>DFS</span>, keep track on the number of time a function is called to get the number of components

Time complexity : <b><mark class="hltr-red">O(V + E)</mark></b>

## Topological Sort

A topological sort is a graph traversal where a node is only visited after all its <span style='color:#f7b731'>inbound vertices</span> are visited.

A <span style='color:#0fb9b1'>DAG</span> has at least 1 possible permutation

A graph with only 1 direction (Like a link list) has only 1 permutation
A graph that is all disconnected can reach all possible permutations ie (n power 2)

### Kahn's Algorithm

All vertices with no <span style='color:#f7b731'>inbound edges will be our starting points</span>. <span style='color:#3867d6'>Equeue</span> all into a <span style='color:#0fb9b1'>queue</span>.

For each vertex, check its neighbors and <span style='color:#f7b731'>reduce the indegree counter by 1</span> for that neighbor. It the indegree for that neighbor is <span style='color:#f7b731'>0, mean all inbounded edges have been visited</span>. And <span style='color:#3867d6'>enqueue</span> it.

```Java
// Initialization Phase
for all v in V
	indeg [v] = 0
	p[v] = -1
for each edge (u,v) // get in in-degree of vertices
	indeg [v] = indeg [v] + 1
for all v’ where indeg [v’] = 0 // Get vertices with no inbound edges
	Q = {v’} // enqueue v’

// Main Loop
while Q is not empty
	u = Q.dequeue()
	// append u to back of toposort which is a string
	for all v adjacent to u // order of neighbor
		indeg [v] = indeg [v] -1
		if indeg [v] = 0 // add to queue
			p[v] = u
			Q.enqueue(v)
```

Time Complexity : <b><mark class="hltr-red">O(V + E)</mark></b>

### DFS Variant

Same as a DFS algorithm, however it uses <span style='color:#f7b731'>post-order processing</span>. Meaning it will fully traverse a path before forming the topo sequence. This give us a <span style='color:#f7b731'>reverse topological sequence</span>.

```Java
```Java
public static void DFSrec(int s) {
	visited[s] = 1; // to avoid cycle
	for all v adjacent to s // order of neighbor O(E)
		if visited[v] == 0; // influences DFS
		p[v] = s; // visitation sequence
		DFSrec(v); // recursive (implicit stack)
	
	// Add this, 
	toposort.append(s); // This is the post order processing
}

public static void main(String[] args){
	// Initialization phase, in addition to this we need to use a DS to store the graph
	for all v in V // O(V)
		visited[v] = 0;
		p[v] = -1;
	}
	
	// Add this
	for all v in V{
		if (visited[v] == 0){
			DFSrec(v);
		}
	}
	// Reverse the toposort and output it for the coorect topological ordering
}
```

Time Complexity : <b><mark class="hltr-red">O(V + E)</mark></b>

## Counting Strongly Connected Components

A <span style='color:#0fb9b1'>Strongly Connected Component (SCC)</span>, is a sub graph of a <mark class="hltr-orange">directed graph</mark>. It contains 1 or more vertices and any 2 vertices are connected by at <span style='color:#f7b731'>least 1 path and no additional vertices</span>.

<span style='color:#0fb9b1'>Strongly connected graph</span>, is a graph with 1 SCC.

A <span style='color:#0fb9b1'>DAG</span> total SCC will be the <span style='color:#f7b731'>number of vertices</span> as there is no cycles. 

In an SCC you want <mark class="hltr-orange">cycles with the maximum</mark> number of vertices and it cannot be reused.

### Kosaraju's Algorithm

Use a <span style='color:#3867d6'>DFS topological sort</span>, on the directed graph G and afterwards <mark class="hltr-orange">transpose</mark> the graph.

When you <span style='color:#f7b731'>transpose</span> (Direction is inversed) the graph it will <span style='color:#f7b731'>always make a DAG</span>. This is to ensure that all vertices in an SCC are visited before going to the next SCC.
> Transpose means if u is a neighbor of v, then after transposing, v is a neighbor of u.

![[SCC Why Transpose the Graph.png|center]]

```Java
// Do DFS topo sort and transport the graph
int ssc = 0;

for all v in V{
	visisted[v] = 0 // Need to reset visited as DFS was used to get the topo ordering
}

for all v in K{ // K is the topo ordering, either reverse the ordering or start from the back
	if visited[v] = 0;
	ssc ++;
	DFS(v);
}
```

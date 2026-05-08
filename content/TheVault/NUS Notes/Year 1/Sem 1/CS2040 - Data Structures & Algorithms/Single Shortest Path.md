---
title: Single Shortest Path
Date Created: 2023-07-18
tags:
  - CS2040
  - Graphs
  - Algorithms
---

# Table of Contents
---
- [[#Single Source Shortest Path|Single Source Shortest Path]]
	- [[#Single Source Shortest Path#Negative Weighted Edges & Cycles|Negative Weighted Edges & Cycles]]
	- [[#Single Source Shortest Path#Relaxation Operation|Relaxation Operation]]
	- [[#Single Source Shortest Path#SSSP Algorithms|SSSP Algorithms]]
		- [[#SSSP Algorithms#Bellman Ford|Bellman Ford]]
			- [[#Bellman Ford#One Pass Bellman Ford|One Pass Bellman Ford]]
		- [[#SSSP Algorithms#DFS / BFS|DFS / BFS]]
		- [[#SSSP Algorithms#Dijkstra's Algorithm|Dijkstra's Algorithm]]
			- [[#Dijkstra's Algorithm#Modified Dijkstra's Algorithm|Modified Dijkstra's Algorithm]]
	- [[#Single Source Shortest Path#When to Use Which SSSP Algorithm|When to Use Which SSSP Algorithm]]
---
# Single Source Shortest Path
---

For a <span style='color:#0fb9b1'>Single Source Shortest Path</span> (SSSP), the graphs are usually,
- Directed with multiple directions, one way or two ways
- Weighted, depending on what the unit represents

**Single-Source**
> From a <span style='color:#f7b731'>specific starting vertex</span>, get the shortest path to <span style='color:#f7b731'>all other vertices</span>.

What if the edges are <span style='color:#f7b731'>unweighted / having the same weight</span>. Then just use <span style='color:#3867d6'>BFS</span>. 

**Example of modified BFS to solve SSSP**
```Java
public static BFS_SSSP (int start){		
	Q = {start} // start from s and Q = queue
	
	while Q is not empty // O(V) will run one for all vertices
		u = Q.dequeue
		
		//O(2E) for undirected graph as an edge can be stored both ways
		for all v adjacent to u // order of neighbor, 
			if (distance[v] == INF){ // influences BFS
				distance[v]  = distance[u] + 1 // visitation sequence
				p[v] = u
				Q.enqueue(v)
			}
}

public static main (String[] args){
	// Initialization phase, in addition to this we need to use a DS to store the graph
	
	for all v in V //O(V)
		distance[v] = INF; // INF means not visited yet
		p[v] = -1; // Path memorization, -1 means there is no in degree
	
	distance[0] = 0; // Assuming 0 is our start
	BFS(s); // Start the recursive call from s
}
```

## Negative Weighted Edges & Cycles

The weight of an edge can also be <span style='color:#eb3b5a'>negative</span> depending on certain applications of the graph.

Therefore, a SSSP algorithm might not work with graphs with <mark class="hltr-orange">negative cycles and not negative edges</mark>. As there can be an infinite path where the weight of going back and forth which will <span style='color:#f7b731'>reduce the weight of the shortest path</span>.

Therefore for cases like this, the <span style='color:#f7b731'>shortest path is not well define</span>. If the <span style='color:#f7b731'>sum</span> of the weightages in a cycle results in a <span style='color:#f7b731'>negative value</span>.

## Relaxation Operation

<span style='color:#3867d6'>Relaxation</span> , is a function which will compare the weight of an existing path to a vertex with another path to the same vertex.

If the weight is smaller, update the weight in the <span style='color:#0fb9b1'>distance array</span> and update the <span style='color:#0fb9b1'>predecessor array</span>.

```Java
public void initSSSP(int start){
	for each v in V{ // For each vertex
		D[v] = INF // Predefine INF, D is the distance array
		p[v] = -1 // Predecessor array is null
	}
	D[s] = 0 // The weight from the start to start is 0
}

public void relax(int start, int dest, int weight){
	// This IF statement also prevent -ve cycles
	if (D[start] != INF && D[dest] > D[u] + weight){ // From start point using this edge can it shorten the SP
		D[dest] = D[start] + weight;
		p[dest] = start; // Update, to indicate to reach this destination come from this vertex
	}
}
```

## SSSP Algorithms

### Bellman Ford

This algorithm will <span style='color:#f7b731'>randomly</span> pick an edge, if the edge can be <span style='color:#3867d6'>relaxed</span>, relax it until all vertices cannot be relaxed anymore.

- For <span style='color:#f7b731'>each vertex</span>, O(V)
- For <span style='color:#f7b731'>each edge</span>, in all edges, O(E)
-  <span style='color:#3867d6'>Relax</span> the 2 vertices that are connected with that edge, O(1)
	-  If the start vertex has a weight of INF, then do not relax, this is to prevent cycles/negative paths.

```Java
// Bellman Ford's routine, implemented using AdjList (note that you can choose to use EdgeList -- similar performance)

// This is placed in the main function or a seperate callable function

// The order for the for loop is very important
for (int i = 0; i < V-1; i++) // relax all E edges V-1 times, O(V)
	// Each increment of i is 1 pass
	for (int u = 0; u < V; u++) // these two loops = O(E),
		for (int j = 0; j < AdjList.get(u).size(); j++) {
		// u will iterate through all vertces and j will go through all its neighbors
		IntegerPair v = AdjList.get(u).get(j);
		relax(u, v.first(), v.second());
}
```

If <span style='color:#3867d6'>Bellman Ford</span>, fails to converge after V - 1 passes, that means there is a <span style='color:#eb3b5a'>negative cycle</span> somewhere.

Thus it can also detect negative cycles as well, just execute one more pass of <span style='color:#3867d6'>Bellman Ford</span>

```Java
// Before running this function, run bellman ford once!
public void got_negative_cycles(){
	boolean negative_cycle_exist = false;
	for (int u = 0; u < V; u++) // one more pass to check
		for (int j = 0; j < AdjList.get(u).size(); j++) {
			IntegerPair v = AdjList.get(u).get(j); // try relaxing this edge one more time
			// If the weight can be decreased again then there is a negative cycle
			if (D.get(u) != INF && D.get(v.first()) > D.get(u) + v.second())
				negative_cycle_exist = true; // if this is true, then negative cycle exists!
		}
}
```
#### One Pass Bellman Ford

This will only work if the graph is a <b><mark class="hltr-cyan">DAG</mark></b>.

A <span style='color:#0fb9b1'>DAG</span> does not have any cycles and a <span style='color:#f7b731'>good ordering</span> of the edges can be imposed by using topological ordering. Thus <span style='color:#3867d6'>bellman ford</span> can be modified to just <span style='color:#f7b731'>one pass</span>.

Using any <span style='color:#3867d6'>topological algorithm</span> and get a <span style='color:#0fb9b1'>topological order</span>. The <span style='color:#f7b731'>first item is the starting vertex</span> and then iterate through the order and <span style='color:#f7b731'>relax all of each vertex's neighbors</span>.

This works because, in a topological order, before reaching a vertex, it will have found its shortest path as only vertices to the left can only affect its shortest path.

Time complexity : <b><mark class="hltr-red">O(V + E)</mark></b>

### DFS / BFS

This will only work if the <b><mark class="hltr-cyan">weighted graph is a tree</mark></b>.

It works as a each vertex in a <span style='color:#0fb9b1'>tree</span>, only has <span style='color:#f7b731'>1 possible path</span> and there are <span style='color:#f7b731'>no cycles</span> thus eliminating the possibility of a negative cycle.

Thus, just running <span style='color:#3867d6'>BFS</span> or <span style='color:#3867d6'>DFS</span> will give the SSSP solution.

Time complexity : <b><mark class="hltr-red">O(V)</mark></b>
> Is not O(V + E), as a tree has <span style='color:#f7b731'>V - 1 edges</span>, O(V + V - 1) = O(V)

If the graph is <b><mark class="hltr-cyan">unweighted</mark></b>, then only <span style='color:#3867d6'>BFS</span> can be used.

Time complexity : <b><mark class="hltr-red">O(V + E)</mark></b>


### Dijkstra's Algorithm

This works for any <b><mark class="hltr-cyan">non negative weighted graph</mark></b>.

<span style='color:#3867d6'>Bellman Ford's</span> algorithm does work however for denser graphs like a <span style='color:#0fb9b1'>complete graph</span>, it will run very slow. Thus if the <span style='color:#f7b731'>graph has no negative weights</span>, Dijkstra's algorithm can be used.

- Have a `Solved` array, which stores vertices where the <span style='color:#f7b731'>shortest path weights have been determined</span>. Initially the starting point will be in this array.
-  Repeatedly select vertex with the <span style='color:#f7b731'>minimum shortest path</span> using a <span style='color:#0fb9b1'>BST</span>
-  Afterwards <span style='color:#3867d6'>relax</span> all the neighbors of the selected vertex.
-  Repeat until the priority queue is empty.

The priority queue will initially have all vertices with an <span style='color:#0fb9b1'>Integer Pair</span>, (distance, vertex). Where only the starting point will be (0, start), the rest will be (INF, v).

If a vertex has been relaxed, it needs to be updated in the priority queue, thus a better data structure is to use a <span style='color:#0fb9b1'>balanced binary search tree</span>.

**How can a BST replace a priority queue:**
-  Enqueue -> <span style='color:#3867d6'>Insert</span>
-  Dequeue -> <span style='color:#3867d6'>Find minimum, delete</span>
-  Decrease Key -> <span style='color:#3867d6'>Find key, delete key, insert updated key</span>

Time complexity : <b><mark class="hltr-red">O((V+E) log V)</mark></b>
-  Inserting V vertices in the priority queue or BST, O(V log V)
-  For every edge, run the <span style='color:#3867d6'>relaxation</span> function, O(1)
-  Update the new weights of the vertices, O(E log V) as there can be E number of updates, if every edge can relax a vertex
- O(V log V) + O(E log V) = O((E+V) log V)

#### Modified Dijkstra's Algorithm

This works for any graph that may have <b><mark class="hltr-cyan">negative edges but not cycles</mark></b>.

For this version, a vertex can be <span style='color:#f7b731'>requeued multiple times</span> and not one time. Thus a <span style='color:#0fb9b1'>priority queue</span> can be used instead of a BST.

- Same as original <span style='color:#3867d6'>Dijkstra's Algorithm</span>, but every time a vertex is dequeued check with the distance array to check if its the most updated one
-  If in the future a vertex gets <span style='color:#3867d6'>relaxed</span> then <span style='color:#3867d6'>enqueue</span> a <span style='color:#f7b731'>new pair</span> (V, D) for future propagation.

```Java
pq.enqueue(0,start)
while (!PQ.isempty()){
	vertex = pq.dequeue();
	if (vertex.d == D[u]){
		for each neighbor of the vertex{
			if (D[neighbor] > D[vertex] + neighbor.weight){
				D[neighbor] = D[vertex] + neighbor.weight;
				pq.enqueue((D[neighbor],neighbor.vertex));
			}
		}
	}
}
```

Time complexity : <b><mark class="hltr-red">O(E log E)</mark></b>
-  Now the <span style='color:#0fb9b1'>priority queue</span>, will have multiple copies of vertices, O(E) assuming all edges will <span style='color:#3867d6'>relax</span> all vertices
-  <span style='color:#3867d6'>Relaxation</span> if O(1) and each <span style='color:#3867d6'>enqueue</span> and <span style='color:#3867d6'>dequeue</span> is O(log E)
-  This will be done E number of time thus, O(E log E)

For <span style='color:#0fb9b1'>sparse graph</span> <span style='color:#3867d6'>modified Dijkstra's </span> is better as the normal version still need to run through V number of vertices. However for a <span style='color:#0fb9b1'>dense graph</span>, there is <span style='color:#f7b731'>no difference in time complexity</span>.

However <span style='color:#3867d6'>modified Dijkstra's </span> not the best algorithm for all SSSP problems, there are some rare cases like binary counting which runs on <b><mark class="hltr-red">O(2<sup>(V / 2 + 1)</sup> - 1)</mark></b>, thus it runs on exponential time.

## When to Use Which SSSP Algorithm

![[Summary of When to Use Which SSSP Algorithm.png|center]]
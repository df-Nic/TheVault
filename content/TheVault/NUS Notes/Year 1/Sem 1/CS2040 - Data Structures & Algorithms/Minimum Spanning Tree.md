---
title: Minimum Spanning Tree
Date Created: 2023-07-24
tags:
  - CS2040
  - Graphs
  - Algorithms
---
# Table of Contents
---
- [[#What is a Minimum Spanning Tree|What is a Minimum Spanning Tree]]
	- [[#What is a Minimum Spanning Tree#Ways to get a Min Spanning Tree|Ways to get a Min Spanning Tree]]
		- [[#Ways to get a Min Spanning Tree#Prims Algorithm|Prims Algorithm]]
			- [[#Prims Algorithm#Prims Variant|Prims Variant]]
		- [[#Ways to get a Min Spanning Tree#Kruskal's Algorithm|Kruskal's Algorithm]]
---

# What is a Minimum Spanning Tree
---

**Minimum Spanning Tree**
> A sub graph which <span style='color:#f7b731'>connects with all vertices</span> with the <span style='color:#f7b731'>least weightage</span>

Since a <span style='color:#0fb9b1'>MST</span> is a type of tree, the graph must be <span style='color:#f7b731'>connected and undirected</span>, in addition it has to be <span style='color:#f7b731'>weighted</span>.

If there is no <span style='color:#0fb9b1'>cycles</span> in the graph, then <span style='color:#f7b731'>the graph itself is a MST</span>.

## Ways to get a Min Spanning Tree

**Cycle Property**
> If an edge is <span style='color:#f7b731'>larger than any other edge</span> in a <span style='color:#0fb9b1'>cycle</span>, then the edge cannot be included in the <span style='color:#0fb9b1'>MST</span>.

Thus to find a MST, which longest edges in the cycles are needed to be excluded.

### Prims Algorithm

Start with a <span style='color:#0fb9b1'>tree</span> with the <span style='color:#f7b731'>starting node only</span>. Afterwards look at its neighbors and pick the <span style='color:#f7b731'>edge with the smallest weight</span>. Repeat until all vertices are added into the tree.

-  Have a <span style='color:#0fb9b1'>tree</span> with a <span style='color:#f7b731'>starting vertex</span>.
-  For all <span style='color:#0fb9b1'>neighbors</span> of the starting vertex, <span style='color:#3867d6'>enqueue</span> all into a <span style='color:#f7b731'>priority queue (min heap)</span>.
-  <span style='color:#3867d6'>Dequeue</span>, the smallest weighted edge. If it is not in the <span style='color:#0fb9b1'>tree</span>, add it and <span style='color:#3867d6'>enqueue</span> its neighbors into the priority queue.
-  Repeat until all vertices are in the tree.

```Java
public static void prims(int v){
	PriorityQueue<IntTrio> pq = new PriorityQueue<IntTrio>(new IntTrioComparitor());
	
	ArrayList<IntTrio> neighbor = map.get(v);
	visited[v] = 1;

	for (IntTrio p : neighbor){
		pq.offer(p);
	}
	
	while (pq.size() != 0){
		IntTrio next = pq.poll();
		
		if(visited[next.destination] != 1){
			visited[next.destination] = 1;
		}
		
		neighbor = map.get(next.destination);
		
		for (IntTrio p : neighbor){
			if (visited[p.destination] != 1){
			pq.offer(p);
			}
		}
	}
}
// Note this code does not build the MST, to build, just have an array of v vertices and so the same as BFS / DFS
```

Time complexity : <b><mark class="hltr-red">O(E log V)</mark></b>
- The priority queue can have a <span style='color:#f7b731'>maximum of E edges</span>, O(E)
-  Each edge will be <span style='color:#3867d6'>enqueued</span> and <span style='color:#3867d6'>dequeued</span> <span style='color:#f7b731'>once</span>, O(log E)
-  E can be V or V<sup>2</sup>, thus for a total time of O(E log V)

**Cut of a graph**
> It is a partition of the graph which forms <span style='color:#f7b731'>2 disjoint sets</span>.

No matter how the graph is cut, there will always be edges that links the 2 sets as the graph has to be connected. These edges are called a <span style='color:#0fb9b1'>cut set or a bridges</span>. 

**Cut Property**
> If an edge in a cut set is the <span style='color:#f7b731'>smallest</span>, then that <span style='color:#f7b731'>edge must belong</span> to all <span style='color:#0fb9b1'>MST</span> of the graph.

#### Prims Variant

This variant of prims, can improve the <span style='color:#eb3b5a'>time complexity</span> for <span style='color:#0fb9b1'>dense graphs</span>.

Instead of a priority queue, just use an <span style='color:#f7b731'>array of size V</span>.

- Have an <span style='color:#0fb9b1'>array</span> of <span style='color:#f7b731'>size V</span> and set all to (+infinity, source vertex), at the start the <span style='color:#0fb9b1'>source vertex is itself</span>.
- For the starting vertex, set `arr[s]` to (0, s), as the <span style='color:#f7b731'>starting vertex has no weight</span>.
- While not all vertices are in the T, get the <span style='color:#f7b731'>smallest</span> edge weight in the array and get its <span style='color:#0fb9b1'>neighbors</span>.
- Add that vertex that the edge is connected to into the <span style='color:#0fb9b1'>MST</span> and set `arr[s].first` to be +infinity.
- For all neighbors, if its <span style='color:#f7b731'>not added</span> and `arr[u].first` smaller than the weight from v to u, update, the new weight and the source vertex.
- Repeat step 3 to 5 until all vertices are added into the tree.

Time complexity : <b><mark class="hltr-red">O(V<sup>2</sup>)</mark></b>
- The while loop will iterate for <span style='color:#f7b731'>V vertices</span>, O(V)
-  <span style='color:#f7b731'>Every vertex's neighbors will be scanned</span> to get the smallest edge, O(V) for <span style='color:#0fb9b1'>dense graph</span>

For a <span style='color:#0fb9b1'>sparse graph</span>, using <span style='color:#3867d6'>prims variant</span> will still be O(V<sup>2</sup>).

### Kruskal's Algorithm

Start with a empty <span style='color:#0fb9b1'>tree</span>. Afterwards <span style='color:#f7b731'>pick the smallest edge</span> where it will not form a cycle until all vertices are added.

-  Add all <span style='color:#0fb9b1'>edges</span> into an array.
-  Sort the array in <span style='color:#f7b731'>ascending order</span> based on <span style='color:#f7b731'>weight</span> value.
-  To check for cycles, create a <span style='color:#0fb9b1'>UFDS</span> with V number of disjoint sets. If in the same set it forms a cycle.
-  Remove the <span style='color:#f7b731'>smallest edge</span> and if it <span style='color:#f7b731'>does not form a cycle</span>, add the edge into the <span style='color:#0fb9b1'>tree</span>.
-  <span style='color:#3867d6'>Union</span> the <span style='color:#f7b731'>source vertex and the destination vertex</span> of the <span style='color:#f7b731'>edge</span> in the UFDS.
-  Repeat until all vertices are in the tree.

```Java
public static void main(String[] args){
	
	UnionFind UF = new UnionFind(V); // all V are disjoint sets at the beginning
	int i, mst_cost = 0;
	for (i = 0; i < E; i++) { // process all edges, O(E)
		IntegerTriple e = EdgeList.get(i);
		int src = e.second(), dest = e.third(), weight = e.first();
		
		if (!UF.isSameSet(u, v)) { // if no cycle
			mst_cost += w; // add weight w of e to MST
			System.out.println("Adding   edge: " + e + ", MST cost now = " + mst_cost)
			UF.unionSet(u, v); // link these two vertices
		}
		else{
			System.out.println("Ignoring edge: " + e + ", MST cost now = " + mst_cost);
		}
		// We can add a breaker, once V-1 vertices have been added.
	}
	System.out.printf("Final MST cost %d\n", mst_cost);
}
```

Time complexity : <b><mark class="hltr-red">O(E log V)</mark></b>
-  <span style='color:#3867d6'>Sorting</span> the edge list, O(E log V)
-  Pick the <span style='color:#f7b731'>smallest edge</span>, O(1), just take from index 0.
-  Check if the edge forms a cycle by check if its in he <span style='color:#3867d6'>same set</span>, α(V)
-  If not, add it into the <span style='color:#0fb9b1'>tree</span>, O(1)
-  E can be V or V<sup>2</sup>, thus for a total time of O(E log V)
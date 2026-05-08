---
title: Dynamic Programming
Date Created: 2024-04-22
Last Updated: 2025-10-20
tags:
  - CS2040S
  - Algorithms/DynamicProgramming
---
# Fundamentals of Dynamic Programming
---
**Optimal sub-structure**
>It is the optimal <span style='color:var(--mk-color-yellow)'>solution</span> that can be constructed <span style='color:var(--mk-color-yellow)'>from</span> optimal solutions to <span style='color:var(--mk-color-yellow)'>smaller sub-problems</span>

This condition allows dynamic programming to be <span style='color:var(--mk-color-orange)'>efficient</span>, because it can <span style='color:var(--mk-color-yellow)'>use the smaller sub problems to solve a bigger problem</span>.

**Some examples are**
- [[content/Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Sorting.md#Merge Sort|Merge sort]]
- [[Single Source Shortest Path#Dijkstra's Algorithm|Dijkstra's Algorithm]]
- String reversal
- Greedy & Divide and conquer algorithms

But this can be extended to something called <span style='color:var(--mk-color-turquoise)'>overlapping sub-problems</span>. This is when the <span style='color:var(--mk-color-yellow)'>same smaller problem</span> is used to <span style='color:var(--mk-color-yellow)'>solve multiple different bigger problem</span>. A simple algorithm is the **recursive Fibonacci sequence (With memoization)**.

**Bottom up approach**
>The idea is to <span style='color:var(--mk-color-yellow)'>solve the smallest problems</span> (**Base cases**) first, the <span style='color:var(--mk-color-yellow)'>combine</span> these <span style='color:var(--mk-color-yellow)'>results to solver bigger problems</span>. Repeat until the root problem (**Main problem**) is solved.

This is the same as finding the [[quartz/content/Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Directed Acyclic Graph|topological ordering]] and solve the problems in <span style='color:var(--mk-color-yellow)'>reverse order</span>.

**Top down approach**
>This is the main idea for <span style='color:var(--mk-color-orange)'>recursion</span>. Start with the root problem and then <span style='color:var(--mk-color-yellow)'>recurse</span> down <span style='color:var(--mk-color-yellow)'>until the base case has been reached</span>. Afterwards memorize the result and recurse back up.
<div style="break-after: page;"></div>

# Dynamic Programing Problems
---
## Longest Increasing Subsequence

The task is given an <span style='color:var(--mk-color-purple)'>array</span> of integers, <span style='color:var(--mk-color-orange)'>find the longest increasing subsequence</span>.
- Given an array `[8, 3, 6, 4, 5, 7, 7`
- A **subsequence** can be `[4, 5, 7]` with length 3
- But the<span style='color:var(--mk-color-yellow)'> longest subsequence</span> will be `[3, 4, 5, 7]`

Firstly, this can be modelled as a <span style='color:var(--mk-color-purple)'>DAG</span> where there will be an <span style='color:var(--mk-color-yellow)'>edge</span> connected to numbers if the <span style='color:var(--mk-color-yellow)'>value is greater</span> and the <span style='color:var(--mk-color-yellow)'>value lies to the right of it</span>.

Now it is just using <span style='color:var(--mk-color-teal)'>DFS</span> to find the longest path then add 1 to the result (**DFS counts edges not vertices**).

**Time complexity :** <b><span style='color: var(--mk-color-red)'>O(n<sup>3</sup>)</span></b>
- Firstly the time to construct the <span style='color:var(--mk-color-purple)'>DAG</span> will take O(n<sup>2</sup>)
- Afterwards the cost to run <span style='color:var(--mk-color-teal)'>DFS</span> is O(V + E) or at worst O(n<sup>2</sup>)
- Then <span style='color:var(--mk-color-yellow)'>for each item</span> <span style='color:var(--mk-color-teal)'>DFS</span> will be executed, thus a run time of O(n<sup>3</sup>)

Now see that <span style='color:var(--mk-color-orange)'>many calculations are being redone</span> :
- The original solution look at value 4 <span style='color:var(--mk-color-teal)'>DFS</span> will calculate the longest distance, 4, 5 then 7.
- Then when reaching 5, <span style='color:var(--mk-color-teal)'>DFS</span> will be called on 5 again, it is doing double work
- But what if the <span style='color:var(--mk-color-orange)'>longest path is already calculated</span> for 5, then there is no need to DFS more than once for each value

### Optimisations

Thus a <span style='color:var(--mk-color-green)'>optimisation</span> strategy will be so <span style='color:var(--mk-color-yellow)'>start</span> the <span style='color:var(--mk-color-teal)'>DFS</span> from the <span style='color:var(--mk-color-yellow)'>last item in the topological order</span>, then memorize the result into a <span style='color:var(--mk-color-purple)'>hash table</span> (**suffix optimisation**).

For **any node with outgoing edges**, <span style='color:var(--mk-color-yellow)'>check</span> if the destination node by the outgoing edge longest path is in the <span style='color:var(--mk-color-purple)'>hash table</span>. It it is just retrieve the value, <span style='color:var(--mk-color-red)'>if it is not</span> then <span style='color:var(--mk-color-yellow)'>calculate the longest distance</span> from the destination node. The answer will be to take the maximum value and + 1.

What about **prefix optimisation**, yes it can be done as well just ensure that the answer must be maximum value + 1 for items to the left of the current item.
<div style="break-after: page;"></div>

**How to carry out prefix optimisation**
- `[5, 3, 4]`, given this array start the search range from index 0 to 0, since there is no items then the result is 0 + 1
- Now move on to range 0 to 1, for value 3 <b>check all numbers to the left and they must be smaller</b>. Then get the maximum value and add 1
- Repeat until the array is finished

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(n<sup>2</sup>)</span></b>

**Binary search** can be used to find it optimally, the approach is the same but now start checking in the middle number and go left as it is more likely that items to the left adds on to the sequence, it it is less then go right. 

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(n Log n)</span></b>
## Price Collecting

The task is given a <span style='color:var(--mk-color-purple)'>weighted directed graph</span>, <span style='color:var(--mk-color-yellow)'>find a route that gives the maximum total weight</span>. If there is a <span style='color:var(--mk-color-yellow)'>positive cycle</span>, then the result is <span style='color:var(--mk-color-yellow)'>infinite</span>.

To <span style='color:var(--mk-color-orange)'>find this positive weight cycle</span>, <span style='color:var(--mk-color-yellow)'>negate</span> the graph and run [[Single Source Shortest Path#Bellman Ford|bellman ford]]. But the problem comes with the <span style='color:var(--mk-color-yellow)'>limitation</span> of the <span style='color:var(--mk-color-yellow)'>number of walks</span> to take.
### DAG Solution

1 idea is to use the <span style='color:var(--mk-color-purple)'>DAG</span> solution, assume there are $k$ steps maximum. Then <span style='color:var(--mk-color-yellow)'>copy</span> all $V$ nodes $k$ times and <span style='color:var(--mk-color-yellow)'>link them up accordingly based on the graph</span>.
- If there is an edge from node $A$ to $B$, then connect node $A$ in copy $n$ and link to node $B$ in copy $n + 1$. I copy of all $V$ is for 1 step.

Then using <span style='color:var(--mk-color-teal)'>DFS</span> find the <span style='color:var(--mk-color-yellow)'>longest path</span> in the constructed <span style='color:var(--mk-color-purple)'>DAG</span>, for every source.

**Time complexity :** <b><span style='color: var(--mk-color-red)'>O(kVE)</span></b>
- First the graph is transformed, thus there will be $kV$ nodes and $kE$ edges
- Doing a topological sort or a longest path algorithm will take O($kV + kE$)
- Then the above will run for all $V$ nodes thus $O(kVE)$

However, similar as before, there is a lot of <span style='color:var(--mk-color-orange)'>repeated calculations</span> and a <span style='color:var(--mk-color-green)'>optimisation suggestion</span> is to add a <span style='color:var(--mk-color-turquoise)'>super node</span> as a <span style='color:var(--mk-color-yellow)'>starting point</span> connected to all the source nodes in the <span style='color:var(--mk-color-purple)'>DAG</span> with weight 0. Then <span style='color:var(--mk-color-yellow)'>run DFS once</span>.

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(kE)</span></b>
<div style="break-after: page;"></div>

### Dynamic Programing Solution

There is <span style='color:var(--mk-color-orange)'>another solution</span> however, **using dynamic programming** instead. Now given `fn(v, k)` is to find the maximum distance from a given $v$ in exactly $k$ steps. 

It is to say find the <span style='color:var(--mk-color-yellow)'>maximum distance</span> from one of $v$'s <span style='color:var(--mk-color-yellow)'>neighbours</span> with $k-1$ steps **plus edge weight to the neighbour**. Now the <span style='color:var(--mk-color-orange)'>base case</span> will be `fn(v,0)` which will return 0.

If there is **more than 1 neighbour**, then <span style='color:var(--mk-color-yellow)'>take the maximum</span> among the $x$ neighbours.

This can be <span style='color:var(--mk-color-yellow)'>further improved with memoization</span>, remembering the maximum weight from this node given $k$ steps.

**Time Complexity :** <b><span style='color: var(--mk-color-green)'>O(kV<sup>2</sup>)</span></b> or <b><span style='color: var(--mk-color-green)'>O(kE)</span></b> (For non dense graphs)
## Vertex Cover

Now given a <span style='color:var(--mk-color-purple)'>unweighted and undirected graph</span>. Find a set of vertices such that <span style='color:var(--mk-color-yellow)'>all edges is adjacent to at least 1 node in this set</span>.

**Vertex cover example**
![[Vertex Cover Example.png|center]]
The <span style='color:var(--mk-color-teal)'>blue nodes</span> are the nodes in the set.

Of course, taking all nodes yields a vertex cover set, but the problem wants to <span style='color:var(--mk-color-yellow)'>find the minimum set</span>. This will be hard on a normal graph, thus the solution will focus on <span style='color:var(--mk-color-purple)'>trees</span>.
<div style="break-after: page;"></div>

**Subproblems**
1) `S[v, 0]` is the <span style='color:var(--mk-color-yellow)'>size of the vertex cover</span> of the subtree rooted at vertex $v$ where vertex $v$ is <span style='color:var(--mk-color-red)'>not covered</span>
2) `S[v, 1]` is the <span style='color:var(--mk-color-yellow)'>size of the vertex cover</span> of the subtree rooted at vertex $v$ where vertex $v$ is <span style='color:var(--mk-color-green)'>covered</span>

Thus the <span style='color:var(--mk-color-orange)'>total number of subproblems</span> in any <span style='color:var(--mk-color-purple)'>tree</span> with $v$ vertices is $2v$.

**Subproblem visualisation**
![[Vertex Cover Subproblem Visualisation.png|center]]

**Base Case**
1) If the root is <span style='color:var(--mk-color-green)'>covered</span>, then return 0
2) If the root is <span style='color:var(--mk-color-red)'>not covered</span> then return 1

**Intermediary sub problems**
For the case `S(v, 0)`, means if the root is not covered then <span style='color:var(--mk-color-yellow)'>all of its children must be covered</span>. Thus the result will be, `S[v, 0] = S[c1, 1] + S[c2, 1] + S[c3, 1] + ... + S[ck, 1]` 

For the case `S(v, 1)`, means that <span style='color:var(--mk-color-yellow)'>there can be a choice</span> to cover the children or not. Therefore, f<span style='color:var(--mk-color-orange)'>or each children</span> get the minimum of `min(S[c1, 0], S[c1, 1])`. Once done <span style='color:var(--mk-color-yellow)'>sum all of the minimum values</span> and then + 1 (**Don't forget to count the root**).

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(V)</span></b>
- Each edge is explored **once**
<div style="break-after: page;"></div>

## All-Pairs Shortest Paths

Unlike single source shortest path problems, <span style='color:var(--mk-color-turquoise)'>APSP</span> problems is to <span style='color:var(--mk-color-yellow)'>find the shortest distance from any 2 vertices</span> in a graph. This can help to find the diameter of the graph.

The **naive solution** is to run [[Single Source Shortest Path#Dijkstra's Algorithm|Dijkstra's algorithm]] $V$ times, which does work and the time complexity will be <b><span style='color: var(--mk-color-red)'>O(VE Log V)</span></b>.

This will be fine but when given <span style='color:var(--mk-color-orange)'>cliques or dense graphs</span>, this will run in <b><span style='color: var(--mk-color-red)'>O(V<sup>3</sup> Log V)</span></b>.

If all the weights are the same then use <span style='color:var(--mk-color-teal)'>BFS</span> for a running time of <b><span style='color: var(--mk-color-green)'>O(VE)</span></b>. $V^{2}$ is the best because, it needs to output $V^{2}$ number of iterations.
### Floyd-Warshall

This algorithm uses the fact that given a shortest path $A \rightarrow B \rightarrow C$. Then it contains the shortest path from $A \rightarrow B$ and $B \rightarrow C$.

The <span style='color:var(--mk-color-orange)'>sub-problem</span> for Floyd-Warshall's is to find the distance from vertex $v$ to $w$ using a restricted set of nodes $P$.

**Base case**
>The base case is to find the distance from `S(v, w, P)` where $P$ is a <span style='color:var(--mk-color-yellow)'>empty set</span>, which is just the edge weight  `E[v, w]`.

But $P$ can have $2^{V}$ possible set permutations and thus this algorithm <span style='color:var(--mk-color-yellow)'>limits</span> to using $n + 1$ <span style='color:var(--mk-color-yellow)'>sets</span>.

**Intermediary sub problem**
- Assume that `S(v, w, P7)`, where `P7 = [1, 2, 3, 4, 5, 6, 7]` (Nodes 1 to 7) has already been calculated
- Now given this query `S(v, w, P8)` which includes a new node 8, to calculate the minimum distance it is as follows
	- `min(S(v, w, P7), S(v, 8, P7) + S(8, w, P7)`

If 1 new vertex is added, then the shortest path can :
- <span style='color:var(--mk-color-green)'>Pass</span> by this new vertex
- <span style='color:var(--mk-color-red)'>Does not pass</span> by this new vertex

And assuming <span style='color:var(--mk-color-orange)'>it does pass the new vertex</span>. Then by logic, then it is just the shortest path from $v$ to the new vertex and from the new vertex to $w$.
<div style="break-after: page;"></div>

**Example code of Floyd-Warshall**
```Java
public void floydWarshall(int V, int[][] D) { // D is the memo table
	// This is to iterate through our sets P0, P1, P2, ...
	for (k = 0; k < V; k++) {
		// These next 2 for loops are to loop through every pair of nodes
		for (i = 0; i < V; i++) {
			for (j = 0; j < V; j++) {
				D[i][j] = Math.min(D[i][j], D[i][k] + D[k][j]); 
			}
		}
    }
}
```

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(V<sup>3</sup>)</span></b>, which can be better than the naive solution suggested just now.

What about <span style='color:var(--mk-color-orange)'>path reconstruction</span>, well it can be very space costly as it needs <b><span style='color: var(--mk-color-red)'>O(V<sup>3</sup>)</span></b> space for every single path using a simple array. But can it be better.

How about something similar to a routing table, only use a <span style='color:var(--mk-color-yellow)'>2D array</span> and <span style='color:var(--mk-color-yellow)'>store the first node visited</span> in the shortest path to its destination. 

**Example of a routing table**
![[APSP Path Reconstruction Routing Table.png|center|400]]

With this **example**, our query will look in `P[V][W]` which will return $Z$, then after wards search for `P[Z][W]` and so on until the destination has been reached. This takes <b><span style='color: var(--mk-color-green)'>O(V<sup>2</sup>)</span></b> space.

This can also work by <span style='color:var(--mk-color-yellow)'>storing any node in the path between source and destination</span> and the search function and cost will be the same.

**Variants of Floyd-Warshall**
- Transitive closure where, the matrix will just <span style='color:var(--mk-color-yellow)'>return if there is a path</span> from $v$ to $w$
- Minimum bottleneck edge, where a <span style='color:var(--mk-color-orange)'>bottle neck is the heaviest edge</span> on a particular path. But now it will <span style='color:var(--mk-color-yellow)'>return the minimum bottle neck</span>
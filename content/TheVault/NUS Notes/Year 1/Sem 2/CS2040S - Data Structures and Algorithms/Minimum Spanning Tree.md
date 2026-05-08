---
title: Minimum Spanning Tree
Date Created: 2024-04-21
Last Updated: 2025-10-20
tags:
  - CS2040S
  - DataStructures/Graphs
  - DataStructures/Tree
---
# What is a MST
---
**Spanning Tree**
>It is a collection of edges that<span style='color:var(--mk-color-yellow)'> form a tree</span> that covers <span style='color:var(--mk-color-yellow)'>every node in the graph</span> (One connected component)

**Minimum Spanning Tree**
> It is a <span style='color:var(--mk-color-purple)'>spanning tree</span> but all of its <span style='color:var(--mk-color-yellow)'>edge weights are minimised</span> (Total weight of the tree is the minimum). And it is a <span style='color:var(--mk-color-yellow)'>sub graph of the original graph</span>

Since it is a <span style='color:var(--mk-color-purple)'>tree</span>, it follows certain <span style='color:var(--mk-color-orange)'>properties</span> :
- There are **no cycles**
- There are <span style='color:var(--mk-color-yellow)'>only V - 1 edges</span>, if not there are unconnected nodes or cycles

For now, the graphs will be **undirected** and **weighted**. Also, the edge weight can be negative.

The reason why a MST on a **directed graph** does not work because it **violates MST properties**. In addition, these problems are usually called <span style='color:var(--mk-color-yellow)'>rooted spanning tree</span> (A source to all other nodes) <span style='color:var(--mk-color-yellow)'>which may not exist</span>. 

But on a special case like a [[quartz/content/Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Directed Acyclic Graph|DAG]] with <b>only one root</b> it will work by just adding the minimum weight of an incoming edge. This time complexity is  <b><span style='color: var(--mk-color-green)'>O(E)</span></b> time.

Obviously on a **unweighted** or when **all edges are the same weight** [[quartz/content/Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Breadth-First Search|BFS]] can be used to construct the <span style='color:var(--mk-color-purple)'>MST</span> on <b><span style='color: var(--mk-color-green)'>O(E)</span></b> time. And the total weight is $W \times (V - 1)$, where $W$ is the weight of the edge.

A <span style='color:var(--mk-color-yellow)'>MST is not always unique</span> depending on the graph, but **a graph with unique edge weights**, the **MST will be unique**.

It is important to know that a <b>MST does not give a shortest path</b>.

Be it **adding, subtracting, multiplication, division**, of a constant to the graph, the <span style='color:var(--mk-color-yellow)'>MST will be the same</span>.
<div style="break-after: page;"></div>

**Example on MST**
![[MST Example.png|center]]
## Properties of a MST

As mentioned previously, a <span style='color:var(--mk-color-purple)'>MST</span> has <span style='color:var(--mk-color-yellow)'>no cycles</span>.

What happens when a MST is cut (**Remove 1 edge**), firstly it will <span style='color:var(--mk-color-yellow)'>spilt into 2 connected components</span> and the resulting components will be be a sub <span style='color:var(--mk-color-purple)'>MST</span>.

No matter how the graph is cut, there will always be 1 edge that links 2 disjoint sets as the graph has to be connected. These edges are called a <span style='color:#0fb9b1'>cut set or a bridges</span>.

**Cycle Property**
>For <span style='color:var(--mk-color-orange)'>every cycle</span>, the <span style='color:var(--mk-color-yellow)'>maximum weight edge is not in the MST</span>, no matter what happens. This is <span style='color:var(--mk-color-red)'>not true for minimum weight edge</span>

**Cut Property**
>For <span style='color:var(--mk-color-orange)'>every partition</span> of the nodes, the <span style='color:var(--mk-color-yellow)'>minimum weight edge</span> accords the cut (In the cut set) <span style='color: var(--mk-color-yellow)'>must be in the MST</span>.

The cut property <span style='color:var(--mk-color-orange)'>holds</span>, because given a <span style='color:var(--mk-color-purple)'>MST</span> that does not have this edge, then add the minimum edge in, it will form a cycle and by the <span style='color:var(--mk-color-teal)'>cycle property</span>, the larger weight will be removed. This then <span style='color:var(--mk-color-yellow)'>leaves with the minimum edge</span> which will result in a <span style='color:var(--mk-color-yellow)'>smaller tree</span>.

Because of the <span style='color:var(--mk-color-teal)'>cut property</span>, the <span style='color:var(--mk-color-yellow)'>smallest outgoing edge must be in the MST</span>. This <span style='color:var(--mk-color-red)'>cannot be said for the maximum edge weight that must not be in the MST</span>.
<div style="break-after: page;"></div>

# Generic MST Algorithm
---
It is made up of the <span style='color:var(--mk-color-red)'>red</span> <span style='color:var(--mk-color-teal)'>blue</span> rule

**<b><span style='color:var(--mk-color-red)'>Red</span></b> rule**
>Given a <span style='color:var(--mk-color-yellow)'>cycle</span> in the graph, if it has no red edges, the <span style='color:var(--mk-color-yellow)'>color the max-weight red</span>

**<b><span style='color:var(--mk-color-blue)'>Blue</span></b> rule**
>If given a <span style='color:var(--mk-color-yellow)'>cut</span> with no blue edges, then <span style='color:var(--mk-color-yellow)'>color the minimum weight edge blue</span>

Then <span style='color:var(--mk-color-yellow)'>repeat</span> these 2 rules until <span style='color:var(--mk-color-yellow)'>no more edges can be colored</span>.
# Prim's Algorithm
---
Start with a <span style='color:var(--mk-color-purple)'>set</span> consisting with the <span style='color:#f7b731'>starting node only</span> (Can be any node). Afterwards look at its neighbors and pick the <span style='color:#f7b731'>edge with the smallest weight</span> and <span style='color:var(--mk-color-yellow)'>add the vertex into the set</span>. Repeat until all vertices are added into the tree.

**How does Prims work**
- Firstly, create a <span style='color:var(--mk-color-purple)'>set</span> then <span style='color:var(--mk-color-yellow)'>add the starting</span> node into the set
- For the recently added vertex <span style='color:var(--mk-color-yellow)'>find the cut</span> (Smallest edge)
- This cut must be in the <span style='color:var(--mk-color-purple)'>MST</span> because of the <span style='color:var(--mk-color-teal)'>cut property</span> then add the vertex it is connected to into the <span style='color:var(--mk-color-purple)'>set</span>
- **Repeat** until all vertices are added into the set

To <span style='color:var(--mk-color-orange)'>find the cut</span>, a <span style='color:var(--mk-color-purple)'>minimum heap</span> can be used, at the beginning, add the **starting vertex with weight 0**. Afterwards use the `extractMin` function. Afterwards <span style='color:var(--mk-color-teal)'>relax</span> all neighbouring vertices. <span style='color:var(--mk-color-orange)'>If the vertex is relaxed</span>, <span style='color:var(--mk-color-yellow)'>add to the heap</span> or <span style='color:var(--mk-color-yellow)'>update its priority</span> using `decreaseKey`.

This works because, the <span style='color:var(--mk-color-yellow)'>minimum weight vertex is precisely the cut</span> (smallest weight edge) that will be in the MST. 

To <span style='color:var(--mk-color-orange)'>reconstruct the path</span>, use a <span style='color:var(--mk-color-purple)'>array</span> or a <span style='color:var(--mk-color-purple)'>hash table</span> to update (If <span style='color:var(--mk-color-teal)'>relaxed</span>) and keep track of the parent node.

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(E Log V)</span></b>
-  Each vertex will be <span style='color:var(--mk-color-teal)'>enqueued</span> and <span style='color:var(--mk-color-teal)'>dequeued</span> <span style='color:#f7b731'>once</span>, **O(V Log V)**
- Also <span style='color:var(--mk-color-teal)'>relaxing</span> can cause a update to the priority in the <span style='color:var(--mk-color-purple)'>heap</span> which takes at most **O(E Log V)**

**What if it is known that all edges are between some range** (Lets say 1 to 10) :
- Instead of a <span style='color:var(--mk-color-purple)'>priority queue</span> use a <span style='color:var(--mk-color-purple)'>list of lists</span> of <span style='color:var(--mk-color-yellow)'>size</span> $w$ where $w$ is the <span style='color:var(--mk-color-yellow)'>maximum edge weight</span>
- Then based on the node weight, add it into the correct list, O(1)
- To <span style='color:var(--mk-color-teal)'>remove</span> the node or <span style='color:var(--mk-color-teal)'>extract the minimum node</span>, just use a hash table and remove it, O(1)
- And to <span style='color:var(--mk-color-teal)'>decrease key</span>, use the hash table for lookup and move it to the correct list, O(1)

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(E)</span></b>
# Kruskal's Algorithm
---
Instead of starting with a set, <span style='color:var(--mk-color-yellow)'>get all of the edges and sort it from smallest to biggest weight</span>. And the <span style='color:var(--mk-color-purple)'>spanning tree</span> will be formed by <span style='color:var(--mk-color-teal)'>taking the smallest weighted edges</span>.

**How does Kruskal's work**
-  Add all edges into an <span style='color:var(--mk-color-purple)'>array</span> or a <span style='color:var(--mk-color-purple)'>minimum heap</span> (Need to sort if using an array)
- Also initialise a <span style='color:var(--mk-color-purple)'>union set</span> with $V$ disjoint sets
-  <span style='color:var(--mk-color-yellow)'>Remove the smallest edge</span> and <span style='color:var(--mk-color-yellow)'>check</span> if the <span style='color:var(--mk-color-yellow)'>source</span> and <span style='color:var(--mk-color-yellow)'>destination</span> vertex of the edge are in the <span style='color:var(--mk-color-yellow)'>same component</span>
-  It it is discard it if not add the edge into the tree
-  <span style='color:var(--mk-color-teal)'>Union</span> the <span style='color:#f7b731'>source vertex and the destination vertex</span> of the <span style='color:#f7b731'>edge</span> in the UFDS.

If the <b>edges are already sorted</b> then it will just be <b><span style='color: var(--mk-color-green)'>α(V)</span></b>.

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(E Log V)</span></b>
- <span style='color:var(--mk-color-teal)'>Sorting</span> the edge list, O(E log V) or O (E log E), both are the same
-  Pick the <span style='color:#f7b731'>smallest edge</span>, O(1), just take from index 0.
-  Check if the edge forms a cycle by check if its in the <span style='color:var(--mk-color-teal)'>same set</span>, α(V)
-  If not, add it into the <span style='color:var(--mk-color-teal)'>tree</span>, O(1)

**What if it is known that all edges are between some range** (Lets say 1 to 10) :
- Have a <span style='color:var(--mk-color-purple)'>list of lists</span> of <span style='color:var(--mk-color-yellow)'>size</span> $w$ where $w$ is the <span style='color:var(--mk-color-yellow)'>maximum edge weight</span>
- Then go through all edges and <span style='color:var(--mk-color-yellow)'>add</span> them in the <span style='color:var(--mk-color-yellow)'>corresponding</span> slot based on their <span style='color:var(--mk-color-yellow)'>edge</span>, O(E)
- Then <span style='color:var(--mk-color-yellow)'>iterate</span> through all edges in the list <span style='color:var(--mk-color-yellow)'>sequentially</span> O(E)
- Then similar to <span style='color:var(--mk-color-teal)'>Kruskal's</span>, <span style='color:var(--mk-color-yellow)'>check</span> if the <span style='color:var(--mk-color-yellow)'>vertices are in the same set</span> and <span style='color:var(--mk-color-teal)'>union</span> if not, α(V)

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(αE)</span></b>

# Boruvka's Algorithm
---
The idea is to use connected components to make the <span style='color:var(--mk-color-purple)'>spanning tree</span>.

**How does Boruvka's work**
-  Create $V$ disjoint <span style='color:var(--mk-color-purple)'>sets</span>, which will be the $V$ connected components
- For <span style='color:var(--mk-color-yellow)'>each of these connected components</span>, <span style='color:var(--mk-color-yellow)'>find the smallest outgoing edge</span> that connects the 2 together
- Union both sets once connected
- Repeat until all components are merged

At each step (After going through $v$ components), if there are $v$ components initially there will be $v/2$ components and edges merged and added.

**Time complexity :** <b><span style='color: var(--mk-color-green)'>O(E Log V)</span></b>
# Maximum Spanning Trees
---
Now instead of the minimum spanning tree, now the interest is the <span style='color:var(--mk-color-yellow)'>maximum</span>. Similar to MST, but now the total weight of the <span style='color:var(--mk-color-yellow)'>spanning tree must be the maximum</span>.

Fortunately, this **does not break any MST properties** and there for <span style='color:var(--mk-color-yellow)'>using either Kruskal's or Prims will work</span> no matter what. Just change the logic to <span style='color:var(--mk-color-yellow)'>use the largest edge instead</span>.
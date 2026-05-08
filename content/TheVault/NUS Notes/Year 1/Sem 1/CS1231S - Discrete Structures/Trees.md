---
Title: Trees
Date Created: 2023-11-14
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - DataStructures/Tree
  - Math/Logic
---
# Definitions
---
## Tree

**Circuit-free**
> It is a graph with <span style='color:#f7b731'>no circuits</span>

**Tree**
> A graph is a <span style='color:#0fb9b1'>tree</span> if and only if it is <span style='color:#0fb9b1'>circuit-free</span> and is <span style='color:#f7b731'>connected</span>

**Trivial Tree**
> It is a graph that consist of a <span style='color:#f7b731'>single vertex</span>

**Forest**
> A graph is called a <span style='color:#0fb9b1'>forest</span> if and only if it is <span style='color:#0fb9b1'>circuit-free</span> and is <span style='color:#f7b731'>not connected</span> (collection of trees)

**Lemma 10.5.1**
> Every <span style='color:#eb3b5a'>non</span> <span style='color:#0fb9b1'>trivial tree</span>, there is at <span style='color:#f7b731'>least one vertex of degree one</span>

**Terminal Vertex (Leaf)**
> It is a vertex with a <span style='color:#f7b731'>degree of 1</span>

A graph with 1 or 2 vertices, all its vertices are <span style='color:#0fb9b1'>terminal vertices</span>

**Internal Vertex**
> It is a vertex with a <span style='color:#f7b731'>degree greater than 1</span>

**Theorem 10.5.2**
> Any tree with n vertices ($n \gt 0$) have $n - 1$ edges

**Lemma 10.5.3**
> If $G$ is any connected graph, $C$ is any circuit in $G$ and one of the edges of $C$ is removed from $G$, then <span style='color:#f7b731'>the graph that remains is still connected</span>

This is because in a circuit, there are 2 ways to get from point A to B, either clockwise or anti-clockwise

**Theorem 10.5.4**
> If $G$ is a <mark class="hltr-orange">connected graph</mark> with $n$ vertices and $n – 1$ edges, then $G$ is a tree.

This is just the <mark class="hltr-orange">definition of a tree</mark>

# Rooted Trees
---

**Rooted Tree**
> It is a tree where <span style='color:#f7b731'>one vertex is distinguished</span> from the others and is called the <span style='color:#0fb9b1'>root</span>

**Level**
> The <span style='color:#0fb9b1'>level</span> of the vertex is the <span style='color:#f7b731'>number of edges</span> along the unique path <span style='color:#f7b731'>between it and the root</span>

**height**
> It is the <span style='color:#f7b731'>maximum level of any vertex</span> in the tree

**Children**
> Given any vertex $v$ <span style='color:#f7b731'>all vertices adjacent</span> to $v$ and is <span style='color:#f7b731'>one level farther away from the root</span> is called a <span style='color:#0fb9b1'>child</span> of $v$

**Parent**
> Let $w$ be the <span style='color:#0fb9b1'>child</span> of $v$ then $v$ is the <span style='color:#0fb9b1'>parent</span> of $w$

**Sibling**
> 2 <span style='color:#f7b731'>distinct</span> vertices with the <span style='color:#f7b731'>same</span> <span style='color:#0fb9b1'>parent</span> are called <span style='color:#0fb9b1'>siblings</span>

**Ancestor & Descendant**
> $w$ and $v$ are vertices on a graph, if $v$ lies on a unique path between the root  and $w$ then $v$ is the <span style='color:#0fb9b1'>ancestor</span> of $w$ and $w$ is called the <span style='color:#0fb9b1'>descendent</span> of $b$

## Binary Trees

**Binary Tree**
> A <span style='color:#0fb9b1'>rooted tree</span> in which <span style='color:#f7b731'>every parent has at most two children</span>. Each <span style='color:#0fb9b1'>child</span> is designated either a <span style='color:#0fb9b1'>left child</span> or a <span style='color:#0fb9b1'>right child</span> (but not both), and every parent has at most one left child and one right child

**Full Binary Tree**
> A <span style='color:#0fb9b1'>binary tree</span> in which <span style='color:#f7b731'>each parent has exactly two children</span> (Except the root)

It is just a complete binary tree, were its sub-trees are also full

**Left Subtree**
> For any <span style='color:#0fb9b1'>parent</span> if it has a <span style='color:#0fb9b1'>left child</span> then the <span style='color:#0fb9b1'>left subtree</span> is a <span style='color:#f7b731'>binary tree whose root is the left child</span>

**Right Subtree**
> For any <span style='color:#0fb9b1'>parent</span> if it has a <span style='color:#0fb9b1'>right child</span> then the <span style='color:#0fb9b1'>right subtree</span> is a <span style='color:#f7b731'>binary tree whose root is the right child</span>

**Theorem 10.6.1 Full Binary Tree Theorem**
> If $T$ is a <span style='color:#0fb9b1'>full binary tree</span> with $k$ <span style='color:#0fb9b1'>internal vertices</span>, then $T$ has a total of $2k + 1$ vertices and has $k + 1$ <span style='color:#0fb9b1'>terminal vertices </span>(leaves).

**Theorem 10.6.2**
> For non-negative integers $h$, if $T$ is any <span style='color:#0fb9b1'>binary tree</span> with <span style='color:#0fb9b1'>height</span> $h$ and $t$ <span style='color:#0fb9b1'>terminal vertices</span> (leaves), then;

-   $t \le 2^{h}$
	 Equivalently, $\log_{2} t \le h$

The above is saying that the <span style='color:#f7b731'>maximum number </span>of <span style='color:#0fb9b1'>leaves</span> of height $h$ is $2^{h}$

## Binary Tree Traversal

It is also know as <span style='color:#0fb9b1'>tree traversal</span> or <span style='color:#0fb9b1'>tree search</span> where <span style='color:#f7b731'>each vertex is visited exactly once</span>
### Breadth-First Search (BFS)

The search <span style='color:#f7b731'>starts from the root</span> of the binary tree, it visits every vertex in the next level before proceeding to the next level. (<span style='color:#f7b731'>Level by level traversal</span>)

By convention it starts from the <span style='color:#f7b731'>left most node </span>in the tree
### Depth-First Search (DFS)

The search <span style='color:#f7b731'>starts from the root</span> of the binary tree, it goes as deep as possible before heading up to the parent vertex. Starting from the left

**Pre-Order**
1) Print the value inside the <span style='color:#0fb9b1'>root</span> vertex
2) Go to the <span style='color:#0fb9b1'>left subtree</span> and recursively call the pre-order traversal function
3) Go to the <span style='color:#0fb9b1'>right subtree</span> and recursively call the pre-order traversal function

**In-Order**
1) Go to the <span style='color:#0fb9b1'>left subtree</span> and recursively call the in-order traversal function
2) Print the value inside the <span style='color:#0fb9b1'>root</span> vertex
3) Go to the <span style='color:#0fb9b1'>right subtree</span> and recursively call the in-order traversal function

**Post-Order**
1) Go to the <span style='color:#0fb9b1'>left subtree</span> and recursively call the post-order traversal function
2) Go to the <span style='color:#0fb9b1'>right subtree</span> and recursively call the post-order traversal function
3) Print the value inside the <span style='color:#0fb9b1'>root</span> vertex

# Spanning Tree
---
A <span style='color:#0fb9b1'>spanning tree</span>, is a subgraph of a graph $G$ where vertices are chosen to connect the graph such that
1) It becomes a tree
2) It visits every vertex

**Proposition 10.7.1**
> <span style='color:#f7b731'>Every connected graph</span> has a <span style='color:#0fb9b1'>spanning tree</span> and <span style='color:#f7b731'>any 2</span> <span style='color:#0fb9b1'>spanning trees</span> for a graph have the <span style='color:#f7b731'>same number of edges</span>

## Minimum Spanning Tree (MST)

It is a optimisation problem <mark class="hltr-orange">on a weighted graph</mark> and similar to a <span style='color:#0fb9b1'>spanning tree</span>

**Weighted Graph**
> It is a graph for which <span style='color:#f7b731'>each edge has an associated positive real number weight</span>. The <span style='color:#f7b731'>sum</span> of the weights of all the edges is the <span style='color:#0fb9b1'>total weight</span> of the graph

Where : 
- $w(e)$ denotes the weight an edge
- $w(G)$ denotes the total weight of the graph $G$

**Minimum Spanning Tree**
> A connected weighted graph is a spanning tree that has the <mark class="hltr-orange">least possible total weight</mark> compared to all other spanning trees for the graph

**Ways to get a MST**
1) Kruskal's Algorithm
2) Prim's Algorithm
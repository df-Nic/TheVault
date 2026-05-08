---
Title: Graphs
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - DataStructures/Graphs
  - Math/Logic
---
# Basic Properties & Definitions
---
## Undirected Graphs

It consists of 2 non-empty finite sets of <span style='color:#0fb9b1'>vertices</span> and <span style='color:#0fb9b1'>edges</span> where each edge is associated with <span style='color:#f7b731'>1 or 2 vertices called endpoints</span>

$G$ is denoted as a undirected graph by $G = (V,E)$
$V$ is defined as a set of vertices (or nodes) in $G$ 
$E$ is defined as a set of edges in $G$

**Types of Endpoints**
An edge is said to <span style='color:#0fb9b1'>connect</span> its endpoints;
1)  Adjacent Vertices
	 2 vertices connected by an edge

2)  Adjacent to Itself
	 A vertex that is an endpoint of a <span style='color:#0fb9b1'>loop</span>

An edge is said to be <span style='color:#f7b731'>incident on</span> each of its end points and if 2 edges have the same end point(s) they are called <span style='color:#0fb9b1'>adjacent edges</span>. This <mark class="hltr-orange">undirected edge</mark> is defined as $e = {v,w}$ where $v$ and $w$ are vertices

An undirected graph is <span style='color:#0fb9b1'>cyclic</span> if it <span style='color:#f7b731'>contains a loop or a cycle</span>, otherwise, it is <span style='color:#0fb9b1'>acyclic</span>.

Note that all <mark class="hltr-orange">graphs are finite</mark>
## Directed Graph 

Also known as <span style='color:#0fb9b1'>digraph</span>, consisting of 2 non-empty finite sets of <span style='color:#0fb9b1'>vertices</span> and <span style='color:#0fb9b1'>directed edges</span> associated with an <span style='color:#f7b731'>ordered pair</span>. This <mark class="hltr-orange">directed edge</mark> is defined as $e = {v,w}$ for an edge from $v$ to $w$.

**Indegree**
> Denoted as $deg^{-}(v)$ is the number of <mark class="hltr-orange">directed edges that end</mark> at $v$

**Outdegree**
> Denoted as $deg^{+}(v)$ is the number of <mark class="hltr-orange">directed edges that originate</mark> from $v$

**Note that :** $\sum_{v \in V} deg^{-}(v) = \sum_{v \in V} deg^{+}(v) = \vert E \vert$
## Vertex Coloring

It is a problem to find the<span style='color:#f7b731'> minimum number of colours</span> to colour a graph <span style='color:#f7b731'>without any neighbouring vertices </span>having the <span style='color:#f7b731'>same colour </span>

Used for
-  Class Scheduling
-  Assign Non-interfering frequencies to stations
-  Design sets of signal that can be green at the same time (Traffic light)

## Types of Undirected Graphs

1) Simple Graph
	 It is a <span style='color:#f7b731'>undirected graph that does not</span> have any <span style='color:#0fb9b1'>loops</span> or <span style='color:#0fb9b1'>adjacent edges</span>

2) Complete Graph
	 A complete graph of $n$ vertices, $n \gt 0$, denoted as $K_{n}$, is a <span style='color:#0fb9b1'>simple graph</span> with <span style='color:#f7b731'>exactly one edge</span> connecting <span style='color:#f7b731'>each pair of distinct vertices</span>

The total number of edges in $K_{n} = n(n - 1) / 2$ 

3) Bipartite Graph
	 Also known as <span style='color:#0fb9b1'>bigraph</span> is a simple graph whose vertices can be divided into 2 disjoint sets and <span style='color:#f7b731'>every edge connects a vertex in one set to another</span> and <span style='color:#eb3b5a'>never to a vertex in the same set</span>

4) Complete Bipartite Graph
	 It is a <span style='color:#0fb9b1'>bigraph</span> with the same properties but <span style='color:#f7b731'>every vertex in a set must connect to every vertex in the other set</span>. If $\vert U \vert = m$ and $\vert V \vert = n$, then $K_{m,n}$ 

## Subgraphs of a Graph

A graph $H$ is said to be a <span style='color:#0fb9b1'>subgraph</span> of graph $G$ if and only if :
1) <span style='color:#f7b731'>Every vertex</span> in $H$ is in $G$
2) <span style='color:#f7b731'>Every edge</span> in $H$ is also in $G$
3) <span style='color:#f7b731'>Every edge</span> in $H$ has the <span style='color:#f7b731'>same endpoints</span> as it has in $G$

<mark class="hltr-orange">An exactly same graph</mark> is also a <span style='color:#0fb9b1'>subgraph</span>

## Degree of a Vertex

Let $G$ be a <span style='color:#0fb9b1'>undirected graph</span> and $v$ a <span style='color:#0fb9b1'>vertex</span> of $G$. The <span style='color:#0fb9b1'>degree</span> of $v$, denoted $deg(v)$, equals the <span style='color:#f7b731'>number of edges that are</span> <span style='color:#0fb9b1'>incident on</span> $v$ (connected to $v$), with an <mark class="hltr-orange">edge that is a loop counted twice</mark>

The <span style='color:#0fb9b1'>total degree </span>of $G$ is the <span style='color:#f7b731'>sum of the degrees of all the vertices</span> of G

### Theorems for Degrees of a Vertex

**Theorem 10.1.1 The Handshake Theorem**
> For any graph $G$ the<span style='color:#0fb9b1'> total degree</span> is the <span style='color:#f7b731'>twice the number of edges</span> where $\vert V \vert \ge 0$

**Total Degree** of $G$ = $2 \times \text{(Number of edges of G)}$

**Corollary 10.1.2**
> <span style='color:#0fb9b1'>Total degree</span> of a graph is <span style='color:#f7b731'>even</span>

**Corollary 10.1.3**
> Any graph there are an <span style='color:#f7b731'>even number of vertices of odd degrees</span>.

**Corollary 10.1.3** is based of **10.1.2** as since the total degree is even, to make any odd number even is to add with another odd number

# Trails, Paths and Circuits
---

**Walk**
> A <span style='color:#0fb9b1'>walk</span> from vertex $v$ to $w$ is an <span style='color:#f7b731'>alternating sequence</span> of <span style='color:#0fb9b1'>adjacent vertices</span> and edges in a form of $v_{0}e_{1}v_{1} \dots v_{n-1}e_{n}v_{n}$. Where the <span style='color:#0fb9b1'>length</span> of the walk is the <span style='color:#f7b731'>number of edges </span>

**Trivial Walk**
> It is a <span style='color:#0fb9b1'>walk</span> from vertex $v$ to $v$ and <span style='color:#f7b731'>it consists of the single vertex</span> $v$

**Closed Walk**
> A <span style='color:#0fb9b1'>walk</span> that <span style='color:#f7b731'>starts and ends at the same vertex</span>

**Trail**
> It is a <span style='color:#0fb9b1'>walk</span> that <span style='color:#f7b731'>does not contain repeated edges</span>

**Path**
> It is a <span style='color:#0fb9b1'>trail</span> that <span style='color:#f7b731'>does not contain repeated vertexes</span>

**Circuit or Cycle**
> It is a <span style='color:#0fb9b1'>closed walk </span>of <span style='color:#f7b731'>at least length 3</span> that <span style='color:#f7b731'>does not contain a repeated edges</span>

**Simple Circuit or Simple Cycle**
> It is a <span style='color:#0fb9b1'>circuit</span> that<span style='color:#f7b731'> does not have other repeated vertex except the start and the end</span>

## Connectedness

Two vertices are <span style='color:#0fb9b1'>connected</span> if and only if there is a <span style='color:#0fb9b1'>walk</span> from $v$ to $w$

The <span style='color:#f7b731'>graph is connected</span> if and only if <span style='color:#f7b731'>any 2 vertices</span> there exist a <span style='color:#0fb9b1'>walk</span>
	 Symbolically : G is connected iff $\forall$ vertices $v,w \in V, \exists$ a walk from $v$ to $w$

**Lemma 10.2.1**

Let $G$ be a graph

1)  If $G$ is <span style='color:#0fb9b1'>connected</span>, then <span style='color:#f7b731'>any 2 distinct vertices</span> can be connected by a <span style='color:#0fb9b1'>path</span>
2)  If vertices $v$ and $w$ are part of a <span style='color:#0fb9b1'>circuit</span> and <span style='color:#f7b731'>one edge is removed</span>, then there <span style='color:#f7b731'>still exits a</span> <span style='color:#0fb9b1'>trail</span> from $v$ to $w$
3)  If $G$ is <span style='color:#0fb9b1'>connected</span> and contains a <span style='color:#0fb9b1'>circuit</span>, then an <span style='color:#f7b731'>edge of the circuit can be removed without disconnecting</span> $G$

### Connected Component

It is a <span style='color:#f7b731'>connected subgraph</span> of $G$ which might <span style='color:#f7b731'>not necessary be</span> <span style='color:#0fb9b1'>connected</span> where its <mark class="hltr-orange">size is the largest</mark>

For a graph $H$ to be a <span style='color:#0fb9b1'>connected component</span>;
1)  The graph $H$ <span style='color:#f7b731'>must be a subgraph</span> of $G$
2)  The graph $H$ <span style='color:#f7b731'>must be connected</span>
3)  <span style='color:#f7b731'>No connected subgraph</span> of $G$ has $H$ as a subgraph and <span style='color:#f7b731'>contains vertices or edges that are not in</span> $H$
	 This point refers to $H$ being the <mark class="hltr-orange">largest size</mark> and there should be no other subgraph besides itself

## Euler

**Euler Circuit**
> It is a <span style='color:#0fb9b1'>circuit</span> in a graph $G$ such that it <span style='color:#f7b731'>contains every vertex and traverses every edge</span> in $G$ <mark class="hltr-orange">exactly once</mark>

**Eulerian Graph**
> It is a graph that contains an <span style='color:#0fb9b1'>Euler circuit</span>

**Theorem 10.2.2**
> If a graph has an <span style='color:#0fb9b1'>Euler circuit</span>, then <span style='color:#f7b731'>every vertex</span> of the graph has <span style='color:#f7b731'>positive even degree</span>

But this is <mark class="hltr-red">not true</mark> for if <span style='color:#eb3b5a'>every vertex has a positive even degree then it is a Euler circuit</span>

**Contrapositive Version of Theorem 10.2.2**
> If some vertex of a graph has <span style='color:#f7b731'>odd degree</span>, then the <span style='color:#f7b731'>graph does not have</span> an <span style='color:#0fb9b1'>Euler circuit</span>

**Euler Trail / Path**
> It is a <span style='color:#0fb9b1'>path</span> from $v$ to $w$ such that <span style='color:#f7b731'>every vertex </span> is traversed <mark class="hltr-orange">at least once</mark> and <span style='color:#f7b731'>every edge</span> has been traversed <mark class="hltr-orange">exactly once</mark>

**Corollary 10.2.5**
> There is a <span style='color:#0fb9b1'>Euler trail</span> from $v$ to $w$ if and only if $G$ is <span style='color:#0fb9b1'>connected</span>, $v$ and $w$ have <span style='color:#f7b731'>odd degrees</span> and <span style='color:#f7b731'>all other vertices</span> have <span style='color:#f7b731'>positive even degrees</span>

## Hamiltonian Circuits

**Hamiltonian Circuit**
> It is a <span style='color:#f7b731'>simple circuit</span> on a graph $G$ that <span style='color:#f7b731'>includes every vertex exactly once except the first and the last</span>

**Hamiltonian Graph**
> Also called a <span style='color:#0fb9b1'>Hamilton graph</span>, is a graph that contains a Hamiltonian circuit

An Euler circuit maybe not be a Hamiltonian circuit if it includes more than one vertices, similarly, a Hamiltonian circuit may not be a Euler circuit if it does not include all edges 

**Proposition 10.2.6**
If the graph is <span style='color:#0fb9b1'>Hamiltonian</span>, then it has a subgraph $H$ with the following properties

1)  $H$ <span style='color:#f7b731'>contains every vertex</span> of $G$
2)  $H$ is <span style='color:#0fb9b1'>connected</span>
3)  $H$ has the <span style='color:#f7b731'>same number of edges as vertices</span>
4)  <mark class="hltr-orange">Every vertex</mark> of $H$ has a <span style='color:#f7b731'>degree of 2</span>

By contraposition, if $G$ does not have a subgraph with all 4 properties then it <span style='color:#f7b731'>does not have a Hamiltonian circuit</span>

# Matrix Representation for Graphs
---
## Matrix

A m by n matrix $A$ over a set $S$ is a rectangular array of elements <span style='color:#f7b731'>arranged into m rows and n columns  </span>

2 matrixes $A$ and $B$ are considered equal if
1)  Both their <span style='color:#f7b731'>row and column are of equal size</span>
2)  <span style='color:#f7b731'>Every</span> corresponding element are <span style='color:#f7b731'>all equal</span>
### Square Matrix

A square matrix is where the <span style='color:#f7b731'>row and column are of equal length</span>

If a matrix $A$ is a <span style='color:#0fb9b1'>square matrix</span> then the <span style='color:#0fb9b1'>main diagonal</span> consists of all entries $a_{11}, a_{22}, \dots, a_{nn}$
### Matrix Multiplication

To be able to multiply 2 matrixes $A$ and $B$, the <span style='color:#f7b731'>column length of A must equals to the row length of B</span>. The result will be the <span style='color:#f7b731'>row length of A by the column length of B</span> denoted as $AB$

The <span style='color:#0fb9b1'>scalar product </span>or <span style='color:#0fb9b1'>dot product</span> will return a real number as follows:
$$
\begin{bmatrix}
a_{1} & a_{2} & \dots & a_{i} \\
\end{bmatrix} 
\cdot
\begin{bmatrix}
b_{1} \\ 
b_{2} \\
\vdots \\
b_{j} \\
\end{bmatrix} = a_{1} \times b_{1} + a_{2} \times b_{2} + \dots + a_{i} \times b_{j}
$$

Note that matrix multiplication is <span style='color:#eb3b5a'>not commutative</span> but <span style='color:#20bf6b'>is associative</span>

### Identity Matrix

It is denoted as $I$ or $\updelta_{ij}$ is of size n by n where <span style='color:#f7b731'>n is the column size</span> of matrix $A$, in which all the entries in the <span style='color:#0fb9b1'>main diagonal</span> are 1's and all other entries are 0's

$$
\updelta_{ij} =
\begin{cases}
1,  & \text{if $i=j$} \\
0, & \text{if $i \ne j$}
\end{cases}
\text{ for all i,j = 1, $\dots$, n}
$$

It is a matrix when multiplied by matrix $A$, will return $A$ <span style='color:#f7b731'>no matter which size it is being multiplied from</span>

### Nth Power of a Matrix

For any n by n matrix $A$, the <span style='color:#0fb9b1'>powers of</span> $A$ are defined as : 
-  $A^{0} = I$ where $I$ is the n by n identity matrix
-  $A^{n} = A A^{n-1}$ for all integers $n \ge 1$

$AA^{n-1}$ is the <span style='color:#f7b731'>matrix multiplication</span> of $A$ and the previous power of $A$

### Counting walks of length N

To find the number of walks from $v_{i}$ to $v_{j}$ of length n, then to do this <span style='color:#f7b731'>multiply</span> $A$ to the power of n ($A^{n}$)

Afterwards get the $a_{ij}$ value in the matrix

**Theorem 10.3.2**
> If $G$ is a graph with vertices $v_{1}, v_{2}, \dots, v_{m}$ and $A$ is the <span style='color:#0fb9b1'>adjacency matrix</span> of $G$, then for each positive integer n and for all integers i, j = 1, 2, …, m, the ij-th entry of $A^{n}$ = the <span style='color:#f7b731'>number of walks of length n from</span> $v_{i}$ to $v_{j}$.
## Adjacency Matrix

It is one way to represent a graph. Where $A$ is a n by n matrix and $A = (a_{ij})$ for which $a_{ij}$ = the <span style='color:#f7b731'>number of arrows</span> from $v_{i}$ to $v_{j}$

$$
\begin{bmatrix}
1 & 0 & 0 \\
1 & 1 & 2 \\
1 & 0 & 0 \\
\end{bmatrix} 
$$

Thus from the above example, it tells us that there are 2 edges pointing from $v_{2}$ to $v_{3}$. And this is for <mark class="hltr-orange">directed graphs</mark>

For<span style='color:#f7b731'> undirected graphs</span>, the matrix will be symmetric along the <span style='color:#0fb9b1'>main diagonal </span>

There is another way as well and it is call the <span style='color:#0fb9b1'>adjacency list</span>

# Planar Graphs
---
## Isomorphic Graphs

They are graphs that are <mark class="hltr-orange">exactly the same</mark> except for their labeling of their vertices and edges, this is called <span style='color:#0fb9b1'>isomorphic</span>

Let $G = (V_{G}, E_{G})$ and $G'= (V_{G'}, E_{G'})$, $G$ is <span style='color:#0fb9b1'>isomorphic</span> to $G'$ ($G \cong G'$) if and only if there exist a [[Functions#Properties of Functions|bijection]], $g : V_{G} \rightarrow V_{G'}$ and $h : E_{g} \rightarrow E_{G'}$, <span style='color:#f7b731'>preserving the edge-endpoint functions</span> of $G$ and $G'$ for all $v \in V_{G}$ and $e \in E_G$, 
	 $v$ is an endpoint of $e \iff g(v) \text{ is an endpoint of } h(e)$ 

An alternative to the definition above is, $G$ is <span style='color:#0fb9b1'>isomorphic</span> to $G'$ if and only if there exist a <span style='color:#f7b731'>permutation</span> $\pi : V_{G} \rightarrow V_{G'}$ such that $\{u,v\} \in E_{G} \iff \{\pi(u), \pi(v)\} \in E_{G}$

**Theorem 10.4.1 Graph Isomorphism is an Equivalence Relation**
> Let $S$ be a set of graphs and let $\cong$ by the relation of graph isomorphism on $S$. Then $\cong$ is an [[Relations#Definition of Equivalence Relation|equivalence relation]] on $S$

## Planar Graph

It is a graph that can be drawn on a 2-Dimensional plane <span style='color:#f7b731'>without the edges crossing</span>

A <span style='color:#0fb9b1'>non-planner representation of a graph</span> is a graph which edges overlap one another

**Kuratowski's Theorem**
> A finite graph is a <span style='color:#0fb9b1'>planar</span> if and only if it <span style='color:#f7b731'>does not contain a subgraph that is a subdivision</span> of the complete graph of $K_{5}$ or the complete bipartite graph $K_{3,3}$

<span style='color:#0fb9b1'>Subdivision</span> is the <span style='color:#f7b731'>addition of more vertices and edges</span> in between an existing edge

### Euler's Formula

If a graph is a <span style='color:#0fb9b1'>planar graph</span> it divides the plane up into<span style='color:#f7b731'> regions or faces</span>

A <span style='color:#0fb9b1'>face</span> can have at <span style='color:#f7b731'>least 3 edges</span> (Needs to be encased) and <span style='color:#f7b731'>each edge will share a boarder with 2 faces</span>

For a connected <span style='color:#0fb9b1'>planar</span> simple graph $G = (V,E)$ with $e = \vert E \vert$ and $v = \vert V \vert$, if we let $f$ be the number of faces then $f = e - v + 2$ 

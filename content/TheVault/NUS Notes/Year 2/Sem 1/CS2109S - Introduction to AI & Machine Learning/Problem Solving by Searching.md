---
title: Problem Solving by Searching
Date Created: 2024-08-19
Last Updated: 2025-09-28
tags:
  - CS2109S
  - AI
  - Graphs
  - Searching
---
# Designing an Agent
---
Typically when a problem is **solved using searching**, we are building a [[Designing an AI#Types of Agent Structures|goal based agent]]. And for this to work, there are <span style='color:var(--mk-color-orange)'>certain constraints necessary for the environment</span>: 
1) **Fully-observable**
2) **Deterministic**
3) **Static**
4) **Discrete**

**Steps in building an Agent:**
![[Building an Agent.png|center]]

> [!info] Understanding the Environment
> To understand how the environment works, the agent will **need to know the following**:
> - States (*The different nodes in the graph*)
> - Initial state (*Starting point*)
> - Goal state & test (*The state is the end point, a test is to check if the state is a goal state*)
> - Actions (*What can the agent do at the current state*)
> - Transition model (*Tells the agent what if you took this action*)
> - Action cost function (*Cost for executing a action*)

When **modeling an environment** it is good to ensure that the <span style='color:var(--mk-color-yellow)'>states</span> are abstract <span style='color:var(--mk-color-yellow)'>representations of something concrete</span>. This is known as the <b><mark style='background:var(--mk-color-turquoise)'>representation invariant</mark></b>.
# Search Algorithms
---
In terms of AI, a search algorithm takes in a problem and returns a <span style='color:var(--mk-color-green)'>solution</span> or a <span style='color:var(--mk-color-red)'>failure</span>.
> Each search algorithm is defined by the <span style='color:var(--mk-color-yellow)'>order of node expansion</span> (*Traversal method*), which depends on the data structure used.

> [!attention] Evaluation Citeria is Different from the norm
> The analysis of search algorithms is slightly different from the [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Graph Traversal|ususal]].
> 
> **Time complexity** - Number of nodes <span style='color:var(--mk-color-yellow)'>generated or expanded</span> (*Visited*)
> **Space complexity** - Maximum number of <span style='color:var(--mk-color-yellow)'>nodes inside the memory</span>
> **Completeness** - If a solution exist does it return it
> **Optimality** - Does it find the best solution (*Shortest path or least cost*)

Some <span style='color:var(--mk-color-orange)'>terms</span> used in **analysis** are:
- Branching factor ($b$), which are the **number of children**
- Depth ($d$)
- Maximum depth (m)

There are <span style='color:var(--mk-color-orange)'>2 classes of searches</span>:
1) **Tree Search**
> By the [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Graph Terminologies|definition of a tree]], a tree search should be used when there are <b><mark style='background:var(--mk-color-yellow)'>no cycles</mark></b> and <b><mark style='background:var(--mk-color-yellow)'>no backtracking</mark></b> (*Or limit the depth*).
2) **Graph Search**
> Similar to tree search but it **keeps track of weather nodes have been visited or not**.

However traditional search algorithms can be classified into <span style='color:var(--mk-color-turquoise)'>uninformed</span> and <span style='color:var(--mk-color-turquoise)'>informed</span> search algorithms.

These **searches** given the time constraint <span style='color:var(--mk-color-yellow)'>gives either a solution or not</span> and it is <b><mark style='background:var(--mk-color-yellow)'>optimal</mark></b>. It also works only on **low to moderate** state spaces.
## Uninformed Search Algorithms

An uninformed search or <span style='color:var(--mk-color-turquoise)'>blind search</span>, is when the agent has <span style='color:var(--mk-color-red)'>no information on how close it is</span> (*Current state*) to its goal when traversing the graph.
### Types of Uninformed Search Algorithms
#### Breadth-First Search (BFS)

[[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Breadth-First Search|BFS]] traverses the graph in a **level by level style**. It is **uninformed** as at any point it has no information about whereabouts of the goal state.

Its **order of expansion** is defined by a <span style='color:var(--mk-color-purple)'>queue data structure</span>.

**Time complexity** - $1 + b + b^{2} + b^{3} + \dots + b^{d} =$ O($b^{d}$)
**Space complexity** - O($b^{d}$), since the worst case is when the <span style='color:var(--mk-color-orange)'>last node visited is the goal state</span>
**Completeness** - As long as $b$ is finite, it will terminate
**Optimality** - <span style='color:var(--mk-color-green)'>Yes</span> it provides the minimal path solution granted <span style='color:var(--mk-color-orange)'>every action costs the same</span>
#### Uniform-Cost Search (UCS)

Unlike BFS which is a special case of <span style='color:var(--mk-color-turquoise)'>UCS</span>, it behaves and similarly to how [[Single Source Shortest Path#Dijkstra's Algorithm|Dijkstra's algorithm]] works.

Its **order of expansion** is defined by a <span style='color:var(--mk-color-purple)'>priority queue data structure</span>.

**Time complexity** - O($b^{C^{*} / \epsilon}$) where $C^{*}$ is the optimal cost & $\epsilon$****** is the minimum edge cost along the path
**Space complexity** - O($b^{C^{*} / \epsilon}$), thus the the **depth for UCS is formulated** as, $d = C^{*} / \epsilon$
**Completeness** - <span style='color:var(--mk-color-green)'>Yes</span> as long as $\epsilon \gt 0$ (*0 cost cycle*) & $C^{*}$ is finite. 
**Optimality** - <span style='color:var(--mk-color-green)'>Yes</span> as long as $\epsilon \gt 0$

> [!question] Why the Condition for Complete & Optimal?
> If $\epsilon \le 0$ then that means that there is <span style='color:var(--mk-color-red)'>no path</span> and there is no such thing as a 0 cost path because of the **representation invariant**.
> 
> If $C^{*}$ is infinite, then the algorithm will <span style='color:var(--mk-color-red)'>never terminate</span>.
#### Depth-First Search (DFS)

[[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Depth-First Search|DFS]] traverses the graph as deep as possible before reverting. It is **uninformed** as at any point it has no information about whereabouts of the goal state.

Its **order of expansion** is defined by a <span style='color:var(--mk-color-purple)'>stack data structure</span>.

**Time complexity** - O($b^{m}$)
**Space complexity** - O($bm$), since the worst case is when the search goes to the maximum depth
**Completeness** - <span style='color:var(--mk-color-red)'>No</span> if the depth is infinite or there are cycles
**Optimality** - <span style='color:var(--mk-color-red)'>No</span>
#### Bidirectional Search

This type of searching requires **2 connected components to be linked together by 1 bridge**. It uses the tactics of <span style='color:var(--mk-color-yellow)'>forwards and backwards searching at the same time</span> and terminating when it meets.

This will be <span style='color:var(--mk-color-green)'>better than BFS</span> given that the graph satisfy the conditions ($2 \times O(b^{d/2}) \lt O(b^{d})$).

> [!warning] Issues with Bidirectional Search
> Firstly the conditions for this to work is very specfic since if there are <span style='color:var(--mk-color-red)'>more than 2 bridges it might not terminate</span>.
> 
> If there are **many goal states** then it might be more <span style='color:var(--mk-color-red)'>complex to impliment</span>.
### Iterations of Uninformed Search Algorithms

Some modifications to the above mentioned algorithms can be made. One is called depth-limited search (<span style='color:var(--mk-color-turquoise)'>DLS</span>) & the other is called iterative deepening search (<span style='color:var(--mk-color-turquoise)'>IDS</span>).

**Depth-limited search**
> To **set a depth limit** ($l$) during searching. And backtrack when the limit is hit (*More for DFS & UCS*)

**Time complexity** - O($b^{l}$)
**Space complexity** - O($bl$) for DFS or O($b^{l}$) for BFS
**Completeness** - <span style='color:var(--mk-color-red)'>No</span>, as long as the depth in which the goal resides exceeds the limit 
**Optimality** - <span style='color:var(--mk-color-red)'>No</span> if used with DFS & <span style='color:var(--mk-color-green)'>yes</span> if it is used with BFS

**Iterative deepening search**
> Which is just **DLS** but we <span style='color:var(--mk-color-yellow)'>iterate through all possible depth length</span> ($0 \to \infty$)

**Time complexity** - O($b^{d}$), <span style='color:var(--mk-color-red)'>Overhead</span>: $d \times b^{0} + (d-1) \times b^{1} + \dots + b^{d-1}$
**Space complexity** - O($bd$) for DFS or O($b^{d}$) for BFS
**Completeness** - <span style='color:var(--mk-color-green)'>Yes</span> as long as the goal is in the graph
**Optimality** - <span style='color:var(--mk-color-green)'>Yes</span> if the cost is the same throughout
## Informed Search Algorithms

Unlike uninformed search algorithms, the agent has <span style='color:var(--mk-color-green)'>some estimate on how close it is to the goal</span> (*Current state*) to its goal when traversing the graph.

In addition to the algorithm, there is a **function** which <span style='color:var(--mk-color-teal)'>estimates how good a state is</span> given the current goal state.
### Types of Informed Search Algorithms

### Best-First Search

Instead of a <span style='color:var(--mk-color-purple)'>priority queue</span> which orders based on the cost, it takes the <span style='color:var(--mk-color-yellow)'>cost</span> of the state and feed it into the <span style='color:var(--mk-color-yellow)'>evaluation function</span> and the result will determine the ordering.

This is just a **skeleton search** which should be incorporated into other searches.
#### Greedy Best-First Search

The evaluation function, uses a <span style='color:var(--mk-color-teal)'>heuristic</span> which <span style='color:var(--mk-color-yellow)'>estimates the cost of n to the goal</span>.

A <span style='color:var(--mk-color-teal)'>heruistic</span> is some criteria used to **calculate the estimate of a current state to its goal**. 

One problem with this is that it <span style='color:var(--mk-color-red)'>might not terminate</span> as it is possible for our heuristic to generate a loop.

**Time complexity** - O($b^{m}$), but a good heuristic can improve the time
**Space complexity** - O($b^{m}$)
**Completeness** - <span style='color:var(--mk-color-red)'>No</span>
**Optimality** - <span style='color:var(--mk-color-red)'>No</span>
### A* Search

This algorithm helps <span style='color:var(--mk-color-green)'>solves</span> the problem mentioned in the greedy best-first search. By **adding in the true cost** to get to a state with the heuristic function in the <span style='color:var(--mk-color-teal)'>evaluation function</span>.

**Time complexity** - O($b^{m}$), but a good heuristic can improve the time
**Space complexity** - O($b^{m}$)
**Completeness** - <span style='color:var(--mk-color-green)'>Yes</span> as the value from the evaluation function **keeps growing** thus it will terminate
**Optimality** - <span style='color:var(--mk-color-orange)'>Depends</span> on the heuristics used (*Good if the heuristics is consistent*)
# Heuristic
---
When deciding on a heuristic ($h(n)$), it <span style='color:var(--mk-color-orange)'>must follow the following properties</span>:
1) **Admissible**
2) **Consistent**

When **designing heuristics**, try and <span style='color:var(--mk-color-yellow)'>relax the problem</span> (*Less restrictions*).

**Admissible**
For it to be <span style='color:var(--mk-color-turquoise)'>admissible</span>, for every node $n$, $h(n) \le h^{*}(n)$, where $h^{*}(n)$ is defined as the **true cost** to reach the goal from state $n$.

In words, it means that the <span style='color:var(--mk-color-teal)'>heuristic</span> should <span style='color:var(--mk-color-red)'>never over estimates the cost</span> to reach the goal (*Conservative estimates*). One way to achieve this is by <span style='color:var(--mk-color-yellow)'>relaxing the problem</span> (*Fewer restrictions*).

If it is <span style='color:var(--mk-color-turquoise)'>admissible</span> then **tree search is optimal**.

**Consistent**
For it to be <span style='color:var(--mk-color-turquoise)'>consistent</span>, for every action $h(n) \le c(n,a,n') + h(n')$ and $h(G) = 0$. Where $G$ is the goal, $n'$ is some node before the goal and $a$ is some action.

In other words, if there is a direct path to the goal, <span style='color:var(--mk-color-yellow)'>any other path that deviates should be greater than or equals</span> to the heuristic cost of the direct path.

If this is the case then $f(n) = g(n) + h(n)$ is a **non-decreasing function** along any path.

If it is <span style='color:var(--mk-color-turquoise)'>admissible</span> then **graph search is optimal**. And it is <span style='color:var(--mk-color-yellow)'>also admissible</span>.
## Dominance

Given 2 heuristics, $h_{1}$ and $h_{2}$ if $h_{2}(n) \ge h_{1}(n)$ for all $n$ , then $h_{2}$ <span style='color:var(--mk-color-turquoise)'>dominates</span> $h_{1}$, as long as **both are admissible**.

This is because, heuristics never over-estimate thus if an <b><mark style='background:var(--mk-color-yellow)'>estimate is bigger, means it is closer to the true cost</mark></b>.

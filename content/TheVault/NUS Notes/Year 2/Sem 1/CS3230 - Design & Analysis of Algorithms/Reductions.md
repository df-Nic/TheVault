---
title: Reductions
Date Created: 2024-10-21
Last Updated: 2025-09-28
tags:
  - CS3230
  - AlgorithmDesign
  - NPProblems
---
# Problem Reductions
---
<span style='color:var(--mk-color-turquoise)'>Reductions</span>, is essentially the **reusing of some existing algorithm** that works <span style='color:var(--mk-color-yellow)'>on some other problem</span> by tweaking the input.

The **idea behind reductions**, is that we can<span style='color:var(--mk-color-yellow)'> link the "hardness" of 1 problem to another</span>:
>Supposed that problem B is $O(n^{2})$ then if we can use problem B to solve problem A then A is in $O(n^{2})$ as well

Usually the above statement will mean that <span style='color:var(--mk-color-yellow)'>problem A reduces to problem B</span>.

> [!question] How Can we Interprit the Statement?
> - Let $\alpha$ be the input for problem A and $A(\alpha) = x$
> - Convert $\alpha$ to $\beta$ an input to problem B and $B(\beta) = y$
> - We can convert y to x or y = x, then we can take <span style='color:var(--mk-color-yellow)'>y to be the solution to the problem A</span>.

> [!example] Example of Problem Reduction
> Lets say we have 2 functions `Sum(0)` which find **2 numbers that add to 0** and `Sum(T)` which finds **2 numbers that adds to** $T$.
> 
> Can we reduce `Sum(T)` to `Sum(0)`?
> 
> What we can do is to just <span style='color:var(--mk-color-yellow)'>take every element in the array and deduct</span> by $T/2$, then this will be our input array for `Sum(0)`. And the result will be for `Sum(T)`.
## Polynomial-Time Reduction

When we say $p(n)$ **time reduction**, it means that the <span style='color:var(--mk-color-yellow)'>conversion of the input is at most</span> $p(n)$ (*Linear*).

Then the **running time composition** is the sum of the time complexity plus conversion which is, $O(T(p(n)) + O(p(n)))$.

Now for a <span style='color:var(--mk-color-turquoise)'>polynomial-time reduction</span> from A to B, it means that the conversion can be done in $O(n^{c})$ where $c$ is some constant. We also denote this as $A \le_{p} B$.
<div style="page-break-after: always;"></div>

> [!note] What can we Infer $A \le_{p} B$
> Suppose that $A \le_{p} B$ is <span style='color:var(--mk-color-green)'>true</span>.
> 
> If **B has a polynomial run time** ($T(n) \in O(n^{c}$), then <span style='color:var(--mk-color-yellow)'>A also has a polynomial run time</span> ($O(T(p(n)) + O(p(n))) \in O(n^{c}$)
> 
> The **inverse is also true**
> 
> If **A cannot be solved in polynomial time**, then <span style='color:var(--mk-color-yellow)'>B also cannot be solved in polynomial time</span>.

**Why polynomial?:**
1) It is **closed under compositions**, if $T(n)$ and $p(n)$ are polynomial then $T(p(n))$ is also polynomial.
2) <span style='color:var(--mk-color-red)'>Not good</span> to <span style='color:var(--mk-color-yellow)'>define what is efficient with a distinct value</span>, if $O(n^{2})$ is efficient then $O(n^{2.0000001})$ is not?
3) It is <span style='color:var(--mk-color-green)'>robust</span>, if 2 people analyse correctly but 1 is $O(n^{2})$ the other is $O(n^{3})$ (*Bits vs integers*) but both are in polynomial time.

One downside is that $O(n^{1000})$ is <span style='color:var(--mk-color-red)'>inefficient</span> but our **assumption** (*Polynomial time is efficient*) says it will be <span style='color:var(--mk-color-green)'>efficient</span>.
## Measuring Input Size

> [!faq] Why does it Matter?
> Lets look at `fib` the iterative version. If we take $n$ to be an integer then it is $O(n)$.
> 
> But if we take the **input as bits** means the input is $l = \lceil \log 2 \rceil$. Thus the run time now will be $O(2^{l})$ which is <span style='color:var(--mk-color-red)'>not polynomial</span>.

This for now, **all inputs** will be in the length of the encoding in terms of the <b><mark style='background:var(--mk-color-yellow)'>number of bits</mark></b>. And the good this is that **how we encode** <span style='color:var(--mk-color-green)'>will not affect</span> the notion of polynomial-time algorithms.

But if we look at the **input as a numerical value** instead of in bits and prove that it is polynomial time, then this is known as <span style='color:var(--mk-color-turquoise)'>pseudo-polynomial time</span>.
# Computational Complexity Theory
---
It is a research field <span style='color:var(--mk-color-yellow)'>studying sets of computational problems</span> and not individual computational problems.

**Example:**
- $P = PSPACE$ - Is it true that any problem solvable in polynomial space can be solved in polynomial time.
- $P = BPP$ - Is it true that any problem solvable in randomized polynomial time can be solved in deterministic polynomial time.
## Framework

Here we only focus on <span style='color:var(--mk-color-turquoise)'>decision problem</span>, which is given some **instance space** $I$ (*valid inputs*) output only `True` or `False`.

We can **convert** any <span style='color:var(--mk-color-yellow)'>optimization problem into a decision problem</span>. And thus a <span style='color:var(--mk-color-green)'>decision problem should be no harder than a optimisation problem</span>.

> [!example] 
> In our SSSP problem (*Optimization problem*) we are task to find the shortest path from $u$ to $v$.
> 
> A decision problem will be to check if there is a path from $u$ to $v$ which is $\le k$ (*The direction depends on the problem*).
> 
> So all we need to do is to <span style='color:var(--mk-color-yellow)'>run the optimization algorithm and use its result</span> to see if it is $\le k$.

We can also <span style='color:var(--mk-color-yellow)'>do it the other way round</span> by using <span style='color:var(--mk-color-teal)'>binary search</span> and finding the minimum value. Basically treat the **decision problem as a Blackbox function** and based on the result, move left or right.

Thus a **optimisation problem reduces to a decision problem**, then if the decision problem is in polynomial time <b><mark style='background:var(--mk-color-yellow)'>if and only if</mark></b> the optimisation problem can be solved in polynomial time.
## Karp Reduction

This **special case** only implies to <b><mark style='background:var(--mk-color-yellow)'>2 decision problems</mark></b>:
- The transformation from $\alpha$ to $\beta$ is in polynomial time of size $\alpha$
- Then $A(\alpha) = Yes$ **if and only if** $B(\beta) = Yes$

Thus unlike normal reductions, the output is a <span style='color:var(--mk-color-yellow)'>1 to 1 mapping</span> and there is <span style='color:var(--mk-color-red)'>no transformation back</span>.

**Example:**
For this example we will use the **vertex cover problem** and the **independent set** problem.

**Vertex cover** - A **minimum** set of vertices in which for <span style='color:var(--mk-color-yellow)'>all edges one of its end points is in the set</span>
**Independent set** - A **maximum** set of vertices in which <span style='color:var(--mk-color-yellow)'>no 2 vertices in the set are neighbours</span>

**Claim**
>Then $X \subseteq V$ is a vertex cover **if and only if** $V \setminus X$  is an independent set

For any $\{u,v\} \in E$ then there must be 1 vertices in $X$, if <span style='color:var(--mk-color-red)'>not then the edge is not covered</span> and it will not be an independent set.

And if the same 2 vertices $u$ and $v$ are not in $X$, then they are in $V \setminus X$ which is <span style='color:var(--mk-color-red)'>impossible</span> since $V \setminus X$ **is already a independent set**.

**Therefore:**

![[Karp Redution Example.png|center|500]]
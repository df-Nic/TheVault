---
title: NP-Completeness
Date Created: 2024-10-27
Last Updated: 2025-09-28
tags:
  - CS3230
  - AlgorithmDesign
  - NPProblems
---
# What is NP
---
It stands for <span style='color:var(--mk-color-turquoise)'>nondeterministic polynomial</span>. Which means that given a <span style='color:var(--mk-color-turquoise)'>certificate</span> (*just some proposed solution*) we can <span style='color:var(--mk-color-yellow)'>verify it in polynomial time</span> (*[[Reductions#Karp Reduction|Karp reduction]], yes solution means a yes to the other problem*).

But if you were to **search for a solution** it can be <span style='color:var(--mk-color-red)'>very long</span>. 

Formally, if given a problem $F$ and an input $I$ and a <span style='color:var(--mk-color-turquoise)'>certificate</span> $S$, then if $F(I,S)$ is a yes instance **if and only if** there exist a $S$ that when verified using some algorithm $A$, it outputs yes as well.

$A$ <span style='color:var(--mk-color-yellow)'>must run in polynomial time</span> and $\vert S \vert \le p(\vert I \vert) - p$, this means the certificate must be short.

> [!example] Hamiltonian-Cycle (HC)
> Why is HC in NP?
> 
> Firstly if there is a solution we can **solve it in polynomial time** more specfically $O(\vert V \vert)$ time. Since we just need to loop though the proposed solution, <span style='color:var(--mk-color-yellow)'>check if it is a cycle</span> and <span style='color:var(--mk-color-yellow)'>vists each vertex at most once</span>.
> 
> In addition the solution size in respect to the input is also polynomial since, for any path we can only have $V$ number of vertices if it is a correct solution.

$NP$ differs from $P$ as $P$ means <b><mark style='background:var(--mk-color-turquoise)'>polynomial time algorithm</mark></b>. Thus is $P \in NP$? Well <span style='color:var(--mk-color-green)'>yes</span>. If **a problem has a polynomial time algorithm** (*solver*), then given a certificate, we can just <span style='color:var(--mk-color-yellow)'>ignore it and run the actual algorithm</span> to get the yes or no decision.
## NP-Hard & NP-Complete

![[NP-Hard & NP-Complete.png|center|300]]

Given a problem $X$ if <span style='color:var(--mk-color-yellow)'>every problem</span> in $NP$ than can be reduced to X ($A \le_{p} X$), then $X$ is considered to be in **NP-Hard**. Additionally, if $X$ is <span style='color:var(--mk-color-yellow)'>proven to be in</span> $NP$ means that $X$ is **NP-complete** (*there is a polynomial verifier*).
<div style="page-break-after: always;"></div>

> [!example] C-SAT In NP-Complete
> What is <span style='color:var(--mk-color-turquoise)'>circuit-satisfiabiity</span> (*C-SAT*), we can **represent a curcuit as a DAG or binary tree** where all its <span style='color:var(--mk-color-yellow)'>vertices are logic gates</span> and the <span style='color:var(--mk-color-yellow)'>inputs are the leaves</span> and the output is at the head.
> 
> Given any problem $A \in NP$, then there is a polynomial verifier $Q$, and since the <span style='color:var(--mk-color-yellow)'>verifier outputs only yes and no</span>. Then it can be transformed into the corrposponding binary tree or DAG with binary inputs of 1 and 0.
> 
> And then run C-SAT to get the output.
### CNF-SAT & 3-SAT

Here are some <span style='color:var(--mk-color-orange)'>terms</span> we need to define before elaborating on this:
**Literal**
>Boolean variable or its negation ($x_{i}$ or $\bar{x_{i}}$)

**Clause**
>A disjunction (*OR*) if literals ($C_{j} = x_{1} \lor \bar{x_{2}} \lor x_{3} \lor x_{4}$)

**Conjunctive Normal Form** (*CNF*)
>A formula $\upphi$ that is a conjunction (*AND*) of clauses ($\upphi = C_{1} \land C_{2} \land C_{3}$)

For <span style='color:var(--mk-color-turquoise)'>CNF-SAT</span>, it is to find if a formula $\upphi$ <span style='color:var(--mk-color-orange)'>does it have a satisfying truth assignment</span> (*Output true*).

And as for <span style='color:var(--mk-color-turquoise)'>3-SAT</span>, it is CNF-SAT but the <span style='color:var(--mk-color-yellow)'>clause only can have exactly 3 literals</span>. Thus CNF-SAT can be reduce into 3-SAT.

Example: $\upphi = (\bar{x_{1}} \lor x_{2} \lor x_{3}) \land (x_{1} \lor \bar{x_{2}} \lor x_{3}) \land (\bar{x_{1}} \lor x_{2} \lor x_{4})$

## Proving a Problem is in NP-Complete

There are <span style='color:var(--mk-color-orange)'>2 steps</span> to follow:
1) Given a problem $X$ show that $X \in NP$. Essentially <span style='color:var(--mk-color-yellow)'>show that there is a polynomial verifier of a solution</span>
2) Pick a problem $A$ that is **already in NP-complete** then show that $A \le_{p} X$ 

**List of NP-Complete problems**
![[List of NP-Complete Problems.png|center]]

> [!example] Proving Hitting-Set is in NP-Complete
> **What is a hitting set**?
> >Given a set of sets, find the <span style='color:var(--mk-color-yellow)'>smallest non empty set</span> where it will **intersect all the other sets**
> 
> **Polynomal verification:**
> Just check if **1 element in all the sets are in the proposed hitting set**.
> 
> **Vertex cover reduced to hitting set:**
> 
> The polynomial conversion is just to <span style='color:var(--mk-color-yellow)'>let all vertices be the unnique elements</span> in all the set and the <span style='color:var(--mk-color-yellow)'>edges be the connection between the different sets</span>. For example if we have {1,2} {1,3}, then 1 will have an edge to 2 and 3.
> 
> Then the <span style='color:var(--mk-color-yellow)'>solution to the vertex cover is a 1 to 1 solution to hitting set</span> and vice versa (*Remember must show 2 ways since is if and only if*).

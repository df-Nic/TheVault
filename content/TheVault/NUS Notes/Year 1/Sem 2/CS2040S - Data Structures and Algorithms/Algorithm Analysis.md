---
title: Algorithm Analysis
Date Created: 2024-01-23
Last Updated: 2025-10-20
tags:
  - CS2040S
  - AlgorithmAnalysis/TimeComplexity
---

# Big-O Notation
---
<span style='color:#0fb9b1'>Big O</span>, is a good way to approximate how fast an algorithm can execute as $n$ (input) increases.

A formal definition is that given a function $T(n)$ which is equals to $O(f(n))$ then <b><span style='color: var(--mk-color-yellow)'> T grows no faster than f</span></b>. This is because <span style='color:#0fb9b1'>Big O</span>, <span style='color:#f7b731'>serves as a upper bound for run time</span>.

Mathematically $T(n) = O(f(n))$ if :
- There exist a constant $c \gt 0$
- There exist a constant $n_{0} \ge 0$
Such that $\forall n \gt n_{0} : T(n) \le cf(n)$. This is saying at some point $n_0$ (Input size) <span style='color:#f7b731'>everything above will be upper bounded</span> by some $cf(n)$. 

But usually the preferred **bound must be the tightest** and only the <span style='color:#f7b731'>highest power</span> is the most significant one.

![[Time Complexity Table for Big O.png|center]]
<span style='color:#fa8231'>Also</span> $O(\log(n!)) = O(n \log n)$

Note that <span style='color:#f7b731'>every function will have a time complexity</span>, **even if the function is incorrect**.
<div style="break-after: page;"></div>

## Lower Bound

The <span style='color:#f7b731'>opposite</span> of <span style='color:#0fb9b1'>Big-O</span>, where it proves some function is slower than some other function. This is denoted by omega ($\Omega$).

Mathematically $T(n) = \Omega(f(n))$ if :
- There exist a constant $c \gt 0$
- There exist a constant $n_{0} \ge 0$
Such that $\forall n \gt n_{0} : T(n) \ge cf(n)$. This is saying at some point $n_0$ (Input size) <span style='color:#f7b731'>everything above will be lower bounded</span> by some $cf(n)$. 

However this is <span style='color:#eb3b5a'>not that interesting</span>.
## Same Rate

For <span style='color:#fa8231'>2 functions to be of same rate</span>, it is denoted as theta $\Theta$ and for something to be theta, it <b><span style='color: var(--mk-color-yellow)'>has to be the tightest bound</span></b> for both $O(f(x))$ and $\Omega(f(x))$.

Mathematically $T(n) = \Theta(f(n))$ if :
- There exist a constant $T(n) = \Omega(f(n))$
- There exist a constant $T(n) = O(f(n))$

Such that $\forall n \gt n_{0} : T(n) \le c_{1}f(n) \land T(n) \ge c_{2}f(n)$. This is saying at some point $n_0$ (Input size) <span style='color:#f7b731'>everything will be in between some function</span> multiplied by $c_{1}$ and $c_{2}$. 

## Rules of Analysis

In this module, it <span style='color:#f7b731'>focuses on sequential code</span>, no parallel code analysis.

Most operations (*functions in the java library*) are **O(1)** with some exceptions like string concatenation which is $O(n^2)$.

<span style='color:#fa8231'>For loops and nested loops</span>, the cost is equals to $\text{num of iterations } \times \text{ max cost of one iteration}$.

<span style='color:#fa8231'>For sequential statements</span>, the cost is equals to $\text{cost of first } \times \text{ cost of second}$.

<span style='color:#fa8231'>For if / else statements</span>, the cost is equals to $\text{max(cost of first, cost of second)} \rightarrow \text{cost of second } + \text{ cost of first}$.

<span style='color:#fa8231'>For recursion</span>, the cost is equals to $\text{num of recursive calls } \times \text{ max cost of one recursion}$.

<span style='color:#fa8231'>For multiple unknowns</span>, $n^{2} + mlog_{n} + 17$, take both constants as m can be bigger or smaller than n, thus $O(n^{2} + mlog_{n})$.
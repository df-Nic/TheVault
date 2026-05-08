---
title: Asymptotic Analysis
Date Created: 2024-08-13
Last Updated: 2025-09-28
tags:
  - CS3230
  - TimeComplexity
---
# Algorithms
---
When **talking about algorithms**, it is assumed that all inputs are <span style='color:var(--mk-color-yellow)'>valid</span> (*Unambiguous*), <span style='color:var(--mk-color-yellow)'>deterministic</span> (*Most of the time*) and it will <span style='color:var(--mk-color-yellow)'>terminate</span> after finite number of instructions (*Halting problem*).

**Properties of good algorithms** in order of <span style='color:var(--mk-color-orange)'>importance</span> :
1) Correct
2) Efficient - In terms of <span style='color:var(--mk-color-teal)'>time</span> and <span style='color:var(--mk-color-teal)'>space</span>
3) Generality - Applicable to a wide range of inputs
4) Usability
5) Simplicity
6) Well documented

When not dealing with **big data**, it is <span style='color:var(--mk-color-green)'>better to sacrifice space for time</span>.

**Algorithmic paradigms** :
- Complete Search (*for example, using brute force, backtracking, branch and bound*)
- Divide and Conquer (D&C)
- Dynamic Programming (DP)
- Greedy Algorithm
- Deterministic versus non-deterministic strategies
- Iterative Improvement
# Analysis of an Algorithm
---
## RAM

One model of computation is through **counting the number of instructions** (*How RAM works*). It calculates the time by **counting the number of checks plus arithmetic operations and return statement**.

> [!tldr]+ Proving Recursive Fib Time Complexity of O(2<sup>n</sup>)
> We know that `Fib(n) = Fib(n-1) + Fib(n-2)`.
> 
> This can be interpreted as `Fib(n) >= 2 * Fib(n-2)`.
> This tells us that when n increases by 2 (*i.e., n = 1, 3, 5, ..., or n = 0, 2, 4, 6, ...*), the <span style='color:var(--mk-color-orange)'>values doubles</span>.
> 
> Between 1 to n, there will be $\lceil \frac{n-2}{2} \rceil$ doublings. Thus $Fib(n) \ge 2^{\frac{n-2}{2}}$

## Big O Notation

This analysis method, does not worry about the number of instructions but rather the running time based on the <b><mark style='background:var(--mk-color-yellow)'>size of the input</mark></b>.

There are <span style='color:var(--mk-color-orange)'>3 types</span> of big O analysis:
1) **Worst case analysis**
2) **Average case analysis** (*Expected time taken over all inputs n and its probability distribution of all inputs*)
3) **Best case analysis**
### Big O (Upper Bound)

The **definition** is, $f \in O(g)$ if there exist a constant $c \gt 0$ & $n_{0} \gt 0$ (*Some input size*) such that for all $n \ge n_{0}$ : $\color {#89CFF0} {0 \le f(n) \le c \times g(n)}$.

This interprets as <span style='color:var(--mk-color-yellow)'>g is an upper bound of f</span>. And note that O(g) is <b><mark style='background:var(--mk-color-red)'>not a function but rather a set of functions</mark></b>.
### Lower Bound

For lower bound the **symbol** used is $\Omega$. The definition is, $f \in \Omega(g)$ if there exist a constant $c \gt 0$ & $n_{0} \gt 0$ (*Some input size*) such that for all $n \ge n_{0}$ : $\color {#89CFF0} {0 \le c \times g(n) \le f(n)}$.

The <span style='color:var(--mk-color-yellow)'>constant can be set as the reciprocal</span> of the constant in big O.
### Tight Bound

For tight bound the **symbol** used is $\Theta$. The definition is, $f \in \Theta(g)$ if there exist a constant $c_{1}, c_{2} \gt 0$ & $n_{0} \gt 0$ (*Some input size*) such that for all $n \ge n_{0}$ : $\color {#89CFF0} {0 \le c_{1} \times g(n) \le f(n) \le c_{2} \times g(n)}$.

For tight bound, $c_{1}$ <span style='color:var(--mk-color-orange)'>will be less than</span> $c_{2}$.

> [!example]+ Proving 10n<sup>2</sup> + n $\in \Theta$ (n<sup>2</sup>)
> First make $n$ to become $n^{2}$, which will give $11n^{2}$.
> 
> From here, $0 \le 5n^{2} \le (10n^{2} + n) \le 11n^{2}$.
> 
> Where, $c_{1} = 5$, $c_{2} = 11$ and $n_{0} = 2$. For $n_{0}$ it can be **any value below 10**.

The **relationship** between tight bound with upper and lower bound is that, $\color {orange} {\Theta(g) = O(g) \cap \Omega(g)}$.
### Little o (Strict Upper Bound)

The **definition** is, $f \in o(g)$, <b><mark style='background:var(--mk-color-yellow)'>for any constant</mark></b> $c \gt 0$ & $n_{0} \gt 0$ (*Some input size*) such that for all $n \ge n_{0}$ : $\color {#89CFF0} {0 \le f(n) \lt c \times g(n)}$.
### Strict Lower Bound

The **definition** is, $f \in \omega(g)$, <b><mark style='background:var(--mk-color-yellow)'>for any constant</mark></b> $c \gt 0$ & $n_{0} \gt 0$ (*Some input size*) such that for all $n \ge n_{0}$ : $\color {#89CFF0} {0 \le c \times g(n) \lt f(n)}$.
## Using Limits

Using **limits to infinity** can also help analyse functions :
- $\lim_{n \to \infty} \frac{f(n)}{g(n)} = 0 \Rightarrow f(n) \in o(g(n))$
- $\lim_{n \to \infty} \frac{f(n)}{g(n)} \lt \infty \Rightarrow f(n) \in O(g(n))$ 
- $0 \lt \lim_{n \to \infty} \frac{f(n)}{g(n)} \lt \infty \Rightarrow f(n) \in \Theta(g(n))$ 
- $\lim_{n \to \infty} \frac{f(n)}{g(n)} \gt 0 \Rightarrow f(n) \in \Omega(g(n))$ 
- $\lim_{n \to \infty} \frac{f(n)}{g(n)} = \infty \Rightarrow f(n) \in \omega(g(n))$ 

This is <span style='color:var(--mk-color-green)'>easier</span> to prove for $\Theta$, $\omega$, o.
## Properties for Asymptotic Notations

**Reflexivity**
> This only applies for O, $\Omega$ & $\Theta$, $f(n) \in O(f(n))$

**Transitivity**
> This is for all 5, $f(n) \in O(g(n))$ and $g(n) \in O(h(n))$ implies $f(n) \in O(h(n))$

**Symmetry**
> Only for $\Theta$, $f(n) \in \Theta(g(n)) \iff g(n) \in \Theta(f(n))$

**Complementary**
>This is only for the pairs O and $\Omega$, o and $\omega$
>$f(n) \in O(g(n)) \iff g(n) \in \Omega(f(n))$
>$f(n) \in o(g(n)) \iff g(n) \in \omega(f(n))$


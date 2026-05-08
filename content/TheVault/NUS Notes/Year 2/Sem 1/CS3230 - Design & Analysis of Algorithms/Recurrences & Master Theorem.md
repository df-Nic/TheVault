---
title: Recurrences & Master Theorem
Date Created: 2024-08-20
Last Updated: 2025-09-28
tags:
  - CS3230
  - TimeComplexity
---
# Solving Recurrences
---
In recurrences, when finding **upper or lower bound**, any <span style='color:var(--mk-color-yellow)'>big O notation in the recurrence equation can be replaced</span>.

For example, **merge sort** is: $T(n) = 2T\left(\frac{n}{2}\right)+ \Theta(n)$

Based on the <span style='color:var(--mk-color-orange)'>definition of theta</span> ($\Theta$), $\Theta(n)$ can be replace by $cn$.
## Telescoping Method

What is <span style='color:var(--mk-color-turquoise)'>telescoping</span>? Lets take a look at this example:
$$
\sum\limits^{n}_{k = 1} \left(\frac{1}{k} -\frac{1}{k + 1}\right) = \left(\frac{1}{1} - \frac{1}{2}\right) + \left(\frac{1}{2} - \frac{1}{3}\right) + \dots + \left(\frac{1}{n - 1} - \frac{1}{n}\right) + \left(\frac{1}{n} - \frac{1}{n + 1}\right)
$$
Here every <span style='color:var(--mk-color-yellow)'>2 terms after the first one will cancel each other out</span>, this will then leave with just $1 - \frac{1}{n + 1}$.

**Applying this method in a recursion function**
![[Telescoping Method Example.png|center|600]]

The key here is to **manipulate the recurrence equation** such that its subsequent terms can follow the same pattern.

And at the end **multiply everything** by $n$ to get back $T(n)$ and thus $\Theta(n log n)$.
<div style="page-break-after: always;"></div>

## Substitution Method

The main idea of substitution is to <span style='color:var(--mk-color-orange)'>guess a possible function</span> in which the recurrence will be **upper bounded** by. And prove it through induction.

![[Substitution Method Example.png|center|600]]

**Steps to carry out substitution method**
1) **Guess** a function that is **upper bounding** the recursive function
2) Create a induction hypothesis and <span style='color:var(--mk-color-orange)'>test for the base case</span> ($n = 1$)
3) Test for all $n \ge 2$, in the event of failure <span style='color:var(--mk-color-red)'>repeat step 1 by modifying the function</span>
4) If the proof is correct the function will be upper bounded by that function

To prove for $\Theta$, you need to do the same thing but for the **lower bound** instead.
## Recurrence Tree

A good thing about this method is that there is no guessing involved, it can be <span style='color:var(--mk-color-green)'>directly applied</span>.

![[Recursion Tree Example.png|center|600]]

The goal is to <span style='color:var(--mk-color-yellow)'>unravel the recurrence relation</span>, till it reaches the base cases or a pattern emerges.

**Main things to take note**
1) Know the **height** of the tree
2) How much **time is taken for each level** of the tree
3) The **time taken at the last level** with all the leaves

Then the time complexity for a recursive function $f(n)$ can just be summed up.
<div style="page-break-after: always;"></div>

## Master Theorem

This method can be used to solve any general recurrences in this <span style='color:var(--mk-color-orange)'>generic form</span>:
$$
T(n) = aT(n / b) + f(n)
$$

Recall from the [[#Recurrence Tree|recurrence tree]] method that when solving the time complexity for a recurrence function, we are <span style='color:var(--mk-color-orange)'>calculating</span>:
1) **Cost of splitting and combining**
2) **Cost of solving the base cases** (*Number of leaves*)

Here $f(n)$ is the <span style='color:var(--mk-color-yellow)'>cost of splitting and combining</span>. And the <span style='color:var(--mk-color-orange)'>number of leaves</span> in a tree is $n^{d}$. The *<span style='color:var(--mk-color-orange)'>height of the tree</span>* is $log_{b} n$.

$d$ can be calculated as such $log_{b} a$ and this is known as the <span style='color:var(--mk-color-turquoise)'>critical exponent</span>.

**Cases for Master Theorem**
![[The 3 Cases for Master Theorem.png|center|600]]

> [!important] Conditions for Each Case
> To determine which case to use, **compare these 2 values** $n^{d}$ where $d = log_{b} a$ and $f(n)$.
> 
> **Case 1** only applies if <span style='color:var(--mk-color-yellow)'>d is the dominant term</span>.
> 
> **Case 2** only applies if <span style='color:var(--mk-color-yellow)'>both are the same</span>. And $k$ depends on weather $f(n)$ has some polynominal log factor (*e.g. $nlogn \rightarrow k = 1$*)
> - If $k = -1$, $\Theta(n^{d}\log{\log{n}})$
> - If $k \le -2$, $\Theta(n^{d})$
> 
> **Case 3** only applies of the cost to <span style='color:var(--mk-color-yellow)'>spilt and combining is the dominan term</span> ($f(n)$).

What is the <span style='color:var(--mk-color-turquoise)'>regularity condition</span> for case 3. If the cost of splitting and merging is dominant, then the **cost at the root of the tree** (*Top most level*) <span style='color:var(--mk-color-red)'>should cost the most</span>. Since the other levels will handle $n / b$ inputs.

Thus this check ensures that each <span style='color:var(--mk-color-yellow)'>splitting and merging will be upper bounded</span> by $f(n)$ at the first level.

If the <span style='color:var(--mk-color-red)'>regularity condition fails</span> then do [[#Substitution Method|substitution]] or [[#Recurrence Tree|recursion tree]] method.
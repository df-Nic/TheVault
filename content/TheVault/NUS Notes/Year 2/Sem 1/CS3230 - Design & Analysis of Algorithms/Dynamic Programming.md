---
title: Dynamic Programming
Date Created: 2024-09-23
Last Updated: 2025-09-28
tags:
  - CS3230
  - AlgorithmDesign
  - DP
---
# Idea of Dynamic Programming
----
Dynamic programming is the process of <span style='color:var(--mk-color-yellow)'>breaking down problems into subproblems</span> and then solving these sub problems to **get the solution to the original problem**.

> [!question]  Is this Not Just Divide & Conqure?
> Yes both does spilt problems into sub problems, but for dynamic programming, these <span style='color:var(--mk-color-yellow)'>sub problems can overlap</span>.
> 
> Therefore dynamic programming only **computes the solution to the subproblem** <span style='color:var(--mk-color-green)'>at most one time</span>. Which can make it more efficient.
# Memoization
---
Lets look a the **recursive** solution to Fibonacci.

```python
def fib(n): # O(n^2) Time
	if n <= 1:
		return n
	else:
		return fib(n - 1) + fib(n - 2)
```

From there we can see that we are <span style='color:var(--mk-color-red)'>recomputing a lot of steps</span>, if $n = 10$, we are computing `fib(8)` 2 times!

Thus the <span style='color:var(--mk-color-orange)'>idea of memoization</span> is to simply <span style='color:var(--mk-color-yellow)'>remember which computations are done</span> and just pull our the values which we have already computed.
>A simple way is to use a list of size $n$ and just store `fn(i)` into index `i` in the array.

This **ensures** we only <span style='color:var(--mk-color-green)'>compute something at most once</span>.
# Approaches to Dynamic Programming
---
## Bottom-up

![[DP Bottom-up Approach.png|center|500]]

For a **bottom-up approach** we are <span style='color:var(--mk-color-yellow)'>starting from the base case and then building upwards</span>.

We will usually use a table (*2D Array*) to solve the solution.
<div style="page-break-after: always;"></div>

## Top-down

![[DP Top-down Approach.png|center|500]]

For a **top-down approach** we will <span style='color:var(--mk-color-yellow)'>start from the top</span> and then we will continue <span style='color:var(--mk-color-yellow)'>downwards until the base case is reached</span>. Then we will use what was computed to solve the original problem.

Usually we will use [[#Memoization|memoization]] and <span style='color:var(--mk-color-yellow)'>recursion</span> when doing a top-down approach.

**Example:**
![[Bottom-up Approach Using a Table.png|center|550]]
# Cut & Paste
---
This is a **proof technique** that can be used.

**Example using LCM:**
![[Cut & Paste Example with LCM.png|center|550]]

Essentially, the answer to the $n - 1$ term will be smaller than or equal to the solution to the subproblem. Then by adding the last $n$ term, the solution will be equivalent by taking `fn(n - 1) + 1`.


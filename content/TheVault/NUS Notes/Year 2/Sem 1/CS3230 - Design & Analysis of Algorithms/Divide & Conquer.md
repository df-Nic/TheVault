---
title: Divide & Conquer
Date Created: 2024-09-01
Last Updated: 2025-09-28
tags:
  - CS3230
  - Algorithms
  - AlgorithmDesign
---
# Idea of Divide & Conquer
---
There are <span style='color:var(--mk-color-orange)'>3 main steps</span> to think of when designing a <span style='color:var(--mk-color-turquoise)'>divide & conquer algorithm</span>.
1) **Divide** the problem into smaller subproblems
2) **Solve** the subproblems **recursively**
3) **Combine** the results of the subproblems to <span style='color:var(--mk-color-green)'>get the solution of the full problem</span>.

A classical algorithm that uses this technique is [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Sorting#Merge Sort|merge sort]].

Then to <span style='color:var(--mk-color-orange)'>compute the time complexity</span> of a divide and conquer algorithm, it will be in this format:
$$
T(n) = aT\frac{n}{b}+ f(n)
$$
**Where:**
- $f(n)$ is a function for **merging and splitting**

Which is the **general formula of a recurrence algorithm** which can be solved using [[Recurrences & Master Theorem#Master Theorem|master theorem]].
# Exponentiation
---
We can also <span style='color:var(--mk-color-yellow)'>use matrixes</span> to compute the nth term of a problem. Lets look into an <span style='color:var(--mk-color-orange)'>example using Fibonacci</span>.
$$
\left(\begin{matrix}
F_{n+1} & F_{n} \\
F_{n} & F_{n-1} \\
\end{matrix}\right)
=
\left(\begin{matrix}
F_{n} + F_{n-1} & F_{n} \\
F_{n-1} + F_{n-2} & F_{n-1} \\
\end{matrix}\right)
=
\left(\begin{matrix}
F_{n} & F_{n-1} \\
F_{n-1} & F_{n-2} \\
\end{matrix}\right)
\left(\begin{matrix}
1 & 1 \\
1 & 0 \\
\end{matrix}\right)^{n}
$$
Essentially if we can use <span style='color:var(--mk-color-yellow)'>matrix multiplication and exponentiation</span> to form our divide and conquer then:
$$
\left(\begin{matrix}
F_{n+1} & F_{n} \\
F_{n} & F_{n-1} \\
\end{matrix}\right)
=
\left(\begin{matrix}
1 & 1 \\
1 & 0 \\
\end{matrix}\right)^{n}
$$
Which can be computed in $O(\log{n})$ time.
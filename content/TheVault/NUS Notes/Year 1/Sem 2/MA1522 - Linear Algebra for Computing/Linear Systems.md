---
title: Linear Systems
Date Created: 2024-01-23
Last Updated: 2025-09-27
tags:
  - MA1522
  - Math
---

# Cartesian Coordinates
---
A <span style='color:#0fb9b1'>point</span> on a xy-plane can be <span style='color:#f7b731'>represent by a pair of numbers</span> $(x_{0}, y_{0})$.

A <span style='color:#0fb9b1'>plane</span> is similar but is is on the xyz-plane instead and it is in the form of $ax + by + cz = d$

A <span style='color:#0fb9b1'>straight line</span> is a <span style='color:#f7b731'>collection</span> of <span style='color:#0fb9b1'>points</span> which <span style='color:#f7b731'>satisfy the linear equation</span> in the form of $ax + by = c$.
# Linear Equations
---
A <span style='color:#f7b731'>linear equation with </span>$n$ <span style='color:#f7b731'>variables / unknowns</span> is in the form of $a_{1}x_{1} + a_{2}x_{2} + \dots + a_{n}x_{n} = b$. Which has <span style='color:#fa8231'>3 types</span> :
1) **Inconsistent**
>$a_{1} = \dots = a_{n} = 0$ however $b \neq 0$, it is inconsistent as LHS $\neq$ RHS and thus <span style='color:#eb3b5a'>there are no solutions</span> (Empty set).
2) **Zero equation**
>$a_{1} = \dots = a_{n} = b = 0$, this means <span style='color:#f7b731'>all values</span> of $x$ are <span style='color:#f7b731'>solutions</span> as there are <span style='color:#f7b731'>no restrictions</span>.
3) **Nonzero equation**
>Anything that is not a zero equation is a nonzero equation
## Solving Linear Equations

A <span style='color:#0fb9b1'>solution</span> for a given linear equation is in the form of $x_{1} = s_{1} \dots x_{n} = s_{n}$. Where <span style='color:#f7b731'>every value</span> of $x_{n}$ <span style='color:#f7b731'>satisfy the equation  </span> and $s$ is some arbitrary value.

Once <span style='color:#f7b731'>all possible solutions</span> are found, then a <span style='color:#0fb9b1'>solution set</span> can be formed. These collection of points which are <mark style='background:#f7b731'>not all zeros</mark> represents the equation.

Before a <span style='color:#0fb9b1'>solution set</span> can be obtained, a <span style='color:#0fb9b1'>general solution</span> can be made. It <span style='color:#f7b731'>provides a general expression</span> for the entire solution of the equation.

**Example :**

A trick to solve a linear equation is to make the <mark style='background:#0fb9b1'>degree of freedom</mark> (DF) which is the <span style='color:#f7b731'>number of unknown variables to 1</span>.

Given this equation $x_{1} - 4x_{2} + 7x_{3} = 5$, there is a <span style='color:#f7b731'>DF of 3</span> thus just pick any 2 to be an <mark style='background:#f7b731'>arbitrary number</mark>. Note that if the <span style='color:#f7b731'>coefficient is 0 for any</span> $x$ term, then that <mark style='background:#f7b731'>value must be chosen as the arbitrary number</mark>.

Lets take $x_2$ and $x_3$ to be chosen arbitrarily and assign them to $s$ and $t$ respectively, thus the <span style='color:#0fb9b1'>general solution</span> can be written as such : 
$$
  \text{General Solution} =
\begin{cases}
x_{1} = 5 + 4s - 7t \\
x_{2} = s \\
x_{3}= t
\end{cases}
$$
## Linear System

A <span style='color:#0fb9b1'>system</span>, is basically a <span style='color:#f7b731'>collection of linear equations</span> 
$$  \text{Linear System} =
\begin{cases}
a_{11}x_{1} + \dots + a_{1n}x_{n} = b_{1} \\
\vdots \\
a_{m1}x_{1} + \dots + a_{mn}x_{n} = b_{m}
\end{cases}$$
It is a <span style='color:#0fb9b1'>zero system</span>, if <mark style='background:#f7b731'>all coefficients are zero</mark>, else it is a nonzero system.

If a linear equation in a given system is <span style='color:#eb3b5a'>inconsistent</span>, then the <mark style='background:#eb3b5a'>whole system is inconsistent</mark>. However the <span style='color:#eb3b5a'>converse is not true</span>, take a look at this example where the equations are valid but <span style='color:#f7b731'>both cannot hold simultaneously</span>.
$$  
\begin{cases}
x + y = 2 \\
2x + y = 1
\end{cases}$$
If there is a set of values $x_{1} = s_{1} \dots x_{n} = s_{n}$ which <mark style='background:#f7b731'>satisfies all equations in the system</mark>, it is called a <span style='color:#0fb9b1'>solution</span>. If there are <span style='color:#eb3b5a'>no solutions</span>, then the system is <span style='color:#0fb9b1'>inconsistent</span>, else <span style='color:#0fb9b1'>consistent</span>.

**Scenarios** :
1) <span style='color:#eb3b5a'>No solution</span>, when the linear equations are <mark style='background:#f7b731'>distinct and parallel</mark>
2) <span style='color:#20bf6b'>One solution</span>, when the linear equations are <mark style='background:#f7b731'>not parallel</mark> (<mark style='background:#eb3b5a'>Does not apply to planes</mark>)
3) <span style='color:#8854d0'>Infinite solutions</span>, when the linear equations are <mark style='background:#f7b731'>parallel to itself</mark> or when <mark style='background:#f7b731'>2 planes intersect</mark>

### Augmented Matrix

It is <span style='color:#fa8231'>another way of displaying a linear system</span>, which looks like this : 
$$ \left(
\begin{array}{cccc|c}
  a_{11} & a_{12} & \dots & a_{1n} & b_{1} \\
  \vdots & \vdots & & \vdots & \vdots \\
  a_{m1} & a_{m2} & \dots & a_{mn} & b_{mn}
\end{array}
\right)$$
Where $a_{mn}$ represents the <span style='color:#f7b731'>coefficients</span> of each variable for that specific row and column.
# Elementary Row Operations
---
There are <span style='color:#fa8231'>3 types of elementary row operations</span>, these are used to <span style='color:#f7b731'>solve linear systems</span> :
1) <span style='color:#0fb9b1'>Scaler multiplication</span>, where an equation is <span style='color:#f7b731'>multiplied</span> by some <span style='color:#f7b731'>nonzero constant</span> ($cR_{i} \land c \neq 0$), **Type 1**
2) <span style='color:#0fb9b1'>Row swap</span>, where <span style='color:#f7b731'>2 equations are interchanged</span> with one another ($R_{i} \leftrightarrow R_{j}$),** Type 2**
3) <span style='color:#0fb9b1'>Row sum</span>, where a constant multiple of a <span style='color:#f7b731'>row is added to another row</span> ($R_{j} + cR_{i}$ or $R_{j} \mapsto R_{j} + cR_{i}$), **Type 3**

<span style='color:#0fb9b1'>Row equivalence</span>, is when <span style='color:#f7b731'>2 augmented matrices are the exact same</span> either from original or from a <span style='color:#f7b731'>series of elementary row operations</span>. <span style='color:#eb3b5a'>Multiplying a row by 0 does not work</span>.

If they are <span style='color:#0fb9b1'>row equivalent</span>, then they both have the <mark style='background:#f7b731'>same solution set</mark>. They are also an [[Relations#Definition of Equivalence Relation|equivalence relation]] (Reflexive, Symmetric and Transitive).
# Row-Echelon Form
---
A augmented matrix is said to be <span style='color:#0fb9b1'>simple</span> or in a <span style='color:#0fb9b1'>simplest form</span>, will be either in:
- <mark style='background:#0fb9b1'>Row-echelon Form</mark>
- <mark style='background:#0fb9b1'>Reduced row-echelon form</mark>

For a augmented matrix to be in <span style='color:#0fb9b1'>row-echelon form</span> (REF), it has to <span style='color:#fa8231'>satisfy the following properties</span> :
1) All the <span style='color:#0fb9b1'>zero rows</span> are <mark style='background:#f7b731'>grouped at the bottom</mark>
2) <span style='color:#f7b731'>Any 2 successive nonzero rows</span>, the <span style='color:#0fb9b1'>leading entry</span> (1st nonzero number) in the <mark style='background:#f7b731'>lower row appears to the right of the first leading entry in the first row</mark>
3) If the 2nd point follows, then <span style='color:#f7b731'>everything below the leading entry will be all zeros</span>.

The <span style='color:#fa8231'>leading entry of a nonzero row</span> is also called a <span style='color:#0fb9b1'>pivot point</span>. And a <span style='color:#fa8231'>column with a pivot point</span> is called a <span style='color:#0fb9b1'>pivot column</span>, else is a non-pivot column.

If <span style='color:#fa8231'>any column has a constant</span> $a, \dots$, then it <span style='color:#eb3b5a'>cannot be assumed that the matrix is in REF form</span>, since the <span style='color:#f7b731'>constant can be of any value</span>.

**Example :**
$$ \left(
\begin{array}{cccc|c}
  -1 & 2 & 5 & 2 & 4 \\
  0 & 1 & 2 & 7 & 2 \\
  0 & 0 & 8 & 4 & 16
\end{array}
\right)$$
## Reduced Row-Echelon Form

For an augmented matrix to be in <span style='color:#0fb9b1'>reduce row-echelon form</span> (RREF) it must meet these requirements :
- The matrix must be in <span style='color:#f7b731'>REF first</span>
- <span style='color:#f7b731'>Every pivot column</span> must be an entry with <mark style='background:#f7b731'>all zeros, except the pivot point</mark>
- <mark style='background:#f7b731'>Every pivot point must be 1</mark>

**Example :**
$$ \left(
\begin{array}{cccc|c}
  1 & 0 & 2 & 0 & 4 \\
  0 & 1 & 2 & 0 & 2 \\
  0 & 0 & 0 & 1 & 16 \\
\end{array}
\right)$$
<div style="page-break-after: always;"></div>

So to <span style='color:#fa8231'>solve this linear system</span> :
1) <span style='color:#f7b731'>Set</span> variables corresponding to <span style='color:#0fb9b1'>non-pivot columns</span> an <span style='color:#f7b731'>arbitrary parameter</span>
2) <span style='color:#f7b731'>Solve</span> remaining variables that are <span style='color:#0fb9b1'>pivot columns</span> by <mark style='background:#f7b731'>back substitution</mark> (From the last equation to the first)

A <span style='color:#fa8231'>system with everything 0</span> is <mark style='background:#f7b731'>always in REF and RREF</mark>.
## Gaussian Elimination

When if the augmented matrix is <span style='color:#fa8231'>not in a simple form</span>, then this is where the <span style='color:#0fb9b1'>gaussian elimination</span> comes in. Given a augmented matrix $A$, a <span style='color:#f7b731'>series of elementary row operations</span> can $A$ become $R$ (**Row echelon form** of $A$). Where if there is a pivot column, anything to the left should be 0
## Gauss-Jordan Elimination

This is to <span style='color:#fa8231'>create a reduced row-echelon form</span> which is to make an augmented matrix into its <span style='color:#f7b731'>simplest</span> form. The main difference its that you <span style='color:#f7b731'>start from the bottom</span>. Given a augmented matrix in <mark style='background:#f7b731'>reduced echelon form</mark> $A$, a <span style='color:#f7b731'>series of elementary row operations</span> can $A$ become $R$ (**Reduced row echelon form** of $A$). Where only the pivot value is 1, everything else is 0.
## Consistency

It is to <span style='color:#f7b731'>determine the total number of solutions</span> in a given linear system. Given a system $R$ in **REF** form;
1) When will there be **no solution** (**Inconsistent**)
>A system will have no solution when the <mark style='background:#f7b731'>last column is a pivot column and nonzero</mark> which makes it inconsistent. 
2) When will there be **one solution**
><mark style='background:#eb3b5a'>No arbitrary parameters </mark>used, <mark style='background:#f7b731'>all columns are pivot columns</mark>, meaning there is a pivot point <mark style='background:#f7b731'>except the last column</mark>.
3) When will there be **infinitely many solution**
> Some arbitrary parameters used, <mark style='background:#f7b731'>some columns are pivot columns</mark>, <mark style='background:#f7b731'>except the last column</mark>.

# Homogeneous Linear Systems
---
A <span style='color:#fa8231'>linear equation is said to be</span> <span style='color:#0fb9b1'>homogeneous</span> if its in the following form, $a_{1}x_{1} + \dots = 0$, thus is just an <span style='color:#f7b731'>equation which is equals to 0</span> when <span style='color:#f7b731'>all values of</span> $x_{n}$ <span style='color:#f7b731'>is 0</span>.

This is because, on the left hand side it is equals to 0 and the right hand side is also 0. and this equation <span style='color:#f7b731'>passes through the origin</span> (Both line and plane).

Therefore a <span style='color:#0fb9b1'>homogeneous</span> system is where <span style='color:#f7b731'>every equation is homogeneous</span> and thus <span style='color:#f7b731'>everything is 0 is a solution</span>, which is a <span style='color:#0fb9b1'>trivial solution </span>(**Not useful**) which is not interested in.


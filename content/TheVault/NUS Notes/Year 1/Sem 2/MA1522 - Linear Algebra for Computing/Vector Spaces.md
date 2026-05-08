---
title: Vector Spaces
Date Created: 2024-02-20
Last Updated: 2025-09-27
tags:
  - MA1522
  - Math
  - Vectors
---
# Euclidean $n$-Spaces
---
## $xy$-Plane

A point, $P$ in a $xy$-plane is represented as such $(a,b)$. There is a special point called the <span style='color:#0fb9b1'>origin</span> denoted as $O$, with the <span style='color:#fa8231'>following coordinate</span> $(0,0)$.

Now <span style='color:#fa8231'>draw a line from</span> $O$ to $P$ and the result $\overrightarrow{ OP }$, which is called <span style='color:#0fb9b1'>vector</span>. It <span style='color:#f7b731'>represents change from a initial point to an end point</span>, in the form of $v = [v_{1}, v_{2}]$

Given a vector $v = [1,2]$ just means that at <span style='color:#f7b731'>any starting point</span>, its ending point will be $x + 1$ and $y + 2$. 

**Parallel vectors**
> Given a <span style='color:#0fb9b1'>vector</span> $\overrightarrow{ PQ }$, if it is <span style='color:#f7b731'>parallel shifted</span> into $\overrightarrow{ P'Q' }$, then it is <span style='color:#fa8231'>parallel to one another</span>, meaning $(a_{2} - a_{1}, b_{2} - b_{1}) = (a'_{2} - a'_{1}, b'_{2} - b'_{1})$, which just means the <b><mark style='background:#f7b731'>gradian are the same </mark></b>.

A <b><mark style='background:#0fb9b1'>parallel shift</mark></b> is a movement of the vector anywhere as long as the <span style='color:#f7b731'>rate of change</span> of $x$ & $y$ <span style='color:#f7b731'>remains the same</span>

**Length of a vector**
> Now given a <span style='color:#0fb9b1'>vector</span> $V$, the length or <b><mark style='background:#0fb9b1'>magnitude</mark></b> can be calculated by using <span style='color:#3867d6'>pythagoras theorem</span>, which is denoted by, $\Vert{V}\Vert$.

$$\Vert{V}\Vert = \sqrt{(v_{1})^{2} + (v_{2})^{2}}$$
**Scalar Multiplication**
> Multiplying a vector by a scalar constant, <span style='color:#f7b731'>increases the length by a factor of the constant</span>, $cv = (cx, cy)$

1) If $c = 0$, then $cv = 0$, and this vector is called a <b><mark style='background:#0fb9b1'>zero vector</mark></b>, who's <span style='color:#f7b731'>start and end point is the origin</span>
2) If $c \gt 0$, then $cv$ will have the <span style='color:#f7b731'>same direction</span> as $v$
3) If $c \lt 0$, then $cv$ will have the <span style='color:#f7b731'>opposite direction</span> of $v$, in particular $(-1)v$ is called the <b><mark style='background:#f7b731'>negative</mark></b> of $v$.

**Addition and Subtraction**
>Let $a$ & $b$ be <span style='color:#fa8231'>some vector</span> on the $xy$-plane.
- **Addition** : $a + b = (a_{1} + b_{1}, a_{2} + b_{2})$
- **Subtraction** : $a - b = (a_{1} - b_{1}, a_{2} - b_{2})$ another way to do this is $a + -(b)$

The <span style='color:#fa8231'>pre-requisite</span> <span style='color:#0fb9b1'>addition</span> is that $b$ <b><mark style='background:#f7b731'>start point must be the same as the end point</mark></b> of $a$ by using <span style='color:#0fb9b1'>parallel shift</span>. The result, is a vector from the initial point of $b$ to the end point of $a$. 

Think of this as taking a path $a$, then path $b$, the resulting vector is just from the start point $a$ to the end point $b$.

The <span style='color:#fa8231'>pre-requisite</span> <span style='color:#0fb9b1'>subtraction</span> is that $b$ <b><mark style='background:#f7b731'>start point must be the same as</mark></b> $a$ by using <span style='color:#0fb9b1'>parallel shift</span>. The result, is a vector from the end point of $b$ to the end point of $a$.

Just think of this as $a$ + $b$, however, $b$ is now negative meaning the <span style='color:#f7b731'>direction swapped</span>!

A <span style='color:#0fb9b1'>parallel shift</span>, is the movement of the vector such that its <span style='color:#f7b731'>direction and magnitude does not change</span>.

**Geographic visualisation**
![[Vector Addition  & Subtraction Visualisation.png|center|400]]
## $xyz$-Plane

Similar to the $xy$-plane, but now there is a <span style='color:#fa8231'>need for an additional point</span> $z$, thus $P = (x,y,z)$. And the <span style='color:#0fb9b1'>vector</span> $\overrightarrow{ OP }$ can be denoted by $v = (x,y,z)$.

**$xyz$ plane visualisation :** ![[3D Plane Visualisation.png|center|250]]
## $n$-Plane

What about, the 4th dimension and above, how to<span style='color:#fa8231'> represent or visualise</span> is by using a<span style='color:#f7b731'> ordered</span> $\color{#f7b731}{n}$ <span style='color:#f7b731'>tuple</span> or a $\color{#f7b731}{n}$<span style='color:#f7b731'>-vector</span>.

Let $V = (v_{1}, \dots, v_{i}, \dots, v_{n})$ and $U = (v_{1}, \dots, u_{i}, \dots, u_{n})$, then :
- The<span style='color:#0fb9b1'> ith component / coordinate</span> of $V$ is $v_{i} \in \Bbb {R}$
- $V$ & $U$ are <span style='color:#fa8231'>equal</span> or <span style='color:#fa8231'>component wise the same</span>, if $\color{#f7b731}{v_{i} = u_{i}, \forall i \text{ in range 1 to n}}$ 
- $0n$-vector is a <span style='color:#0fb9b1'>zero vector</span> $(0, 0, \dots, 0)$
- The same rules for **addition**, **subtraction** and **negation** applies here.
<div style="page-break-after: always;"></div>

This vector can be expressed as a [[Matrices#Types of Matrices|row / column matrix]] like such
$$
\text{ Column vector :}
\begin{pmatrix}
v_{1} \\
v_{2} \\
\vdots \\
v_{n}
\end{pmatrix}
\text{ Column vector : }
\begin{pmatrix}
v_{1} & v_{2} & \dots & v_{n}
\end{pmatrix}
$$

And this is just a special matrix.
### $n$-Space

Now a space, is a <span style='color:#f7b731'>set of all possible n-vectors</span> of real numbers.

$\forall V_{i} \in \Bbb{R}^{n}$, $(v_{1}, v_{2}, \dots, v_{n})$ are all in <span style='color:#f7b731'>real numbers</span>. Basically every value must be real.

**Something to take note of**
- $\Bbb {R} = \Bbb {R}^{1}$ denotes the <span style='color:#f7b731'>real line</span>, **1D**
- $\Bbb {R}^{2}$ denotes the <span style='color:#f7b731'>xy-plane</span>, **2D**
- $\Bbb {R}^{3}$ denotes the <span style='color:#f7b731'>xyz-plane</span>, **3D**

The linear system $Ax = b$ with $m$ equations and $n$ variables, $x$ can be <span style='color:#f7b731'>viewed as a n-column vector</span>. Whose solution is a subset of $\Bbb{R}^{n}$. Since a vector is just a special matrix, it can be interchangeable.

Thus the goal is to <span style='color:#fa8231'>find a subset</span>, where <span style='color:#f7b731'>all the vectors are a solution</span> to this equation.
## Implicit & Explicit Forms

Now the [[Linear Systems#Linear System|linear systems]] that was shown are all given in <b><span style='color:#0fb9b1'>implicit form</span></b>. As it just gives us a general idea of the values of $x_{1}, \dots, x_{n}$ and <span style='color:#fa8231'>what it must satisfy in terms of an equation</span>. A broad view of the solution subset in $\Bbb {R}^n$.

An <b><span style='color:#0fb9b1'>explicit form</span></b> is the [[Linear Systems#Linear Equations|general solution]] of the linear system. Where $\color {#f7b731} {x_{i}}$ <span style='color:#f7b731'>is expressed in terms of something</span>. For example $y = \frac{1}{2} + \frac{3}{2}t$.
### Lines in $\Bbb{R}^{2}$

An equation of a line in <span style='color:#fa8231'>terms of coordinates</span> is $ax + by = c$ :
 - **Implicit form :** $\{ (x, y) | ax + by = c \}$
 - **Explicit form :**
	 1) If $a \neq 0$, let $y = t$ then $\{ (\frac{c-bt}{a}, t) | t \in \Bbb{R} \}$
	 2) If $b \neq 0$, let $x = s$ then $\{ (s, \frac{c - as}{b}) | s \in \Bbb{R} \}$

In <span style='color:#fa8231'>terms of vectors</span>, a straight line is determined by a <span style='color:#fa8231'>point</span> $p$ and the <span style='color:#fa8231'>direction of vector</span> $V = (a, b)$ which <b><mark style='background:#f7b731'>must be parallel to this line</mark></b>, such that $(a, b) \neq 0$.

Then a <span style='color:#fa8231'>point of the line is in the form</span> of $(x_{0}, y_{0}) + t(a, b)$ and its **explicit form** will be, $\{ (x_{0} + ta, y_{0} + tb) | t \in \Bbb{R} \}$.
<div style="page-break-after: always;"></div>

**Visualisation**
![[2D Line Represented by Vectors.png|center|300]]

How about its **implicit form** : 
1) let $x = a_{0} + ta$ and $y =y_{0} +tb$. 
2) Make <span style='color:#f7b731'>both equations in terms of</span> $\color {#f7b731} {t}$, which will be $t = \frac{x - x_{0}}{a}$ and $t = \frac{y_{0} - y}{b}$
3) Both equations must be equals and when combined it will result in, $\{ (x,y) | bx + ay = bx_{0} + ay_{0}\}$, which is the <span style='color:#fa8231'>equation of the line</span>
### Plane in $\Bbb{R}^{3}$

For a plane to exist, pick <span style='color:#f7b731'>3 points that are not on the same line</span> (non-linear).

![[3D Plane Represented by Vectors.png|center|300]]

This will all be the same on a $\color {#f7b731} {\Bbb{R}^3}$ <span style='color:#f7b731'>plane</span>, and the <span style='color:#fa8231'>point on a plane</span> is given as : 
$$r = a + sU + tV$$
**Where :**
- $a$ is **some point on the plane**
- $U$ and $B$ are <b><mark style='background:#f7b731'>2 non parallel vectors to each other</mark></b> but are <span style='color:#f7b731'>parallel to the plane</span>.
- $s$ and $t$ are a **scalar constants** and must be a real number

Then to find its **implicit form** :
- $x = a_{1} + su_{1} + t(v_{1})$
- $y = a_{2} + su_{2} + t(v_{2})$
- $x = a_{3} + su_{3} + t(v_{3})$

Once the above is formed, then make $\color {#f7b731} {s}$ <span style='color:#f7b731'>&</span> $\color {#f7b731} {t}$ <span style='color:#f7b731'>in terms of</span> $x$, $y$ and $z$ respectively for the 3 equations. Then once done <span style='color:#f7b731'>write down the augmented matrix</span>.

**Example**
$$
\left(
\begin{array}{cc|c}
1 & -1 & x - 1 \\
2 & 1 & y - 2 \\
-2 & 5 & z + 4 
\end{array}
\right)
$$
The above is just an example when writing the augmented matrix where the <span style='color:#f7b731'>left values are the coefficients</span> of the $s$ and $t$. Once that is achieved make it into a <b><mark style='background:#f7b731'>row echelon form</mark></b>.

One the **REF** is achieved the last row will be 0 except for the right most column. 

And thus the <b><mark style='background:#f7b731'> system must be consistent</mark></b> this, the bottom right entry must be 0 and that is the <span style='color:#fa8231'>equation of the plane</span>.
### Line in $\Bbb{R}^{3}$

When <span style='color:#f7b731'>2 non-parallel planes</span> intersect, the intersection point is a line. Thus the **implicit form** is written as such it is a set of all triples where $\{(x, y, z) \vert a_{1}x + b_{1}y + c_{1}z = d_{1} \text{ and } a_{2}x + b_{2}y + c_{2}z = d2\}$.

To get the **implicit form** is just as simple as solving for the 2 linear equations using the augmented matrix. Take note that $z$ <span style='color:#f7b731'>will be arbitrary</span> since there are only 2 equations and express $x$, $y$ and $z$ in terms of that arbitrary number.

Thus the result will be $(a,b,c) + t (x,y,z)$ which <span style='color:#fa8231'>describes the line as having</span> the point $(a,b,c)$ parallel to some vector $(x,y,z)$. 

So <span style='color:#fa8231'>in general</span>, to go from a **implicit form, into an explicit form**, just make the <span style='color:#f7b731'>arbitrary values in terms of</span> $x$, $y$ and $z$m then using the <span style='color:#f7b731'>gaussian elimination</span>, the explicit form can be achieved.
# Linear Combinations & Spans
---
There are <span style='color:#fa8231'>2 basic operations</span> for vectors and they are :
1) **Scalar Multiplication**
2) **Addition**

A <b><span style='color:#0fb9b1'>linear combination</span></b> is a series of <span style='color:#fa8231'>scalar multiplication and addition</span> to form another vector, which has the form $c_{1}v_{1} + c_{2}v_{2} + \dots + c_{n}v_{n}$.

A vector $V$ is a <span style='color:#0fb9b1'>linear combination</span> if, using a <span style='color:#f7b731'>series of basic operations on a set of vectors can result in</span> $V$.

For example, $\color {#f7b731} {0}$ is <b><mark style='background:#f7b731'>always a linear combination</mark></b> of a set of vectors as, $0 = 0v_{1} + 0v_{2} + \dots 0v_{n}$.

**How to know if $V$ is a linear combination :**
![[Finding if a Vector is a Linear Combination.png|center|]]

Now how about a collection of linear combinations, well this is known as a <b><span style='color:#0fb9b1'>span</span></b> or <b><span style='color:#0fb9b1'>linear span</span></b>.

Let $S$ be some subset of $\Bbb{R}^{n}$, then the <span style='color:#fa8231'>set of all linear combinations</span> is denoted as $span(S)$ or $span\{v_{1}, v_{2}, \dots, v_{n}\}$.

Now is there a $S$ what <span style='color:#f7b731'>can span the whole</span> $\Bbb{R}^{n}$ space? Well there is, take a $\Bbb {R}^{3}$ space, and let $S = {(1,0,0),(0,1,0),(0,0,1)}$ , then <span style='color:#f7b731'>every possible vector</span> in the $\Bbb{R}^{3}$ space <span style='color:#f7b731'>is a linear combination</span> of this subset.

**Finding the span**
- Let $S = \{(1,0,1),(1,1,0)\}$
- A linear combination will be in the form of $a(1,0,1) + b(1,1,0) = (a + b, b, a)$
- Thus $span(S) = \{(a+b, b,a ) \vert a,b \in \Bbb{R}\}$ 

**Finding the subset S**
- Let $span(S) = \{(2a + b, a, 3b-a) \vert a,b \in \Bbb{R}\}$ 
- It can be spilt into $(2a,a,-a) + (b,0,3b) = a(2,1,-1) + b(1,0,3)$
- Thus $S = \{(2,1,-1), (1,0,3)\}$

**How to find if a given subset spans the whole of** $\Bbb {R}^{n}$ :
![[How to Know if a Subset Spans the whole R Space.png|center|400]]

## Criterion to span the whole $\Bbb{R}^{n}$ space

Let $S = \{v_{1}, v_{2}, \dots, v_{n}\}$ and lets view each of these vectors as a <span style='color:#0fb9b1'>column vector</span>. Now in order for $V$ to be a linear composition, then the <span style='color:#fa8231'>following must hold</span> :
$$
\begin{pmatrix}
    V_{1} \\ 
    V_{2} \\
    \vdots \\
    V_{n}
\end{pmatrix} = 
c_{1}
\begin{pmatrix}
    v_{11} \\ 
    v_{12} \\
    \vdots \\
    v_{1n}
\end{pmatrix} + \dots + c_{n}
\begin{pmatrix}
    v_{n1} \\ 
    v_{n2} \\
    \vdots \\
    v_{nm}
\end{pmatrix}
= 
\begin{pmatrix}
    v_{11} & v_{12} & \dots & v_{1n} \\ 
    v_{21} & v_{22} & \dots & v_{2n} \\
    \vdots & \vdots &       & \vdots \\
    v_{n1} & v_{n2} & \dots & v_{mn}  
\end{pmatrix}
\begin{pmatrix}
    c_{1} \\ 
    c_{2} \\
    \vdots \\
    c_{n}
\end{pmatrix}
$$
Remember the equation $Ax = b$, now $b = V$ since the $V$ is the target and the column matrix with $(c_{1}, c_{2}, \dots, c_{n})$ is $x$.

Similar to what was shown above, using <span style='color:#f7b731'>gaussian elimination</span> get the row-echelon from of $A$, which will result in $(R \vert v')$.

For it to <span style='color:#fa8231'>span the whole system</span>, it must be <b><mark style='background:#f7b731'>consistent</mark></b>, which means the <span style='color:#f7b731'>right most column is non-pivot</span>, thus $\color {#eb3b5a} {R}$ <span style='color:#eb3b5a'>cannot contain non zero rows</span>.

Thus it is very simple
- Take all vectors in $S$ and <span style='color:#f7b731'>view them as column vectors</span>
- Make the <span style='color:#f7b731'>augmented matrix</span> and use the gaussian elimination to <span style='color:#f7b731'>find the REF</span>
- If the resulting **REF** <b><mark style='background:#f7b731'>has a zero row</mark></b>, then it <span style='color:#eb3b5a'>cannot span</span> the whole $R^{n}$ space.

Another way, is just to see the size of $A$, if the <span style='color:#f7b731'>number of columns is smaller than the number of rows</span> then it cannot span the whole $\Bbb {R}^{n}$ space.

## Properties of a Span

A <b><span style='color:#0fb9b1'>zero vector</span></b>, is <span style='color:#f7b731'>always</span> a linear combination of any $span(S)$.

Given $(v_{1}, v_{2}, \dots, v_{n}) \in span(S)$, then the <span style='color:#f7b731'>linear combination of all these vectors, is also inside the same span</span>.
>Linear combinations are **closed** under the same <span style='color:#0fb9b1'>span</span>.

In particular, take any <span style='color:#fa8231'>2 vectors from</span> the $\color {#fa8231} {span(S)}$, and do either <span style='color:#f7b731'>addition</span> or <span style='color:#f7b731'>scalar multiplication</span>. The result will be a linear combination in $span(S)$. If one is <span style='color:#eb3b5a'>not in the span the resulting vector might not be in the span</span>.

Thus this shows that $span(S)$ are **closed under addition and scalar multiplication**.

$span(S_{1}) \subseteq span(S_{2})$, is considered to be <span style='color:#20bf6b'>true</span>, if for <span style='color:#f7b731'>all vectors</span> in $S= \{s_{1}, s_{2}, ,\dots, s_{n}\}$ <span style='color:#f7b731'>are in</span> $span(S_{2})$, meaning it is some linear combination of $S_{2} = \{v_{1}, v_{2}, \dots, v_{n}\}$.

![[Checking if 2 Spans are Equal.png|center|400]]

Given a span $S = {v_{1}, \dots, v_{n-1}, v_{n}}$ if $v_{n}$ is <span style='color:#fa8231'>some linear combination of</span> $v_{1}$ to $v_{n-1}$ and $Span(S) = V$. Then, by <span style='color:#f7b731'>removing</span> $v_{n}$ from $S$ to make $S'$, $\color {#f7b731} {Span(S')}$ will still be <span style='color:#f7b731'>equals to</span> $\color {#f7b731} {V}$. 
# Subspaces
---
Lets say $V$ is a <span style='color:#fa8231'>subset</span> of $\Bbb{R}^{n}$ which is just a set of n-vectors. $V$ is considered a <b><span style='color:#0fb9b1'>subspace</span></b> if <span style='color:#f7b731'>there exist some combination of vectors</span> in $\Bbb{R}^{n}$, denoted by $S$, such that $\color {#f7b731} {V = Span(S)}$.

**Other ways to say this are**
- $V$ is the subspace spanned by $S$
- $S$ spans the subspace $V$

$\{0\} = span\{0\}$ or similarly, this is known as a <b><span style='color:#0fb9b1'>zero space</span></b>, which is the <b><mark style='background:#f7b731'>smallest subspace possible</mark></b>

Can $\color {#f7b731} {\Bbb{R}^n}$ itself be a<span style='color:#f7b731'> subspace of itself</span>, well it can as long as $\color {#f7b731} {Span(S)}$ <span style='color:#f7b731'>spans the whole of </span>$\color {#f7b731} {\Bbb{R}^{n}}$. Which is the <b><mark style='background:#f7b731'>largest subspace possible</mark></b>.
- **Example :** For $\Bbb{R}^{3} = span {(1,0,0),(0,1,0),(0,0,1)}$ which will make $\Bbb{R}^{n}$ a subspace of itself
<div style="page-break-after: always;"></div>

**Finding the Span given a subset**
![[Finding Span Given Subset.png|center|400]]

Therefore, if $V = Span(S)$, then :
1) $0 \in V$
2) $c \in \Bbb{R}$ and $v \in V \implies cv \in V$, this is saying it is **closed under scalar multiplication**
3) $v \in V$ and $u \in V \implies u + v \in V$, this is saying it is **closed under addition**

If it does <span style='color:#fa8231'>not satisfy any of the 3 condition</span> then it <span style='color:#eb3b5a'>cannot be a subspace</span>. Find the counter example, for example $V_{4} = \{(1,a) \vert a \in \Bbb{R}\}$, then the $0$ vector is not inside $V_{4}$ since $x$ has to be 1.

**Scenarios for subspaces :**
1) For $\Bbb{R}^{1}$ 
	- $\{0\} = \{0\}$
	- $\Bbb{R}^{1}$
2) For $\Bbb{R}^{2}$
	 - $\{0\} = \{(0,0)\}$
	 - A straight line passing through the origin $(0,0)$
	 - $\Bbb{R}^{2}$
3) For $\Bbb{R}^{3}$
	 - $\{0\} = \{(0,0)\}$
	 - A straight line passing through the origin $(0,0)$
	 - A plane containing the origin $(0,0)$
	 - $\Bbb{R}^{3}$

# Solution Space
---
How can this be translated into <span style='color:#fa8231'>solving a linear system</span>. Surely if the $Span(S)$ of the linear system can be found, then the subspace $V$ can be formed, which is all possible linear combinations, which is a <b><span style='color:#0fb9b1'>solution space</span></b>. 

Thus, the <span style='color:#0fb9b1'>solution set </span>of a <span style='color:#f7b731'>homogeneous linear system is a subspace</span> of $\Bbb{R}^{n}$.

**Example:**

Given this linear system
$$  
\begin{cases}
x -2y + 3z = 0 \\
-3x + 7y - 8z = 0 \\
-2x + 4y - 6z = 0
\end{cases}$$

Its augmented matrix is written as such :
$$
\left(
\begin{array}{ccc|c}
1 & -2 & 3 & 0 \\
-3 & 7 & -8 & 0 \\
-2 & 4 & -6 & 0 
\end{array}
\right) \xrightarrow{\text{Gauss-Jordan Elimination}}
\left(
\begin{array}{ccc|c}
1 & 0 & 5 & 0 \\
0 & 1 & 1 & 0 \\
0 & 0 & 0 & 0 
\end{array}
\right) 
$$
Now $z$ will be <span style='color:#fa8231'>set to an arbitrary value</span> $t$, since it is not a pivot column, resulting in :
- $x = -5t$
- $y = -t$
- $z = t$

Then $(x,y,z) = (-5t, -t, t)$, factorising it will result in $t(-5, -1, 1)$ and this the solution space is $\color {#f7b731} {Span\{(-5,1,1)\}}$.

So <span style='color:#f7b731'>any linear combination</span> of $(-5,1,1)$ <span style='color:#f7b731'>will be a solution</span> to the linear system.

# Linear Independence
---
Now a span can be as big as possible and still be a solution to the linear system, but <span style='color:#fa8231'>how to find the smallest span</span>.

For a subset to be <b><span style='color:#0fb9b1'>linearly independent</span></b>, then <span style='color:#f7b731'>no vector can be written as some linear combination</span> of other vectors in the set. And this set has <span style='color:#f7b731'>no redundant vector</span>.

Now let $S = \{v_{1}, v_{2}, v_{n}\}$ be a subset of $\Bbb{R}^{n}$, which has an equation of $c_{1}v_{1} + \dots + c_{n}v_{n} = 0$
- There is obviously a <span style='color:#fa8231'>trivial solution</span>, by letting $c_{1} = 0 = c_{2} = \dots = c_{n}$
- If it has a <span style='color:#fa8231'>non trivial solution</span>, then $S$ is called a <span style='color:#0fb9b1'>linearly dependent set</span> and the vectors are <span style='color:#0fb9b1'>linearly dependent</span>, as there exist some $c_{i}$ that are not 0 for the equation to hold
- If it <span style='color:#fa8231'>only has the trivial solution</span>, then $S$ is called a <span style='color:#0fb9b1'>linearly independent set</span> and the vectors are <span style='color:#0fb9b1'>linearly independent</span>
<div style="page-break-after: always;"></div>

**Determining dependent or independent**
![[Determine if the Subset is Dependent or Independent.png|center|400]]

**Properties of linear independence**
Let $S_{1}, S_{2}$ be a <span style='color:#fa8231'>finite subset</span> of $\Bbb{R}^{n}$ such that $S_{1} \subseteq S_{2}$ then :
- $S_{1}$ is linearly dependent $\implies$ $S_{2}$ is also linearly dependent
- $S_{2}$ is linearly independent $\implies$ $S_{1}$ is also linearly independent

$c0 = 0$ has an infinitely many solutions, and this $\{0\}$ is linearly dependent
- If any $S$ contains the <span style='color:#0fb9b1'>zero vector </span>then it is also linearly dependent

If $cV = 0$, then either $c = 0$ or $V$ is a <span style='color:#fa8231'>set of zero vectors </span>
- $\color {#f7b731} {c = 0}$ means that $V$ is **linearly independent**
- $V$ is <span style='color:#f7b731'>a set of zero vectors</span>, then $V$ is **linearly dependent** 

If the following is <span style='color:#fa8231'>linearly dependent</span> $\{u,v\}$ then $u = cv$ or $v = cu$.

If $S = \{v_{1}, v_{2}, \dots, v_{k}\}$ for a $\Bbb{R}^{n}$ if $k > n$, then $S$ is <span style='color:#f7b731'>linearly dependent</span>.
# Bases
---
Let $S$ be a subset in $\Bbb{R}^{n}$ and $S$ is <span style='color:#fa8231'>linearly independent</span> and the $Span(S) \neq \Bbb{R}^{n}$.
- Pick any $v_{i}$ such that $v_{i} \notin Span(S)$, then $S$ is <span style='color:#f7b731'>still linearly independent</span> because no other vector in $S$ can produce $v_{i}$ since it originally was not in $S$
- Continue until $S$ spans the whole of $\Bbb{R}^{n}$

This <span style='color:#fa8231'>can only happen if</span> the **number of vectors** in $S$ is **equals to** $n$.

Now let $S$ be some subset of the <span style='color:#0fb9b1'>vector space</span> $V$, where the <span style='color:#f7b731'>vector space is just another term for subspace</span> of $\Bbb{R}^{n}$.

For $S$ to be a <span style='color:#0fb9b1'>basis</span> of $V$ it <b><mark style='background:#fa8231'>show that the following is true</mark></b> :
1) $S$ is **linearly independent** (<span style='color:#f7b731'>No redundant vectors</span>)
2) $span(S) = V$

In words, the **aim** for a <span style='color:#0fb9b1'>basis</span> is :
1) **Smallest possible** number of vectors to span $V$
2) **Largest possible** number of vectors that is linearly independent

The basis for $\{0\}$ is just the $\emptyset$. And other than that the other have an infinite number of basis.

Now a <b><span style='color:#0fb9b1'>coordinate vector</span></b> of $v$ is defined as such
$$
(v)S = (c_{1}, c_{2},\dots, c_{n})
$$
**Where :**
- $v$ is some vector
- $S$ is a subset of a vector space
- $c_{i}$ are constants

This just means that to get vector $v$ **through a linear combination using** $S = \{v_{1}, v_{2}, \dots , v_{k}\}$ like so,$c_{1}v_{1} +c_{2} v_{2} + \dots + c_{n}v_{n}$. If it is $[v]S = \{(v)S\}^T$ is <span style='color:#f7b731'>just in column form</span>.

This <span style='color:#fa8231'>only works if</span> :
- $S$ <span style='color:#f7b731'>is a span</span> of $V$ which contains $v$ and because it is a span every $v \in V$ <span style='color:#f7b731'>can be uniquely written in this form</span>

**Properties of a basis**
Let $S$ be a basis of the vector $V$
- $(v)S = 0 \iff v = 0$ 
- For any $c \in \Bbb{R}$ and $v \in \Bbb{R}$ then $(cv)S = c(v)S$
- For any $u,v \in V$, $(v+u)S = (v)S + (u)S$
- Therefore in general it is <b><mark style='background:#f7b731'>closed under scaler multiplication and addition</mark></b>

Now lets say that $S$ is a <span style='color:#0fb9b1'>basis</span> for $V$ and let $v_{1}, v_{2}, \dots, v_{n} \in V$ and these vectors must be :
- **Linearly independent**
- they **span** $V$ as well

Then $Span\{(v_{1})S, \dots, (v_{n})S\} = \Bbb{R}^{k}$ where $k = \vert S \vert$. Then it can be said that $V$ and $\Bbb{R}^{k}$ are <b><span style='color:#0fb9b1'>isomorphic</span></b> as vector spaces.

[[Matrices#Invertibility|Invertibility]] can also be used to <span style='color:#fa8231'>determine bases</span>. View the vectors as <span style='color:#f7b731'>row vectors</span> instead of column vectors, the if the <span style='color:#f7b731'>matrix is invertible, then it is a bases</span> for $\Bbb{R}^{n}$
## Standard Basis

This is a <span style='color:#fa8231'>special type of bases</span> where $E = \{e_{1}, e_{2}, \dots, e_{n}\}$ which is a subset of $\Bbb{R}^{n}$ and $e_{1} = (1,0,\dots,0)$, $e_{2} = (0,1,\dots,0)$, $e_{n} = \{0,0,\dots, 1\}$ basically at $e_{i}$ <span style='color:#f7b731'>the ith element is 1</span>.

Then as proven $Span(E) = \Bbb{R}^{n}$ and $E$ is <span style='color:#fa8231'>linearly independent</span>. Then for any $v \in \Bbb{R}^{n}$ its coordinate vector is just $v$ itself, $(v)E = (v1, v2, \dots, v_{n}) = v$ 

**For example** :

$E = \{(1,0,0),(0,1,0),(0,0,1)\}$ which is a <span style='color:#0fb9b1'>standard basis</span> and it spans the whole of $\Bbb{R}^3$.

Let $v = (5,4,-1)$, then to get $v$ using the span of $E$ will be as follows :
- $(5,4,-1) = c_{1}(1,0,0) + c_{2}(0,1,0) + c_{3}(0,0,1)$
- Simplifying it, $(5,4,-1) = (c_{1}, c_{2}, c_{3})$
- Then $c_{1} = 5$, $c_{2} = 4$ and $c_{3} = -1$
- Therefore, $(v)E = (5,4,-1) = v$

## Dimensions

For something lets say $S$ to be a <span style='color:#fa8231'>basis of </span>$\color {#fa8231} {\Bbb{R}^n}$, these 2 <b><mark style='background:#f7b731'>conditions has to be met</mark></b>:
- **Linearly Independent**
- $Span(S) = \Bbb{R}^{n}$

And if the <span style='color:#fa8231'>number of vectors</span> in $S$
- Is <span style='color:#f7b731'>smaller</span> than $n$ where $n$ is the $\Bbb{R}^{n}$space then it <span style='color:#eb3b5a'>cannot span the whole</span> of $\color {#eb3b5a} {\Bbb{R}^{n}}$
- If it is <span style='color:#f7b731'>bigger</span> than $n$, then it <span style='color:#eb3b5a'>will not be linearly independent</span>

Therefore, if $\color {#fa8231} {S}$ and $\color {#fa8231} {T}$ are a <span style='color:#fa8231'>basis for</span> $\color {#fa8231} {V}$ then the <span style='color:#f7b731'>cardinality</span> (size) of both $S$ and $T$ are the <span style='color:#f7b731'>same</span>, $\vert S \vert = \vert T \vert$. This cardinality has a special name called <b><span style='color:#0fb9b1'>dimension</span></b>.

If in $\Bbb{R}^{2}$ and $\Bbb{R}^{3}$ a <span style='color:#fa8231'>straight line through the origin</span> in the form of $span\{v\}$ where $v \neq 0$ the the <span style='color:#f7b731'>dimension is 1</span>. And for $\Bbb{R}^{3}$ a <span style='color:#fa8231'>plane through the origin</span> in the form of $span\{v,u\}$ where $v$ and $u$ are linearly independent, the <span style='color:#f7b731'>dimension is 2</span>.

**How to find the dimension of a solution space :**
- First let $Ax = 0$ be a <span style='color:#f7b731'>homogeneous linear system</span>
- Make $A$ into a <span style='color:#f7b731'>row-echelon form</span> $R$
- The <span style='color:#f7b731'>number of arbitrary parameters</span> used (number of non-pivot columns) is the <span style='color:#0fb9b1'>dimension</span> of $V$

To know if $S$ is a basis of $V$ then <b><mark style='background:#fa8231'>any of he following 2 conditions must be true</mark></b>
1) $S$ is linearly independent
2) $Span(S) = V$
3) $\vert S \vert = dim(V)$

**Properties of Dimensions**
Let $S \subseteq T$
- Then the $dim(S) \le dim(T)$
- But if $S \neq T$ then $dim(S) \lt dim(T)$
- If $S = T$ then $dim(S) = dim(T)$

**Properties of a Square Matrix & Basis**
Let $A$ be a square matrix of order $n$ :
- $A$ is invertible
- $Ax = b$ has only a unique solution
- $Ax = 0$ has only the trivial solution
- The **REF** form of $A$ is $I_{n}$
- $A$ is the product of **elementary matrices**
- $det(A) \neq 0$
- Rows of $A$ forms a basis of $\Bbb{R}^{n}$
- Columns of $A$ forms a basis of $\Bbb{R}^{n}$, which **leads back to point 1**
# Transition Matrices
---
Let $S$ and $T$ be a bases for a vector space $V$, then is it possible to find a relation between them such that $[w]S$ can be written in the form of $[w]T$ where $w \in V$. 

Yes it is possible with a <span style='color:#0fb9b1'>transaction matrix</span> from $S$ to $T$. Let $S = {u_{1}, u_{2}, \dots, u_{k}}$ and this transition matrix is in the form of $([u_{1}]T, \dots, [u_{k}]T)$ which is denoted by $P$, then $P[w]S = [w]T, \forall w \in V$

**Finding the Transition Matrix**
![[Finding the Transition Matrix.png|center|400]]

<span style='color:#0fb9b1'>Transition matrices</span> are <span style='color:#f7b731'>transitive in nature</span> :
- Let $S_{1} S_{2}S_{3}$ be bases for a vector space $V$
- Then let $P$ be the transition matrix from $S_{1} \to S_{2}$ and $Q$ be the transition matrix from $S_{2} \to S_{3}$
- Then the transition matrix from $S_{1} \to S_{3}$ is simply $QP$
$$
[v]S_{1} \xrightarrow{\text{P}} [v]S_{2}  \xrightarrow{\text{Q}}[v]S_{3}
$$
Then what about if :
$$
[v]S_{1} \xrightarrow{\text{P}} [v]S_{2}  \xrightarrow{\text{Q}}[v]S_{1}
$$
Simplifying this, $QP[v]S_{1} = [v]S_{1}$, this means that $QP = I$ an <span style='color:#f7b731'>identity matrix</span>, and therefore $Q$ is the <span style='color:#f7b731'>inverse of</span> $\color {#f7b731} {P}$
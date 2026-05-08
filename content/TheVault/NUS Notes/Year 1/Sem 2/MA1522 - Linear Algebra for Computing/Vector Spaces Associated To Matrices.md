---
title: Vector Spaces Associated To Matrices
Date Created: 2024-03-03
Last Updated: 2025-09-27
tags:
  - MA1522
  - Math
  - Vectors
---
# Row & Column Spaces
---
Given a matrix $A$ with $n \times m$ size;
1) **Row Spaces**
Let $r_{i}$ denote teach row in $A$, then A can be represented as :
$$A =
\left(
\begin{matrix}
r_{1} \\
r_{2} \\
\vdots \\
r_{m} 
\end{matrix}
\right)
$$

This is known as a <span style='color:#0fb9b1'>row space</span> of $A$ which is <span style='color:#f7b731'>spanned by the rows</span> of $A$ and the $Span(A)$ is a <span style='color:#f7b731'>subspace</span> of $\Bbb{R}^{n}$.

And if 2 matrices $A$ and $B$ are [[Matrices#Invertibility|row equivalent]], then they will also have the <span style='color:#f7b731'>same row space</span>.

Building on on this, let $R$ be the <span style='color:#f7b731'>REF</span> of $A$, 
1) Then all <span style='color:#f7b731'>nonzero rows</span> in $R$ are <span style='color:#f7b731'>linearly independent</span>
2) The <span style='color:#f7b731'>nonzero rows</span> forms a <span style='color:#f7b731'>basis</span> for the row space $A$
3) The <span style='color:#f7b731'>number of nonzero rows is the dimension</span> of the row space $A$

Thus if $A$ and $B$ are <span style='color:#f7b731'>row equivalent</span> then $Span(A) = Span(B)$ and $A$ is a <span style='color:#f7b731'>basis</span> of $B$.

2) **Column Spaces**
Let $c_{i}$ denote teach column in $A$, then A can be represented as :
$$A =
\left(
\begin{matrix}
c_{1} & c_{2} & \dots & c_{n}
\end{matrix}
\right)
$$

This is known as a <span style='color:#0fb9b1'>column space</span> of $A$ which is <span style='color:#f7b731'>spanned by the columns</span> of $A$ and the $Span(A)$ is a <span style='color:#f7b731'>subspace</span> of $\Bbb{R}^{m}$.

If $A$ is <span style='color:#f7b731'>transposed</span> then the row space of $A^{T}$ is the column space and vice versa.

Similarly, the row operations can be translated to the column space as well. Because, it it is <span style='color:#f7b731'>row equivalent</span>, then it <span style='color:#f7b731'>preserves the linear relations on the columns</span>.

Supposed that $A$ and $B$ are <span style='color:#0fb9b1'>row equivalent</span>, then $a_{i} = c_{1}a_{1} + \dots + c_{n}a_{n} \iff b_{j} =c_{1}b_{1} + \dots + c_{n}b_{n}$. Meaning the **linear relations in the columns are preserved**.  

Building on on this, let $R$ be the <span style='color:#f7b731'>REF</span> of $A$, 
1) The <span style='color:#f7b731'>pivot columns</span> forms a <span style='color:#f7b731'>basis</span> for the column space $R$ <b><mark style='background:#f7b731'>then only they are a basis of</mark></b> $A$.
2) The <span style='color:#f7b731'>number of pivot columns is the dimension</span> of the column space $A$
3) The <span style='color:#f7b731'>pivot columns</span> in $R$ form a bases for the column space of $R$.

**In general**

Let $V = span(S)$, then there are <span style='color:#fa8231'>2 methods to find the basis</span> :

1) **View as row vectors (Row Space)**
Viewing each vector as a <span style='color:#0fb9b1'>row vector</span>, then when making it into **RREF**, the <b><mark style='background:#f7b731'>number of nonzero rows</mark></b> in $R$ form a basis for $V$.

2) **View as column vectors (Column Space)**
View each vector as a <span style='color:#0fb9b1'>column vector</span>, then making it into **RREF**, the <b><mark style='background:#f7b731'>number of pivot columns</mark></b> in $R$ represents the vectors in $S$ form a basis for $V$.

An <span style='color:#fa8231'>addition functionality</span> is that the <span style='color:#0fb9b1'>pivot columns</span> form a basis $S'$ from $S$ and $V = span(S')$ and $S' \subseteq S$.

Then what about <span style='color:#f7b731'>extending</span> $S$ such that it is the basis of $\Bbb{R}^{n}$ instead of $V$. Now <span style='color:#f7b731'>view each vector as a row vector</span> and let $R$ be the **REF** of $S$ and it looks like this :
$$
R = 
  \begin{pmatrix}
    1 & 4 & -2 & 5 & 1 \\ 
    0 & 1 & 3 & -2 & 0 \\
    0 & 0 & 0 & 1 & 1  
   \end{pmatrix}
$$
To accomplish this, the <span style='color:#eb3b5a'>columns that are not pivot</span>, will have to become pivot, and the easiest way with the above is using $E_{3} = (0, 0, 1, 0, 0)$ and $E_{5} =(0, 0, 0, 0, 1)$.

 **Consistency**

Let $A$ be some $m \times n$ matrix, the <span style='color:#0fb9b1'>column space</span> of $A$ is of the following $\{Av \vert v \in \Bbb{R}^{n}\}$. Then the linear system $Ax = b$ is <span style='color:#0fb9b1'>consistent</span> if $b$ lies in the <span style='color:#0fb9b1'>column space</span> of $A$.

If they ask for <span style='color:#0fb9b1'>row space</span>, transform $A$ and $b$, then do the same thing.

# Rank
---
Let $R$ be the **REF** of $A$ then :
- $dim(\text{Row space of A})$ is just the<span style='color:#f7b731'> number of nonzero rows</span> in $R$
- $dim(\text{Col space of A})$ is the<span style='color:#f7b731'> number of pivot columns</span> in $R$
- $Rank(A) = Rank(A^{T})$

Also the $dim(\text{Row space of A}) = dim(\text{Col space of A})$, which is called the <span style='color:#0fb9b1'>rank</span> of $A$.

**Properties of rank**
- $Rank(A) = 0$ then $A$ is the <span style='color:#f7b731'>zero matrix</span>
- $Rank(A) \le$ the number of <span style='color:#f7b731'>rows</span> and the number of <span style='color:#f7b731'>columns</span> in $A$. In other words $Rank(A) \le min(r, c)$
- And $A$ is a <b><span style='color:#0fb9b1'>full rank</span></b> if $Rank(A) = min(r, c)$ and with this a <span style='color:#f7b731'>square matrix is of full rank</span>

**Example**
$$
A = 
  \begin{pmatrix}
    2 & 0 & 3 & -1 & 8 \\ 
    2 & 1 & 1 & -2 & 5 \\
    -4 & -3 & 0 & 5 & -7  
   \end{pmatrix}
R = 
  \begin{pmatrix}
    2 & 0 & 3 & -1 & 8 \\ 
    0 & 1 & -2 & -1 & -3 \\
    0 & 0 & 0 & 0 & 0  
   \end{pmatrix}
$$
**Conclusion**
- The <span style='color:#f7b731'>row space</span> of $A$ has a <span style='color:#f7b731'>basis</span> of $\{(2, 0, 3, -1, 8),(0, 1, -2, -1, -3)\}$
- The <span style='color:#f7b731'>column space</span> of $A$ has a <span style='color:#f7b731'>basis</span> of $\{(2, 2, -4), (0, 1, -3)\}$
- $rank(A) = 2$ and $A$ is <span style='color:#eb3b5a'>not full rank</span> since it is not 3

This can be tied to the <span style='color:#0fb9b1'>consistency</span> of the matrix. Let $A$ be some matrix and $R$ be the **REF** of $A$, also let $b$ be any vector :
- Then $(A \vert b)$ can be in the form of $(R \vert b')$ basically convert to **REF**
- If $Ax = b$ is <span style='color:#f7b731'>consistent</span> then $b'$ is <span style='color:#f7b731'>not pivot</span> in $(R \vert b')$
- Therefore, $\color {#f7b731} {Rank(A) = Rank(R\vert b')}$

This is because by adding $b$, <span style='color:#f7b731'>at most it adds 1 to the rank</span>, therefore, $Rank (A) \le Rank(A \vert b) \le Rank(A) + 1$.

Now let $A$ be a $m \times n$ matrix and $B$ be a $n \times p$ matrix then :
- <span style='color:#0fb9b1'>Column space</span> of $AB \subseteq$ column space of $A$
- <span style='color:#0fb9b1'>Row space</span> of $AB \subseteq$ row space of $B$

And in particular :
- $Rank(AB) \le Rank(A)$
- $Rank(AB) \le Rank(B)$
- $Rank(AB) \le min\{Rank(A), Rank(B)\}$

# Null Space & Nullity
---
Let $A$ be a $m \times n$ matrix, then the <span style='color:#0fb9b1'>null space</span> is when $Ax = 0$ or $\{v \in \Bbb{R}^ {n} \vert Av = 0 \}$. The <span style='color:#fa8231'>dimension of this is called</span> the <span style='color:#0fb9b1'>nullity</span>.

Unless stated, the vectors in the <span style='color:#0fb9b1'>null space</span> <span style='color:#f7b731'>viewed as column vectors</span>.

Then let $R$ be the **REF** of $A$ then $Ax = 0 \iff Rx =0$, which means the <span style='color:#f7b731'>null space</span> of $A$ is <span style='color:#f7b731'>equals</span> to the null space of $R$.

This the $Nullity(A) = Nullity (R) = \text{The number of non-pivot columns in R}$.
<div style="page-break-after: always;"></div>

**Example**
![[Finding Null space and Nullity.png|center|500]]

From here there is a observation where $\color {#f7b731} {n = rank(A) + nullity(A)}$. This is called the <span style='color:#0fb9b1'>dimension theorem</span>.

Therefore if $Nullity(A) = dim(\Bbb{R}^{n}) = n$, then the null space of $A = \Bbb{R}^{n}$.

And if <span style='color:#f7b731'>row space and column space</span> of $A = \{0\} \subseteq \Bbb{R}^{n}$, then the $rank(A) = 0$
## Inhomogeneous Linear System

Now what if $Ax = b$ instead of 0. If the <span style='color:#f7b731'>system is consistent</span> and have a solution $v$, then the solutions are in the form of $v + w$.

Then what about it being <span style='color:#f7b731'>inconsistent</span>, the the solution set is the $\emptyset$.

**In particular**
- If $Ax = b$ has only one solution then $Ax = 0$ has <span style='color:#f7b731'>only one solution</span> the zero vector
- $Nullspace(A) = \{0\}$ and the $nullity(A) = 0$
- $Rank(A) =$ number of columns of $A$
- Then the columns of $A$ are linearly independent

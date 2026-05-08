---
title: Diagonalisation
Date Created: 2024-04-09
Last Updated: 2025-09-27
tags:
  - MA1522
  - Math
  - Vectors
---
# Eigenvalue & Eigenvector
---
It is known that given a matrix $A$ and $A^{m}$ is just $A_{1}A_{2}A_{3} \dots A_{m}$, which takes a long time to calculate. However given a [[Matrices#Types of Matrices|diagonal matrix]], the following can be observed,
$$
  A^{m}  = 
  \begin{pmatrix}
    a_{11}^{m} & 0 & \dots & 0 \\ 
    0 & a_{22}^{m} & \dots & 0 \\
    \vdots & \vdots &       & \vdots \\
    0 & 0 & \dots & a_{nn}^{m}  
   \end{pmatrix}
$$
The diagonals are all just $x^{m}$.

So is there a way to <span style='color:#f7b731'>make a vector similar to a diagonal matrix</span>. This is the objective

Now let $A$ be <span style='color:#f7b731'>some square matrix</span> of order 4 and suppose that there is a <span style='color:#f7b731'>invertible matrix</span> $P$ such that $D$ which is a diagonal matrix is in the form of $P^{-1}AP$, hence the result for $\color {#f7b731} {A^{m} = PD^{m}P^{-1}}$.

With some manipulation, $D = P^{-1}AP$ can be converted into $AP = PD$. Let $P = (v_{1}, v_{2}, v_{3}, v_{4})$

 Then $AP = PD$ :
$$
A(v_{1}, v_{2}, v_{3}, v_{4}) = (v_{1}, v_{2}, v_{3}, v_{4})
  \begin{pmatrix}
    \lambda_{1} & 0 & 0 & 0 \\ 
    0 & \lambda_{2} & 0 & 0 \\
    0 & 0 & \lambda_{3} & 0 \\
    0 & 0 & 0 & \lambda_{4}  
   \end{pmatrix}
$$
**Where :**
- $\lambda \in \Bbb{R}$
- $v \in \Bbb{R}^{n}$ and $v$ <b><mark style='background:#f7b731'>must be a nonzero vector</mark></b>

Thus :
- $Av_{1} = \lambda_{1}v_{1}$ 
- $Av_{2} = \lambda_{2}v_{2}$ 
- $Av_{3} = \lambda_{3}v_{3}$ 
- $Av_{4} = \lambda_{4}v_{4}$ 

Take note that the **LHS** is a matrix multiplication while the **RHS** is a scalar multiplication.

Therefore :
- $\lambda$ is called the <span style='color:#0fb9b1'>eigenvalue</span> of $A$
- $v_{i}$ is the <span style='color:#0fb9b1'>eigenvector</span> of $A$ <span style='color:#f7b731'>associated to the eigenvalue</span> $\lambda_{i}$

A **special case** if $A$ is a <span style='color:#fa8231'>triangular matrix</span>, then its <span style='color:#f7b731'>diagonal entries</span> are precisely the <span style='color:#0fb9b1'>eigenvalues</span>.
## Finding the Eigenvalue

Given $A v = \lambda v$ :
- Since the RHS is a **scalar multiplication**, it <span style='color:#eb3b5a'>cannot be brought over</span> to the LHS since it is a **matrix multiplication**
- Rewrite it as $A v = \lambda I v$, which the RHS is not a matrix multiplication
- Then $\lambda I v - A v = 0 \iff (\lambda I - A)v = 0$  
- Since $v$ <span style='color:#f7b731'>cannot be a zero vector</span>, then $\lambda I - A$ which must be a square matrix then the equation <span style='color:#f7b731'>only has the non trivial solution</span>
- Meaning $\lambda I - A$ is a **singular matrix**, thus the $det(\lambda I - A) = 0$, <span style='color:#f7b731'>solving for this will give all the eigenvalues</span>.
$$
det(\lambda I - A) = \lambda^{n} + c_{n-1}\lambda^{n-1} + c_{n-2}\lambda^{n-2} + \dots + c_{1}\lambda + c_{0}
$$
**Where :**
- $n$ is the degree of the square matrix $A$, so the example for $A$ is degree 4 thus $n = 4$
- $c_{i}$ is the coefficient
- The <span style='color:#f7b731'>roots of the equation will be the eigenvalues</span> (This course only focuses on real roots).

To get this equation [[Matrices#Determinant|use the determinant equation]] and simplify.

The $\lambda^{n}$ is called a <span style='color:#0fb9b1'>monic</span> because its leading coefficient is 1.

$det(\lambda I - A)$ or $P(\lambda)$ is called the <span style='color:#0fb9b1'>characteristic polynomial</span> of $A$ and $det(\lambda I - A) = 0$ is the <span style='color:#0fb9b1'>characteristic equation</span> of $A$

**Example :**
![[Finding the Eigenvalues.png|center|]]

The <span style='color:#fa8231'>product</span> of all the eigenvalues <span style='color:#f7b731'>gives the determinant</span> of $A$. Therefore, if a <span style='color:#fa8231'>matrix is invertible</span>, its <b><mark style='background:#f7b731'>eigenvalue cannot be 0</mark></b>. In addition the powers for $D^{m}$, $\color{#f7b731} {m}$ <span style='color:var(--mk-color-yellow)'>can be any integer</span>, else only nonnegative integers.

The <span style='color:#fa8231'>sum</span> of the eigenvalues <span style='color:#f7b731'>gives the trace</span> of $A$ or simply the sum of the diagonal entries.
# Eigenspace
---
Recall that $(\lambda I - A)v = 0$, and $v$ is a non-zero vector, thus $(\lambda I - A)$ is a singular matrix and therefore $v \in nullspace of (\lambda I - A)$.

The eigenvectors of $A$ associated with the eigenvalue $\lambda$ are <span style='color:#f7b731'>all the nonzero vectors in the eigenspace</span> $E_{A,\lambda}$.
<div style="page-break-after: always;"></div>

**How to find the Eigenspace**
![[Finding the Eigenspace.png|center|]]

**Repeat** for all the eigenvalues, thus for the example above repeat for $0$.

# Diagonalisation
---
For $A$ which is a **square matrix**, to be <span style='color:#0fb9b1'>diagonalisable</span> if there is a <span style='color:#f7b731'>invertible matrix</span> $P$ such that $P^{-1} A P$ is a <span style='color:#f7b731'>diagonal matrix</span>.

If $A$ is <span style='color:#fa8231'>originally a diagonal matrix</span>, then it will <span style='color:#f7b731'>always be diagonalisable</span> by taking $\color {#f7b731} {P}$ to be the <span style='color:#f7b731'>identity matrix</span>. Also for this $P$ its corresponding columns are the eigenvectors of $A$ associated to the eigenvalue (Column 1 $\rightarrow \lambda_{1,1}$).

For $A_{n \times n}$ to be <span style='color:#fa8231'>diagonalisable</span>, then it <b><mark style='background:#f7b731'>must have n linearly independent eigenvectors</mark></b>.

**Steps :**
1) Find **all** the eigenvalues of $A$
2) **For each** eigenvalue, find the corresponding basis, solving $(\lambda_{i} I - A)x = 0$ and find its eigenspace
3) If the **sum of all vectors in each basis is n**, then it is diagonalisable, else no.
4) If there are any <span style='color:#f7b731'>non real</span> $\lambda$ then it is <span style='color:#eb3b5a'>not diagonalisable</span> over $\Bbb{R}$.

The $det(\lambda I - A)$ is a polynomial of degree $n$ in terms of $\lambda$ which can be expressed in $(\lambda - c_{1})^{r_{1}}(\lambda - c_{2})^{r_{2}}\dots(\lambda - c_{k})^{r_{k}}$.

Then $a(\lambda_{i})$ is known as the <span style='color:#0fb9b1'>algebraic multiplicity</span> of $\lambda_{i}$. For example, $(\lambda + 1)^{3}(\lambda - 1)^{2}(\lambda +2)$ then :
- $3$ is the algebraic multiplicity for $\lambda = -1$
- $2$ is the algebraic multiplicity for $\lambda = 1$
- $1$ is the algebraic multiplicity for $\lambda = -2$

Then $g(\lambda_{i})$ is known as the <span style='color:#0fb9b1'>geometric multiplicity</span> for the $dim(E_{i})$, which is the eigenspace of $A$ associated to $\lambda_{i}$. For example, $(\lambda + 1)^{3}(\lambda - 1)^{2}(\lambda +2)$ then :
- $3$ is the geometric multiplicity for the eigenspace ($E_{-1}$), thus $dim(E_{-1}) = 3$
- $2$ is the geometric multiplicity for the eigenspace ($E_{1}$), thus $dim(E_{1}) = 2$
- $1$ is the geometric multiplicity for the eigenspace ($E_{-2}$), thus $dim(E_{-2}) = 1$

$a(\lambda_{i}) \le a(\lambda_{i})$ and also the sum of all $a(\lambda_{i}) = n$.
<div style="page-break-after: always;"></div>

**Quick Check for Diagonalisation**
1) $det(\lambda I - A)$ <span style='color:#eb3b5a'>cannot</span> be completely factorised in $\Bbb{R}$, its <span style='color:#f7b731'>roots are not real numbers </span>
	- $A$ is not diagonalisable
2) $det(\lambda I - A)$ <span style='color:#20bf6b'>can</span> be completely factorised in $\Bbb{R}$, its <span style='color:#f7b731'>roots are all real numbers </span>
	- If the <span style='color:#f7b731'>number of eigenvalues is the same</span> as $n$ which is the size of the square matrix $A$, then it is diagonalisable.
	- <span style='color:#f7b731'>Find</span> the basis for the <span style='color:#f7b731'>eigenspace</span> for each eigenvalue ($\lambda_{i}$)
	2) $g(\lambda_{i}) \lt a(\lambda_{i})$, then it is not diagonalisable 
	3) $g(\lambda_{i}) = a(\lambda_{i}) = n$, then it is diagonalisable 

**Example**
![[Determining if a Matrix is Diagonalisable.png|center|]]

The key point is to <span style='color:#f7b731'>start checking those with higher algebraic multiplicity</span>.
# Orthogonal Diagonalisation
---
There are many ways to <span style='color:#fa8231'>get an invertible matrix</span> $P$
1) Using the Gauss-Jordan elimination ($(P \vert I) \to (I \vert P^{-1}$)
2) Using the adjoint matrix ($P^{-1} = \frac{1}{det(p)} \times adj(P)$), **only for 2 by 2**.
3) If the $P$ is orthogonal then $P^{-1} = P^{T}$, which is <span style='color:#20bf6b'>easier compared to the other 2</span>

Let $A$ be a **square matrix**, it is <span style='color:#0fb9b1'>orthogonally diagonalisable</span> if there exist an orthogonal matrix $P$ such that $P^{-1} A P = P^{T} A P = D$ .

However for this to be true, $A$ <span style='color:#f7b731'>must</span> also be a <span style='color:#0fb9b1'>symmetric matrix</span>.
- $P^{T} A P = D$, here $D$ is a symmetric matrix
- $D = D^{T} = (P^{T}AP)^{T} = P^{T}A^{T}P$
- Thus $A = A^{T}$

And therefore, $A$ <span style='color:#fa8231'>since it is a symmetric matrix</span> :
- Its eigenvalues $\lambda_{1} \dots \lambda_{k}$ are all **real numbers**
- For each eigenvalue of A, $a(\lambda) = g(\lambda) = dim(E_{\lambda})$.
- The eigenvectors associated to distinct eigenvalues are orthogonal to one another.
<div style="page-break-after: always;"></div>

**Steps to get $P$ an orthogonally diagonalisable matrix**
1) $A$ <b><mark style='background:#f7b731'>must be a symmetric matrix</mark></b> of order $n$
2) Solve for $det(\lambda I - A) = 0$ to find all the eigenvalues of $A$
3) For each eigenvalue ($\lambda_{i}$) of $A$
	- Find the eigenspace using the equation $(\lambda_{i} I - A) = 0$ which will be a basis $(S_{i})$ 
	- Using the [[Orthogonality#Gram-Schmidt Process|Gram-Schmidt process]] to convert $S_{i}$ into an <span style='color:#f7b731'>orthonormal</span> basis $T_{i}$
4) Lastly combine all the $T_{i} \dots T_{n}$ which will be $\{w_{1}, w_{2}, \dots, w_{k}\}$ which is an orthonormal basis for $\Bbb{R}^{n}$
5) And this basis call it $P$ which is a <span style='color:var(--mk-color-yellow)'>orthogonal matrix</span> will orthogonally diagonalise $A$

# Single Value Decomposition
---
This method is to find a <span style='color:var(--mk-color-yellow)'>close estimate for a diagonalisable matrix for non square matrices</span>.

$A$ can be **any matrix** of size $m \times n$ and $A^{T}A$ <span style='color:var(--mk-color-yellow)'>will be a symmetric matrix</span> of order $n$, which can be diagonalisable.

The **eigenvalues** for $A^{T}A$ are <span style='color:var(--mk-color-yellow)'>nonnegative</span> and because of this, if <span style='color:var(--mk-color-orange)'>every eigenvalue is square rooted</span>, then this value is called the <span style='color:var(--mk-color-turquoise)'>singular values</span> of $A$, $\sigma_{i} = \sqrt{\lambda_{i}}$.

**Doing the decomposition**
- $A$ be any $m \times n$ matrix
- **Find the eigenvalues** for $A^{T}A$, and arrange them in<span style='color:var(--mk-color-yellow)'> descending order</span>. Afterwards find the <span style='color:var(--mk-color-yellow)'>orthonormal set</span>, denoted as $V = \{w_{i}, \dots, w_{n}\}$
- Get the <span style='color:var(--mk-color-turquoise)'>singular values</span> such that $\sigma_{i} = \sqrt{\lambda_{i}}$ and $u_{i} = \frac{1}{\sigma_{i}} Aw_{i}$, for <span style='color:var(--mk-color-yellow)'>all positive eigenvalues</span> $\lambda_{i} \gt 0$.
- The resulting $U = \{u_{1}, \dots, u_{r}\}$ is an orthonormal set and <span style='color:var(--mk-color-yellow)'>extended to be a orthornormal basis</span> for $\Bbb{R}^{m}$ and this matrix $U$ <span style='color:var(--mk-color-yellow)'>can give</span> the <span style='color:var(--mk-color-yellow)'>rank</span> for $A$.
	- After extending need to normalise the vectors added using the [[Orthogonality#Gram-Schmidt Process|Gram-Schmidt process]]
-  Afterwards form the $\Sigma$ matrix which <span style='color:var(--mk-color-yellow)'>uses the singular values</span>

![[Forming the Sigma Matrix.png|center|]]

The main goal is to view $AV = U\Sigma$ which can be converted into, $\Sigma = U^{T}AV$ or $A = U\Sigma V^{T}$ 
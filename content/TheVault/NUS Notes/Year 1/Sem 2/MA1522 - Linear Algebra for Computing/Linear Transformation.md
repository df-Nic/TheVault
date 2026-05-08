---
title: Linear Transformation
Date Created: 2024-04-25
Last Updated: 2025-09-27
tags:
  - MA1522
  - Math
  - Vectors
---
# Transforming from $\Bbb{R}^{n}$ to $\Bbb{R}^{m}$
---
A **linear equation** is usually in the form of $a_{1}x_{1} + a_{2}x_{2} + \dots + a_{n}x_{n} = b$, where $a_{i}$ are <span style='color:var(--mk-color-turquoise)'>constants</span> and $x_{i}$ are <span style='color:var(--mk-color-turquoise)'>variables</span>.

This can be visualised as a<span style='color:var(--mk-color-yellow)'> function or mapping</span> denoted by $f : \Bbb{R}^{n} \to \Bbb{R}$ or a <span style='color:var(--mk-color-turquoise)'>linear transformation</span> from $\Bbb{R}^{n}$ to $\Bbb{R}$.
- This is just $f(x_{1}, \dots, x_{n}) = a_{1}x_{1} + a_{2}x_{2} + \dots + a_{n}x_{n}$

In the <span style='color:var(--mk-color-orange)'>matrix form</span> it will look like :
$$f\left(
\begin{pmatrix}
    x_{1} \\
    x_{2} \\
    \vdots \\
    x_{n} \\
\end{pmatrix}\right)
= \begin{pmatrix}
    a_{1} & a_{2} & \dots & a_{n} \\
\end{pmatrix}
\begin{pmatrix}
    x_{1} \\
    x_{2} \\
    \vdots \\
    x_{n} \\
\end{pmatrix}
$$
**The vectors are viewed as column vectors**

What if a <span style='color:var(--mk-color-orange)'>linear system</span> is given, which is a **collection of linear equations**, then the mapping is denoted by $T : \Bbb{R}^{n} \to \Bbb{R}^{m}$ :
$$
T\left(
\begin{pmatrix}
    x_{1} \\
    x_{2} \\
    \vdots \\
    x_{n} \\
\end{pmatrix}\right)
=\begin{pmatrix}
    a_{11} & a_{12} & \dots & a_{1n} \\
    \vdots & \vdots & \vdots & \vdots \\
    a_{m1} & + a_{m2} & \dots & a_{mn} \\
\end{pmatrix}
\begin{pmatrix}
    x_{1} \\
    x_{2} \\
    \vdots \\
    x_{n} \\
\end{pmatrix}
$$
This is a <span style='color:var(--mk-color-turquoise)'>linear transformation</span> from $\Bbb{R}^{n}$ to $\Bbb{R}^m$ and if $n = m$ then $T$ is known as a <span style='color:var(--mk-color-turquoise)'>linear operator</span>. And $T(x) = Ax$

Let $A$ to be the $(a_{ij})_{m \times n}$ matrix (**Middle one**), As long as $T(x)$ can be written as $Ax$ then <span style='color:var(--mk-color-yellow)'>it is a linear transformation</span>.
- A is then called the <span style='color:var(--mk-color-turquoise)'>standard matrix</span> for $T$.

A special linear operator called the <span style='color:var(--mk-color-teal)'>identity operator</span> if a transformation from $\Bbb{R}^{n} \to \Bbb{R}^{n}$, which is denoted as $I(x) = x = I_{n}x$.

Given T : $\Bbb{R}^{n} \to \Bbb{R}^{m}$, which means the <span style='color:var(--mk-color-yellow)'>input is a vector of size</span> $n \times 1$. therefore to satisfy $T(x) = Ax$, $A$ must have a column size of $n$ and the output is of size $m$, thus $A$ must have a row size of $m$, thus $A_{m \times n}$.

A special transformation called the <span style='color:var(--mk-color-teal)'>zero transofrmation</span>, which is denoted as $O(x) = 0 = 0_{m \times n}x$.

The <span style='color:var(--mk-color-turquoise)'>uniqueness</span> of the <span style='color:var(--mk-color-yellow)'>standard matrix</span> means that for any $T : \Bbb{R}^{n} \to \Bbb{R}^{m}$ can the <span style='color:var(--mk-color-yellow)'>standard matrix be represented by more than 1 different matrix</span>, such that :
- $T(x) = Ax$
- $T(x)= Bx$
## Finding Uniqueness

In the **matrix form**, the <b><mark style='background:var(--mk-color-yellow)'>standard matrix must be unique</mark></b> for it to **be a linear transformation**,

Given $T : \Bbb{R}^{n} \to \Bbb{R}^{m}$, and **assume** that the <span style='color:var(--mk-color-red)'>standard matrix is not unique</span>.
- Thus $T(x) = Ax = Bx, \forall x \in \Bbb{R}^{n}$
- Then $Ax - Bx = (A - B) x = 0, \forall x \in \Bbb{R}^n$ 
- Then <span style='color:var(--mk-color-yellow)'>null space</span> of $(A - B)$ is $\Bbb{R}^{n}$
- Then the <span style='color:var(--mk-color-yellow)'>nullity</span> of $(A - B)$ = dim($\Bbb{R}^n$) = n
- Then the <span style='color:var(--mk-color-yellow)'>rank will be 0</span> and therefore $A - B = 0$ and then, $A = B$ 

**Alternatively**, proving uniqueness can be done <span style='color:var(--mk-color-yellow)'>using the standard vectors</span> which is the $\{e_{1}, e_{2}, \dots, e_{n}\}$.

Now $A = (Ae_{1}, \dots, Ae_{n}) = (Be_{1}, \dots, Be_{n}) = B$ and <span style='color:var(--mk-color-green)'>if this is true</span>, then it is <span style='color:var(--mk-color-yellow)'>unique</span>.
### Linearity

Before finding the standard matrix, <b><mark style='background:var(--mk-color-yellow)'>first determine of if the function is linear</mark></b>.

For a <span style='color:var(--mk-color-orange)'>transformation to be linear</span> it must <span style='color:var(--mk-color-yellow)'>hold true for all of the following cases</span> :
- $T(0_{n}) = A0_{n} = 0_{m}$
- $T(cv)= A(cv) = cT(v)$, bringing the scalar constant out will not affect the result
- $T(u + v) = A(u + v) = Au + Av = T(u) + T(v)$, this is the **distributive law**
- As the result of points 2 and 3, $T(c_{1}v_{1} + \dots + c_{n}v_{n}) = c_{1}T(v_{1}) + \dots + c_{n}T(v_{n})$.

These **must hold for all** $v \in \Bbb{R}^{n}$

However **if standard matrix** $A$ <span style='color:var(--mk-color-yellow)'>can be found</span> such that $T(v) = Av$, then it is **linear**.

Now the <span style='color:var(--mk-color-yellow)'>standard vectors</span> are a basis of $\Bbb{R}^{n}$, therefore, linearity depends on $T(e_{1}) \dots T(e_{n})$. Thus, the set of the standard vectors gives an identity matrix, thus $A = AI = (T(e_{1}), \dots, T(e_{n}))$, this means that $T(e_{i})$ is the $i$th column of $A$. If $T$ is <span style='color:var(--mk-color-yellow)'>given to be linear</span>.
## Finding the Standard Matrix

Only <span style='color:var(--mk-color-yellow)'>find the standard matrix if function is linear</span>, if not do not.

**Using the standard vectors**
![[Using Standard Vectors to form the Standard Matrix.png|center|500]]

<div style="page-break-after: always;"></div>

**Using other vectors**
![[Using Any Vectors to Form the Standard Matrix.png|center|]]

As long as the <span style='color:var(--mk-color-yellow)'>given vertices forms a basis</span> of $\Bbb{R}^{n}$, then it is sufficient to find the standard matrix $A$ because it will work for every vertices in $\Bbb{R}^{n}$.
### Change of Bases

Let $S$ be a basis for $\Bbb{R}^{n}$, thus for all $v \in \Bbb{R}^{n}$ it can be expressed as it <span style='color:var(--mk-color-yellow)'>coordinate vector</span>.
- $v = c_{1}v_{1} + \dots + c_{n}v_{n} = (v_{1} \dots v_{n})[v]s = P[v]s$

Let $T$ be some <span style='color:var(--mk-color-yellow)'>linear transformation</span>, then $T(v) = (T(v_{1}) \dots T(v_{n}))[v]s = B[v]s$. Let $A$ be the standard matrix to $T$

Then $B[v]s = T(v) = Av = AP[v]s$, therefore it can be <span style='color:var(--mk-color-yellow)'>concluded</span> that $B = AP$ equivalently $A = BP^{-1}$.

This will only apply if all possible inputs to the function (**images**) for a <span style='color:var(--mk-color-yellow)'>bases</span> of $\Bbb{R}^{n}$.

**Example of doing change of bases**
![[Change of Bases Example.png|center|500]]

This is a <span style='color:var(--mk-color-green)'>faster way to find the standard matrix</span> $A$. And this $P$ is the transition matrix from $E$ to $S$.

Let $T : \Bbb{R}^{n} \to \Bbb{R}^{n}$, let $A$ be the <span style='color:var(--mk-color-yellow)'>transition matrix </span>for $T$ and it is a **square matrix**. Let $S$ be any basis for $\Bbb{R}^{n}$, then if $P$ is all the vectors in $S$ then it is <span style='color:var(--mk-color-yellow)'>invertible</span> and also $v = P[u]s$.

Then $T(v) = P[T(v)]s$ and $Av = AP[v]s$, therefore,$T[v]s = P^{-1}AP[v]s$ which is <span style='color:var(--mk-color-yellow)'>diagonalisable</span>. If so then $T : v[s] \to B[v]s$, where $B = P^{-1}AP$.

Thus $A$ and $B$ are <span style='color:var(--mk-color-turquoise)'>similar</span>. And if a square matrix is <span style='color:var(--mk-color-yellow)'>diagonalisable then it is similar to a diagonal matrix</span>.

![[Change of Bases using Diagonalization.png|center|300]]

# Composition
---
Given 2 functions $f : X \to Y$ and $g : Y \to Z$, then $g \circ f : X \to Z$. In simpler terms $g \circ f = g(f(x))$.

Now in <span style='color:var(--mk-color-orange)'>terms</span> of matrices and <span style='color:var(--mk-color-orange)'>linear transformations</span>, let $S : \Bbb{R}^{n} \to \Bbb{R}^{m}$ and $T : \Bbb{R}^{m} \to \Bbb{R}^{k}$. Then the <span style='color:var(--mk-color-turquoise)'>composition</span> of $T$ with $S$ is given as such $(T \circ S)(u) = T(S(u))$.

$T \circ S \neq S \circ T$.

**Finding the standard matrix for a composite function**
![[Finding the Standard Matrix for a Composite Function.png|center|300]]

Is there a <span style='color:var(--mk-color-orange)'>faster way</span>, besides subbing in, Given 2 functions $T$ and $S$. And let $A$ and $B$ be the standard matrix for functions $T$ and $S$ respectively. 

Then the standard matrix for $T \circ S$ is the matrix multiplication of $BA$.
# Ranges and Kernels
---
**Range**
>Is <span style='color:var(--mk-color-yellow)'>all possible images/outputs</span> that can be output from the function $T$.

Thus the <span style='color:var(--mk-color-turquoise)'>range</span> can be denoted as $R(T) = \{T(v) \vert v \in \Bbb{R}^{n}\} = span\{T(v_{1}), \dots, T(v_{n})\}$.
> Where ${v_{1}, v_{2}, \dots, v_{n}}$ is <span style='color:var(--mk-color-yellow)'>any basis</span> for $\Bbb{R}^{n}$

And if the basis <span style='color:var(--mk-color-yellow)'>consists of only the standard vectors</span>, then $R(T)$ is the column space of $A$.

The <span style='color:var(--mk-color-yellow)'>rank</span> of $T$ is the $dim(R(T))$, which is just the rank of $A$ the **standard matrix**. 

**Finding the rank of $T$**
![[Finding the Rank of a Linear Transformation.png|center|400]]

**Kernel**
>It is a set of <span style='color:var(--mk-color-yellow)'>vectors whose image/output is the zero vector</span>. This should also **include the zero vector itself**.

Thus the <span style='color:var(--mk-color-turquoise)'>kernel</span> can be denoted as $Ker(T) = \{v \in \Bbb{R}^{n} \vert T(v) = 0\}$ which is a $\subseteq \Bbb{R]^{n}}$.

Then the $Ker(T)$ is just the null space of $A$, thus with this $nullity(T) = dim(Ker(T)) = nullity(A)$.

**Finding the kernel of a linear transformation**
![[Finding the Kernel of a Linear Transformation.png|center|600]]


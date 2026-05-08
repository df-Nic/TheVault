---
title: Orthogonality
Date Created: 2024-03-21
Last Updated: 2025-09-27
tags:
  - MA1522
  - Math
  - Vectors
---
# Dot Product
---
<span style='color:#0fb9b1'>Orthogonal</span>, it is another word for perpendicular, 2 lines intersect at a **90 degree angle**.

From the <span style='color:#2d98da'>Pythagoras theorem</span>, comes about the <span style='color:#0fb9b1'>cosine rule</span>, which is the more generalised form :
$$
C^{2} = A^{2} + B^{2} - 2AB\cos{\theta}
$$
The <span style='color:#0fb9b1'>dot product</span> is given as such, let $u$ and $v$ be some <span style='color:#fa8231'>vector</span> :
$$
u \cdot v = u_{1}v_{1} + u_{2}v_{2} + \dots + u_{n}v_{n}
$$
This <span style='color:#0fb9b1'>dot product</span> will give us a number.

And from the <span style='color:#fa8231'>cosine rule</span> 
$$
\theta = \cos{}^{-1}(\frac{u \cdot v}{\Vert x \Vert \times \Vert v \Vert})
$$
**Properties :**
- $\Vert u \Vert = \sqrt{u \cdot u}$, this is the length also known as <span style='color:#0fb9b1'>norm</span>
- If $u$ and $v$ = 0 then, it is <span style='color:#0fb9b1'>orthogonal</span>
- $-1 \le \frac{u \cdot v}{\Vert x \Vert \times \Vert v \Vert} \le 1 \iff \vert u \cdot v\vert \le \Vert u \Vert \Vert v \Vert$
- $u \cdot v = (v_{1}, v_{2}) \times (u_{1}, u_{2}) = uv^{T}$ (**Note that the middle is a matrix multiplication**)
- $v \cdot v \ge 0$ (**Important**)
- $\Vert cv \Vert$ where $c$ is some constant can be written as $\vert c \vert \Vert v \Vert$
- $\vert u \cdot v \vert \le \Vert u \Vert \Vert v \Vert$
- $\Vert u + v \Vert \le \Vert u \Vert  + \Vert v \Vert$ (This is known as the <span style='color:#2d98da'>triangular inequality</span>)
- $d(u,w) \le d(u,v) + d(v,w)$

Let $v$ be some matrix and $\Vert v \Vert = \sqrt{v_{1}^{2} + \dots + v_{n}^{2}}$ .

If this $\Vert v \Vert = 1$, then $v$ is <span style='color:#f7b731'>called a unit vector</span>.

The distance between 2 vectors is given as such $\Vert u - v \Vert$.

In terms of [[Matrices#Matrix Multiplication|matrix multiplication]], it can also be achieved through the <span style='color:#0fb9b1'>dot product</span>, the $(i,j)$ entry in the resulting matrix $AB$ for example is just the dot product of $a_{i} \cdot b_{j}$.

The dot product is <span style='color:#eb3b5a'>not commutative</span> but it <span style='color:#20bf6b'>is distributive</span>.
<div style="page-break-after: always;"></div>

# Orthogonality
---
As mentioned above **given 2 vectors** in $\Bbb{R}^{n}$, if their <span style='color:#f7b731'>dot product is 0</span>, $u \cdot v = 0$, then the <span style='color:#f7b731'>angle</span> between the 2 vectors is <span style='color:#f7b731'>90 degrees</span>, which means they are <span style='color:#0fb9b1'>orthogonal</span>.

**Formal Definition :** $u \perp v$ if $u \cdot v = 0$ and $u,v \in \Bbb{R}^n$.

If either $u$ or $v$ is a <span style='color:#f7b731'>zero vector</span>, then this <b><mark style='background:#f7b731'>zero vector is orthogonal to every vector</mark></b> in $\Bbb{R}^{n}$.

This <span style='color:#fa8231'>can be extended</span> to a collection of vectors or it is known as a <span style='color:#fa8231'>subset</span> of $\Bbb{R}^{n}$. Let $S$ be this subset and for it to be <span style='color:#0fb9b1'>orthogonal</span>, <b><mark style='background:#f7b731'>every distinct pair of vectors must be orthogonal</mark></b>, $v_{i} \cdot v_{j} = 0, i \neq j$.

There is also another term called <span style='color:#0fb9b1'>orthonormal</span>, where it is <span style='color:#f7b731'>orthogonal</span> and <span style='color:#f7b731'>every vector is a unit vector</span>.

**Properties :**
- $S$ is **orthonormal** then it is also orthogonal
- $S$ is **orthogonal** then its subset is also orthogonal
- $S$ is **orthonormal** then its subset is also orthonormal
- Adding the zero vector, will retain the orthogonal status.
- If $S$ is **orthonormal**, then $0 \notin S$ 

When <span style='color:#fa8231'>orthogonal is more useful</span>, is to find the coefficient vector to find the linear combination for a vector $w$.

Then $(w)_{S} = (w \cdot v_{1}, \dots, w \cdot v_{n})$

**For example :**
- Let $w \in V = Span(S)$ where $S$ is **orthogonal** and $S = \{v_{1}, v_{2}\}$. 
- Let $w = (x,y) \in \Bbb{R}^{2}$
- Then $(w)_{S} = (w \cdot v_{1}, w \cdot v_{2})$
## Normalizing

It is a process of converting a <span style='color:#f7b731'>orthogonal set of vertices into a orthonormal set</span>. To do this it is simple :

Let $S = \{u_{1}, u_{2}, \dots, u_{n}\}$

Then create a new subset called $T$ where it will contain the following :
$$T =\{\frac{u_{1}}{\Vert u_{1} \Vert}, \frac{u_{2}}{\Vert u_{2} \Vert}, \dots, \frac{u_{n}}{\Vert u_{n} \Vert}\}$$
**Where :**
- If $u_{1} = (1, 2, 2, -1)$ and $\Vert u_{1} \Vert = \sqrt{10}$
- Then $\frac{u_{1}}{\Vert u_{1} \Vert} = (\frac{1}{\sqrt{10}}, \frac{2}{\sqrt{10}}, \frac{2}{\sqrt{10}}, \frac{-1}{\sqrt{10}})$

Thus $T$ is now <span style='color:#0fb9b1'>orthonormal</span>.
<div style="page-break-after: always;"></div>

**Properties**
- If $A$ is <span style='color:#0fb9b1'>orthogonal</span>, then $A^{T}A$ is a <span style='color:#f7b731'>diagonal matrix</span> (Columns)
- If $A$ is <span style='color:#0fb9b1'>orthonormal</span>, then $A^{T}A$ is a <span style='color:#f7b731'>identity matrix</span> (Columns)
- If $A$ <span style='color:#f7b731'>does not contain zero vectors</span>, then if it is <span style='color:#0fb9b1'>orthogonal</span> then $A$ is linear independent. If it is <span style='color:#0fb9b1'>orthonormal</span> the it will be linearly independent. The term for this is called <b><span style='color:#0fb9b1'>orthogonal / orthonormal basis</span></b>

If $A = (u_{1}, u_{2}, \dots, u_{n})$ which is a subset of $\Bbb{R}^{n}$. Notice that the <span style='color:#f7b731'>number of vectors coincides with the space</span>. Thus the following can be concluded :
- If $A^{T}A = I_{n}$ then $A$ is <span style='color:#f7b731'>orthonormal and it is also invertible</span> (Since it is a square matrix) 
- And $A$ is a basis for $\Bbb{R}^{n}$

## Finding A Orthogonal Vector

Lets make $u$ some vector and $V$ be some subspace of $\Bbb{R}^{n}$, if, for all $v \in V$ such that $u \cdot v = 0$, then $u$ is known to be the <span style='color:#0fb9b1'>normal vector</span> <span style='color:#f7b731'>of the plane V</span>.

Then $V$ can be rewritten as $V = \{ v \in \Bbb{R}^{n} \vert v \cdot u = 0\}$.

**How to Find Orthogonal Vectors**
![[Finding the Set of Orthogonal Vectors.png|center|400]]
<div style="page-break-after: always;"></div>

# Projection
---
**What is a Projection?**
![[Projection Visualisation.png|center|200]]

Denote the <span style='color:#0fb9b1'>projection</span> as $p$, then : $$p = \left(\frac{u \cdot v}{\Vert u \Vert \Vert v \Vert}\right)\times v$$
 And if $v$ is a <span style='color:#f7b731'>unit vector</span>, then $p = (u \cdot v)v$.

Remember <span style='color:#2d98da'>vector addition</span>, thus $u = p + n$ and $n$ is <b><mark style='background:#f7b731'>orthogonal to the plane</mark></b>.

Now given a <b><span style='color:#fa8231'>orthogonal basis</span></b>, how to find a <span style='color:#f7b731'>projection of a vector</span> ($w$) onto a given the vector space $V$ :
$$
p = (\frac{w \cdot v_{1}}{\Vert v_{1} \Vert^{2}})v_{1} + (\frac{w \cdot v_{2}}{\Vert v_{2} \Vert^{2}})v_{2} + \dots + (\frac{w \cdot v_{n}}{\Vert v_{n} \Vert^{2}})v_{n}
$$
**Where :**
- $v_{i}$ is a vector in the vector space $V$
- $w$ is a **vector to be projected on**

## Gram-Schmidt Process

Given a set of vectors $S$ which is a <span style='color:var(--mk-color-orange)'>basis</span> for $T$, then $S$ is an <span style='color:var(--mk-color-yellow)'>orthogonal basis if all of their dot products are 0</span>.

Is there a way to<span style='color:#fa8231'> find a orthogonal basis given any vector space</span>.

For dimension $= 1$, **any basis is orthogonal**.

For dimension 2, know that the vector $v_{2} - p$ where $p$ is the projection of $v_{2}$ onto $v_{1}$ is <b><mark style='background:#f7b731'>always orthogonal</mark></b>. Assuming that $v_{2}- p \neq 0$ as this means they are parallel.

Therefore if $\{v_{1}, v_{2}\}$ is a basis for $V$, then $\{v_{1}, v_{2} - p\}$ is an <span style='color:#f7b731'>orthogonal basis</span> for $V$.

How about given $\{u_{1}, u_{2}, \dots, u_{n}\}$, to <span style='color:#fa8231'>find the orthogonal basis</span>, do the following
- $v_{1} = u_{1}$
- $v_{2} = u_{2} - \left(\frac{u_{2} \cdot v_{1}}{\Vert v_{1} \Vert^{2}}\right)v_{1}$
- $v_{3} = u_{3} - \left(\frac{u_{3} \cdot v_{1}}{\Vert v_{1} \Vert^{2}}\right)v_{1} - \left(\frac{u_{3} \cdot v_{2}}{\Vert v_{2} \Vert^{2}}\right)v_{2}$
- $v_{k} = u_{k} - \left(\frac{u_{k} \cdot v_{1}}{\Vert v_{1} \Vert^{2}}\right)v_{1} - \left(\frac{u_{k} \cdot v_{2}}{\Vert v_{2} \Vert^{2}}\right)v_{2} \dots \left(\frac{u_{k} \cdot v_{k-1}}{\Vert v_{k-1} \Vert^{2}}\right)v_{k-1}$ 

Then $\{v_{1}, v_{2}, \dots, v_{k}\}$ <span style='color:#f7b731'>will be an orthogonal basis</span> for $V$. Then what about an orthonormal basis.

Then same as before but for each $v_{i}$, $w_{i} = \frac{v_{i}}{\Vert v_{i} \Vert}$ for all $v \in \{v_{1}, v_{2}, \dots, v_{k}\}$. Thus the result $\{w_{1}, w_{2}, \dots, w_{k}\}$ is a <span style='color:#f7b731'>orthonormal basis</span> for $V$.

If the goal is to find a vector such that $S$ is an orthogonal basis for $\Bbb{R}^{n}$, instead of going into REF, can try an error with $\{e_{1}, e_{2}, \dots, e_{n}\}$.

# Best Approximations
---
So what is the <span style='color:#fa8231'>purpose of the the projection</span>, it is to find the <span style='color:#f7b731'>shortest distance a particular vector</span>.

![[Purpose of the Projection.png|center|300]]

From the image it is observed that $d(u,p) \le d(u,v) \forall v \in V$. ($d(u,p)$ is read as distance from $p$ to $u$).

If $d(u,p) = d(u,v)$, then $v = p$.

This means that no matter what vector is picked, the projection of $u$ <span style='color:#f7b731'>will always be the shortest</span>. Which is <span style='color:#fa8231'>also called</span> the <span style='color:#0fb9b1'>best approximation</span> of $u$ in $V$.

**How to find the Shortest Distance**
![[Finding the Shortest Distance.png|center|400]]

## Least Squares Solution

Let $A$ be a matrix and the linear system $Ax = b$ is <span style='color:#f7b731'>inconsistent</span>. The goal is to find $x$ such that $Ax$ is <span style='color:#f7b731'>closest</span> to $b$, meaning $\color {#f7b731} {\Vert Ax - b \Vert}$ is <span style='color:#f7b731'>minimised</span>.

The solution $x$ is known as the <span style='color:#0fb9b1'>least square solution</span>. This simply means $Ax = p$ which is the projection of $b$ onto $V$, where $V$ is the <span style='color:#f7b731'>column space</span> of $A$ such that $V = \{Ax \vert x \in \Bbb{R}^n\}$.

Then what if $Ax = b$ is <span style='color:#f7b731'>consistent</span>, then the <span style='color:#0fb9b1'>least square solution</span> is <span style='color:#f7b731'>all the solutions to the equation</span>.

**Example :**
![[Example of Finding the Least Squares Solution.png|center|400]]

How about a <span style='color:#fa8231'>faster way</span>. If $u$ is a least square solution to $Ax = b$, then $u$ is a <span style='color:#f7b731'>solution to</span> $\color {#f7b731} {A^{T}Ax = A^{T}b}$.

**Example :**
![[Using REF to Find the Least Square Solution.png|center|400]]

Now both $Ax = p$ and $A^{T}Ax = A^{T}b$ <span style='color:#f7b731'>are both consistent</span>.

Thus if $u$ is a solution to $A^{T}Ax = A^{T}b$, then $Au$ <b><mark style='background:#f7b731'>will be the projection</mark></b>.

It is possible that there are <span style='color:#fa8231'>infinitely many points closest</span> to $b$. But just need to sub in a random variable to get the <span style='color:#f7b731'>projection which is unique</span>.
## QR Decomposition

Let $A$ is a $m \times n$ matrix whose <span style='color:#f7b731'>columns are linearly independent</span>. Then :
- There is a $m \times n$ matrix $Q$ such that its columns forms an <span style='color:#f7b731'>orthonormal</span> set
- And there is a <span style='color:#f7b731'>invertible upper triangular matrix</span> $R$ of order $n$

Such that $A = QR$.

So how to find $Q$ and $R$ given $A = (u_{1}, u_{2}, \dots, u_{n})$
1) Use the <span style='color:#2d98da'>Gram-Schmidt process</span> and find the <b><mark style='background:#f7b731'>orthonormal basis for the column space</mark></b>, $(w_{1}, w_{2}, \dots, w_{n})$.
2) $Q = (w_{1}, w_{2}, \dots, w_{n})$, which are <span style='color:#f7b731'>column vectors</span> and extend to $\Bbb{R}^{n}$
3) Form the upper triangular matrix $R$, where every $i,j$ entry, the value will be $w_{i} \cdot u_{j}$ 

Anything below the diagonal will be 0, since $w_{i} \cdot u_{j} = 0$ since it is orthogonal to $A$.

Now what if $A$ is <span style='color:#f7b731'>not independent</span>, then the same process can be applied but during the <span style='color:#2d98da'>Gram-Schmidt process</span>, <span style='color:#f7b731'>any 0 vector will be ignored</span>.

If so then is is possible that the resulting vectors might not span the $\Bbb{R}^{n}$, the fastest way is to use the $e_{k}$ vector <span style='color:#f7b731'>minus the projection</span> and it should not be a 0 matrix. Afterwards do the QR decomposition.
### Applications of QR Decomposition

Now recall that using the <span style='color:#f7b731'>least square solution</span>, it is possible to find the vector closest to $b$, given the equation $Ax = b$ which is inconsistent (Actually it does not matter).

Now from the QR decomposition, it is known that $A = QR$ and thus $QRx = b$ which can be simplified into $\color {#f7b731} {Rx = Q^{T}b}$ which is <span style='color:#f7b731'>now consistent</span> and its <span style='color:#f7b731'>solution is a unique least square solution</span>.

# Orthogonal Matrices
---
Let $A$ be a <span style='color:#f7b731'>square matrix</span>. Then $A$ is a <span style='color:#0fb9b1'>orthogonal matrix</span> if $A^{T}A = I$.

This is equivalent to :
- $A^{-1} = A^{T}$, which means $A^{-1}$ is also an <span style='color:#0fb9b1'>orthogonal matrix</span>
- $A^{T}A = I$

This will <span style='color:#fa8231'>not always work</span> if $A$ is <span style='color:#eb3b5a'>not a square matrix</span>.

Thus an **identity matrix is an orthogonal matrix**.

This also works with matrix multiplication, $(AB)^{T}(AB) = B^{T}A^{T}AB = B^{T}B = I$. If this is the case then $AB$ is a <span style='color:#0fb9b1'>orthogonal matrix</span>.

Another property is that let $S \{v_{1}, \dots, v_{k}\} \subseteq \Bbb{R}^{n}$ and let $A = (v_{1}, \dots, v_{k})$. Notice that $S$ is a <span style='color:#f7b731'>set</span> while $A$ is a <span style='color:#f7b731'>matrix</span>.

If $k = n$ and $A^{T}A = I_{n}$ then $A$ is <span style='color:#f7b731'>orthogonal matrix</span> and $S$ is a <b><mark style='background:#f7b731'>orthonormal basis</mark></b> for $\Bbb{R}^{n}$. If it is not use the $e_{i}$ vectors to make it an orthonormal basis.

If it is known that $S$ is a <span style='color:#f7b731'>orthonormal</span> set in $\Bbb{R}^{n}$ and $A$ is a <span style='color:#f7b731'>orthogonal matrix</span> of order $n$, then $AS$ will be an <span style='color:#f7b731'>orthonormal set of vectors</span>.

Thus in <span style='color:#fa8231'>general</span> :
- Let $A$ be a $m \times n$ matrix
- If $A^{T}A = I_{n}$ then the <span style='color:#f7b731'>columns</span> of $A$ form an orthonormal basis in $\Bbb{R}^{m}$
- If $AA^{T} = I_{m}$ then the <span style='color:#f7b731'>rows</span> of $A$ form an orthonormal basis in $\Bbb{R}^{n}$
- And if $n = m$ and <span style='color:#f7b731'>both are true</span>, then $A$ is a orthogonal matrix

<div style="page-break-after: always;"></div>

## Transition Matrix Between 2 Orthonormal Bases

If, $S$ and $T$ are <span style='color:#fa8231'>2 orthonormal bases</span>, then the <span style='color:#f7b731'>transition matrix is an orthogonal matrix</span>.

Let $A$ and $B$ be the matrices of the 2 bases for $S$ and $T$ respectively, then
- $P = B^{T}A$ is the **transition matrix** from $S$ to $T$
- $Q = A^{T}B$ is the **transition matrix** from $T$ to $S$

If $P$ is found then a faster way to get the transition matrix from $T$ to $S$ is just $P^{T}$ or $P^{-1}$.

## Uses of Orthogonal Matrices

**With the transaction matrix** of an orthogonal vector, a point can be expressed as point $P'$ with its <span style='color:#f7b731'>axis as the vectors in the matrix</span>.

![[Expressing a Point where the Axis are Vectors.png|center|400]]

**A rotation about an angle $\theta$** can also be done **with the transition matrix**

![[Rotation of a Point Using the Transition Matrix.png|center|400]]

Let $\alpha$ and $\beta$ be 2 fixed angles. Then $P_{\beta}P_{\alpha}u$ is <span style='color:#f7b731'>the same as</span> $P_{\alpha + \beta}u$.
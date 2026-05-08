---
title: Matrices
Date Created: 2024-01-31
Last Updated: 2025-09-27
tags:
  - MA1522
  - Math
  - Matrices
---
# What are Matrices
---
It is just a rectangular array of numbers in the form of :
$$
  A = 
  \begin{pmatrix}
    a_{11} & a_{12} & \dots & a_{1n} \\ 
    a_{21} & a_{22} & \dots & a_{2n} \\
    \vdots & \vdots &       & \vdots \\
    a_{n1} & b_{n2} & \dots & a_{mn}  
   \end{pmatrix}
$$

**Where :**
- $m$ is the <span style='color:#f7b731'>row</span>
- $n$ is the <span style='color:#f7b731'>column</span>
- <span style='color:#f7b731'>Size</span> = $m \times n$
- ($i, j$) - entry is the entry in the i-th row and j-th column

A matrix is <span style='color:#f7b731'>denoted by capital letters</span>, and to <span style='color:#fa8231'>access an item</span> it will be denoted as $A = (a_{ij})_{m\times n}$ or $A = (a_{ij})$.
## Types of Matrices

<span style='color:#0fb9b1'>Row matrix</span> (Row vector), is a matrix with only 1 row.

<span style='color:#0fb9b1'>Column matrix</span> (Column vector), is a matrix with only 1 column.

<span style='color:#0fb9b1'>Square matrix</span> (Order $n$), is a matrix with the same number of rows and columns ($n \times n$).
> The <span style='color:#0fb9b1'>diagonal</span> <span style='color:#f7b731'>for a square matrix </span>consisting of <span style='color:#0fb9b1'>diagonal entries </span>, $a_{ij}, i = j$, else it is called a <span style='color:#0fb9b1'>non-diagonal entry</span>. It is also known as the principle / major diagonal, while the diagonal from top right to bottom left is called anti / minor diagonal.

<span style='color:#0fb9b1'>Diagonal matrix</span>, a <span style='color:#f7b731'>subtype of a square matrix</span> where only its <mark style='background:#f7b731'>diagonal entries are non-zero</mark> while the rest are all 0. Which are <mark style='background:#0fb9b1'>both lower and upper triangular</mark>.

<span style='color:#0fb9b1'>Scalar matrix</span>, a <span style='color:#f7b731'>subtype of a diagonal matrix</span>, which additionally requires <mark style='background:#f7b731'>all diagonal entries to be of a same constant</mark> $c$.

<span style='color:#0fb9b1'>Identity matrix</span>, it is denoted by $I_{n}$, where instead of a constant, <mark style='background:#f7b731'>all diagonal entries are of value 1</mark>.

<span style='color:#0fb9b1'>Zero matrix</span>, denoted by $0_{m \times n}$ or $O_{m \times n}$, where all values in the <span style='color:#f7b731'>matrix are all 0</span>. This is also known as the <span style='color:#0fb9b1'>additive identity</span>.

<span style='color:#0fb9b1'>Symmetric matrix</span>, which is a <span style='color:#f7b731'>subtype of a square matrix</span> is where $A_{ij} = A_{ji} \ \forall i,j$. 

<span style='color:#0fb9b1'>Upper triangular</span>, another <span style='color:#f7b731'>subtype of a square matrix</span> where all <span style='color:#f7b731'>values below</span> the <span style='color:#0fb9b1'>diagonal</span> are <mark style='background:#f7b731'>all 0</mark> ($A_{ij} = 0 \text{ if } i \gt j$). The diagonals can be 0 also.
> There is a <span style='color:#0fb9b1'>lower triangular</span> which is the <span style='color:#f7b731'>opposite of a upper triangle</span>.

# Matrix Operations
---
To determine if 2 matrices $A$ and $B$ are <span style='color:#fa8231'>identical</span> ;
- Both matrices have the<mark style='background:#f7b731'> same size</mark> 
- Their <mark style='background:#f7b731'>corresponding entries are the same</mark>, $\forall i,j , a_{ij} = b(ij)$
## Addition, Subtraction

It is basically the addition or subtraction of the <span style='color:#f7b731'>corresponding values in the matrix</span>.

**Example of Addition**
$$  
  \begin{pmatrix}
    1 & 2 \\
    3 & 4  
  \end{pmatrix} 
   +
   \begin{pmatrix} 
    -1 & 2 \\
    3 & 4  
  \end{pmatrix}
   =
  \begin{pmatrix}
    0 & 4 \\
    6 & 8 
  \end{pmatrix}
$$
Subtraction is <span style='color:#f7b731'>similar</span> to addition.

## Scalar Multiplication

Given an matrix $A$ and some constant $c$, then a<span style='color:#0fb9b1'> scalar multiplication</span> is to <span style='color:#f7b731'>multiply each value in</span> $A$ by the constant $c$.

**Example of Scalar Multiplication**
$$ A =
\begin{pmatrix}
    1 & 2 \\
    3 & 4  
  \end{pmatrix}
\text{ and } -A = (-1)A =
 \begin{pmatrix}
    -1 & -2 \\
    -3 & -4  
  \end{pmatrix}
$$
With <span style='color:#0fb9b1'>scalar multiplication</span>, $A - B = A + (-1)B$ and thus only addition and scalar multiplication are considered.

### Properties of Matrix Addition, Subtraction and Scalar Multiplication

Lets assume $A,B,C$ are matrices with the <span style='color:#fa8231'>same size</span> and $0$ to be a <span style='color:#fa8231'>zero matrix</span> with the same size as well;
1) $A - B = A + (-1)B)$
2) **Commutative** law for addition : $A + B = B + A$
3) **Associative** law for addition : $(A + B) + C = A + (B + C)$
4) $0 + A = A$ and $A - A = 0$ and $0A = 0$ and $c0 = 0$
5) **Distributive** law : $c(A + B) = cA + cB$, $(c + d)A = cA + dA$, $c(d)A = (cd)A$, $1A = A$

For all the properties, the <span style='color:#fa8231'>resulting matrices </span>will <mark style='background:#f7b731'>always have the same size</mark>, it will not change.

## Matrix Multiplication

Assuming there are 2 matrices $A$ and $B$ where $A$ denotes $x \rightarrow y$ and $B$ denotes $y -> z$, then through <span style='color:#0fb9b1'>matrix multiplication</span>, the resulting matrix will be from $x \rightarrow z$.

Before 2 matrices can be multiplied, first the <mark style='background:#f7b731'>number of columns for the first matrix must be the same as the number of rows in the second matrix</mark>. 

Thus, $A = (a_{ij})_{m \times p}$ and $B = (b_{ij})_{p \times n}$ , $AB = (ab_{ij})_{m \times n}$ . Meaning the resultant matrix will be of size, <span style='color:#f7b731'>number of rows in the first matrix and the number of columns in the second matrix</span>.

If a <span style='color:#fa8231'>row matrix get multiplied by a column matrix</span>, then the result will be a number. 

To get the ($i,j$) entry ;
1) Take the ith <span style='color:#f7b731'>row</span> from the first matrix ($a_{i}$)
2) Take the jth <span style='color:#f7b731'>column</span> from the second matrix ($b_{j}$)
3) Multiply the corresponding entries
4) Sum all the products up
$$  
  \begin{pmatrix}
    1 & 2 & 3\\
    4 & 5 & 6  
  \end{pmatrix} 
   \begin{pmatrix} 
    1 & 1 \\
    2 & 3 \\
    -1 & -2 
  \end{pmatrix}
   =
  \begin{pmatrix}
    -1 & 1 \\
    8 & 7 
  \end{pmatrix}$$
One thing to take note is that <mark style='background:#eb3b5a'>matrix multiplication is not commutative</mark>, but <mark style='background:#f7b731'>associative</mark>.

<span style='color:#0fb9b1'>Pre-multiplication</span> of $A$ to $B$ or simply, pre-multiply $B$ by $A$, means that $A$ is the <span style='color:#f7b731'>first matrix</span>.
<span style='color:#0fb9b1'>Post-multiplication</span> of $A$ to $B$ or simply, pre-multiply $B$ by $A$, mean that $A$ is the <span style='color:#f7b731'>second matrix</span>.
### Properties of Matrix Multiplication

Lets assume $A,B,C$ are matrices of size $m \times p$, $p \times q$ and $q \times n$;
1) **Associative** law : $A(BC) = (AB)C$
2) **Distributive** law : $A(B_{1} + B_{2}) = AB_{1} + AB_{2}$, provided $B_{1}$ and $B_{2}$ are of size $p \times q$
3) $c(AB) = (cA)B = A(cB)$
4) $A0_{m \times p} = 0_{m \times p}$
5) $AI_{n} = A$
## Power of Square Matrices

$AA$ is well defined $\iff$ $m = n$, which means that $A$ is a <span style='color:#f7b731'>square matrix</span>. This is also called $A$ square ($A^{2}$).

Therefore $A^4$ is just $AAAA$, it does not matter which one gets multiplied first since <span style='color:#f7b731'>it is commutative</span>.

If $A^k$ where $k = 0$, then the resulting matrix will <mark style='background:#f7b731'>always be a identity matrix</mark> $I_{n}$. Even if the matrix is a zero matrix.
$$ A = 
  \begin{pmatrix}
    0 & 0 \\
    0 & 0  
  \end{pmatrix}, A^{0} = 
   \begin{pmatrix} 
    1 & 0 \\
    0 & 1 
  \end{pmatrix}$$
### Properties of Power of Square Matrices

Lets assume $A, B$ is a <span style='color:#fa8231'>square matrix</span> of size $p$;
1) $A^{m}A^{n} = A^{m + n}$
2) $(A^{m})^{n} = A^{mn}$
3) $(AB)^{n} \neq A^{n}B^{n}$, <span style='color:#fa8231'>this work if</span> $A$ and $B$ are the <mark style='background:#f7b731'>same size</mark> and $AB = BA$, meaning $A$ and $B$ are <mark style='background:#f7b731'>the same matrix</mark>

## Transpose

Suppose that a matrix $A = (a_{ij})_{m \times n}$ and the matrix must be of size $n \times m$ instead, then this is where <span style='color:#0fb9b1'>transposition</span> come in handy.

<span style='color:#0fb9b1'>Transposing</span> $A$ is denoted as $A^{T}$ or $A^{t}$ or $(a'_{ij})_{n\times m}$. The ($i,j$) entry in $A$ is the ($j,i$) entry in $A^{T}$ and $(A^T)^T$ <span style='color:#f7b731'>is the original matrix</span>.
$$
 A = 
  \begin{pmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6 
  \end{pmatrix}, A^{T} = 
   \begin{pmatrix} 
    1 & 4 \\
    2 & 5 \\
    3 & 6
  \end{pmatrix}
$$
### Properties of Transposing

Lets assume $A, B$ is a $m \times n$ matrix and $C$ be a $n \times p$ matrix;
1) $(A^{T})^{T} = A$
2) $A^{T}= A$ if $A$ is <span style='color:#f7b731'>symmetric</span>
3) $cA^{T} = (cA)^T$ where $c$ is just some constant
4) $(A + B)^{T} = A^{T} + B^{T}$
5) $(AC)^{T}= C^{T}A^{T}$, this is just rearranging to get the same row and column size

# Matrix Representation
---
Suppose that there are <span style='color:#fa8231'>2 matrices </span>$A_{m \times p}$ and $B_{p \times n}$. From [[#Matrix Multiplication|matrix multiplication]], the $(i,j)$ entry of $AB$, the $A_{i}$ row must be multiplied and summed up with $B_{j}$ column. <mark style='background:#f7b731'>The first matrix must be spilt into rows wilt the second matrix into columns</mark>.

Now let $a_{i}$ be the ith row of $A$ and $b_{j}$ as the jth row of $B$, by <span style='color:#fa8231'>multiplying both up, the result will be a number</span>. Therefore, $AB$ can also be written as such : 
$$AB = 
\begin{pmatrix}
a_{1}b_{1} & a_{1}b_{2} & \dots & a_{1}b_{n} \\
a_{2}b_{1} & a_{2}b_{2} & \dots & a_{2}b_{n} \\
\vdots & \vdots & & \vdots \\
a_{m}b_{1} & a_{m}b_{2} & \dots & a_{m}b_{n} \\
\end{pmatrix}$$
Now with the base case shown above, it can be further reduced as such ;
$$a_{i}B = 
a_{i} \begin{pmatrix}
b_{1} & b_{2} & \dots & b_{n} \\
\end{pmatrix} = 
\begin{pmatrix}
a_{i}b_{1} & a_{i}b_{2} & \dots & a_{i}b_{n} \\
\end{pmatrix}$$
**Where :**
- $a_{i}$ is ith row for matrix $A$.

which is observed to be the <mark style='background:#f7b731'>ith row of AB</mark>. Which result in this simplified form ;

$$AB = 
\begin{pmatrix}
a_{1} \\
a_{2} \\
\vdots \\
a_{m}
\end{pmatrix} B = 
\begin{pmatrix}
a_{1}B \\
a_{2}B \\
\vdots \\
a_{m}B
\end{pmatrix}$$
This is <span style='color:#fa8231'>also the same </span>if the columns of $B$ is used ;
$$Ab_{j} = 
\begin{pmatrix}
a_{1} \\
a_{2} \\
\vdots \\
a_{m}
\end{pmatrix} b_{j} = 
\begin{pmatrix}
a_{1}b_j \\
a_{2}b_{j} \\
\vdots \\
a_{m}b_{j}
\end{pmatrix}$$
which is observed to be the <mark style='background:#f7b731'>jth column of AB</mark>. Which result in this simplified form ;
$$AB = 
A \begin{pmatrix}
b_{1} & b_{2} & \dots & b_{n} \\
\end{pmatrix} = 
\begin{pmatrix}
Ab_{1} & Ab_{2} & \dots & Ab_{n} \\
\end{pmatrix}$$

**Where :**
- $b_{j}$ is the jth column for matrix $B$
## Matrix Representation of Linear System

 A <span style='color:#fa8231'>linear system can be represented by matrices</span>, given the following linear system : 
$$
\begin{cases}
a_{11}x_{1} + \dots + a_{1n}x_{n} = b_{1} \\
\  \  \ \vdots \\
a_{m1}x_{1} + \dots + a_{mn}x_{n} = b_{m}
\end{cases}$$
This can be represented by the following matrices :
$$ 
\begin{pmatrix}
a_{11} & \dots & a_{1n} \\
a_{21} & \dots & a_{2n} \\
\vdots \\
a_{m1} & \dots & a_{mn}
\end{pmatrix} 
\begin{pmatrix}
x_{1} \\
x_{2} \\
\vdots \\
x_{n}
\end{pmatrix}$$
Therefore to get $b1$, just take the first row in the <span style='color:#f7b731'>left matrix</span> and do a <span style='color:#f7b731'>matrix multiplication on the right matrix</span>.

The left matrix is called the, <span style='color:#0fb9b1'>coefficient matrix</span>
The right matrix is called the <span style='color:#0fb9b1'>variable matrix</span>

The resulting matrix after doing matrix multiplication is called the <span style='color:#0fb9b1'>constant matrix</span>, $Ax = b$ <span style='color:#f7b731'>which is the linear system</span>.
$$b =
\begin{pmatrix}
b_{1} \\
b_{2} \\
\vdots \\
b_{m}
\end{pmatrix}$$

Therefore to <span style='color:#fa8231'>determine</span> if there is <span style='color:#fa8231'>a solution</span> to the given system. Then there must be a <mark style='background:#f7b731'>matrix in the form of the variable matrix</mark>, lets call it $u$. Where $Au = b$, thus making $u$ a solution to the given system.

And therefore, $Ax = b = x_{1}a_{1} + \dots x_{n}a_{n} = \sum^{n}_{j=i}x_{j}a_{j}$.

In <span style='color:#fa8231'>a given system there can be only 3 outcomes</span> :
1) **No solution**
2) **One Solution**
3) **Infinitely many solutions**

As long as there are <span style='color:#f7b731'>more then 1 solution</span>, then there will <span style='color:#f7b731'>be an infinite number of solution</span> :
- Let $u_{1}\neq u_{2}$ which are **both solutions** to a given system
- Consider this $A(c_{1}u_{1} + c_{2}u_{2})$ where $c_1$ and $c_{2}$ are some **constants**
- It can be simplified into $c_{1}Au_{1} + c_{2}Au_{2} = c_{1}b + c_{2}b = (c_{1}+ c_{2})b$
- **As long** as $c_{1} + c_{2} = 1$ then <span style='color:#20bf6b'>it will be a solution to the system</span> as there are an infinitely many ways to get 1 from 2 numbers
# Inverses
---
Given, $a + x = b \rightarrow x = b + (-a)$, $-a$ is called the <span style='color:#0fb9b1'>additive inverse</span> of $a$.

Given $ax = b \rightarrow x = a^{-1}b$, $a^{-1}$ is called the <span style='color:#0fb9b1'>multiplicative inverse</span> of $a$ when $a \neq 0$.

This both represents number but it can be <span style='color:#f7b731'>applied to matrices</span> as well, but denoted as $-A$ for an inverse matrix.
## Inverses for Square Matrix

If the <span style='color:#fa8231'>2 conditions below hold</span> :
1) The matrix, $A$, <mark style='background:#f7b731'>must be a square matrix</mark>. 
2) If its a square matrix, and lets say there is another square matrix $B$ with the same size as $A$. Then :
	-  $AB = I_{n}$ &
	- $BA = I_{n}$

Then $A$ is <span style='color:#0fb9b1'>invertible</span> and $B$ is an <span style='color:#0fb9b1'>inverse</span> of $A$, ($A^{-1}$), which is <mark style='background:#f7b731'>unique</mark>. Else if its <span style='color:#fa8231'>not invertible</span>, then $A$ is called <span style='color:#0fb9b1'>singular</span>.

These <span style='color:#f7b731'>only applies to square matrices</span>, for non square matrices they may be <mark style='background:#f7b731'>neither invertible nor singular</mark>. <mark style='background:#f7b731'>Not all square matrices have a inverse</mark> as well (Zero Matrix).

Now $B$ is an inverse of $A$, thus $AB = I_{n}$ and $C$ is a <span style='color:#fa8231'>constant matrix</span> and $X$ is a <span style='color:#fa8231'>variable matrix</span>. How to <mark style='background:#fa8231'>solve a system</mark> :
1) $AX = C$, lets say this is given and thus the **values of x is to be solved**, $X$
2) Multiply by $B$ ; $B(AX) = BC$ and since <span style='color:#f7b731'>matrix multiplication is associative</span> it can be rewritten as, $X(AB) = BC$
3) $X(AB) = BC$ is also equals to $XI = BC$
4) And anything times Identity is the matrix itself and therefore, $X = BC$ or $X = A^{-1}C$

### 2 x 2 Matrix

Now consider $A$ and $B$ which are a 2 by 2 matrix in this form :
$$ A =
\begin{pmatrix}
a & b \\
c & d
\end{pmatrix} B =
\begin{pmatrix}
w & x \\
y & z
\end{pmatrix}$$
Now lets assume that $B$ is the inverse of $A$ then carry out a matrix multiplication to get : 
$$ AB =
\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}$$
From this <span style='color:#f7b731'>two linear systems can be formed</span> :
$$
\begin{cases}
aw + by = 1 \\
cw + dy = 0 \\
\end{cases} 
\text{ \& }
\begin{cases}
ax + bz = 0 \\
cx + dz = 1 \\
\end{cases} 
$$
From here solve for $w$, $x$, $y$, $z$, which there are 2 outcomes :
1) There are <span style='color:#eb3b5a'>no solutions</span> which happens then the 2 linear equations in a system are <span style='color:#f7b731'>parallel</span> $\frac{a}{c} = \frac{b}{d}$, therefore making the <span style='color:#f7b731'>system inconsistent</span> and making $A$ <span style='color:#f7b731'>singular</span>.
2) There <span style='color:#20bf6b'>is a solution</span>, when $\frac{a}{c} \neq \frac{b}{d}$ therefore they intersect making the <span style='color:#f7b731'>system consistent</span> and making $A$ <span style='color:#f7b731'>invertible</span>.

Thus <mark style='background:#f7b731'>only for a 2 by 2 matrix</mark> a formula for $A^{-1}$ is as follows : 
$$ A^{-1} = \frac{1}{ad - bc}
\begin{pmatrix}
d & -b \\
-c & a
\end{pmatrix}
$$

### Properties of an Invertible Matrix

#### Cancellation Law

Let $A$ be an <span style='color:#f7b731'>invertible matrix</span>, then the following is true
1) $AB_{1} = AB_{2} \rightarrow B_{1} = B_{2}$, this is because, $AB_{1} = AB_{2} \rightarrow AA^{-1}B_{1} = AA^{-1}B_{2} \rightarrow IB_{1} = IB_{2} \rightarrow B_{1} = B_{2}$
2) $AB = 0 \rightarrow B = 0$
#### Other Laws
- If $cA$ is invertible, then $(cA)^{-1} = \frac{1}{c}A^{-1}$
- $A^{T}$ is invertible, then $(A^{T})^{-1} = (A^{-1})^{T}$
- $(A^{-1})^{-1} = A$
- If $AB$ is invertible then $(AB)^{-1} = B^{-1}A^{-1}$
- The inverse of $A^{T}$ is $(A^{-1})^{T}$
- If $A$ is invertible, $A^{m + n} = A^{m}A^{n}$ and $(A^{m})^{n} = A^{mn}$
#### Powers of an Invertible Matrix

Given $A_{1}, A_{2}, \dots, A_{k}$ where $A$ is invertible then $(A_{1}, A_{2}, \dots, A_{k})^{-1} = A_{1}^{-1}, A_{2}^{-1}, \dots, A_{k}^{-1}$.

Now given any integer $k$, if $A$ is a invertible matrix, then $A^{-k} = (A^{-1})^{k}$. This <span style='color:#f7b731'>application is for negative powers</span>.
# Elementary Matrices
---
Recall the 3 <span style='color:#fa8231'>elementary row operations</span> :
1) Swapping 2 rows
2) Multiplying a row by a constant that is not 0
3) Adding a constant multiple of a row to another row

Now a square matrix can be called a <span style='color:#0fb9b1'>elementary matrix</span>, if it can be obtained from a <span style='color:#f7b731'>identity matrix </span>by performing <mark style='background:#f7b731'>only one type of elementary row operation</mark>.
## Connection with Matrix Multiplication

The <span style='color:#fa8231'>3 elementary row operations</span> can also be done through matrix multiplication. Supposed that $I_{4}$ is some identity matrix.

**Multiply row by a constant**
$$
 EA =
\begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & C & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22} \\
a_{31} & a_{32} \\
a_{41} & a_{42} \\
\end{pmatrix} =
\begin{pmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22} \\
Ca_{31} & Ca_{32} \\
a_{41} & a_{42} \\
\end{pmatrix}
$$
Notice that $E$ is just $I_{4}$ where $R_{3}$ is <span style='color:#f7b731'>multiplied by some constant</span> $C; C \ne 0$.

**Interchanging 2 Rows**
$$
 EA =
\begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 1 & 0 \\
0 & 1 & 0 & 0
\end{pmatrix}
\begin{pmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22} \\
a_{31} & a_{32} \\
a_{41} & a_{42} \\
\end{pmatrix} =
\begin{pmatrix}
a_{11} & a_{12} \\
a_{41} & a_{42} \\
a_{31} & a_{32} \\
a_{21} & a_{22} \\
\end{pmatrix}
$$
Notice that $E$ is just $I_{4}$ where $R_{2}$ and $R_{4}$ have <span style='color:#f7b731'>swapped positions</span>.

**Adding one row to some constant of another row**
$$
 EA =
\begin{pmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & C \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22} \\
a_{31} & a_{32} \\
a_{41} & a_{42} \\
\end{pmatrix} =
\begin{pmatrix}
a_{11} & a_{12} \\
a_{21} + Ca_{41} & a_{22} + Ca_{42} \\
a_{31} & a_{32} \\
a_{41} & a_{42} \\
\end{pmatrix}
$$
Notice that $E$ is just $I_{4}$ where $R_{2}$ is <span style='color:#f7b731'>added by some constant multiplied</span> to $R_{4}$.

Therefore, this shows that performing a <span style='color:#f7b731'>elementary row operation on</span> a $I_{m}$ and doing a <b><mark style='background:#f7b731'>pre matrix multiplication</mark></b> on a matrix $A_{m \times n}$, is the same as performing it on the matrix it self.
## Invertibility

<mark style='background:#f7b731'>Every elementary matrix is invertible</mark>. As for all of the operations, to revert back just reverse what was done originally.

Let $I_{4}$ be some identity matrix, then :
- $I \xrightarrow{CR_{i}} E$
- Then to revert it back just do the reverse $E \xrightarrow{{1}/{C}R_{i}} I$

Therefore the following equation is made :
$$
I \overset{CR_{i}}{\underset{E}{\to}} E \overset{\frac{1}{c}R_{i}}{\underset{D}{\to}} I, ED = I
$$
**Where** :
- $E$ & $D$ are some elementary matrix

Thus, if a matrix $B$ can be obtain from a <span style='color:#f7b731'>sequence of elementary matrix multiplication</span> of $A$ and vice versa. Then $Ax = c$ and $Bx = d$ have the <mark style='background:#f7b731'>same solution set</mark>, meaning they are row equivalent

Therefore, some properties are, if $A$ is a <span style='color:#fa8231'>square matrix</span>, then the following are equivalent :
- If $A$ is invertible matrix then,
- $Ax = b$ has a unique solution
- $Ax = 0$ has only the trivial solution
- The <span style='color:#0fb9b1'>RREF</span> of $A$ is $I$ (Identity matrix)
- $A$ is a product of some elementary matrices

## Finding Invertibility

If $A$ <span style='color:#fa8231'>is invertible</span>, then its inverse is just the matrix multiplication of $E_{k} \dots E_{1}$ where $E_{k} \dots E_{1}A = I_{n}$. However this can be quite slow.

**Theorem :** Let $A$ be an invertible matrix $(A | I)$, then in its <span style='color:#0fb9b1'>RREF</span> it will be $(I | A^{-1})$

$$ (A|I) =
\left(
\begin{array}{ccc|ccc}
1 & 2 & 3 & 1 & 0 & 0 \\
2 & 5 & 3 & 0 & 1 & 0 \\
1 & 0 & 8 & 0 & 0 & 1
\end{array}
\right) \xrightarrow{\text{Some ERO to get}}
\left(
\begin{array}{ccc|ccc}
1 & 0 & 0 & -40 & 16 & 9 \\
0 & 1 & 0 & 13 & -5 & -3 \\
0 & 0 & 1 & 5 & -2 & -1
\end{array}
\right) = (I|A^{-1})
$$

And thus <span style='color:#fa8231'>on the right</span>, the matrix after the $|$ will be the <b><mark style='background:#f7b731'>inverse of matrix A</mark></b> or $A^{-1}$.

But how to know if $A$ is <span style='color:#fa8231'>originally invertible</span>? For a <b><mark style='background:#fa8231'>square matrix to be invertible</mark></b> :
- Its <span style='color:#f7b731'>reduce-echelon form is</span> $I$, which means all columns are pivot columns <span style='color:#f7b731'>in row-echelon form</span> (Have a pivot point)
- All the <span style='color:#f7b731'>rows in the row-echelon form are nonzero</span>

And if it is <span style='color:#0fb9b1'>singular</span>, then it <span style='color:#eb3b5a'>will not satisfy</span> the above conditions.

**Prove :** $A^{2} - 3A - 4I = 0$
- <span style='color:#eb3b5a'>Cannot solve using the quadratic way</span> since its dealing with matrices and it need not be a zero matrix to give a 0 result
- $4I = A^{2}- 3A$
- $I = \frac{1}{4}(A^{2} -3A)$
- $A[\frac{1}{4}(A-3I)] = I$ 
- Therefore the above is in the form of $AB = I$ and thus $A^{-1}$ is invertible
# LU Decomposition
---
Why is it called [[#Types of Matrices|LU]], well $L$ is the notation for lower triangular matrix while $U$ is for upper triangular matrix.

Notice in the [[Linear Systems#Gaussian Elimination|gaussian elimination]] <span style='color:#fa8231'>only type 2 and 3</span> <span style='color:#0fb9b1'>elementary row operations</span> are used.

![[LU Decomposition Example.png|center]]

**Where :**
- $A$ can be a matrix of any size
- When doing the operations on the $I$ matrix, it <b><mark style='background:#f7b731'>must be reversed</mark></b>
- <b><mark style='background:#f7b731'>Only type 3</mark></b> operations are used and each operation $R_{i} \pm cR_{j}$, $i \gt j$ 
- If the corresponding $i$ and $j$ operation does not exist then the $(i, j)$ entry is just 0
- If $A_{n\times m}$ is not a square matrix, then the identity matrix will be $I_{n}$

Now supposed the above is all executed, then $A = LU$. Then this <span style='color:#fa8231'>gives us another way to solve</span> $Ax = b$.
- Since $Ax = b$ and $A = LU$, then $LUx = b$
- Now make $Ux = y$ and then it will result in $Ly = b$
- Now solve for this linear system $(L | b)$ which is what was taught in the beginning of the class. This part is known as <span style='color:#0fb9b1'>forward substitution</span>
- Once $y$ is solved from the step above, then $Ux = y$ can be solved similarly, this step is called <span style='color:#0fb9b1'>backward substitution</span>. Which will result in known $x$.

Note that $U$ is <span style='color:#f7b731'>in a row echelon form</span> and thus it is upper triangular.

If there <span style='color:#fa8231'>are unknowns</span>, then remember to always <b><mark style='background:#f7b731'>check what happens when they are 0</mark></b>.
## Partial Pivoting

But suppose that <span style='color:#fa8231'>interchanging of rows is needed</span> (Type 2), then the matrix $A$ need to be multiplied by $E$.

For example :
- $A {\underset{E_{1}}{\to}} {\underset{E_{2}}{\to}} \overset{R_{i}\iff R_{j}}{\underset{E_{3}}{\to}} {\underset{E_{4}}{\to}} R$
- $A = E_{1}^{-1}E_{2}^{-1}E_{3}E_{4}^{-1}R$
- $E_{3}A = (E_{3}E_{1}^{-1}E_{2}^{-1}E_{3})E_{4}^{-1}R$

As shown, the <span style='color:#fa8231'>elementary matrix where the rows are swapped</span> will need to be multiplied. Let this be denoted as $E_{3} = P$ which is called a <span style='color:#0fb9b1'>permutation matrix</span>.

Then in this case $PA = LU$.

## Elementary Column Operations

Now, instead of elementary row operations, there ware <span style='color:#0fb9b1'>elementary column operations</span> (**ECO**) :
1) <span style='color:#0fb9b1'>Scaler multiplication</span>, where an equation is <span style='color:#f7b731'>multiplied</span> by some <span style='color:#f7b731'>nonzero constant</span> ($kC_{i} \land k \neq 0$), **Type 1**
2) <span style='color:#0fb9b1'>Column swap</span>, where <span style='color:#f7b731'>2 Column are interchanged</span> with one another ($C_{i} \leftrightarrow C_{j}$), **Type 2**
3) <span style='color:#0fb9b1'>Column sum</span>, where a constant multiple of a <span style='color:#f7b731'>column is added to another column</span> ($C_{j} + kC_{i}$ or $C_{j} \mapsto C_{j} + kC_{i}$), **Type 3**

Everything that applies for ERO also applies to ECO, for example properties of elementary matrices. 

Given $I \xrightarrow{C_{j} + kC_{i}} E$, then it will be the same as $I \xrightarrow{R_{j} + kC_{i}} E^{-1}$.
# Determinant
---
A <span style='color:#0fb9b1'>determinant</span>, is a value which can <span style='color:#f7b731'>determine the invertibility of a square matrix</span>.

## Determinant for a 2 by 2 Matrix

Let $A$ be a square matrix : 
$$
 A =
\begin{pmatrix}
a & b \\
c & d
\end{pmatrix}
$$
Then its <span style='color:#0fb9b1'>determinant</span> is defined as $det(A)  =|A| = ad - bc$. If the <span style='color:#f7b731'>determinant value is 0</span>, then $A$ will be <span style='color:#f7b731'>singular</span>.

**Determinant relationship for a 2 x 2 matrix** :
1) $det(I_{2}) = 1$
2) $A \xrightarrow{cR_{i}} B$, then the $det(B) = cdet(A)$
3) $A \xrightarrow{R_{i} \leftrightarrow R_{j}} B$, then the $det(B) = -det(A)$
4) $A \xrightarrow{R_{i} + cR_{j}} B$, then the $det(B) = det(A)$, where $i \ne j$
<div style="page-break-after: always;"></div>

**Using Determinant to solve a system :**
![[Solving a System for a 2 x 2 Matrix.png|center|400]]
## Determinant for a 3 by 3 Matrix

Similarly if the <span style='color:#f7b731'>determinant value is 0</span>, then $A$ will be <span style='color:#f7b731'>singular</span>, else $A$ is invertible.

**Determinant relationship for a 3 x 3 matrix** :
1) $det(I_{3}) = 1$
2) $A \xrightarrow{cR_{i}} B$, then the $det(B) = cdet(A)$
	- In particular $I \xrightarrow{cR_{i}} E$, then the $det(E) = c$
3) $A \xrightarrow{R_{i} \leftrightarrow R_{j}} B$, then the $det(B) = -det(A)$, where $i \ne j$
4) $A \xrightarrow{R_{i} + cR_{j}} B$, then the $det(B) = det(A)$, where $i \ne j$

To <span style='color:#fa8231'>find the determinant of a 3 x 3 matrix </span>, it is given as such :
![[Determinant of a 3 x 3 Matrix.png|center|400]]

In general $M_{ij}$ is denoted a a <span style='color:#0fb9b1'>submatrix</span>, where the<span style='color:#f7b731'> ith row and jth column are not included</span>.

To simplify it further, let $A_{ij} = (-1)^{i+j}det(M_{ij})$, this $A_{ij}$ is called the <b><mark style='background:#0fb9b1'>(i, j) - cofactor of A</mark></b>. This means that the $det(A)$ can be rewritten as $det(A) = a_{11}A_{11} + a_{12}A_{12} +a_{13}A_{13}$.

If 2 rows in $A$ are <span style='color:#fa8231'>identical</span>, then one can become a<span style='color:#f7b731'> zero row</span>, thus <span style='color:#f7b731'>making the determinant 0</span>.
<div style="page-break-after: always;"></div>

This can be generalised for any $A_{n \times n}$ where $n \ge 3$, where the generalised formula will be :
$$det(A) = a_{11}A_{11} - a_{12}A_{12} + \dots - \dots + a_{1n}A_{1n}$$

Remember to <b><mark style='background:#f7b731'>alternate between positive and negative</mark></b>.
## Broken Diagonals Method

There is another way to get the <span style='color:#0fb9b1'>determinant</span> of a 3 x 3 matrix and it is called the <span style='color:#0fb9b1'>diagonal expansion method</span>.
![[Broken Diagonals.png|center|400]]

Just remember that the <span style='color:#fa8231'>positive terms</span> are from the <span style='color:#f7b731'>3 diagonals are from the top left to the bottom right</span> (**Left A**).

Just remember that the <span style='color:#fa8231'>negative terms</span> are from the <span style='color:#f7b731'>3 diagonals are from the top right to the bottom left</span> (**Right A**).

This <b><mark style='background:#f7b731'>only works for 3 by 3 matrices</mark></b>.

**Additional pointers** :
- $A \xrightarrow{cR_{i}} EA \implies det(EA) = cdet(A) = det(E)det(A)$
- $A \xrightarrow{R_{i} \leftrightarrow R_{j}} EA \implies det(EA) = det(E)det(A)$
- $A \xrightarrow{R_{i} + cR_{j}} EA \implies det(EA) = det(E)det(A)$

Therefore if $A$ is <span style='color:#fa8231'>invertible</span>, then a <span style='color:#f7b731'>series of elementary matrices multiplication, will reach</span> $I$. Then $det(A) = det(I) \times det(E_{1}^{-1}) \dots \times det(E_{k}^{-1})$.

If it is <span style='color:#fa8231'>not invertible</span>, then the resulting matrix $R$ <span style='color:#f7b731'>will be zero in the last row</span> then, $det(R) = 0$ and thus $det(A) = 0$.

If a matrix $R$ is <span style='color:#f7b731'>in its row echelon form</span> and it is a <span style='color:#f7b731'>square matrix</span>, its <span style='color:#fa8231'>determinant will be the product of the diagonals</span>.

## Properties of Determinant

Assuming $A$ is a <span style='color:#fa8231'>square matrix</span> :
- $det(A) = 0 \iff A$ is **singular**
- $det(A) \neq 0 \iff A$ is **invertible**
- $det(A) = det(A^{T})$, meaning the <span style='color:#f7b731'>transposed determinant is the same</span> as its original determinant

Assuming $A$ is a <span style='color:#fa8231'>square matrix of order</span> $n$ :
- $det(cA) = c^{n}det(A)$
> This is because $cA$ is where all rows are multiplied by a constant $c$ which needs $n$ number of type 1 <span style='color:#0fb9b1'>ERO</span>

Assuming $A$ is a <span style='color:#fa8231'>triangular matrix</span> :
- $det(A)$ is the <span style='color:#f7b731'>product of the diagonal entries</span> of $A$

Assuming $A$ & $B$ are <span style='color:#fa8231'>square matrices of the same order</span> :
- $det(AB) = det(A)det(B)$

Assuming $A$ to be <span style='color:#fa8231'>inveritible</span> :
- $det(A^{-1}) = [det(A)]^{-1}$ 
> This is because $AA^{-1} = I$ thus the resulting determinant is 1. If $det(x) = n$, then $det(A^{-1}) = \frac{1}{n}$

<b><mark style='background:#f7b731'>In general </mark></b> the $det(A) = (-1)^{t}det(R)$ where $t$ is the <span style='color:#fa8231'>number of type 2 operations</span>.

## Cofactor Expansion

To find the [[#Determinant for a 3 by 3 Matrix|determinant of a 3 by 3 matric]], the way to do it is through the use of a <span style='color:#0fb9b1'>cofactor</span>.

The formula is as such given a matrix $A$ :
$$
\begin{align}  
\text{Using Rows : } det(A) = a_{i1}A_{i1} + \dots + a_{in}A_{in}  \\  
\text{Using Cols : } det(A) = a_{1j}A_{1j} + \dots + a_{nj}A_{nj}
\end{align}
$$
**Where :**
- the values 1 and 2 determine which column or row was selected

Now which one to use, well if a particular row column / row has <span style='color:#f7b731'>more zero values</span> then use that. Since there will be less computation needed since, 0 times anything is 0.

Therefore <span style='color:#fa8231'>this is recommended</span> if :
- Some row or column has <span style='color:#f7b731'>many 0s</span>
- And it is <span style='color:#f7b731'>not a 2 by 2 matrix</span>

## Adjoint Matrix

The terms adjoint, adjugated or adjunct refers to the same thing where :
$$
adj(A) = (A_{ij})_{n \times n} = (A_{ij}^{T})_{n \times n}
$$
**Where** :
- $A_{ij}$ is the $(i,j)$ - <b><mark style='background:#f7b731'>cofactor</mark></b> of $A$
- $A$ must be a **square matrix**

<span style='color:#f7b731'>Do this for all elements</span> in the matrix and a adjoin matrix of $A$ can be formed.
<div style="page-break-after: always;"></div>

Let $A$ be a 3 by 3 matrix, then $adj(A)$ is :
$$ adj(A) =
\begin{pmatrix}
A_{11} & A_{12} & A_{13} \\
A_{21} & A_{22} & A_{23} \\
A_{31} & A_{32} & A_{33}
\end{pmatrix} 
$$

This adjoint matrix will be invertible ad thus $A^{-1} = [det(A)]^{-1} adj(A)$

**Properties**
- $A[adj(A)] = det(A)I$
- $[adj(A)]A = det(A)I$
- $A^{-1} = \frac{1}{det(A)} \times adj(A)$, given that $A$ is **invertible**, This can be <b><mark style='background:#f7b731'>used to find the inverse</mark></b>, just find the $det(A)$ and the adjoin matrix of $A$
## Cramer's Rule
$$
\begin{pmatrix}
a_{11} & a_{12} & a_{13} \\
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & a_{33}
\end{pmatrix} 
\begin{pmatrix}
x_{1} \\
x_{2} \\
x_{3}
\end{pmatrix} =
\begin{pmatrix}
y_{1} \\
y_{2} \\
y_{3}
\end{pmatrix}
$$
Now suppose, the given system as shown above, what if the interest is only in $x_{1}$. Is there a faster way of getting the value of only $x_{1}$.

This is where <span style='color:#0fb9b1'>cramer's rule</span> come into play. It is <span style='color:#fa8231'>used when only one value</span> of $x$ is of interest.

If $A$ is <span style='color:#f7b731'>invertible</span> or order $n$, then the system has a unique solution 
$$
x = 1/det(A)
\begin{pmatrix}
det(A_{1}) \\
det(A_{2}) \\
\vdots \\
det(A_{n})
\end{pmatrix}
$$

**How to use Cramer's Rule**
![[Cramer's Rule.png|center|250]]
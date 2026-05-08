---
Title: Mathematical Induction
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - Math/Logic
  - Math/Proofs
---
# Sequences
---
**Sequence**
> A <span style='color:#0fb9b1'>sequence</span> is an ordered set with members called <span style='color:#0fb9b1'>terms</span>. Usually, the terms are numbers. A sequence may have infinite terms.

In general they can be expressed as $a_{m},a_{m+1}, a_{m+2}, \dots, a_{n}$ where $m \le n$ and $n = \infty$

**Explicit Formula**
> It is a<span style='color:#f7b731'> rule for a particular sequence</span> that shows how the values of $a_{k}$ depend on $k$

**Sequence Builder**
> A way to build a sequence

For **finite sequences** : $[f(k) : k \in [n..m]] : Seq(B)$ (Replace $f(k)$ with the sequence equation)

For **Infinite sequences** : $[f(k) : k \in [n,,]] : Seq(B)$

Writing in **recursion** : Fibonacci = 1.1.$[fibs(k-1) + fibs(k-2) : k \in [3..]]$
> The first numbers before the brackets are called <span style='color:#f7b731'>base cases</span> while those in the backets are the <span style='color:#f7b731'>recursive cases</span>
## Equality of Sequence

For 2 sequences to be equal, check that <mark class="hltr-orange">for all index</mark> for sequences a and b, the <mark class="hltr-orange">values must be the same</mark>

Example:
$a_{k} = \frac{k}{k+1} \text{ where } k \ge 1$ is the same as $b_{k-1} = \frac{k-1}{k} \text{ where } k \ge 2$

## Summation

The <span style='color:#0fb9b1'>summation sequence</span> is expressed in terms of: $$\sum^{n}_{k = m} a_{k}$$
Where:
1)  $\sum$ is called <span style='color:#f7b731'>sigma</span>
2)  $m$ is the starting value or <span style='color:#f7b731'>lower limit</span> for x
3)  $n$ is the ending value or <span style='color:#f7b731'>upper limit</span> for x
4)  $k$ is called the <span style='color:#f7b731'>index</span> of the summation

The summation can be <span style='color:#f7b731'>expanded</span> and rewritten as $\sum^{n}_{k = m} a_{k} = a_{m} + a_{m+1} + a_{m+2} + \dots + a_{n}$

If $m \gt n$, then it is called a <span style='color:#0fb9b1'>empty sum</span> where it is equal to the <span style='color:#0fb9b1'>additive identity</span> 0

**Telescoping Sums**
> It is a special sequence where it can be rewritten into a simpler expression

For example: $\sum^{n}_{k = 1} \frac{1}{k(k+1)} = 1 - \frac{1}{n+1}$

## Product

The product of all terms is expressed as: $$\prod^{n}_{k = m} a_{k}$$
Similar to [[#Summation|summation]], however instead of summing all the terms up, now it will be the <span style='color:#f7b731'>product of all terms</span>

The product can be <span style='color:#f7b731'>expanded</span> and rewritten as $\prod^{n}_{k = m} a_{k} = a_{m} \times a_{m+1} \times a_{m+2} \times \dots \times a_{n}$

If $m \gt n$, then it is called a <span style='color:#0fb9b1'>empty product</span> where it is equal to the <span style='color:#0fb9b1'>multiplicative identity</span> 1

## Properties of Summation and Products

If there are <span style='color:#f7b731'>2 sequences of real numbers and c is any real number</span>, then the following equations hold for any integer $n≥m$ (Theorem 5.1.1):

1) $\sum^{n}_{k = m} a_{k} + \sum^{n}_{k = m} b_{k} = \sum^{n}_{k = m} (a_{k} + b_{k})$

2) $c \times \sum^{n}_{k = m} a_{k} = \sum^{n}_{k = m} c \times a_{k}$

3) $\prod^{n}_{k = m} a_{k} \times \prod^{n}_{k = m} b_{k} = \prod^{n}_{k = m} (a_{k} \times b_{k})$

For all these to be valid, $n$ and $m$ <mark class="hltr-orange">must be the same value</mark>

## Change of Variable

To change the variables of a sequence, the lower bound , upper bound, variables, sequence equation must change in respect with <mark class="hltr-red">any change made so to not fundamentally change the sequence</mark>.

**Acceptable Changes**
$$\sum^{3}_{k = 1} k^{2} = \sum^{3}_{i = m} i^{2} =\sum^{5}_{k = 3} (k-2)^{2}$$

## Common Sequences

### Arithmetic Sequence

A sequence is called an <span style='color:#0fb9b1'>arithmetic sequence</span> (or <span style='color:#0fb9b1'>arithmetic progression</span>) if and only if there is a constant d such that $a_k=a_(k-1)+d$  for all integers $k \ge 1$.

It follows that, $a_n=a_0+dn$  for all integers $n \ge 0$.

$d$ is known as the <span style='color:#f7b731'>common difference</span>
$a_{0}$ is known as the <span style='color:#f7b731'>initial value</span>

There is a general formula to calculate the sum of this sequence $$\sum^{n-1}_{k = 0} a_{k} = \frac{n}{2}(2a_{0} + (n - 1)d)$$
### Geometric Sequence

A sequence is called a <span style='color:#0fb9b1'>geometric sequence</span> (or <span style='color:#0fb9b1'>geometric progression</span>) if and only if there is a constant r such that $a_{k} = ra_{(k-1)}$  for all integers $k \ge 1$.

It follows that, $a_n=a_0 r^n$  for all integers $n \ge 0$.

$r$ is known as the <span style='color:#f7b731'>common ratio</span>

There is a general formula to calculate the sum of this sequence $$\sum^{n-1}_{k = 0} a_{k} = a_{0}\left(\frac{1-r^{n}}{1-r}\right)\text{ where } r \ne 1$$
The reason r cannot be 1 is that if r is one then the <span style='color:#0fb9b1'>arithmetic sequence</span> should be used

## Closed Form

If a sum with a variable number of terms is shown to be <span style='color:#f7b731'>equal to a formula</span> that <mark class="hltr-red">does not contain either an</mark> ellipsis (…) or a summation symbol ($\sum$), we say that it is written in <span style='color:#0fb9b1'>closed form</span>.

Example: $\frac{n(n+1)}{2}$ is the closed form formula for $1 + 2 + 3 + 4 + \dots + n$ 

# Mathematical Induction
---

**Simple Principle of Mathematical Induction** (1PI)
1) To prove that $P(n)$ is true for all $n \in Z^+$:
2) <span style='color:#f7b731'>Basis step</span>: Show that $P(1)$ or $P(a)$ is true. This is also known as the <span style='color:#f7b731'>base case</span>
3) <span style='color:#f7b731'>Inductive step</span>: Show that $P(k)\rightarrow P(k+1)$ for all $k \in Z^+$. This is known as the <span style='color:#0fb9b1'>inductive hypothesis</span>
4) Therefore $P(n)$ is true for all $n \in Z^+$.

Symbolically:
$P(a)$
$\forall k \ge a , P(k) \rightarrow P(k+1)$
$\bullet \forall k \ge a, P(k)$

The <mark class="hltr-orange">base cases are important</mark> as without it, the inductive step might be incorrect or there is insufficient base cases to support the inductive hypothesis. There can be <span style='color:#f7b731'>multiple base cases if it is required</span>


**Strong Principle of Mathematical Induction** (2PI)
1) To prove that $P(n)$ is true for all $n \in Z^+$:
2) <span style='color:#f7b731'>Basis step</span>: Show that $P(a), P(a+1), \dots, P(b)$ is true. This is also known as the <span style='color:#f7b731'>base case</span>
3) <span style='color:#f7b731'>Inductive step</span>: Show that $P(a), P(a+1), \dots, P(k)\rightarrow P(k+1)$ for all $k \in Z^+$. This is known as the <span style='color:#0fb9b1'>inductive hypothesis</span>
4) Therefore $P(n)$ is true for all $n \in Z^+$.

Symbolically:
$P(a)$
$\forall k \ge a , P(a) \land P(a+1) \land \dots \land P(k)\rightarrow P(k+1)$
$\bullet \forall k \ge a, P(k)$

**OR**

$P(a) \land P(a+1) \land \dots \land P(b)$
$\forall k \ge a , P(k)\rightarrow P(k+b-a+1)$
$\bullet \forall k \ge a, p(k)$

The difference is that there are <span style='color:#f7b731'>multiple base cases</span>, and they will help in proving the inductive hypothesis

Example of proof by Induction:

Prove that for all integers $n \ge 12, n = 4a + 5b$ for some $a,b \in N$.

Proof (by 2PI):
1. Let $P(n) \equiv (n = 4a + 5b)$, for some $a,b \in \Bbb N, n \ge 12$.
2. Basis step: Show that $P(12),P(13),P(14),P(15)$ hold.
	12 = 4∙3+5∙0; 13 = 4∙2+5∙1; 14 = 4∙1+5∙2; 15 = 4∙0+5∙3;
3. Assume $P(i)$ holds for 12≤i≤k given some  k≥15.
4. Inductive step: (To show P(k+1) is true.)
	4.1 $P(k-3)$ holds  (by induction hypothesis), so, $k-3=4a+5b$ for some $a,b \in \Bbb N$
	4.2.  k+1 = (k-3)+4 =(4a+5b)+4 =4(a+1)+5b
	4.3.  Hence, $P(k+1)$ is true. ($\forall k \ge 15, P(k-3) \rightarrow P(k+1$))
5.  Therefore, $P(n)$ is true for $n \ge 12$.

# Well-Ordering Principle
---
## Well - Ordering for Non-Negative Integers

Every nonempty subset of $\Bbb Z_{\ge 0}$ has a <mark class="hltr-orange">smallest element</mark>

# Recurrence Relations
---
A <span style='color:#0fb9b1'>recurrence relation</span> for a sequence is a formula that relates each term $a_k$ to certain of its predecessors $a_(k-1),a_(k-2),\dots,a_(k-i)$ , where $i$ is an integer with $k-i \ge 0$.

If $i$ is a fixed integer , the <span style='color:#f7b731'>initial conditions</span> for such a recurrent relation specify the values of $a_0,a_1, a_2,\dots,a_{(i-1)}$

If $i$ depends on $k$, the initial conditions specify the values of $a_0,a_1, a_2,\dots,a_m$, where $m$ is an integer with $m \ge 0$

Examples of a recursive relation:

$$\sum^{n}_{k = m} a_{k} = \left(\sum^{n-1}_{k = m} a_{k} \right) + a_{n}$$
**Fibonacci Sequence in recursive form**
$F_0$=0
$F_1$=1
$F_{n} = F_{(n-1)}+F_{(n-2)}$, for $n \gt 1$

## Recursively Defined Sets

Let S be a finite set with at least one element. A<span style='color:#f7b731'> string over</span> S is a finite sequence of elements from S. 

The elements of S are called <span style='color:#0fb9b1'>characters</span> of the string, and the <span style='color:#0fb9b1'>length</span> of a string is the number of characters it contains. The <span style='color:#0fb9b1'>null string over</span> S is defined to be the “string” with no characters. It is usually denoted ϵ and is said to have length 0.

$Str(S) = \varepsilon$ or $c.Str(S), c \in S \text{ Appends a character into the string}$

### Structural Induction 

This proof is based on how the data is <span style='color:#f7b731'>constructed</span>

**Recursive Definition of a set S**
Specify that certain elements, called <span style='color:#0fb9b1'>founders</span>, are in S: if c is a founder, then $c\in S$ (Base clause) 

Specify certain functions, called <span style='color:#0fb9b1'>constructors</span>, under which the set S is closed: if f is a constructor and $x \in S$, then $f(x) \in S$ (recursion clause)  

Membership for S can always be demonstrated by (infinitely many) successive applications of the clauses above (minimality clause) 

**Structural Induction over a set S**
To prove that $\forall x \in S P(x)$ is true, where each $P(x)$ is a proposition, it suffices to:

Show that $P(c)$ is true for every founder c (basis step) 

Show that $\forall x \in S(P(x) \rightarrow P(f(x)))$  is true for every constructor f (induction step)  

In words, if all the founders satisfy a property P, and P is preserved by all constructors, then all elements of S satisfy P.

## Co-Induction

It is usually for <span style='color:#f7b731'>infinite sequences</span>, and it does not have a base case or founders unlike the <span style='color:#0fb9b1'>structural induction</span>

This proof is based on how the data is <span style='color:#f7b731'>deconstructed</span>. It tries to <span style='color:#f7b731'>prove that something bigger is true</span> which will make all is <span style='color:#f7b731'>successors true</span> as well.

Symbolically:
$\forall a \in A , s \in Seq(A), P(s) \rightarrow P(a \times s)$
$\bullet \forall s \in Seq(A), P(s)$

The larger the value of N, the more decomposed it is.
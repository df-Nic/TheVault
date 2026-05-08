---
title: Sequences & Series
Date Created: 2023-09-18
tags:
  - MA1521
  - Math
---
# Sequence
---

**Infinite Sequence**
> An infinite sequence of numbers is a function whose domain is the set of positive integers.

To denote a nth term in a sequence it can be $\{ a_{n} \}^{\infty}_{n = 1}$ OR ${a_n}$
## Arithmetic Progression (AP)

It is given by; 
$$\{ a + (n-1)d \}^{\infty}_{n = 1} \ or \ a_{n}= a+(n-1)d$$
**d** : Is known as the <span style='color:#f7b731'>common difference</span>
Example : 1, 3, 5, 7, 9, ... (a = 1, d = 2)
## Geometric Progression (GP)

It is given by; 
$$\{ ar^{n-1} \}^{\infty}_{n = 1} \ or \ a_{n}= a * r^{n - 1}$$
**r** : Is known as the <span style='color:#f7b731'>common ratio</span>
Example : $1, \frac{1}{2}, \frac{1}{2^{2}}, \frac{1}{2^{3}},\dots$ (a = 1, r = $\frac{1}{2}$)

For this progression, the first term, the power of r must be 0
## Convergence & Divergence

To know if the sequence diverges or converges, we need to know when n reaches infinity what is its value.;
$$\lim_{n \rightarrow \infty} f(x)$$
If the limit exists as a real finite number then the sequence <span style='color:#0fb9b1'>converges</span> or it can be written as $a_{n} \rightarrow L$

If the limit does not exist then it <span style='color:#0fb9b1'>diverges</span>.

If a function is equals to $a_n$ for all n, therefore, $\lim_{x \rightarrow \infty} f(x) = L$ then $\lim_{x \rightarrow \infty} a_n = L$

If $\{a_n\}$ and $\{b_n\}$ are convergent sequences and $c$ is a constant.
- $\lim_{n \rightarrow \infty} ca_{n}= c \lim_{n \rightarrow \infty} a_n$
- $\lim_{n \rightarrow \infty} a_{n} \pm b_{n} = \lim_{n \rightarrow \infty} a_{n} \pm \lim_{n \rightarrow \infty} b_{n}$
- $\lim_{n \rightarrow \infty} a_{n}b_{n} = \lim_{n \rightarrow \infty} a_{n}* \lim_{n \rightarrow \infty} b_{n}$
- $\lim_{n \rightarrow \infty} \frac{a_{n}}{b_{n}} = \lim_{n \rightarrow \infty} \frac{a_{n}}{\lim_{n \rightarrow \infty} b_{n}} if \lim_{n \rightarrow \infty} b_{n}\ne 0$

### Squeeze Theorem

Similar to the squeeze theorem for limits if $a_{n} \lt b_{n} \lt c_n$ ;
$$\lim_{n \rightarrow \infty} a_{n}= \lim_{n \rightarrow \infty} c_{n} = L \ then \lim_{n \rightarrow \infty} b_{n}= L$$
# Series
---

A series is given in the form of 
$$\sum^{\infty}_{n = 1} a_{n} = a_{1} + a_{2} + a_{3} + \dots$$
This is called a <span style='color:#0fb9b1'>infinite series</span> which can be constructed into a new sequence defined by $\{S_{n}\}$, this is called the sequence of <span style='color:#0fb9b1'>partial sums</span>; $$\{S_{n}\} = \sum^{n}_{i = 1} a_{i} = a_{1} + a_{2} + \dots +a_{n}$$ Which can also be defined as the limit of the sequence, 
$$\sum^{\infty}_{n = 1} a_{n} = \lim_{n \rightarrow \infty} S_{n}$$
If the <span style='color:#0fb9b1'>partial sum</span>, is some finite number then it converges, else it diverges.
## Geometric Series

It is defined as
$$\sum^{\infty}_{n = 1} ar^{n-1}, (a \ne 0) \ and  \ its \ sum = \frac{a}{1-r}$$
For this to be <span style='color:#0fb9b1'>convergent</span>, the sum must be equal to $\frac{a}{1 - r}$ when $|r| \lt 1$ and is <span style='color:#0fb9b1'>divergent</span> when $|r| \ge 1$

If $\sum^{\infty}_{n = 1} a_n$ and $\sum^{\infty}_{n = 1} b_{n}$ are convergent;

- $\sum^{\infty}_{n = 1} ca_{n} = c \sum^{\infty}_{n = 1} a_{n}$
- $\sum^{\infty}_{n = 1} (a_{n} + b_{n}) = \sum^{\infty}_{n = 1} a_{n} + \sum^{\infty}_{n = 1} b_{n}$

**Simplification of such a fraction**
$$\frac{1}{n(n+1)} = \frac{1}{n} + \frac{1}{n+1}$$

# Tests for Divergence and Convergence
---
## Nth Term Test for Divergence

If the series $\sum^{\infty}_{n=1} a_{n}$ then the $\lim_{n \rightarrow \infty} a_{n}  = 0$

Therefore, if the limit <span style='color:#f7b731'>does not exist</span> or it is <span style='color:#f7b731'>not 0</span> then the series is divergent. This works for sequences with no <span style='color:#f7b731'>partial sum or difficult to simplify partial sums</span>.

However if it is 0 it <span style='color:#f7b731'>cannot be concluded that it is convergent</span> as it is a sufficient condition. Example the <span style='color:#0fb9b1'>harmonic series</span>
### Harmonic Series
$$\sum^{\infty}_{n = 1} \frac{1}{n} = 1 + \frac{1}{2} + \frac{1}{3} \dots + \frac{1}{n}$$

A series to be <span style='color:#0fb9b1'>Nonnegative</span> it means that for each $a_{n} \ge 0$ therefore, a series $\sum^{\infty}_{n=1} a_{n}$ of nonnegative terms converges if and only if its partial sums are bounded from above (A constant K where  $S_{n}\lt K$ for all n).

This means that the series is either a <span style='color:#f7b731'>finite number of infinite</span> (Upper bound).

Example, given $\sum^{\infty}_{n=1} \frac{1}{n^{2}}$

Let $S_{n} = \sum^{\infty}_{k=1} \frac{1}{k^{2}}$
$$S_{n}= 1 + \frac{1}{2^{2}} + \frac{1}{3^{3}} \dots \frac{1}{(n-1)^{2}} + \frac{1}{n^{2}}$$
$$S_{n}\le 1 + \frac{1}{1*2} + \frac{1}{2*3} \dots \frac{1}{(n-2) * (n-1)} + \frac{1}{(n-1)*(n)}$$

Based on the above $S_n$ is bounded from above summation. If you expand the above;
$$S_{n}\le 1 + \left(1 - \frac{1}{2}\right)+ \left(\frac{1}{2} - \frac{1}{3}\right) \dots + \left(\frac{1}{n-2} - \frac{1}{n-1}\right)+ (\frac{1}{n-1} - \frac{1}{n})$$

Which will be equals to $2 - \frac{1}{n}$ which will be less than 2. Since the partial sum is bounded by 2 therefore $\sum^{\infty}_{n=1} \frac{1}{n^{2}}$ <span style='color:#0fb9b1'>converges</span>.

## Integral Test

To use this test, the function must be <span style='color:#f7b731'>continuous, positive and decreasing </span>for all $x \ge 1$.

The value <span style='color:#eb3b5a'>cannot determine the total value of the series</span>

$$\int^{\infty}_{1} f(x) dx = \sum\limits^{\infty}_{n = 1} f(x)$$

## P-Series

For any function where it is $\frac{1}{x^{p}}$, then $$\sum\limits^{\infty}_{n = 1} \frac{1}{n^{p}}$$
will be convergent <span style='color:#f7b731'>if and only if</span> $p \gt 1$.

## Comparison Test

This test can only be applied if the <span style='color:#f7b731'>2 functions are non negative</span>. One is the actual series and the other is a approximation (Something close) such that, $0 \le a_{n} \le b_{n}$, for all n.

Therefore, if $\sum^{\infty}_{n=1}b_{n}$ is convergent then  $\sum^{\infty}_{n=1}a_{n}$
> If the <span style='color:#f7b731'>bigger series is convergent</span> then the smaller series is also convergent

Therefore, if $\sum^{\infty}_{n=1}a_{n}$ is divergent then  $\sum^{\infty}_{n=1}b_{n}$
> If the <span style='color:#f7b731'>smaller series is divergent</span> then the bigger series will be convergent

This is usually used with the P-Series.

## Ratio Test

Given a series such that $$\lim_{n \rightarrow \infty} |\frac{a_{n}+1}{a_{n}}| = L$$
If $0 \le L \lt 1$ then the sequence is convergent
If $L \gt 1$ then the sequence is divergent
If $L = 1$ then the it is inconclusive

Used when the function has a factorial
## Root Test

Given a series such that $$\lim_{n \rightarrow \infty} \sqrt[n]{|a_{n}|} = L$$
If $0 \le L \lt 1$ then the sequence is convergent
If $L \gt 1$ then the sequence is divergent
If $L = 1$ then the it is inconclusive

Used when the function has a power of n
### Absolute Convergent

If $\sum^{\infty}_{n = 1} |a_{n}|$ is convergent then $\sum^{\infty}_{n = 1} a_{n}$ is also convergent

## Alternating Series

It is a series where it changes between + and -

If a sequence, is all positive numbers such that:
- $b_{n}$ is decreasing for all of n
- $\lim_{n \rightarrow \infty} b_{n}$ = 0

Therefore alternating series $$\sum^{\infty}_{n = 1} (-1)^{n - 1} b_{n}$$
will be <span style='color:#0fb9b1'>convergent</span>.

# Power Series
---
It is in the form of $$\sum^{\infty}_{n = 0} C_{n}(x-a)^{n}$$
X : is a variable
$C_n$ : is a constant where it can be 0

-  This series will always converge when x = a
-  The series converges for all x
-  There is a positive number $R$ such that the series converges absolutely if $|x - a| \lt R$ and diverges if $|x - a| \gt R$
	This value R is called the <span style='color:#f7b731'>radius of convergence </span>
## Interval of Convergence

If $L$ using the ratio or root test is some real number or $\infty$ then $R = \frac{1}{L}$

By convention:
- If $L = 0$ then $R = \infty$
- if $L = \infty$ then $R = 0$

To find the value of R:
$\sum^{\infty}_{n = 0} C_{n}(x-a)^{n}$

Just use the ratio test on $C_n$  which is $L = \lim_{n \rightarrow \infty} |\frac{{C_{n+1}}}{C_{n}}|$

To find the interval of convergence, once $R$ is found
- Sub center of the power series + $R$ into the series and check if its divergent or convergent
- Sub center of the power series +$-R$ into the series and check if its divergent or convergent

The center of the power series is the value of $a$

## Power Series Representation

For $|x| \lt 1$

$\sum^{\infty}_{n = 0} x^n$ is called a power series and can be represented with $\frac{1}{1 - x}$ about x = 0

Thus we need to make the function to be in some form if $\frac{1}{1-x}$ where x can also be some function

If $R \gt 0$ then the power series is differentiable and can be integrated on $|x - a| \lt R$

$$f'(x) = \sum^{\infty}_{n = 1} nc_{n}(x - a)^{n-1} \text{ for } |x - a| \lt R$$

$$\int f(x) dx = \sum^{\infty}_{n = 1} c_{n} * \frac{(x - a)^{n-1}}{n+1} + C \text{ for } |x - a| \lt R$$

## Taylor Series & Maclaurin Series

If to derive the power series is difficult to build a link you can use this method

$$C_{n} = \frac{f^{n}(a)}{n!}$$

$$f(x) = \frac{f^{n}(a)}{n!}(x - a)^{n}$$

---
title: Real Numbers
Date Created: 2023-08-19
tags:
  - MA1521
  - Math
---

# Real Numbers
---
## Symbols

$\Bbb R$ -> It is the set of all <span style='color:#f7b731'>real numbers</span>
$\Bbb Q$ -> It is the set of all <span style='color:#f7b731'>rational numbers</span>, where it can be expressed as a ratio, $\frac{p}{q}$ where $q \neq 0$
$\Bbb P$ -> It is the set of all <span style='color:#f7b731'>irrational numbers</span>

$\in$ -> Means that a variable <span style='color:#f7b731'>is a member</span> of a particular set

$[a,b]$ -> Closed Interval, $a \le x \le b$ where, $a \lt b$
$(a,b)$ -> Open Interval, $a \lt x \lt b$

The above can be use in combination, example $(a,b]$ which is, $a \lt x \le b$

# Absolute Value
---

An <span style='color:#0fb9b1'>absolute value</span>, $|x|$ is the positive value of a number $x \in \Bbb R$

The value of x can be either, <mark class="hltr-yellow">x or -x</mark>.

## Properties of Absolute Values

1) Absolute value of a negative value <span style='color:#f7b731'>is equal</span> to the absolute value of a positive value, $|-x| = |x|$

2) Absolute value of x * y = absolute x * absolute y, $|xy| = |x||y|$

3) For any real number x, $-|x| \le x \le |x|$
	To prove for any absolute inequality is true, just prove that $-(x) \le x \space \land |x| \le x$

5) For $r \gt 0$, $|x| < r \iff x \in (-r,r)$

6) $\sqrt{x^{2}}= |x|$

 6) <span style='color:#0fb9b1'>Triangle Inequality</span>, $|x + y| \le |x| + |y|$
	 There is a <span style='color:#0fb9b1'>reverse triangle inequality</span>, where $||x| - |y|| \le |a + b|$


# Functions
---

Functions are denoted as $f(x)$, where <span style='color:#f7b731'>it will assign a value a to a specific member of b</span>, $a \rightarrow b$

## Definitions

**Domain**
> $a \in A$, is <span style='color:#f7b731'>all possible inputs</span> of a function.

**Codomain**
> $b \in B$, is <span style='color:#f7b731'>all possible outputs</span> of a function, this is taken to be the set of all real numbers, $\Bbb R$.

**Range**
> Very similar to codomain, however it is the set of <b><mark class="hltr-yellow">all actual outputs</mark></b> of a function.

**Real Valued Function**
> A function which maps $A \rightarrow \Bbb R$, on a graphical scale, it will consist of all points where $x \in A$

**Injective Functions**
> As long as for any $x \in A$ maps to <mark class="hltr-yellow">one unique</mark> value in the domain. <mark class="hltr-yellow">Not all</mark> $y \in B$ will be mapped

**Surjective Functions**
> For any $x \in A$ maps to <mark class="hltr-yellow">one value in the domain for all</mark> $y \in B$.

**Bijective**
> If a function is <span style='color:#f7b731'>injective and surjective</span>, then it is a bijective function
## Composite Functions

If, a function **f** maps $A \rightarrow B$ and another function **g** maps $B \rightarrow C$ then the <span style='color:#0fb9b1'>composite function</span>, $g \circ f$, will map $A \rightarrow C$, $g(f(x))$.

## Inverse Functions

An inverse function denoted as $f^{-1}$ <span style='color:#f7b731'>comes in a pair and can work interchangeably</span>, where $x \in A$ is a input into, $g \circ f$ will return $x$.

# Polynomials
---

Any function form where, $a_nx^n +a_{n-1}x^{n-1}...+a_1x+a_0$ is called a <span style='color:#0fb9b1'>polynomial</span> to a <span style='color:#0fb9b1'>degree</span> of n where $n \ne 0$

In general a polynomial of a degree of n has <span style='color:#f7b731'>at most n real roots</span>.

## Rational Functions

It is the same as a rational number but it is in <span style='color:#f7b731'>function form</span>, $\frac{p(x)}{q(x)}$. The <span style='color:#0fb9b1'>domain</span> of the rational function is all the real numbers except the roots of $p(x)$.

# Logarithms
---

An <span style='color:#0fb9b1'>exponential function</span> is, $f(x) = a^x$ and the inverse function $\log_a x$, is called the <span style='color:#0fb9b1'>logarithmic function</span>.

$e$ -> Is called the **Euler Number**

$ln x$ is called the <span style='color:#0fb9b1'>natural logarithm</span>.

# Maximal Domain and Range
---

The domain of a function if its <span style='color:#f7b731'>not specified</span>, will be defined to be as <span style='color:#f7b731'>large as possible</span>. Which is called the <span style='color:#0fb9b1'>maximal domain</span>.

In math, the range is more well sort after compared to the codomain.

## Finding the Maximal Domain

For the maximal domain, it <span style='color:#f7b731'>will usually be</span> $\Bbb R$, minus certain <span style='color:#f7b731'>values which makes the function undefined.</span> This is usually for rational functions and trigonometric or logarithmic equations.

Example:

For $f(x) = \frac{1}{x-1}$, the maximal domain is $\Bbb R \setminus \{1\}$

## Finding the Range

To find the range of the function, let $y = f(x)$. Afterwards <mark class="hltr-yellow">solve for x</mark>, from there the range can be found.

Example:
- Let $f(x) = x^{2} - x + 1$
- $y = f(x) = x^{2} - x + 1$
- $x^{2} - x + (1 - y) = 0$, thus using the quadratic formula; we will get the following
- $$\frac{1 \pm \sqrt{-1^{2}- 4(1)(1-y)}}{2}$$
-  Simplifying it, $$\frac{1 \pm \sqrt{4y - 3)}}{2}$$
-  Here if $y \lt \frac{3}{4}$, it will cause the equation to be undefined, thus the range for $f(x)$ is $[\frac{3}{4}, \infty)$

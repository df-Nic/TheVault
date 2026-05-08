---
title: Limits
Date Created: 2023-08-19
tags:
  - MA1521
  - Math
---
# Basics of Limits
---
## What is a Limit

A limit, is the <span style='color:#f7b731'>value</span> of a function $f(x)$ when $x$ <span style='color:#f7b731'>approaches some value</span> $c$ defined on some interval $I$

**C** is called an <span style='color:#0fb9b1'>interior point</span>.

$\lim\limits_{x \to c^-}$ : This means the behavioral of the value of $f(x)$ when $x$ approaches the value of $c$ <span style='color:#f7b731'>from the left hand side</span>. $x$ will be smaller than $c$.

$\lim\limits_{x \to c^+}$ : This means the behavioral of the value of $f(x)$ when $x$ approaches the value of $c$ <span style='color:#f7b731'>from the right hand side</span>. $x$ will be larger than $c$.

$\lim\limits_{x \to c}$ : For the limit at interior point $c$ (Not an end point) to exist, the l<span style='color:#f7b731'>imit from the right and left</span> side must be <span style='color:#f7b731'>well defined and must equal</span> to each other $\lim\limits_{x \to c^{+}} = \lim\limits_{x \to c^{-}}= L$. Then limit has a value of $L$.
> If $L$ is infinity ($\infty$) then limit is not well defined.

When finding the <span style='color:#0fb9b1'>limit value</span>, it <span style='color:#f7b731'>may not always be the same</span> as the <span style='color:#0fb9b1'>function value</span> when $x = c$. Therefore, when finding the limit value, the function value can be disregarded. 
## Continuity

The term <span style='color:#0fb9b1'>continuity</span> implies that if a function with in a interval $I$, <span style='color:#f7b731'>is continuous</span>, it means the function <span style='color:#f7b731'>is connected</span>.
### Continuity at a Point

<b>C if it is an <span style='color:#8854d0'>interior point</span> of I</b>

The function $f(x)$ is continuous at $x = c$ if
1) $\lim\limits_{x \to c} f(x)$ exists
2) $\lim\limits_{x \to c} f(x) = f(c)$

<b>C if it is an <span style='color:#8854d0'>left end-point</span> of I</b>

The function $f(x)$ is continuous at $x = c$ if
1) $\lim\limits_{x \to c^+} f(x)$ exists
2) $\lim\limits_{x \to c^+} f(x) = f(c)$

<b>C if it is an <span style='color:#8854d0'>right end-point</span> of I</b>

The function $f(x)$ is continuous at $x = c$ if
1) $\lim\limits_{x \to c^-} f(x)$ exists
2) $\lim\limits_{x \to c^-} f(x) = f(c)$

### Continuity at a Interval

For a function $f(x)$ is continuous on an <span style='color:#0fb9b1'>interval</span> if it is continuous at $x = c$ for <span style='color:#f7b731'>all values</span> within the interval.

## Laws of Limits

For all the rules to be true, the <span style='color:#f7b731'>limit must exist for all functions involved</span> and $k$ is the constant.

1)  $\lim\limits_{x \to c} (f(x)\pm g(x)) = \lim\limits_{x \to c} f(x) \pm \lim\limits_{x \to c} g(x)$
2)  $\lim\limits_{x \to c} kf(x) = k \lim\limits_{x \to c} f(x)$
3)  $\lim\limits_{x \to c} (f(x)g(x)) = \lim\limits_{x \to c} f(x) * \lim\limits_{x \to c} g(x)$
4) $\lim\limits_{x \to c} \frac{f(x)}{g(x)} = \frac{\lim\limits_{x \to c} f(x)}{\lim\limits_{x \to c} g(x)}$, provided $\lim\limits_{x \to c} g(x) \ne 0$
5)  If $g(x)$ is continuous at point b, and the $\lim\limits_{x \to c} f(x) = b$ then $\lim\limits_{x \to c} g(f(x)) = g(\lim\limits_{x \to c} f(x))$

Therefore, the <span style='color:#f7b731'>following functions are continuous</span> for any interval in their <span style='color:#0fb9b1'>maximal domain</span>.
1) Polynomials
2) Trigonometric Functions
3) Exponential Functions
4) Logarithmic Functions
5) Any combination
6)  Rational function, where the value of the denominator cannot be 0

If the function is <span style='color:#f7b731'>known the be continuous</span>, then the <span style='color:#f7b731'>limit is just the value at</span> $f(c)$

# Limits at Infinity
---

$\lim\limits_{x \to \infty} f(x) = c$ or $\lim\limits_{x \to -\infty} f(x) = c$ then the line at $y = c$ is the <span style='color:#0fb9b1'>horizontal asymptote</span> of the function $f(x)$.
> A horizontal asymptote is the line that the graph <span style='color:#f7b731'>will approach but never touches</span>.

## Indeterminate Forms

$\lim\limits_{x \to c} \frac{f(x)}{g(x)}$ where $f(x) \rightarrow 0$ and $g(x) \rightarrow 0$ as $x \rightarrow c$, this is an indeterminate form of type $\frac{0}{0}$
> This is the same where $f(x)$ and $g(x)$ goes to $\infty$.

A way around this is the <span style='color:#0fb9b1'>replacement rule</span>.
> Let $I$ be the interval containing a interior point $c$. $f(x) = g(x)$ for all $x \in I$, except possibly at $x = c$. Then $\lim\limits_{x \to c} f(x) = \lim\limits_{x \to c} g(x)$.

### Infinite Indeterminate Forms

This will usually occurs in 2 polynomials where the numerator and denominator is $\frac{\infty}{\infty}$.

A and B are the <span style='color:#f7b731'>coefficients of the leading term</span>, A for the numerator and B is for the denominator.
$\alpha$ and $\beta$ are the <span style='color:#f7b731'>power of the leading term</span>. A for the numerator and B is for the denominator.

Then the limit is:
1) 0 if $\alpha \lt \beta$
2) $\frac{A}{B}$ if $\alpha = \beta$
3)  $\infty$ or $-\infty$ if $\alpha \gt \beta$, depending on the signs of A and B

Note when dealing with square roots, determine if its the negative or positive value.
# Limits on Trigonometric Functions
---

If $\lim\limits_{x \to c} f(x) = 0$ then.
- $\lim\limits_{x \to c} \frac{sin(f(x))}{f(x)} = \lim\limits_{x \to c} \frac{g(x)}{sin(g(x))} = 1$.
- $\lim\limits_{x \to c} \frac{tan(f(x))}{f(x)} = \lim\limits_{x \to c} \frac{g(x)}{tan(g(x))} = 1$.

If just subbing in the value of $c$ gives an <span style='color:#0fb9b1'>indeterminate form</span>, then the solution to <span style='color:#f7b731'>find the limit of a trigonometric function</span> will rely on the statements above.

# Squeeze Theorem
---

Suppose, $g(x) \le f(x) \le h(x)$ for all $x$ in some interval containing point $c$, except possibly at x = c. If $\lim\limits_{x \to c} g(x) = \lim\limits_{x \to c} h(x) = L$, then - $\lim\limits_{x \to c} f(x) = L$.

To summarize the statement, if there is a <span style='color:#f7b731'>upper bound and lower bound function</span>, if the limit at x is the <span style='color:#f7b731'>same for both the upper bound and lower bound function</span>, then the function will have the same limit.
# Intermediate Value Theorem
---
If a real-valued function f is continuous on $[a, b]$ and <span style='color:#f7b731'>k is a number
between f (a) and f (b)</span>, then f (c) = k for some c $\in [a, b]$.

This can be applied if the function is <mark class="hltr-orange">continuous</mark> and <mark class="hltr-orange">interval is closed</mark>.

The intermediate value theorem <span style='color:#f7b731'>guarantees at least one intersection</span> at the line $y = k$. But it <span style='color:#f7b731'>does not show uniqueness</span> as there can be multiple intersections.
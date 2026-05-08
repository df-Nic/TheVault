---
title: Derivatives
Date Created: 2023-08-27
tags:
  - MA1521
  - Math
---
# Differentiability
---
## Definition of Derivative

The <span style='color:#0fb9b1'>derivative</span> of a function at a point is denoted as $f'(x_0)$. Which is given by the following limit, $\lim\limits_{h \to 0} \frac{f(x_{0}+ h) - f(x_0)}{h}$.

An alternative function is, $\lim\limits_{x \to 0} \frac{f(x) - f(x_0)}{x - x_0}$.

The function is the <span style='color:#f7b731'>straight line </span>which passes 2 points $f(x_0)$ and $f(x_{0}+ h)$, $y -y_{0} = m (x-x_{1})$

$h$ the denominator is the rate of change of the graph. As $h$ approaches 0, the gap between $f(x_0)$ and $f(x_{0}+ h)$ will be <span style='color:#f7b731'>smaller</span> and will <span style='color:#f7b731'>eventually hit point P</span> ($f(x_0$)) when $h$ = 0.

If the <span style='color:#f7b731'>limit exists</span> at $x_0$ then the <span style='color:#f7b731'>tangent line also exists</span>.

Therefore, $f'(x)$ exits for all x in a interval then it can be <span style='color:#f7b731'>treated as a function</span>. 
$$\frac{d}{dx}f(x) = \frac{dy}{dx} = \frac{df}{dx} = f'(x) = \lim\limits_{h \to 0} \frac{f(x_{0}+ h) - f(x_0)}{h}$$

If a function is <span style='color:#f7b731'>differentiable, then the function is also continuous</span>. But if <mark class="hltr-orange">a function is continuous, then the function is not guarantee to be differentiable</mark>.

A function is differentiable on an interval $I$, if it is differentiable in every point in I.

## Differentiable Functions and their Derivatives

![[Differentiate Tale.png|center]]


## Rules of Differentiation

![[Rules of Differentiation Table.png|center]]

### Chain Rule

![[Chain Rule Differentiation Formula.png|center]]

The <span style='color:#0fb9b1'>Chain Rule</span> can be simplified to $\frac{dy}{dx} = \frac{dy}{du} * \frac{du}{dx}$.

This can be applied to functions where the <span style='color:#f7b731'>x and y values cannot be separated</span>.

For example $x^3 - xy= 0$, the $\frac{dy}{dx}$ of the function is  $3x^{2} - \left(y + x\frac{dy}{dx}\right)= 0$.
Afterwards make $\frac{dy}{dx}$ the <span style='color:#f7b731'>subject of the equation</span>. Which will be $\frac{3x^{2}- y}{x}$.

# Derivative of Inverse Functions
---

For functions which are <span style='color:#f7b731'>increasing</span> and <span style='color:#f7b731'>decreasing</span>. It is safe to say that they are also <span style='color:#0fb9b1'>bijective</span>. And therefore the exist an inverse function.

Let  $b = f^{-1}(a)$ such that $f(b) = a$, therefore at ($a$,$f^{-1}(x)$) = ($a$,$b$) on the inverse function, the gradient of the tangent is the following.
$$(f^{-1})'(a) = \frac{1}{f'(f^{-1}(a))} = \frac{1}{f'(b)}$$

# Parametric Equations
---

A parametric equation is an equation where <span style='color:#f7b731'>x and y are represented by another similar variable</span>.

Therefore to differentiate such equation it will be: $$\frac{dy}{dx} = \frac{dy}{dt} / \frac{dx}{dt} = \frac{f'(x)}{g'(t)}$$
To find the second derivative, $\frac{d^{2}y}{dx^{2}} = \frac{d}{dx} (\frac{dy}{dx})/ \frac{dx}{dt}$, dividing by $\frac{dx}{dt}$ is because the first derivative is in terms of t as it is a parametric equation. 

# Other Problematic Equations
---

Some examples such as $\log_{10}x$ and $f(x)^{g(X)}$

For the logarithm, use the change of base formula and <span style='color:#f7b731'>change the base to ln</span>, $\frac{ln x}{ln 10}$

As for the other equation with a power of a function, <span style='color:#f7b731'>use ln to bring the power down</span>, $ln y = g(x) * ln(f(x))$

# Applications of Derivatives
---
## Tangent & Normal

The <span style='color:#0fb9b1'>tangent</span> of a function at a point is defined by the equation. Where $x_0$ is a point of the differentiable function.
$$y - f(x_{0)}= m(x-x_0)$$

The <span style='color:#0fb9b1'>normal</span> of a function at a point is defined by the equation. Where $x_0$ is a point of the differentiable function.

$$y - f(x_{0}) = -\frac{1}{m}(x-x_0)$$

$m = f'(x_0)$

When finding some value where the <span style='color:#f7b731'>graph is parallel to the axis</span>. It means that the <span style='color:#f7b731'>gradient for the tangent must be 0</span> (x-axis), and the <span style='color:#f7b731'>gradient of the normal must be 0</span> (y-axis).
### Parametric Tangent & Normal

Similar to above however:

$x = x(t)$ and $y = y(t)$

**Tangent Line Formula**:
$$y - y(t_{0}) = m(x-x(t_0))$$

**Normal**
$$y - y(t_{0}) = -\frac{1}{m}(x-x(t_0))$$

## Increasing and Decreasing Functions

The <span style='color:#0fb9b1'>derivative</span> of a function can also <span style='color:#f7b731'>help in determining if the function is increasing and decreasing</span> in a interval.

For it to work, the interval $(a,b)$ <span style='color:#f7b731'>must be differentiable</span> for function $f$ and it <span style='color:#f7b731'>must be continuous</span> at $[a,b]$.
1) f is <span style='color:#f7b731'>increasing</span> if $f'(x) > 0$ for all x in $(a,b)$, except when $f'(x) = 0$
2) f is <span style='color:#f7b731'>decreasing</span> if $f'(x) < 0$ for all x in $(a,b)$, except when $f'(x) = 0$

However there are some points were $f'(x) = 0$. It <span style='color:#f7b731'>does not mean</span> that the function is not increasing / decreasing.

If a <span style='color:#f7b731'>function is decreasing or decreasing</span> then the function is <span style='color:#0fb9b1'>injective</span>. Why, because for a function to be;
1) Increasing : $f(x_{1}) < f(x_{2})$ for all  $x \in I$ and $x_{1} < x_{2}$
2) Decreasing : $f(x_{1}) > f(x_{2})$ for all $x \in I$ and $x_{1} < x_{2}$

Thus this will prove that a function is injective (one to one).

To prove for range that is in the set of $\Bbb R$, depending on the function if its increasing or decreasing;
1) Increasing : Show that from the <span style='color:#f7b731'>left end point to the right end point</span>, will go from $-\infty$ to $\infty$
2) Decreasing : Show that from the <span style='color:#f7b731'>left end point to the right end point</span>, will go from $\infty$ to $-\infty$

## Concavity of a Function

It is defined as the following:
1) A graph is concave upward if every point on on interval $(a,b)$ is also concave upwards.
2) A graph is concave downwards if every point on on interval $(a,b)$ is also concave downwards.

For a graph to be concaved upwards or downwards, the tangent line at a specific point inside the interval $(a,b)$ <span style='color:#f7b731'>must be a lower-bound and upper-bound</span> for the curve for all values in the interval, respectively.

To find the concavity of a function:
1) If $f''(c) > 0$, then the graph of f is <span style='color:#f7b731'>concave upward</span> at $(c; f(c))$.
2) If $f''(c) < 0$, then the graph of f is <span style='color:#f7b731'>concave downward</span> at $(c; f c))$.

**Point of inflation**
> It is a point $(x, f(x))$ on the graph where $f''(x) = 0$ and the <span style='color:#f7b731'>concavity of the function changes</span> from upwards to downwards or vise versa.

## Related Rates

Let $y = f (x)$ and let x and y be functions of a third variable t that represents, for example, time. By the Chain Rule; $$\frac{dy}{dt} = \frac{dy}{dx} * \frac{dx}{dt}$$
For example if the function represents speed, then the differentiation of the function will be the acceleration.

## Absolute Extrema

It is defined as:
1) absolute/global maximum at x = c if $f(x) \le f(c)$ for all x in the domain of f.
2) absolute/global minimum at x = c if $f(x) \ge f(c)$ for all x in the domain of f.

It can be <span style='color:#f7b731'>difficult to find the maximum or minimum</span> in the entire range, therefore it will help to find the <span style='color:#0fb9b1'>local extrema</span>.
### Local Extrema

It is defined as:
1) relative/local maximum at x = c if $f(x) \le f(c)$ for x in some <span style='color:#f7b731'>open interval</span> containing x = c.
2) relative/local minimum at x = c if $f(x) \ge f(c)$ for x in some <span style='color:#f7b731'>open interval</span> containing x = c.

**Extreme Value Theorem**
> If f is <span style='color:#f7b731'>continuous</span> on a <span style='color:#f7b731'>closed interval</span> $[a,b]$, then it <span style='color:#f7b731'>will contain a absolute maximum and minimum</span> value at some points in $[a,b]$

If the graph is not continuous or not closed, then there is a possibility that the <span style='color:#f7b731'>global maximum and minimum might not exist</span>. (It reaches this extrema value but it cannot be equals to it thus it is not well defined).

If the <span style='color:#f7b731'>derivative of a function</span> where x = c and $f'(c) = 0$, then <span style='color:#f7b731'>it will contain a local maximum/minimum</span>. And there is a <span style='color:#f7b731'>change in the tangent gradient</span> from a negative to positive or vise versa.

**Critical Point**
> It is not an end-point and either $f'(c) = 0$ or $f'(c)$ does not exist.

Take note that not all critical point will provide a local extrema value. For example tan x where x = $\frac{\pi}{2}$. $f'(c)$ does not exist but the function is not defined at that point.

To find the global extrema;
1) Find all critical points in the function from $[a,b]$
2) Then find the values of $f(a)$ and $f(b)$
3) Compare with all the values and the largest and the smallest is the global extrema.

### First Derivative Test for Absolute Extrema

If $f'(x) \gt 0$ for all  $x \lt c$ and $f'(x) \lt 0$ for all $x \gt c$ then <span style='color:#f7b731'>f has an absolute minimum at point c</span>.

If $f'(x) \lt 0$ for all  $x \lt c$ and $f'(x) \gt 0$ for all $x \gt c$ then <span style='color:#f7b731'>f has an absolute maximum at point c</span>.

### First Derivative Test for Local Extrema

Let f be continuous on an interval containing a critical point c.
1)  If $f'$ changes from <span style='color:#f7b731'>positive to negative</span> at x = c, then f has a <span style='color:#f7b731'>local maximum</span> at c.
2)  If $f'$ changes from <span style='color:#f7b731'>negative to positive</span> at x = c, then f has a <span style='color:#f7b731'>local minimum</span> at c.
3)  If $f'$ <span style='color:#f7b731'>does not change sign</span> at x = c, then f has <span style='color:#f7b731'>no local extremum</span> at c.

### Second Derivative Test for Local Extrema

1) If $f'(c) = 0$ and $f''(c) < 0$, then f has a <span style='color:#f7b731'>local maximum</span> at c.
2) If $f'(c) = 0$ and $f''(c) > 0$, then f has a <span style='color:#f7b731'>local minimum</span> at c.
3) No conclusion can be drawn if $f''(c) = 0$.

## L’ Hopital’s Rule

Let $f(x)$ and $g(x)$ be differentiable at all points in some open interval containing x = c

If $\lim\limits_{x \to c} f(x) = 0 / \infty = \lim\limits_{x \to c} g(x)$. Then;

$$\lim\limits_{x \to c} \frac{f(x)}{g(x)} = \lim\limits_{x \to c} \frac{f`(x)}{g`(x)}$$

If the derivate is still gives a undetermined value then <span style='color:#f7b731'>continue to differentiate</span> the function.

### Some Special Cases

$0^0$ : $\lim\limits_{x \to 0^{+}}x^x$ it can be rewritten to $\lim\limits_{x \to 0^{+}}e^{ln(x^x)}$ which is equals to $e ^ {\lim\limits_{x \to c} x ln x}$

$\infty^0$ : $\lim\limits_{x \to 0^{+}} \frac{2}{x}^x$ the power can be brought down and then use L' Hopital's Rule

$1^\infty$ : $\lim\limits_{x \to 0^{+}}(cos x)^\frac{1}{x}$, do the same as $0^0$
## Rolle's Theorem

Let f be <span style='color:#f7b731'>continuous</span> on $[a, b]$ and <span style='color:#f7b731'>differentiable</span> on (a, b).

If f (a) = f (b), then there is at least one number c in (a, b) such that $f'(c) = 0$.

### Mean Value Theorem

Let f be <span style='color:#f7b731'>continuous</span> on $[a, b]$ and <span style='color:#f7b731'>differentiable</span> on $(a, b)$. Then, there is at least one number c in (a; b) such that $f'(c) = \frac{f(b) - f(a)}{b-a}$.

This is the basis where the first derivative can be used to check if the function is increasing or decreasing.
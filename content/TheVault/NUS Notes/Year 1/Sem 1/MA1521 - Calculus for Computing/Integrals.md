---
title: Integrals
Date Created: 2023-08-31
tags:
  - MA1521
  - Math
---
# Antiderivatives
---

It is basically the <span style='color:#f7b731'>original function</span> from the derivate function.

One important point to take note is that all integrations will <span style='color:#f7b731'>have a + c at the back</span>. This is to denote the constant which will be removed after the differentiation.

General Indefinite Integral : $$\int f(x) dx = F(x) + c$$
Let $\alpha$ and $\beta$ be a constant, then :
$$\int \alpha f(x) + \beta g(x) dx = \alpha \int f(x) dx + \beta g(x) dx$$

**Completing the Square**

This can be used to help <span style='color:#f7b731'>simplify</span> a <span style='color:#f7b731'>polynomial function with powers of 2</span>, which allows one of the standard integrals to be used to integrate a function.

Given $x^{2} + ax + b$, if it cannot be simplified, it can be expressed as $(x + \frac{a}{2})^{2} - \frac{a^{2}}{4} + b$

## Standard Integrals

![[Standard Integrals.png|center]]

### Trigonometric Identities

![[Trigonometric Identities.png|center]]

# Partial Fractions
---

![[Partial Fractions Table.png|center]]

Supposed the equation to integrate is a fraction of polynomials, then using partial fractions can help.
$$\int \frac{P(x)}{Q(x)}$$

<span style='color:#0fb9b1'>Partial Fractions</span> can be used for polynomial equations which its leading term is <span style='color:#f7b731'>larger than 2</span>.

If the fraction is <span style='color:#f7b731'>not a proper fraction</span>, then <span style='color:#f7b731'>long division is needed</span> to make it proper, in terms of;
$$\int A(x) + \frac{B(x)}{Q(x)}$$

To start simplify Q(x) to be a product of linear or quadratic factors, afterwards refer to the table and solve for $\alpha$ and $\beta$.

## Integration by Substitution

This will be used for functions with complicated terms to integrate, it can be substitute with a variable.

Let g(x) = u, and therefore $\frac{du}{dx} = g'(x)$ which can be rewritten as $du = g'(x) \ dx$. Then by substitution, $$\int f(g(x))g'(x) \ dx = \int f(u) \ du$$ The above equation <span style='color:#f7b731'>can also be flipped around</span>.

![[Trigonometric Substitution Table.png|center]]

Another way of substitution is by substituting a <span style='color:#f7b731'>trigonometric function</span>.

Lets say given the first expression in the table, $x + b = a sin \theta$, the result will be $\sqrt[2]{a^{2} - a^{2}sin^2\theta}$

Simplifying it, $\sqrt[2] {a^2(1 - sin^2\theta)}$ which will be equals to $\sqrt[2]{a^2(cos^2\theta)}$ which will finally be $a\ cos\theta$.

If the polynomial has <span style='color:#f7b731'>a square root</span>, try and use this to simplify the equation.

## Integration by Parts

Based on the chain rule;
$$f(x)g(x) = \int f'(x)g(x) \ dx + \int f(x)g'(x) dx$$
Therefore;
$$\int f'(x)g(x) dx = f(x)*g(x) - \int f(x)g'(x)$$
**Steps to use integration by parts**:
1) Integrate $f'(x)$
2) Differentiate g(x)
3) With the 2 substitute the values into the function above

To determine $f'(x)$ if it is easier to integrate that term then it will be the $f'(x)$
To determine $g(x)$, if after differentiating it makes it easier to integrate, it will be $g(x)$

### Rule of Thumb on How to Choose f'(x) and g(x)

![[Basic Rules for Integration By Parts.png|center]]


# Reimann Sums
---

A graph which is continuous from $[a, b]$, then one way to <span style='color:#f7b731'>find the area under the curve</span> is bounded by a to b can be donated by; $$\int^{b}_{a} f(x) dx$$
At least when $f(x) \ge 0$ and $a \lt b$

Therefore the Reimann sum which can <span style='color:#f7b731'>approximate</span> the are under the curve is defined as $$\lim_{n \rightarrow \infty}\{\sum^{n}_{k=1} (\frac{b-a}{n})f(a + k(\frac{b-a}{n}))\}$$
Where **a and b** are the <span style='color:#f7b731'>lower and upper limits</span>

We can also prove that the equation above will be equals to some other equation $Q(x)$, how to prove;
1) Make the function be in the form of $\frac{b-a}{n}f(a + k\frac{b-a}{n}))$
2) Afterwards find the values of A and B
3) Find the function F(x)
# Fundamental Theorem of Calculus (FTC)
---
## First Theorem

Another way of calculating the area under the curve bounded by $[a, b]$ is using FTC 1, which is defined as; $$\int^{b}_{a} f'(x) dx = F(b) - F(a)$$
## Second Theorem

If $g(x) = \int^{x}_{a} f(t) dt$ where $a \le x \le b$  and it is<span style='color:#f7b731'> continuous and differentiable on (a, b)</span> and $g'(x) = f(x)$ then; $$\frac{d}{dx}\int^{x}_{a} f(t) dt = f(x)$$
And if $g(x)$ is <span style='color:#f7b731'>differentiable</span> then by <span style='color:#0fb9b1'>chain rule</span>; $$\frac{d}{dx}\int^{g(x)}_{a} f(t) dt = f(g(x))g'(x)$$
![[Properties of Definite Integrals.png|center]]

# Miscellaneous Terms
---

Given a fraction of a <span style='color:#f7b731'>polynomial equation where the denominator cannot be factorized</span>. Example $$\int\frac{3x+7}{x^{2+4x+5}}$$
One way to solve this is to <span style='color:#f7b731'>modify the numerator</span> such that that it is a <span style='color:#f7b731'>product from the differentiation of the denominator</span> ($\frac{dy}{dx} denominator = numerator$). Afterwards the substitution method can be used to solve for the integral.

# Improper Integral
---

It happens when the integral of a function $f(x)$ for the area under the curve from x = 0 to x = $\infty$ or in other words the <span style='color:#f7b731'>bound is infinity</span>.

## Type 1 Improper Integrals

Here are the different variations of the <span style='color:#0fb9b1'>type 1 improper integrals</span>.

1) If $f(x)$ is continuous on $[a, \infty)$;
$$\int^{\infty}_{a}f(x) dx = \lim_{b \rightarrow \infty} \int^{b}_{a}f(x) dx $$
2)  If $f(x)$ is continuous on $(-\infty, b]$;
$$\int^{b}_{-\infty}f(x) dx = \lim_{a \rightarrow -\infty} \int^{b}_{a}f(x) dx $$
 3) If $f(x)$ is continuous on $(\infty, -\infty)$;
$$\int^{\infty}_{-\infty}f(x) dx = \int^{c}_{-\infty} f(x) dx + \int^{\infty}_{c} f(x) dx $$
Where c is any real number.

## Type 2 Improper Integrals

The difference between type 1 is that type 2 is when the <span style='color:#f7b731'>function value goes to infinity within the integration boundry</span>.

1) If $f(x)$ is continuous on $(a, b]$ and is discontinuous at a;
$$\int^{b}_{a}f(x) dx = \lim_{c \rightarrow a^+} \int^{b}_{c}f(x) dx $$
2)  If $f(x)$ is continuous on $[a, b)$ and is discontinuous at b;
$$\int^{b}_{a}f(x) dx = \lim_{c \rightarrow b^-} \int^{c}_{a}f(x) dx $$
 3) If $f(x)$ is discontinuous on $a \lt c \lt b$;
$$\int^{b}_{a} f(x) dx = \int^{c}_{a} f(x) dx + \int^{b}_{c} f(x) dx $$

If the limit is finite then the improper integral converges, it it does not exist then it diverges.

# Applications of Integration
---
## Area Bounded by 2 Curves

### X-axis

Given 2 curves, we can use integration to find the area bounded by the 2 curves.

Assuming $f(x) \ge g(x)$ for all values of x. Then $$Area = \int^{b}_{a} f(x) - g(x) dx$$
However if its not guarantee that $f(x)$ is always greater than $g(x)$ for all of x, then the area will need to be computed at different intervals using; $$Area = \int^{b}_{a} |f(x) - g(x)| dx$$
Therefore it is good to take the <span style='color:#f7b731'>absolute value if you are unsure that it will always be positive</span>.

## Y-axis

The above will be used if the area can be calculated when y is in terms of x. Sometimes given the curve, it can be easier to find the are when x is expressed in terms of y.

Assuming $f(y) \ge g(y)$ for all values of y. Then $$Area = \int^{d}_{c} f(y) - g(y) dy$$
However if its not guarantee that $f(y)$ is always greater than $g(y)$ for all of y, then the area will need to be computed at different intervals using; $$Area = \int^{b}_{a} |f(y) - g(y)| dy$$
## Finding the Volume of a Solid

When the plane region bounded by the curve y = f (x) and the lines x = a and x = b is revolved completely about the x axis, the volume of the solid formed is;
$$Volume = \pi \int^{b}_{a} f(x)^{2}dx$$
This is known as the <span style='color:#0fb9b1'>disk method</span>.

Using the same concept, if assuming $f(x) \ge g(x)$ for all values of x. Then the volume of the disk bounded by the 2 curves is denoted as;
$$Volume = \pi \int^{b}_{a} f(x)^{2} dx \ - \pi \int^{b}_{a} g(x)^{2}dx$$

If it is <span style='color:#f7b731'>rotated along the y-axis</span> instead, then make x in terms of y.

Sometimes X cannot be expressed in terms of y and thus, the <span style='color:#0fb9b1'>shell method</span> can be used. However for this method, if the curve is <span style='color:#f7b731'>rotated along the x-axis</span>, the function must be expressed in terms of y.
$$Volume = 2\pi \int^{b}_{a} x|f(x)|dx$$

## Arc Length of a Curve

The arc length can be visualized as a curve as consisting of many small slanted line segments, and each slanted line segment is the hypotenuse of a right-angled triangle of base length $dx$ and of height $dy$.
$$Arc \ Length = \int^{b}_{a} \sqrt{1 + f'(x)^{2}}dx$$
The same formula can be used when x is expressed in terms of y. Express in terms of x when the graph is not well defined.
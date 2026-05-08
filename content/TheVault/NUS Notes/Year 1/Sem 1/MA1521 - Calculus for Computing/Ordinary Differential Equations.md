---
title: Ordinary Differential Equations
Date Created: 2023-11-08
tags:
  - MA1521
  - Math
---
# ODE
---

What is a ODE, it is an equation involving $x$ and $y$ and <span style='color:#f7b731'>at least one derivative of y</span>

Its <span style='color:#0fb9b1'>order</span> is the order of the <span style='color:#f7b731'>highest derivate </span>that occurs in the equation. For example $y = x + \frac{dy}{dx}$ is a first degree ODE

## Separable ODE

It is a <span style='color:#f7b731'>first degree ODE</span> in the form of : $$\frac{dy}{dx} = f(x)g(y)$$
The meaning of <span style='color:#0fb9b1'>seperable</span> is that x and y can be separated into <span style='color:#f7b731'>2 independent functions</span> in terms of x and y

The goal of the ODE is to get back the function in terms of $y = f(x)$ and the steps to do this are : 
1) $\frac{dy}{dx} = f(x)g(y)$
2) $\frac{1}{g(y)}dy = f(x) dx$
3) $\int \frac{1}{g(y)}dy = \int f(x)dx$
4) After part 3 it will return the equation $y = \text{some x terms} + c$

To go about this, first is to find an equation in terms of $\frac{dy}{dx}$ and $x$ and $y$ then apply the methods solve

**Tips**
1)  $ln$ and $e$ cancel each other out
2) $\tan^{-1} y = x \equiv y = \tan(x)$
3) $ln a - ln b = ln (\frac{a}{b})$ also $lna + ln b = ln(ab))$

### Reduction to a Separable Form

Given some function in the form of $$\frac{dy}{dx} = g(\frac{y}{x})$$
Let $v = \frac{y}{x}$ then $y = vx$ and $\frac{dy}{dx} = v + xv'$

Then the equation can be rewritten as $$v + xv' = g(v) \text{ or } v' = \frac{g(v) - v}{x}$$Afterwards can use the<span style='color:#f7b731'> separation technique</span>

Another general form is $$\frac{dy}{dx} = f(ax + by)$$ 
Such that:
1) $f$ is continuous
2) $b \ne 0$ if it is 0 then the equation is already separable
3) If the <span style='color:#f7b731'>coefficient Infront </span>of $dy/dx$ is not 0

Can be solved by letting $u = ax + by$

**What to substitute**
> In general if there is any common x y term or in the form of $\frac{y}{x}$

Anytime the <span style='color:#f7b731'>denominator</span> (If there is) appears then <mark class="hltr-orange">there is a need to check if it is 0</mark>, if it is then that equation is another solution. In addition if a new factor is introduced then need to check if the factor introduced is a actual solution to the original equation

1) Let the equation be 0
2) Make it in terms of $y = f(x)$
3) Find $y'$
4) Sub $y$ and $y'$ into the original equation and check of it is equals to 0

## Linear First Order ODE

This ODE is in the form of $$\frac{dy}{dx} + P(x)y = Q(x)$$
Where : 
1) $P(x)$ and $Q(x)$ are continuous functions
2) If $P(x)$ is identically equal to $Q(x)$ then it is <span style='color:#0fb9b1'>separable</span>

$I(x) = e^{\int P(x) dx}$ this is the <span style='color:#0fb9b1'>integration factor</span> which will be used to solve this type of ODE. Thus by multiplying with the ODE $$\frac{dy}{dx} e^{\int P(x) dx} + P(x)e^{\int P(x) dx}y = Q(x)e^{\int P(x) dx}$$
However the LHS will be $$\frac{dy}{dx} e^{\int P(x) dx} + P(x)e^{\int P(x) dx}y = \frac{d}{dx}(ye^{\int P(x) dx})$$
Thus to simplify everything it will result in $$\frac{d}{dx}\left(ye^{\int P(x) dx}\right)= Q(x)e^{\int P(x) dx}$$
Integrating both sides $$ye^{\int P(x) dx} = \int Q(x) \cdot e^{\int P(x) dx}$$
## Bernoulli Equation

This ODE is in the form of $$y' + p(x)y = q(x)y^{n}$$
Where : 
1) $P(x)$ and $Q(x)$ are continuous functions on an interval $J$
2) $n \ne 0,1$

Now let $u = y^{1-n}$ and by substituting into the Bernoulli equation $$u' + (1 - n)p(x)u = (1-n)q(x)$$
**Key pointers**

1) When $n = 0$ or $1$ then the equation itself is a<span style='color:#0fb9b1'> first order linear ODE</span>
2)  When $n \gt 0$, the constant 0 function $y(x) = 0$ is <span style='color:#f7b731'>automatically a solution</span> for the Bernoulli equation

Afterwards it can be solved using the <span style='color:#0fb9b1'>linear ODE method</span>. But also remember that y = 0 is also a solution for Bernoulli only

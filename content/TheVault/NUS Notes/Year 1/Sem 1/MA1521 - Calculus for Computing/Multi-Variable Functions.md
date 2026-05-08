---
title: Multi-Variable Functions
Date Created: 2023-10-19
tags:
  - MA1521
  - Math
---
# Single Variable Functions
---
## Vector-Valued Function

$$r(t) = f(t)\mathbf i + g(t)\mathbf j + h(t)\mathbf k \text{ or } r(t) = <f(t)\mathbf, g(t)\mathbf,h(t)\mathbf>$$
Such that:
- $r(t)$ is some mapping to make a vector
	It maps from its domain $D \subseteq \Bbb R$ to its range $R \subseteq \Bbb V_{3}$ ($\Bbb V_{3}$ is $\Bbb R^{3}$, 3 dimensional)
- And each input t will be mapped to <span style='color:#f7b731'>exactly one vector</span>.

It is also called <span style='color:#0fb9b1'>component function</span> of r

This is important as a curve in a 3-D space can be traced by some vector value function and it is called a <span style='color:#0fb9b1'>parametrization</span> of C

### Derivative of a Vector-valued Function

$$r'(t) = \lim_{\Delta t \rightarrow 0} \frac {r(t+\delta t) - r(t)}{\Delta t}$$
Such that:
- $\Delta t$ represents delta t

If the limit exists for $t = a$, then it is differentiable at $t = a$

Then suppose that the components <span style='color:#f7b731'>f , g and h are all differentiable at t = a</span>. Then<span style='color:#f7b731'> r is differentiable at t = a</span> and its derivative is given by $r'(a) = <f'(a), g'(a), h'(a)>$

The rules of differentiation applies to this as well

If $f(t)$ is some scalar function (<span style='color:#eb3b5a'>Not a vector-valued function</span>) then $\frac{d}{dt}f(t) \mathbf r(t)$ is just $$<f(x)x_{1}(t), f(x)y_{1}(t), f(x)z_{1}(t)>$$
Similarly $\frac{d}{dt}\mathbf r(t) \cdot \mathbf s(t)$ will return a <mark class="hltr-orange">real value function</mark> not a vector function $$x_{1}\times x_{2} + y_{1} \times y_{2} + z_{1} \times z_{2}$$
And the <span style='color:#f7b731'>cross product will return a vector valued function</span>

**Tangent Vector**
> Take any point p in $\vec r$ and draw a tangent line. Any line that is parallel to this line is called a <span style='color:#0fb9b1'>tangent vector </span> ($r'(p)$)

Therefore for the derivative when $\Delta t \rightarrow 0$  then it will approach $r'(a)$

## Arc Length of a Space Curve

$$\text{Arc Length } = \int_{a}^{b} \sqrt{f'(x)^{2} + g'(x)^{2} + h'(x)^{2}} dt = \int_{a}^{b} \Vert \Bbb r'(t) \Vert dt$$
This holds if $a \le t \le b$ and $f_0, g_0,h_0$ are continuous. If C is traversed exactly once as t increases from a to b, then its length is

# Functions with 2 Variables
---
A function f of two variables is a rule that assigns <span style='color:#f7b731'>each ordered pair of real numbers</span> (x; y) in a set $D \subseteq \Bbb R^{2} = \Bbb R \times \Bbb R$ a <span style='color:#f7b731'>unique real number denoted by </span>$f(x, y)$.

If a function of two variables with domain D, then the <span style='color:#f7b731'>graph</span> is the set of all points $(x,y,z) \in \Bbb R^{3}$ and $(x,y) \in D$
This is also called a <span style='color:#f7b731'>surface</span> S with the equation $z = f(x,y)$
$$f(x,y) = z$$

**Level Curve**
> A <span style='color:#0fb9b1'>level curve</span> of $f(x, y)$ is the 2 dimensional graph of the equation $f(x, y) = k$ for some constant k. Where it is parallel to the x-y plane

**Contour Plot**
> A <span style='color:#0fb9b1'>contour plot</span> of $f(x, y)$ is a graph of numerous levels curves $f(x, y) = k$ for representative values k.

-  If the level curves are close together, it is steep
-  It will be flatter if the level curves are further apart

## Cylinders and Quadric Surfaces

**Cylinder**
>A surface is a <span style='color:#0fb9b1'>cylinder</span> if there is a <span style='color:#f7b731'>plane P such that all the planes parallel to P intersect the surface</span> in the same curve (when viewed in 2-dimension)

Generally if a equation is missing one variable then it is a cylinder, $y^{2} + z^{2} = 1$ if $x = k$ then the plane is parallel to the y and z plane.

**Quadric Surface**
> It is a graph of second-degree equation in the 3 variables x,y and z

$Ax^2 + By^2 + Cz^2 + Dxy + Eyz + Fxz + Gx + Hy + Iz + J = 0$ where A to J are constants

For this course there are 3 quadric surfaces 

1) **Elliptic Paraboloid** $$\frac{z}{c}= \frac{x^{2}}{a^{2}} + \frac{y^{2}}{b^{2}}$$
Where $c \gt 0$, $z$ cannot be negative and it is symmetric along the z-axis

3) **Ellipsoid** $$\frac{x^{2}}{a^{2}} + \frac{y^{2}}{b^{2}} + \frac{z^{2}}{c^{2}} = 1$$
4) **Double Cone** $$\frac{z^{2}}{c}= \frac{x^{2}}{a^{2}} + \frac{y^{2}}{b^{2}} $$
# Functions with Three Variables
---
A function f of three variables is a rule that assigns to each <span style='color:#f7b731'>ordered triple</span> of real numbers (x; y; z) in a set $D \subseteq \Bbb R^{3} = \Bbb R \times \Bbb R \times \Bbb R$ a <span style='color:#f7b731'>unique real number</span> denoted by f (x; y; z)

**Level Surface**
> A <span style='color:#0fb9b1'>level surface</span> of $f (x; y; z)$ is the three-dimensional graph of the equation $f (x; y; z) = k$ for some constant k.


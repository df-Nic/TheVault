---
title: Double Integral
Date Created: 2023-10-27
tags:
  - MA1521
  - Math
---
# Double Integral
---

Unlike a single variable function, a double variable function<span style='color:#f7b731'> calculates the volume</span> under the plane.

All the rules of integration applies here as well for functions of 2 variables

The double integral of f over the rectangle R is defined as $$\int\int_{R} f(x,y) dA = \lim_{m,n \rightarrow \infty} \sum^{m}_{i = 1}\sum^{n}_{j = 1} (x^{*}_{ij},y^{*}_{ij})\Delta A$$
Where; 
- $\Delta A$ is the area of the rectangle ($\Delta x \Delta y$)

provided the limit exists and is the same for any choice of the sample points $(x^{*}_{ij} ; y^{*}_{ij})$ in $R_{ij}$, for $1 \le i \le m, 1 \le j \le n$.

If $f(x,y) \ge 0$, the volume V of the solid that lies above the rectangle R and below the surface $z = f(x, y)$ is $$V = \int \int_{R} f(x,y) dA$$
Note that the $R$ means it is a <span style='color:#0fb9b1'>rectangle area</span> which is important to know
## Volume of the Solid

Suppose $f(x, y)$ is <span style='color:#0fb9b1'>integrable</span> over the rectangle $R = [a, b] \times [c, d]$ where $[a,b]$ is your bounded x and $[c,d]$ is your bounded y, then

$$\int^{b}_{a} \int_{c}^{d} f(x,y) dy \ dx \text{ Integrate with respect to y then x}$$

$$\int^{d}_{c} \int_{a}^{b} f(x,y) dx \ dy \text{ Integrate with respect to x then u}$$

For both the formulas, the inner integral is called the <span style='color:#0fb9b1'>iterated integral</span>

### Fubini's Theorem

Suppose $f$ is <span style='color:#0fb9b1'>continuous</span> over the rectangle $R = [a, b] \times [c, d]$ then, $$V = \int \int_{R} f(x,y) dA = \int^{b}_{a} \int_{c}^{d} f(x,y) dy \ dx = \int^{d}_{c} \int_{a}^{b} f(x,y) dx \ dy$$
More generally, this is true if we assume that $f$ is <span style='color:#f7b731'>bounded</span> on $R$, $f$ is <span style='color:#f7b731'>discontinuous only on a finite number of smooth curves, and the iterated integrals exist</span>

This shows that the <span style='color:#f7b731'>order</span> of integration weather if its x or y first <span style='color:#f7b731'>does not matter</span> if it is <mark class="hltr-red">integrating on some rectangle area</mark> then this can be applied. More generalized double integration might not work. 

#### Special Cases

Sometimes $f(x,y)$ can be expressed in terms of 2 functions $g(x)$ and $h(y)$; $f(x,y) = g(x)h(h)$

Therefore the Fubini's Theorem $$V = \int \int_{R} f(x,y) dA = \int^{b}_{a} \int_{c}^{d} g(x)h(y) dx \ dy = \int^{d}_{c} h(y) dy \int_{a}^{b} g(x) dx$$
The idea is to treat either $g(x)$ or $h(y)$ as some constant and bring it out of the inner most integral.

# Double Integral over General Region
---

To solve this type of questions;
1)  Draw and identify the region bounded by the 2 curves on the xy-plane (in terms of y or x)
2)  Determine if it is type 1 or 2. To do this see weather the lower bound changes with x or y
3)  Identify the function which is the upper bound and the lower bound
4)  Find $f(x,y)$ or express z in terms of x and y
5)  Apply the formula
## Type 1 Region

A plane region $D$ is said to be of Type I if it <span style='color:#f7b731'>lies between the graphs of two continuous functions of x,</span> that is, $$D = \{ (x,y) : a \le x \le b, g_{1}(x) \le y \le g_{2}(x)\}$$
Where:
1) $g_{1}$ and $g_{2}$ are some functions
2) $g_{1}(x)$ and $g_{2}(x)$ are continuous on $[a,b]$

Then to calculate the double integral over a type 1 Domain $$\int\int_{D} f(x,y)dA = \int_{a}^{b}\int_{g_{1}(x)}^{g_{2}(x)}f(x,y)dy \ dx $$
Take note that the $D$ means that it refers to the <span style='color:#0fb9b1'>general region</span> and <span style='color:#eb3b5a'>not the rectangle region</span>
## Type 2 Region

A plane region $D$ is said to be of Type II if it <span style='color:#f7b731'>lies between the graphs of two continuous functions of y,</span> that is, $$D = \{ (x,y) : c \le y \le d, h_{1}(y) \le x \le h_{2}(y)\}$$
Where:
1) $h_{1}$ and $h_{2}$ are some functions
2) $h_{1}(y)$ and $h_{2}(y)$ are continuous on $[c,d]$

Then to calculate the double integral over a type 2 Domain $$\int\int_{D} f(x,y)dA = \int_{c}^{d}\int_{h_{1}(y)}^{h_{2}(y)}f(x,y)dx \ dy $$
This can be used to <span style='color:#f7b731'>find the volume of the solid</span>

## Additivity with Respect to Domain

Sometimes, there is a need to <span style='color:#f7b731'>calculate the double integral over the entire domain</span>, but sometimes it can be difficult or impossible and thus the <span style='color:#f7b731'>domain can be broken up into subdomains</span> which can all be added up

$$\int\int_{D}f(x,y)dA = \int\int_{D}f(x,y)dA + \dots + \int\int_{D} f(x,y)dA$$

Another property is that if $f(x,y) \ge g(x,y)$ for all $(x,y) \in D$ then $$\int\int_{D}f(x,y)dA \ge \int\int_{D}g(x,y)dA$$
### Double Integrals in Polar Coordinates

Sometimes the region is not easily described in terms of x and y and it is <span style='color:#f7b731'>easier using polar coordinates</span> in terms of $(r,\theta)$. This is <span style='color:#f7b731'>mainly used for circles</span>

**General formula for a circle** : $x^{2} + y^{2} = a^{2}$ where a is the radius of the circle

r : Is the distance from the origin to the point
$\theta$ : is the angle from the positive x-axis to the straight line joining the origin and the point

And similar to the x and y coordinates, before integrating the range for $r$ and $\theta$ must be defined

**Relationship between the cartesian coordinate with the polar coordinate**
$r^{2} = x^{2} + y^{2}$ where $x = r\cos(\theta)$ and $y = r \sin(\theta)$ 

A <span style='color:#0fb9b1'>polar rectangle</span> is a region where $R = \{(r,\theta) : a \le r \le b, \alpha \le \theta \le \beta \}$

However how do express $dA$, $dA = r \times d\theta \times dr$

Therefore to find the double integral using polar coordinates $$\int_{\alpha}^{\beta}\int_{a}^{b} f(r\cos(\theta), r\sin(\theta)) r \ dr \ d\theta$$
Where:
- $0 \le \beta - \alpha \le 2\pi$
- r is some value
# Applications
---
## Finding the Area

Let $f(x,y) = 1$ over a given region $D$. Then the area of D is given as $$A(D) = \int\int_{D} 1 dA$$
## Surface Area

$$\int\int_{D} dS = \int\int_{D} \sqrt{f^{2}_{x} + f_{y}^{2} + 1} dA$$

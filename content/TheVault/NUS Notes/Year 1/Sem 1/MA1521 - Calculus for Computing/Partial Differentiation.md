---
title: Partial Differentiation
Date Created: 2023-10-20
tags:
  - MA1521
  - Math
---
# Partial Differentiation
---
If f is a function of two variables, its partial derivatives are the functions $f(x)$ and $f(y)$ defined by: 
$$f_{x}(x,y) = \frac{\partial f}{\partial x} = \lim_{h \rightarrow 0} \frac{f(x + h,y) - f(x,y)}{h}$$
$$f_{y}(x,y) = \frac{\partial f}{\partial y} = \lim_{h \rightarrow 0} \frac{f(x,y + h) - f(x,y)}{h}$$
The above can be written as $\frac{\partial f}{\partial x}$

Then when differentiating, if it is for $f_x(x,y)$ then treat $y$ <span style='color:#f7b731'>as a constant</span> then differentiate it
Then when differentiating, if it is for $f_y(x,y)$ then treat $x$ <span style='color:#f7b731'>as a constant</span> then differentiate it

Let w be some function that takes in 3 variables, $w = f(x, y, z)$, to differentiate it it can be defined as $\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z}$

Informally, we say that <span style='color:#f7b731'>f is differentiable</span> at (a; b) if the tangent plane at (a; b) is a good approximation to f at points close to (a; b).

## Higher Order Partial Derivatives

Given a function with 2 variables, their partial derivates is $f_{x}$ and $f_{y}$ 

Consider their partial derivates (<span style='color:#0fb9b1'>second partial derivatives</span>) which will be
- $(f_x)_{x}$ and $(f_{x})_{y}$
- $(f_y)_{x}$ and $(f_{y})_{y}$

These in general can be denoted as $\frac{\partial^{2}f}{\partial x^{2}}$ or  $\frac{\partial^{2}f}{\partial x \partial y}$ if its differentiating x then y

**Clairaut's Theorem**
> Suppose f is defined on a disk D that contains $(a, b)$. If the functions $f_{xy}$ and $f_{yx}$ are both continuous on D, then $f_{xy}(a,b) = f_{yx}(a,b)$

This can continue to higher levels of partial derivatives

## Tangent Planes

Previously, in a single variable function, when differentiating a curve, it will get a tangent line at a specific point, but now the partial derivatives will obtain a <span style='color:#0fb9b1'>tangent plane</span> at a given point

The <span style='color:#0fb9b1'>tangent plane</span> to the <span style='color:#f7b731'>surface S at the point P </span>is defined to be the plane that contains both tangent lines T1 and T2 which is the $f_x$ and $f_y$

To get this equation of the plane first is to get the <span style='color:#f7b731'>2 parallel vectors on the tangent plane</span> given by
- $<1,0,f_{x}(a,b)>$
- $<0,1,f_{y}(a,b)>$

Afterwards do a <span style='color:#f7b731'>cross multiplication on these 2 vectors</span> to get another vector which will be the equation of the tangent plane: $$<1,0,f_{x}(a,b)> \times $<0,1,f_{y}(a,b)>$ = <f_{x}(a,b), f_{y}(a,b),-1>$$
OR
$$z = f(a,b) + f_{x}(a,b)(x-a) + f_{y}(a,b)(y-b)$$
## Chain Rule

Supposed a 2 variable function $z = f(x,y)$ and both $x$ and $y$ are some functions $z = f(g(t),h(t))$

Therefore to differentiate z, it will be $$\frac{dz}{dt} = \frac{\partial f}{\partial x} \frac{dx}{dt} + \frac{\partial f}{\partial y} \frac{dy}{dt}$$
Another way is to <span style='color:#f7b731'>substitute the functions</span> $g(t)$ and $h(t)$ as x and y, afterwards<span style='color:#f7b731'> z will be in terms of t</span> and thus just differentiate by t.

But afterwards <mark class="hltr-orange">substitute the respective functions for x and y</mark> to ensure the function is in terms of t
### Functions of 2 variables

What if x and y are not functions of 1 variables but 2 variables; $z = f(g(s,t), h(s,t))$, the same rules apply by using both the chain rule and the differentiation of multi variable functions

If it is <span style='color:#f7b731'>differentiating with respect to t then let s be some fixed variable</span> $$\frac{\partial z}{\partial t} = \frac{\partial f}{\partial x} \frac{\partial x}{\partial t} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial t}$$
If it is <span style='color:#f7b731'>differentiating with respect to s then let t be some fixed variable</span> $$\frac{\partial z}{\partial s} = \frac{\partial f}{\partial x} \frac{\partial x}{\partial s} + \frac{\partial f}{\partial y} \frac{\partial y}{\partial s}$$

But afterwards <mark class="hltr-orange">substitute the respective functions for x and y</mark> to ensure the function is in terms of t

In general if there is <span style='color:#f7b731'>n variables</span> in the initial function there should be<span style='color:#f7b731'> n values being summed up</span>, then $$\frac{\partial z}{\partial u} = \frac{\partial f}{\partial a} \frac{\partial a}{\partial s} + \dots + \frac{\partial f}{\partial n} \frac{\partial n}{\partial s}$$
## Implicit Differentiation

If it is difficult to separate z in terms of x and y which are both <span style='color:#f7b731'>independent variables</span>; $$\frac{\partial z}{\partial x} = -\frac{\frac{\partial F}{\partial x}}{\frac{\partial F}{\partial z}} = -\frac{F_x}{F_z}$$
If it is for partial y, then change $F_{x}$ into $F_{y}$ and all this is provided that $F_{z} \neq 0$ 

Also <span style='color:#eb3b5a'>F is a function that contains x, y and z as its variables and it is not a function of z in terms of x and y</span>

Remember that: $$\frac{\partial x}{\partial x} = 1 \text{ and } \frac{\partial y}{\partial z} = 0$$
## Increments and Differentials

$\Delta$ this symbol is called delta and it means a change in something

Let $\Delta x$ and $\Delta y$ be some increments in the independent variable of x and y, then the <span style='color:#0fb9b1'>increment</span> in z is; $$\Delta z = f(x + \Delta x,y + \Delta y) - f(x,y)$$
Where:
-  $\Delta x = \text{ new x - original x}$
-  $\Delta y = \text{ new y - original y}$

Another way to calculate $\Delta z$;

The differentials, $dx$ and $dy$ of independents variables x and y are such that:
-  $dx = \Delta x$
-  $dy = \Delta y$

Then the <span style='color:#0fb9b1'>differential or total differential</span> of the dependent variable z is; $$dz = f_{x}(x,y)dx+ f_{y}(x,y)dy$$
It it is difficult to calculate $\Delta z$ then there is a good <span style='color:#f7b731'>approximation</span> to it, Suppose f is differentiable at $(a, b)$. Let $\Delta x$ and $\Delta y$ <span style='color:#f7b731'>be small increments in x and y respectively</span> from $(a, b)$, then; $$\Delta z \approx dz = f_x (a, b) dx + f_y (a, b) dy = f_{x} (a, b) \Delta x + f_{y} (a, b) \Delta y$$
## Directional Derivatives

## 2-Dimention

The purpose of this is to find the rate of change at a given point going in a <span style='color:#f7b731'>specific direction</span> 

The <span style='color:#0fb9b1'>directional derivative</span> of $f(x,y)$ at $(x_{0},y_{0})$ in the direction of the unit vector $\mathbf u = <a,b>$ is; $$D_{\mathbf u} f(x_{0},y_{0}) = \lim_{h \rightarrow 0} \frac{f(x_{0} + ha, y_{0} + hb)- f(x_{0},y_{0})}{h} $$
So unlike the others, there is <span style='color:#f7b731'>a unit vector which will denote the direction</span>

A simpler form to calculate is through; $$D_{\mathbf u} f(x_{0},y_{0}) = f_{x}(x,y)a + f_{y}(x,y)b$$
Which it can be rewritten as a [[Vectors & Geometry of Space#Dot Product / Scalar Product|dot product]]  $$D_{\mathbf u} f(x_{0},y_{0}) = <f_{x}, f_{y}> \cdot \mathbf u \text{ or } \nabla f(x,y) \cdot \mathbf u$$ Where:
- $\mathbf u$ us some unit vector $<a,b>$
## Gradient

Consider the vector $<f_{x}, f_{y}>$

The <span style='color:#0fb9b1'>gradient vector</span> of $f(x,y)$ is the vector valued function $$\nabla f(x,y) = <f_{x},f_{y}> = \frac{\partial f}{\partial y} \mathbf i + \frac{\partial f}{\partial y} \mathbf j$$Where: 
-  $\nabla f$ is called del f

Supposed that $\nabla f(x_{0}, y_{0}) \neq 0$ then $\nabla f(x_{0},y_{0})$ will be <span style='color:#f7b731'>perpendicular</span> to the level curve at $f(x_{0},y_{0}) = k$
## 3-Dimention

It is an extension to the 2D way of calculating;

$$D_{\mathbf u} f(x_{0},y_{0},z_{0}) = <f_{x}, f_{y}, f_{z}> \cdot \mathbf u \text{ or } \nabla f(x,y,z) \cdot \mathbf u$$
$$\nabla f(x,yz) = <f_{x},f_{y},f_{z}> = \frac{\partial f}{\partial y} \mathbf i + \frac{\partial f}{\partial y} \mathbf j + \frac{\partial f}{\partial z} \mathbf k$$
This given this theorem, 
-  Suppose $F(x,y,z)$ is differentiable at $P(x_{0}, y_{0},z_{0})$
-  S is some surface level $F(x,y,z) = k$ which contains $(x_{0}, y_{0},z_{0})$
-  Let C be some curve that les on S and the point P
-  Let $\mathbf r(t)$ be a parametric equation of C such that $\mathbf r(t_{0}) = <x_{0}, y_{0}, z_{0}>$

Suppose $\nabla F(x_{0,}y_{0},z_{0}) \ne 0$ then $\nabla F(x_{0,}y_{0},z_{0}) \cdot \mathbf r'(t_{0}) = 0$

Therefore, the equation to the <span style='color:#0fb9b1'>tangent plane to the level surface</span> will be denoted as $$\nabla F(x_{0},y_{0},z_{0}) \cdot <x - x_{0}, y - y_{0}, z - z_{0}> = 0$$
## Maximum and Minimum Rate of Change

$$D_{u}f(P) = \nabla f(P) \cdot \mathbf u = \Vert \nabla f(P) \Vert \cos{\theta}$$
Where:
- $\nabla f(P) \ne 0$
-  $\mathbf u$ is a unit vector which makes an angle with $\nabla f$

The formula above can be used to find the maximum or minimum rate of change;
- The <mark class="hltr-orange">maximum value</mark> occurs when $\theta = 0$ (When $\mathbf u$ points in the direction of $\nabla f$)
- The <mark class="hltr-orange">minimum value</mark> occurs when $\theta = \pi$ (When $\mathbf u$ points in the direction of $-\nabla f$)

## Local and Absolute Maximum

**Local Maximum / Minimum**
> $f$ has a <span style='color:#0fb9b1'>local maximum / minimum</span> at $(a,b)$ if $f(x,y) \le f(a,b) / f(x,y) \ge f(a,b)$ for all points<span style='color:#f7b731'> in some disk with the center</span> $(a,b)$ 

**Absolute Maximum / Minimum**
> $f$ has a <span style='color:#0fb9b1'>absolute maximum / minimum</span> at $(a,b)$ if $f(x,y) \le f(a,b) / f(x,y) \ge f(a,b)$ for all points in the domain $D \rightarrow \Bbb R$

**Critical Points**

A point $P$ at $(a,b)$ is called a critical point of $f$ if'
-  $f_{x}(a,b) = 0$ and $f_{y}(a,b) = 0$
-  OR one of the partial derivatives does not exist

However being <span style='color:#eb3b5a'>a critical point does not mean that point is a maximum or minimum point</span>. It just means that there is a tangent plane along the z axis which is horizontal

To check that it is actually a minimum or maximum point. Let either x or y to be fixed at the point then sub in values of the other variable to check if its really the smallest or largest number

**Saddle Point**
> It is a <span style='color:#0fb9b1'>critical point</span> of $f$ such that every other point centered at critical point $(a,b)$ in the <span style='color:#f7b731'>domain is smaller and larger</span>

### Second Derivative Test

Suppose $f (x, y)$ has <span style='color:#f7b731'>continuous second-order partial derivatives</span> on some open disk centered at $(a, b)$.

Then the <span style='color:#0fb9b1'>discriminant</span> D for the point is given by; $$D = D(a,b) = f_{xx}(a,b)f_{yy}(a,b) - [f_{xy}(a,b)]^2$$
**Scenarios**
1)  If $D \gt 0$ and $f_{xx}(a,b) \gt 0$ then $f(a,b)$ is a <span style='color:#f7b731'>local minimum</span>
2)  If $D \gt 0$ and $f_{xx}(a,b) \lt 0$ then $f(a,b)$ is a <span style='color:#f7b731'>local maximum</span>
3)  If $D \lt 0$ and then $f(a,b)$ is a <span style='color:#f7b731'>saddle point</span> of f
4)  If $D = 0$ <span style='color:#f7b731'>no conclusion</span> can be drawn
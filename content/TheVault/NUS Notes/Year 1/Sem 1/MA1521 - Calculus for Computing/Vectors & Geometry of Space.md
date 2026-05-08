---
title: Vectors & Geometry of Space
Date Created: 2023-10-14
tags:
  - MA1521
  - Math
---

# Vectors
---
A vector is represented by an arrow;
-  The length of the arrow represents the <span style='color:#f7b731'>magnitude</span> of the vector
-  The arrow points in the <span style='color:#f7b731'>direction</span> of the vector

Example: $$\overrightarrow{AB}$$
-  $A$ if the initial point (Tail)
-  $B$ is the terminal point (Tip)
-  And the given example if called a <span style='color:#0fb9b1'>displacement vector</span> also called a <span style='color:#0fb9b1'>line segment</span>
- **0** where the 0 is <span style='color:#f7b731'>bold</span> is not 0 but is called a <span style='color:#f7b731'>zero vector</span>

Let $u$  be some vector $\mathbf {u} = <u_{1},u_2,u_3>$
-  Everything in the <> is called <span style='color:#f7b731'>components</span>
-  While the vector with <> is called a <span style='color:#f7b731'>position vector</span>
-  The position vectors who <mark class="hltr-orange">initial point is the origin</mark> which is denoted as $\mathbf O$

Therefore, $$\overrightarrow{AB} = \overrightarrow{OB} - \overrightarrow{OA} = \mathbf a = <x_2-x_1,y_2-y_1,z_2-z_1> $$
## 3D Coordinate System

Is is a coordinate system with <span style='color:#f7b731'>3 axis</span> the X, Y and Z axis.

In a 3D coordinate system, there will be 3 planes, $XZ$, $YZ$ and $XYZ$ plane and they are perpendicular to one another.

## Distance between 2 Points

It is the same as with only the X and Y coordinates but add the Z coordinate.

$$\text{Distance: } \sqrt{(x_{2}- x_{1})^2 + (y_{2}- y_{1})^2 + (z_{2}-z_{1})^2}$$

## Equation of a Sphere

Let:
1)  $r$ be the radius
2)  $C(h,k,l)$ be the center of the circle
3)  $P(x,y,z)$ be some point on the circumference of the sphere

$$\text{Equation of the Sphere: } (x - h)^{2} + (y - k)^{2} + (z - l)^{2} = r^2$$
## Summation of Vectors

Let u and v be some vector and <span style='color:#f7b731'>using the triangle law</span>

Their sum u + v is the vector from the initial point of u to the terminal point of v when we position the vectors so that the initial point of v coincide with the terminal point of u.

$\mathbf {a} = <a_{1},a_2,a_3>$
$\mathbf {b} = <b_{1},b_2,b_3>$
$a + b = <a_1 + b_1,a_2+a_2,a_3+b_3>$
## Subtraction of Vectors

For subtraction we will use the summation formula
$$u - v = u + (-v)$$
## Scalar Multiplication

Multiplying a vector with some number $c$ will result in its length be $|c|$ <span style='color:#f7b731'>times the length of the vector</span>
-  The direction will be the same if $c \gt 0$
-  The direction will be the apposite if $c \lt 0$
-  If $c = 0$ or $u = \mathbf 0$ then $c\mathbf u = \mathbf 0$

Therefore:
$c\mathbf a = <ca_1,ca_2,ca_3>$

## Properties of Vectors

1)  $\mathbf {a} + \mathbf {b} = \mathbf {b} + \mathbf {a}$
2)  $\mathbf {a} + (\mathbf {b} + \mathbf {c}) = (\mathbf {a} + \mathbf {b}) + \mathbf {c}$
3)  $\mathbf {a} + \mathbf {0} = \mathbf {a}$
4)  $a + (\mathbf {-a}) = \mathbf {0}$
5)  $c(\mathbf {a} + \mathbf {b}) = c\mathbf {a} + c\mathbf {b}$
6)  $(c + d)\mathbf {a} = c\mathbf {a} + d\mathbf {a}$
7)  $(cd)\mathbf {a} = c(d\mathbf {a})$
8)  $1(\mathbf {a}) = \mathbf {a}$
9)  $\mathbf a \text{ is parallel to b if } \mathbf a = c(\mathbf b)$

## Standard Basis Vectors

$\mathbf {i} = <1,0,0>$
$\mathbf {g} = <0,1,0>$
$\mathbf {k} = <0,0,1>$

These vectors is just have a length of 1 in the x, y and z axes. These 3 basis vectors are important can be used in computations. For example the<span style='color:#f7b731'> length of one vector</span>.

Length is denoted as : $\lVert u \rVert$

$$\lVert u \rVert = \sqrt{u_{1}^{2} + u_{2}^{2} + u_{3}^{2}}$$

If the above length is 1 then it is called a <span style='color:#f7b731'>unit vector</span>. which can be derived from $$\lVert u \rVert = \lVert \frac{a}{\lVert a \rVert}\rVert = \frac{1}{\lVert a \rVert}* \lVert a \rVert = 1$$
## Dot Product / Scalar Product

This will give us <span style='color:#eb3b5a'>some value not a vector</span>

$$a \cdot b = a_{1}b_{1} + a_{2}b_{2} + a_{3}b_{3}$$

Take not that $a \cdot b = 0$ does not imply that $\mathbf a = \mathbf 0$ or $\mathbf b = \mathbf 0$ and <span style='color:#f7b731'>it also means that the 2 vectors are orthogonal </span>(perpendicular)

### Angles Between Vectors

The angle $\theta$ <span style='color:#f7b731'>in radians</span> between them to be the <span style='color:#f7b731'>smaller angle between vectors a and b</span>, formed by placing their initial points at the origin.

-  $\mathbf a$ and $\mathbf b$ have the<mark class="hltr-orange"> same direction </mark>if and only if $\theta = 0$
-  $\mathbf a$ and $\mathbf b$ have the<mark class="hltr-orange"> opposite direction</mark> if and only if $\theta = \pi$
-  $\mathbf a$ and $\mathbf b$ are <mark class="hltr-orange">orthogonal</mark> (perpendicular) if and only if $\theta = \frac{\pi}{2}$

Therefore another way to do the dot product is through: $$a\cdot b = \lVert a \rVert \lVert b \rVert \cos{\theta}$$
## Vector Projection

It is also called the scalar projection of <span style='color:#f7b731'>b onto a</span> (component of b along a) is defined to be the signed magnitude of the vector projection

1) $proj_{\mathbf a} \mathbf b$ (Vector Projection) which is a vector
2) $comp_{\mathbf a} \mathbf b$ (Scalar Projection) which is a number

$$comp_{\mathbf a} \mathbf b = \lVert b \rVert \cos{\theta}  = \frac{a \cdot b}{\lVert a \rVert}$$

$$proj_{\mathbf a} \mathbf b = comp_{\mathbf a} \mathbf b \ \times \frac{a}{\lVert a \rVert}  = a  \ \times \frac{a \cdot b}{a \cdot a}$$

## Distance from a Point to a Plane

The (shortest) distance from a point $P(x_0; y_0; z_0)$ to the plane $ax + by + cz = d$ is given by $$\frac{\lvert ax_{0} + by_{0} + cz_{0} - d \rvert}{\sqrt{a^{2}+ b^{2}+c^{2}}}$$
## Cross Multiplication

Given 2 vectors $\mathbf a$ and $\mathbf b$, the cross multiplication is

$$
a \times b =
\begin{vmatrix}
\mathbf i & \mathbf j & \mathbf k \\
a_{1} & a_{2} & a_{3} \\
b_{1} & b_{2} & b_{3} \\
\end{vmatrix}
= (a_{2}b_{3} - a_{3}b_{2})\mathbf i - (a_{1}b_{3} - a_{3}b_{1})\mathbf j + (a_{1}b_{2} - a_{2}b_{1})\mathbf k
$$

The direction of the resulting vector is <span style='color:#f7b731'>orthogonal</span> to both vectors $\mathbf a$ and $\mathbf b$

It can be used to find the <span style='color:#f7b731'>area of a parallelogram</span> and the <span style='color:#f7b731'>distance from a point to a line</span>.

### Finding the Angle based on the Cross Product

$$\lVert a \times b \rVert = \lVert a \rVert \lVert b \rVert \sin{\theta}$$

This can also help to find the <span style='color:#f7b731'>area of the parallelogram </span>

### Distance from A Point to a Line
$$\overrightarrow{PQ} \sin{\theta} = \frac{\lVert \overrightarrow{PQ} \times \overrightarrow{PR} \rVert}{ \lVert \overrightarrow{PR} \rVert }$$

## Vector Equation of a Line
$$\mathbf r = \mathbf r_{0} + tv$$
where v is another point <span style='color:#f7b731'>parallel</span> to some line (L), and the above the vector equation of L

This can be rewritten as $$<x,y,z> = <x_{0}, y_{0}, z_{0}> + t<a,b,c>$$ 
$x = x_{0} + at$
$y = y_{0} + bt$
$x = z_{0} + ct$

This is known as a <span style='color:#f7b731'>parametric equation of a line</span>. And $a, b, c$ are all called <span style='color:#0fb9b1'>direction number</span> of the line L

## Line Intersection

Given 2 lines $L_{1}$ and $L_{2}$, these 2 lines can either be parallel or intersecting or non intersecting. There is also some angle between the lines $\pi - \theta$ 

Any <span style='color:#f7b731'>non parallel </span>and <span style='color:#f7b731'>non intersecting</span> lines are called <span style='color:#0fb9b1'>skew lines</span>.

## Vector Equation of a Plane
$$\mathbf n \cdot (\mathbf r - \mathbf r_{0}) = 0 \text{ or } \mathbf n \cdot \mathbf r = \mathbf n \cdot \mathbf r_{0}$$

The above can be re written as $$<a,b,c> \cdot <x,y,z> = <a,b,c> \cdot <x_{0}, y_{0}, z_{0}>$$
Where : 
- $<a,b,c>$ is a vector <span style='color:#f7b731'>normal</span> to the plane
- $<x_{0}, y_{0}, z_{0}>$ is some point on the plane

$$\text{Which will be: }ax + by + cz = a(x - x_{0}) + b(y - y_{0}) + c(z - z_{0})$$

Where; 
-  ($r-r_{0}$) are 2 position vectors on the plane represented by $\overrightarrow {P_{n}P}$ 
-  $\mathbf n$ is some normal vector that is <span style='color:#f7b731'>perpendicular</span> to the plane.

## Parallel Planes

If the 2 planes are parallel, it means that their <span style='color:#f7b731'>normal vectors are parallel</span>. <span style='color:#eb3b5a'>If not</span> then;
1)  It intersects in a straight line
2)  The angle between the 2 planes is defined as the acute angle ($\lt 90\unicode{xB0}$) between their normal vectors. If it is not then minus $\pi$ from the angle

### To calculate the distance between 2 planes

First the 2 planes <mark class="hltr-orange">must be parallel </mark>

1)  If they are parallel, find a point on one of the planes by making sure that x y and z fulfills the equation
2)  Afterwards use the formula to calculate the <mark class="hltr-orange">distance between a point and a plane</mark>[[Vectors & Geometry of Space#Distance from a Point to a Plane| click here for reference]]

If the 2 points one on each plane, and its length is = 1 then it is perpendicular to the 2 planes.
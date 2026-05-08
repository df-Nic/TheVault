---
title: Sequences & Interests
Date Created: 2024-01-19
Last Updated: 2025-09-27
tags:
  - QF1100
  - Finance
  - Math
---
# Geometric Sequence
---
In short the <span style='color:#0fb9b1'>geometric sequence</span> is as follows $ar^{0}, ar^{1}, ar^{2}, ar^{3}, \dots$, <mark style='background:#f7b731'>each number must be nonzero</mark>.

**Where :**
- $r$ is called the <span style='color:#0fb9b1'>common ratio</span> and <b><mark style='background:#eb3b5a'>r cannot be zero</mark></b>
- $a$ is a <span style='color:#0fb9b1'>scale factor</span>
## Sum of a Geometric Sequence

If $n$ is finite, the <span style='color:#fa8231'>sum of the first n-terms</span> in a geometric sequence uses the following equation : $$\sum^{n}_{k = 1} ar^{k - 1} = \sum^{n - 1}_{k = 0}ar^{k} = \frac{a(1 - r^{n})}{1 - r}$$
However for the equation to work, <b><mark style='background:#eb3b5a'>r cannot be one</mark></b>.

A <span style='color:#fa8231'>more general formula</span> will be : $$\sum^{n}_{k = m} ar^{k} = a \times \frac{r^{m} - r^{n+1}}{1 - r}$$
**Where :**
- $n \ge m$
# Derivatives
---
A function is defined as $f(x)$ while its <span style='color:#0fb9b1'>derivative</span> is $f'(x)$, given by the formula : $$f'(x) = \lim_{h \rightarrow  0} \frac{f(x + h) - f(x)}{h}$$
The [[Derivatives|standard rules of derivatives]] are :
- Chain rule
- Product rule
- Quotient rule

## Increasing & Decreasing Functions

For a function $f$ to be <mark style='background:#f7b731'>increasing</mark>. Its domain $(a, b)$ $\forall x_{1}, x_{2} \in (a, b), \text{ if } x_{1} \lt x_{2} \rightarrow f(x_{1}) \lt f(x_{2})$.

For a function $f$ to be <mark style='background:#f7b731'>decreasing</mark>. Its domain $(a, b)$ $\forall x_{1}, x_{2} \in (a, b), \text{ if } x_{1} \lt x_{2} \rightarrow f(x_{1}) \gt f(x_{2})$.

To <span style='color:#fa8231'>test weather a function is increasing or decreasing</span>, the derivative can be used since $f'(x)$ is the <span style='color:#f7b731'>tangent line at a given point</span>.

For a function to be <mark style='background:#f7b731'>strictly decreasing</mark>, $f'(x) \lt 0, \forall x \in (a, b)$ and the <span style='color:#f7b731'>opposite for strictly increasing</span>.

However for this <span style='color:#0fb9b1'>derivative test </span>to work, the function <mark style='background:#f7b731'>must be continuous</mark> on $[a, b]$ and <mark style='background:#f7b731'>differentiable</mark> on $(a, b)$.

<span style='color:#0fb9b1'>Local minimum and maximum</span>, is a particular min or max point in a particular range in a graph.

<span style='color:#0fb9b1'>Global minimum and maximum</span>, is the same but for the <mark style='background:#f7b731'>whole graph</mark>.

To find these points, $f'(x) = 0$, but this <span style='color:#eb3b5a'>point might be a point of inflation</span>.
# Interests
---
An <span style='color:#0fb9b1'>accumulation function</span> denoted by $a(t)$ is the amount accumulated through interest : $$a(t) = \text{Principle } + \text{ Interest}$$
**Where :**
- $t$ is time
- Interest is based on the rate and time

When $t = 0$, $a(0)$ is just the <span style='color:#0fb9b1'>principle</span>.

The <span style='color:#fa8231'>seven-ten rule</span>,  states that, <span style='color:#f7b731'>money invested at 7% a year doubles in approximately 10 years</span>. <span style='color:#f7b731'>Similarly, the converse</span>, money invested at 10% will doubles in approximately in 7 years.

For<span style='color:#0fb9b1'> simple interest</span> it <span style='color:#f7b731'>grows linearly</span> while <span style='color:#0fb9b1'>compound interest</span> <span style='color:#f7b731'>grows exponentially</span>.
## Simple Interest

<span style='color:#0fb9b1'>Simple interest</span> is calculated <mark style='background:#f7b731'>only on the principle amount</mark>. It is given by the formula : $$\text{Sample interest } = \text{ Principle } + t \times r \times \text{ Principle }$$**Where :**
- $t$ is the number of <span style='color:#f7b731'>years</span>
- $r$ is the <span style='color:#f7b731'>annual rate</span>
## Compound Interest

<span style='color:#0fb9b1'>Compound Interest</span> earns <span style='color:#f7b731'>interest on the interest earned</span>. It is given by the formula : $$\text{Compound Interest } = \text{ Principle } \times (1 + \frac{r}{n})^{t}$$**Where :**
- $t$ is the number of <span style='color:#f7b731'>periods</span>
- $r$ is the <span style='color:#f7b731'>annual rate</span>
- $n$ is the number of times the <span style='color:#f7b731'>interest is compounded</span> in a year

If the interest is compounded quarterly then $t$ must times 4.
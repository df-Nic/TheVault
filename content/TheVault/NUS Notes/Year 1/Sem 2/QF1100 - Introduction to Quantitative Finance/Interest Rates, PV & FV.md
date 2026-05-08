---
title: Interest Rates, PV & FV
Date Created: 2024-02-21
Last Updated: 2025-09-27
tags:
  - QF1100
  - Math
  - Finance
---
# Fixed Interest Rate Securities
---
A <span style='color:#0fb9b1'>fixed-interest rate </span>security, is where the <span style='color:#f7b731'>interest does not change</span> through the duration of the contract. This interest is aggreged upon by both parties at the start of the term.

Now let, $a(0)$ denote the <span style='color:#0fb9b1'>principle</span> :

**Simple Interest**
$$
\text{Total } = a(0)(1 + \sum^{n}_{i=1} t_{i}r_{i})
$$
**Compound Interest**
$$
\text{Total } = a(0)\prod^{n}_{i=1} (1 + r_{i})^{t_{1}}
$$
**Where** :
- $r_{i}$ denotes the interest rate at that particular time period $i$
- $t_{i}$ denotes the number of payments in the whole term

<span style='color:#2d98da'>Bernoulli inequality</span> : If $x \ge 0$ then $(1 + x)^{n} \ge 1 + nx$ for any positive integer $n$. This is just compound greater than simple. 
## Frequency of Compounding

Now recall the[[Sequences & Interests#Compound Interest| compound interest]] formula, now what if the <span style='color:#f7b731'>interest is compounded</span> $\color{#f7b731}{p}$ <span style='color:#f7b731'>times</span>? Well this means that in 1 year, the <span style='color:#f7b731'>interest is paid</span> $\color{#f7b731}{p}$ <span style='color:#f7b731'>times</span>.
$$
p(t) = p(0) \times (1 + \frac{r^{(p)}}{p})^{t \times p}
$$
**Where**
- $p(t)$ is the **total amount** at time $t$
- $r^{(p)}$ is the **interest rate** compounded $p$ times
- $p$ is the <span style='color:#0fb9b1'>frequency of compounding</span> in 1 year
- $t \times p$ is the **number of payments** at the end of $t$

### Continuous Compounding

When interest is <span style='color:#0fb9b1'>compounded continuously</span>, it means the <span style='color:#f7b731'>frequency of compounding tends to be infinity</span>.

It is denoted by $r^{(\infty)}$. and if a financial instrument is <span style='color:#0fb9b1'>compounded continuously</span>, then the return can be calculated as such:
$$
a(t) = a(0) \times \lim_{p \to \infty}(1 + \frac{p^{(\infty)}}{p})^{t \times p} = a(0) \times (e^{r^{\infty}})^{t}
$$

**Where :**
- $e$ is the **Euler number** which approximates to $\approx 2.718$

For $r^{(p)} \equiv r^{(\infty)}$, then the **following must hold**,
$$
(1 + \frac{p^{(p)}}{p})^{p} = e^{r^{(\infty)}} = 1 + r_{e}
$$
If compounded continuously, then the $r$ will be replaced with $e^{r^{(\infty)}}$
## Cash Flow Stream

A <span style='color:#0fb9b1'>cash flow stream</span> is a timeline visualisation of the <span style='color:#f7b731'>changes of deposit/withdrawal</span> over a period $t$. The values in can be either negative or positive.
$$
\text{Cash flow : } (x_{0}, x_{1}, \dots, x_{n - 1}, x_{n})
$$

**Where :**
- $n$ represents the **number of periods**
- $x_{0}$ is the start of the cashflow, meaning $t = 0$
- Each $x_{i}$ represents a cash flow and the <b><mark style='background:#f7b731'>end of the period</mark></b>
## Effective Annual Interest Rate

So far, all the interest rates are called <span style='color:#0fb9b1'>nominal interest rates</span>. This interest rate <span style='color:#f7b731'>does not take compounding into consideration</span>, therefore the power will need to be $t \times p$.

<span style='color:#0fb9b1'>Effective annual interest rates</span> ($r_{e}$), however is <span style='color:#f7b731'>takes compounding into consideration for one year</span>. Think of it as the total amount after $t$ when the interest for each $p$ is automatically added back into the principle.

**To find the effective annual interest rate :**
$$
1 + r_{e} = (1 + \frac{r^{(p)}}{p})^{p}
$$

**Where :**
- $r_{e}$ is the <span style='color:#0fb9b1'>effective annual interest rate</span>
- $r^{(p)}$ is the <span style='color:#0fb9b1'>nominal interest rate</span>

Therefore, the <b><mark style='background:#f7b731'>final amount using both rate will yield the same result</mark></b>.
$$
a(t) = a(0) \times (1 + r_{e})^{t} = a(0) \times (1 + \frac{r^{(p)}}{p})^{p \times t}
$$

From this equation, $\color{#f7b731}{r_{e} \ge r^{(p)}}$ This is for any positive integer $p \ge 1$.
### Equivalent Interest Rates

What if, there is a need to <span style='color:#fa8231'>find an interest rate compounded differently that is equivalent</span>?

Then it can be done as such, let $r^{(p)}$ be the rate compounded $p$ times and $r^{(q)}$ be the rate compounded $q$ times, then :
$$
(1 + \frac{r^{(p)}}{p})^{p} = (1 + \frac{r^{(q)}}{q})^{q}
$$

The above <span style='color:#f7b731'>uses nominal interest rate</span>, if it is to **find effective interest rate, change to** $(1 + r_{e})$.
# Present & Future Value
---
Given 2 financial instruments, a <span style='color:#2d98da'>bond</span> and a <span style='color:#2d98da'>fixed deposit</span>. Here are their cashflows :
$$
\begin{align} \text{Bond : }
(-F,\underbrace{F \times \frac{r^{(p)}}{p}, F \times \frac{r^{(p)}}{p}, \dots, F \times \frac{r^{(p)}}{p} + F}_{t \times p \text{ Number of periods }}) \\
\text{Fixed Deposit : }
(-F, 0, 0,0,0, \dots, F(1 +\frac{r^{(p)}}{p})^{rp})
\end{align}
$$

**Where :**
- The **number of periods** for the bond is called a coupon

Now how to know which one it better? Since the interest is paid differently. This is where present (PV) and future value (FV) will help.

## Present Value

<span style='color:#0fb9b1'>Present value</span> can be described as, <span style='color:#f7b731'>how much money in the future is worth now</span>. Another way of putting it is how much money is needed now such that in $t$ years $x$ will be received .
$$
PV = \frac{A}{(1 + r)^{n}}
$$

**Where :**
- $PV$ is the present value
- $A$ the total amount at the end of $t$ or another word is <b><mark style='background:#0fb9b1'>future value</mark></b>
- $r$ is the **annual interest rate**

$\frac{1}{(1 + r)^{n}}$ is also known as the <span style='color:#0fb9b1'>discount factor</span>.
### Present Value of a Stream

Lets say in $n$ years, there is a need of $x$ amount of dollars. So the question is, with the <span style='color:#fa8231'>help of interest how much is needed at the start</span>.

Given this cash flow stream, $(x_{0}, x_{1}, x_{2}, \dots, x_{n})$. Each $x_{i}$ entry will be it a positive or negative and that at $x_{i}$ a <span style='color:#f7b731'>withdrawal of some amount is possible</span>, then the **PV** for this stream is as such :
$$
PV = \sum^{n}_{k = 0} x_{k}(1 + r)^{-k}
$$

**Where :**
- $n$ is the **total** period
- $k$ is the **current** period
- $x_{k}$ is the **cash at period** $k$
- $r$ is the **interest** rate, the <b><mark style='background:#f7b731'>effective annual interest rate</mark></b>
$$
PV = \sum^{n}_{k = 0} x_{k}(1 + \frac{r^{(p)}}{p})^{-k}
$$
**Where :**
- $n$ is the **total** period ($t \times p$)
- $k$ is the **current** period
- $x_{k}$ is the **cash at period** $k$
- $p$ is the **number of times compounded**
- $r$ is the **interest** rate, the <b><mark style='background:#f7b731'>norminal interest rate</mark></b>

This assumes that at $x_{k}$ is all the same, if it is different the the summation must be calculated separately.

The link between **FV** and **PV** is that the PV of a <span style='color:#f7b731'>cash flow stream</span> is equal to the <span style='color:#f7b731'>present payment amount</span>.
$$
PV = \frac{FV}{(1 + r)^{n}}
$$
## Future Value

<span style='color:#0fb9b1'>Future value</span> can be described as, <span style='color:#f7b731'>how much money now is worth in the future</span>.
$$
FV = {A}{(1 + r)^{n}}
$$

**Where :**
- $PV$ is the present value
- $A$ the total amount at the end of $t$ or another word is <b><mark style='background:#0fb9b1'>present value</mark></b>
- $r$ is the **annual interest rate**
### Future Value of a Stream

Now what if, a <span style='color:#fa8231'>deposit is continuous</span> and not only at the beginning, how to calculate the future value now.

Given this cash flow stream, $(x_{0}, x_{1}, x_{2}, \dots, x_{n})$. Each $x_{i}$ entry will be positive or negative will have a <span style='color:#f7b731'>different time period and possibly a different interest rate</span>. the **FV** of the this stream is as such :
$$
FV = \sum^{n}_{k = 0} x_{k} \times (1 + r)^{n - k}
$$

**Where :**
- $n$ is the **total** period
- $k$ is the **current** period
- $x_{k}$ is the **cash at period** $k$
- $r$ is the **interest** rate, the <b><mark style='background:#f7b731'>effective annual interest rate</mark></b>

$$
FV = \sum^{n}_{k = 0} x_{k} \times (1 + \frac{r^{(p)}}{p})^{n - k}
$$
**Where :**
- $n$ is the **total** period ($t \times p$)
- $k$ is the **current** period
- $x_{k}$ is the **cash at period** $k$
- $p$ is the **number of times compounded**
- $r$ is the **interest** rate, the <b><mark style='background:#f7b731'>norminal interest rate</mark></b>

# Principle of Equivalent
---
Now lets consider 2 different cash flows. How to <span style='color:#fa8231'>conclude that it is equivalent</span> or not.

To determine that $(x_{0}, x_{1}, \dots, x_{n}) \equiv (y_{0}, y_{1}, \dots, y_{n})$, they must have the <b><mark style='background:#f7b731'>same present value </mark></b>.

Thus the **PV** formula and a given cash flow and a given rate is **0**, then it is known as the <span style='color:#0fb9b1'>equation of value</span>. This is because that cash flow $(x_{0}, x_{1}, \dots, x_{n}) \equiv (0, 0, \dots, 0)$.

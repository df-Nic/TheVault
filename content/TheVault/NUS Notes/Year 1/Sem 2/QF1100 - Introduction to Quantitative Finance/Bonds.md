---
title: Bonds
Date Created: 2024-02-21
Last Updated: 2025-09-27
tags:
  - QF1100
  - Math
  - Finance
---
# Internal Rate of Return
---
It is also called <span style='color:#0fb9b1'>yield</span> or <span style='color:#0fb9b1'>IRR</span>, where it calculates the rate of return of an investment <span style='color:#f7b731'>without referencing to the prevailing interest rate</span>.

In short the <span style='color:#20bf6b'>higher the IRR (discount rate) the better the investment</span>.

For this we will set the <span style='color:#0fb9b1'>net present value</span> (NPV) to be 0. This assumes the investment to be a <span style='color:#f7b731'>zero sum game</span>, where $\color {#f7b731} {\text{PV input } - \text{PV Output } = 0}$. Yes it can lose or gain from it but its good to focus on breaking even.

This <span style='color:#0fb9b1'>IRR</span> serves as a bench mark, if another investment has a higher IRR then it will end up earning more.
$$
PV = \sum^{n}_{k = 0} \frac{x_{k}}{(1 + r)^{k}}= 0
$$
**Where**
- $r$ is the <span style='color:#0fb9b1'>IRR</span>
- $x_{k}$ is the cash flow at $k$

In **excel**, the <span style='color:#3867d6'>IRR</span> function can be used.

# Bond
---
There are a few <span style='color:#fa8231'>terms</span> to understand :
- **Face value** -  Which is the price to own the bond
- **Coupon** - The term for a payment, which depends on the terms of the bond
- **Coupon payment** - How much to receive from the coupon
- **Time** - Duration of the bond
- **Nominal Yield** - It is the nominal internal rate of return or IRR of the bond

At the end of the bond, the face value will be returned.

A bond, <span style='color:#fa8231'>provides a steady cashflow</span> and the goal is to <span style='color:#f7b731'>find the present value</span> of the bond at any given time.

$$
P(t) = \frac{F}{(1 + \frac{\lambda(t)\%}{m})^{n-tm}} + \sum\limits_{i = 1}^{n -tm} \frac{F \times c\%/m}{(1 + \frac{\lambda(t)\%}{m})^{t}}  
$$
**Where :**
- $F$ is the **face value**
- $P(t)$ is the **present value** of the bond at time $t$
- $\lambda(t)\%$ is the **nominal yield** of the bond
- $c\%$ is the **coupon rate** or the interest rate of the bond
- $m$ is the **number of coupon payments per year**
- $n$ is the **total number of coupon payments**
- $t$ is the time in **years**

When <span style='color:#fa8231'>calculating for PV for a bond</span>, it is trying to find the <span style='color:#f7b731'>PV for the remaining</span> $\color {#f7b731} {n}$ <span style='color:#f7b731'>coupons</span> which has not been paid.

Simplifying the formula above :
$$
P(t) = F + F \times \left(\frac{c - \lambda(t)}{\lambda(t)}\right)\left[1 - \frac{1}{(1 + \frac{\lambda(t)\%}{m})^{n-tm}}\right]
$$
**Where :**
- $\lambda(t)$ is just the value itself not the %, for example if $\lambda(t)\% = 2$ then $\lambda(t) = 2$

<b><span style='color:#fa8231'>Pricing</span> of a bond is at a:</b>
- **Premium** - $P(t) \gt F$ or $c \gt \lambda(t)$
- **At par** - $P(t) = F$ or $c = \lambda(t)$
- **Discount** - $P(t) \lt F$ or $c \lt \lambda(t)$

A relation between $\lambda$ and $P(t)$ is that a bigger $\lambda$ value, the smaller the $P(t)$ To <span style='color:#f7b731'>maximise the PV, the nominal yield must be 0</span>. 


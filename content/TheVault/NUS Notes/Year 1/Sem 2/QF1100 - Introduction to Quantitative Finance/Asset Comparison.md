---
title: Asset Comparison
Date Created: 2024-03-21
Last Updated: 2025-09-27
tags:
  - QF1100
  - Math
  - Finance
---
# Rate of Return of Assets
---
An <span style='color:#0fb9b1'>asset</span> is anything that can be bought and sold.

To <span style='color:#fa8231'>calculate the rate of return</span> :
$$
\text{Rate of Return }(r) = \frac{P_{1} - P_{0}}{P_{0}} = \frac{P_{1}}{P_{0}} - 1
$$
**Where :**
- $P_{0}$ is the **price of the asset** at $t = 0$, basically when the asset is bought
- $P_{1}$ is the **price of the asset** at $t = 1$, which is a random amount of what it is worth
- $r$ is the rate, which is also a **random variable**

Equivalently, $P_{1} = P_{0} \times (1 + r)$

Now, the is a possibility that the investment will be <span style='color:#20bf6b'>profitable</span> or <span style='color:#eb3b5a'>not profitable</span>. Thus if given a <span style='color:#f7b731'>list of prices with given probability</span>, the probability of loss or gain can be calculated ($P_{1} - P_{0}$)

Using the [[Probability#Expected Value|expected value]] formula $E[P_{1} - P_{0}] = E[r]$, the <span style='color:#fa8231'>mean rate of return can be calculated</span>.

However the <span style='color:#eb3b5a'>following are not true</span> :
- $E[ln x] = ln(E[x])$
- $E[e^{R}] = e^{E[X]}$

And with this the <span style='color:#f7b731'>standard deviation can be calculated</span> as well, who's value signifies the <b><mark style='background:#f7b731'>risk of this asset investment</mark></b>. The <span style='color:#20bf6b'>lower the value the less risk there is</span>,

Using the [[Probability#Covariance|covariance formula]], the <span style='color:#fa8231'>association between 2 assets</span> can be calculated which is denoted as $\sigma_{i,j}$. and with this the <span style='color:#fa8231'>corelation of return</span> is as follows :
$$
p_{i,j} = \frac{\sigma_{i,j}}{\sigma_{i} \times \sigma_{j}}
$$
**Where :**
- $\sigma_{i,j}$ is the <span style='color:#0fb9b1'>corelation coefficient</span> between asset $i$ and asset $j$
- $\sigma_{i}$ is the <span style='color:#0fb9b1'>risk</span> of asset $i$
- $\sigma_{j}$ is the <span style='color:#0fb9b1'>risk</span> of asset $j$
- $\vert p_{i,j} \vert \le 1$

## Portfolio

Given that a person has invested in $n$ number of assets, then the portfolio can be <span style='color:#f7b731'>represented by a vector</span> $V = (v_{1}, v_{2}, \dots, v_{n})$, where each $\color {#f7b731} {v_{i}}$ <span style='color:#f7b731'>represents a percentage of the total investment in all the assets</span>.
$$
\sum_{i = 1}^{n} v_{i} = 1
$$
Usually $n \ge 2$ as if $n = 1$ then it will be just be following the above.

Then the <span style='color:#fa8231'>rate of return for this portfolio</span> is as such :
$$
r_{p} = \sum_{i = 1}^{n} v_{i} \times r_{i}
$$
**Where :**
- $v_{i}$ is the percentage of the asset against the total
- $r_{i}$ is the rate of return for that particular asset

Since there is a vector of assets $V$ then it can be extended to be a <span style='color:#f7b731'>vector of mean rate of returns</span> which is denoted by $\mu = (\mu_{1}, \mu_{2}, \dots, \mu_{n})$, where $\mu_{i} = E[r_{i}]$, this is also known as <span style='color:#0fb9b1'>mean vector</span>.

Therefore the <span style='color:#fa8231'>portfolio mean can be calculated as such</span> :
$$
\mu_{p} = E[r_{p}] = \sum_{i = 1}^{n} v_{i} \times \mu_{i}
$$
Also the <span style='color:#fa8231'>portfolio variance can be calculaed</span> :
$$
\sigma_{p}^{2} = Var\left(\sum_{i = 1}^{n} v_{i}r_{i}\right) = \sum_{i = 1}^{n} v_{i}^{2}\sigma_{i}^{2} + 2 \sum\_{i = 1}^{n}\sum_{j \lt i} v_{i}w_{i}\sigma_{i,j} 
$$
**Where :**
- $\sigma_{i}$ is the **standard deviation** of asset $v_{i}$
- $\sigma_{i,j}$ is the association between 2 assets (**Covariance**)

**Remarks about the portfolio variance formula :**
- $\sigma_{i,j} = \sigma_{j,i} = Cov(r_{i},r_{j})$
- $\sigma_{i,j} = Cov(r_{i}, r_{i}) = \sigma_{i}^{2}$

Therefore to maximise $\mu_{p}$ it is to <span style='color:#20bf6b'>maximise returns</span> and to minimise $\sigma_{p}^{2}$ it is to <span style='color:#20bf6b'>minimise risk</span>.

# Portfolios of 2 Assets
---
Now given the above formulas let a portfolio $W = (w_{i}, w_{2}) = (\alpha, 1 - \alpha)$.

The <span style='color:#fa8231'>mean rate of return</span> for the portfolio is as such :
$$
r_{p} = \alpha{r_{i}} + (1 - \alpha)r_{2}
$$
**Where :**
- $r_{i}$ is the **rate of return** for the asset $w_{i}$

The <span style='color:#fa8231'>portfolio mean</span> can be calculated as such :
$$
\mu_{p} = \alpha{\mu_{1}} + (1 - \alpha)\mu_{2}
$$
**Where :**
- $\mu_{i}$ is the **average rate of return** for the asset $w_{i}$

The <span style='color:#fa8231'>portfolio variance</span> is as follows :
$$
\sigma_{p}^{2} = \mu_{p}^{2} - (\mu_{p})^{2} = {E[(\alpha{r_{i}} + (1 - \alpha)r_{2})^{2}]} -  E[\alpha{r_{i}} + (1 - \alpha)r_{2}]^{2}
$$
**Where :**
- $\mu_{p}$ is the $E[r_{p}]$ which is the **mean rate of return for the portfolio**

**Simplifying this :**
$$
\sigma_{p}^{2} = \alpha^{2}\sigma_{1}^{2} + (1 - \alpha)^{2}\sigma_{2}^{2} + 2\alpha(1 - \alpha)\sigma_{1,2}
$$
**Where :**
- $\sigma_{1,2}$ is the **covariance** between asset 1 and 2
- $\sigma_{i}$ is the **variance** of the asset $w_{i}$

The above can also be **rewritten** as :
$$
\sigma_{p}^{2} = \alpha^{2}\sigma_{1}^{2} + (1 - \alpha)^{2}\sigma_{2}^{2} + 2\alpha(1 - \alpha)p_{1,2}\sigma_{1}\sigma_{2}
$$
$$
\sigma_{p}^{2} = (\sigma_{1}^{2} + \sigma_{2}^{2} - 2p_{1,2}\sigma_{1}\sigma_{2})\alpha^{2} - 2\sigma_{2}(\sigma_{2} - p_{1,2}\sigma_{1})\alpha + \sigma_{2}^{2}
$$
**Where :**
- $p_{1,2}$ is the **corelation of return** for asset $w_{1}$ and $w_{2}$

# Global Minimum-Variance Portfolio
---
Before continuing, given $ax^{2} + bx + c$ can be written in the form of $a(x + b)^{2} + c$ by using the <span style='color:#2d98da'>complete the square formula</span>.
$$
ax^{2} + bx + c = 0 = a(x+d)^{2} + e
$$
**Where :**
- $d = \frac{b}{2a}$
- $e = c - \frac{b^{2}}{4a} = (\frac{b}{2\sqrt{a}})^{2}$ 

Using the <span style='color:#2d98da'>portfolio variance fomula</span> above :
- $a = (\sigma_{1}^{2} + \sigma_{2}^{2} - 2p_{1,2}\sigma_{1}\sigma_{2})$
- $b = 2\sigma_{2}(\sigma_{2} - p_{1,2}\sigma_{1})$
- $c = \sigma_{2}^{2}$

**Therefore :**
$$
\sigma_{p}^{2} = \left(\alpha\sqrt{(\sigma_{1}^{2} + \sigma_{2}^{2} - 2p_{1,2}\sigma_{1}\sigma_{2}}) - \frac{\sigma_{2}(\sigma_{2} - p_{1,2}\sigma_{1})}{\sqrt{(\sigma_{1}^{2} + \sigma_{2}^{2} - 2p_{1,2}\sigma_{1}\sigma_{2})}}\right)^{2} + \sigma_{2}^{2} - \frac{\sigma_{2}^{2}(\sigma_{2} - p_{1,2}\sigma_{1})^{2}}{(\sigma_{1}^{2} + \sigma_{2}^{2} - 2p_{1,2}\sigma_{1}\sigma_{2})}
 $$

Here $\alpha$ is our **variable**.

To <span style='color:#20bf6b'>minimise risk</span>, then :

$$
\alpha = \alpha^{*} = \frac{\sigma_{2}(\sigma_{2} - p_{1,2}\sigma_{1})}{(\sigma_{1}^{2} + \sigma_{2}^{2} - 2p_{1,2}\sigma_{1}\sigma_{2})}
$$
**Where :**
- $\alpha^{*}$ means the smallest value for $\alpha$
- This $\alpha$ will make whatever is in the $(x)^2$ to be 0


Thus the <span style='color:#fa8231'>minimum portfolio variance</span> (**GMVP**) is just :
$$
(\sigma_{p}^{2})^{*} = \frac{\sigma_{1}^{2}\sigma_{2}^{2}(1 - p_{1,2}^{2})}{\sigma_{1}^{2} + \sigma_{2}^{2} - 2p_{1,2}\sigma_{1}\sigma_{2}}
$$

And the <span style='color:#fa8231'>portfolio mean with the minimum risk</span> is as follows :
$$
(\mu_{p})^{*} = \alpha^{*}\mu_{1} + (1 - \alpha^{*})\mu_{2}
$$

This can be **rewritten** in term of $\alpha$ as :
$$
\alpha = \frac{\mu_{p} - \mu_{2}}{\mu_{1} - \mu_{2}}
$$
This $\mu_{p}^{*}$ is <span style='color:#f7b731'>not always the minimum or maximum</span>.

If $\alpha$ is expressed in terms of $\mu$ from the equation above, then <span style='color:#fa8231'>subbing</span> $\color {#fa8231} {\alpha}$ <span style='color:var(--mk-color-orange)'>into the variance formula</span> :
$$
\sigma^{2}_{p} = A\mu_{p}^{2} + B\mu_{p} + C
$$
Which is a <span style='color:#f7b731'>hypobola</span>.

**Where :**
$$
A = \frac{\sigma_{1}^{2} + \sigma_{2}^{2} - 2p_{1,2}\sigma_{1}\sigma_{2}}{(\mu_{1} - \mu_{2})^{2}} \ge 0
$$
$$
B = \frac{-2(\mu_{2}\sigma_{1}^{2} - (\mu_{1} + \mu_{2})p_{1,2}\sigma_{1}\sigma_{2} + \mu_{1}\sigma_{2}^{2})}{(\mu_{1} - \mu_{2})^{2}}
$$
$$
C = \frac{\mu_{2}^2\sigma_{1}^{2} - 2\mu_{1}\mu_{2}p_{1,2}\sigma_{1}\sigma_{2} + \mu_{1}\sigma_{2}^{2}}{(\mu_{1} - \mu_{2})^{2}}
$$
# Logarithmic Return
---
The <span style='color:#0fb9b1'>logarithmic return</span> is denoted by $R$, and the return can be calculated by :
$$
R= ln\left(\frac{P_{n}}{P_{0}}\right)
$$
**Where :**
- $P_{0}$ is the price of the asset at $t = 0$
- $P_{n}$ is the price of the asset at $t = n$

Equivalently, $P_{1}$ can be calculated by :
$$
P_{1} = P_{0}e^{R}
$$
What about the <span style='color:var(--mk-color-orange)'>rate of return</span> of an asset from 0 to $n$ which is denoted by $r(0,n)$ :
$$
r(0,n) = \frac{P_{n}}{P_{0}} - 1
$$

The <span style='color:#fa8231'>relationship</span> between the<span style='color:#fa8231'> rate of return</span> $(r)$ and the <span style='color:#0fb9b1'>log return</span> $(R)$ is given by :
$$
e^{R} = 1 + r \text{ or } R = ln(1+ r)
$$
What about the<span style='color:var(--mk-color-turquoise)'> log return</span> of an asset from 0 to $n$ which is denoted by $R(0,n)$ :
$$
R(0,n) = ln\left(\frac{P_{n}}{p_{0}}\right)= ln(P_{n}) - ln(P_{n-1}) + \dots +ln(P_{1}) - ln(P_{0}) 
$$
**Simplifying** this will give us :
$$
\sum^{n}_{k = 1} ln(P_{k}) - ln(P_{k - 1}) = \sum^{n}_{k=1} R_{k}
$$
## No Probability

What if there is no probability but rather just the <span style='color:#fa8231'>date and the price of the stock at that date</span>, how to calculate the rate of return or the logarithmic return?

Well just follow this formula :
$$
r_\text{date} = \frac{P_\text{date}}{P_\text{date - 1}} - 1
$$
$$
R_\text{date} = ln\left(\frac{P_\text{date}}{P_\text{date - 1}}\right)
$$
**Where :**
- $P_\text{date}$ is the **price** of the asset at that <span style='color:#f7b731'>particular date</span>
- $P_\text{date - 1}$ is the **price** of the asset the <span style='color:#f7b731'>day before</span>
- $r$ stands for the rate of return while $R$ is the logarithmic return
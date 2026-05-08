---
title: Forwards & Futures
Date Created: 2024-04-03
Last Updated: 2025-09-27
tags:
  - QF1100
  - Math
  - Finance
---
# Forwards
---
<span style='color:#0fb9b1'>Derivative security</span> is a security whose <span style='color:#f7b731'>payoff</span> is explicitly <span style='color:#f7b731'>tied to the value of some other variable</span>, usually based on the price of some other financial security.

What is a <span style='color:#0fb9b1'>forward contract</span>, it is basically an <span style='color:#f7b731'>agreement to buy something at an agreed upon price</span> at a later date.

**For example :** A forward contract to buy 5000 bushels (unit of measurement) of wheat at $8 per ton in **3 months**

Using the example above, this means in <span style='color:#f7b731'>3 months time no matter</span> what, the <span style='color:#f7b731'>purchase</span> will be made at <span style='color:#f7b731'>$8 per ton</span>.

And if in 3 months, the <span style='color:#fa8231'>price of wheat goes</span> up to $9 then the <span style='color:#f7b731'>contract will have a value of $1</span> per bushel.

**Terminologies**
- **Short** is when buyers while **Short** is for sellers
- $T$ is denoted as the **expiration / maturity** date
- $F_{0}$ is called the **forward price** which is the <span style='color:#f7b731'>price at expiration</span> or the price of the contract
- $S(t)$ or $S_{t}$ is known as the <span style='color:#f7b731'>spot price</span> which is the market value at time $t$

Here is how to calculate the payoff / Profit from the contracts :
- For a <span style='color:#fa8231'>long forward contract</span> - $S(T) - F_{0}$
- For a <span style='color:#fa8231'>short forward contract</span> - $F_{0} - S(T)$

## Arbitrage

<span style='color:#0fb9b1'>Arbitrage opportunities</span> is a method of <span style='color:#f7b731'>buying</span> something in one place <span style='color:#f7b731'>and selling</span> it in another at the <span style='color:#f7b731'>same time</span> and profiting from the difference.

**Example :**
- Assume that at $t = 0$ a **stock price is $40**
- And that there is a **3 month risk free interest rate of 5%** per annum compounded continuously
- If the forwards price for a contract is at $F_{0} = 40$.

What can be done is that,
1) Short 1 stock thus gaining $40
2) Deposit the $40 into a bank for 3 months earning $40.5
3) At the same time buy the forward contract for $40
4) In 3 months, withdraw from the deposit for $4.50 and buy execute the contact for $40
5) The 1 share brought will be used to **pay back the shorted share in step 1**
6) Thus profiting for $0.5

## Forward Pricing

The objective is to <span style='color:#f7b731'>find a price</span> for the forward contract such that there will <span style='color:#f7b731'>not be any arbitrage opportunity</span>.
$$
F = \frac{S}{d(0,T)} \text{ meaning, } S = d(0,T) \times F 
$$
**Where :**
- $S$ is the spot price, price at $t = 0$ 
- $F$ is the future price at time $t$
- $d(0,T)$ is the <span style='color:#f7b731'>discount factor</span> between 0 and $t$ ($(1 + r)^{-T}$), in general $d(k,M) = (1 + r)^{-(M - k)}$

The formula above will make the <span style='color:#f7b731'>present value</span> of the cashflow $(-S,F)$ to be <span style='color:#f7b731'>0</span>.
## Cost of Carry

What if there is some <span style='color:#f7b731'>cost in between holding an asset to selling it</span>. How to set the price such that there will not be any arbitrage opportunity.

**General Cash Flow :** $(-S - c(0), -c(1), \dots, -c(M-1), F)$

It may <span style='color:#f7b731'>not always be a negative carrying cost</span>, for example bond will have a periodic coupon payment.

Note that when finding $F$, it is for the <span style='color:#f7b731'>future value</span>, thus use the FV formula.

To make the **PV for the above cash flow to be 0** :
$$
F = \frac{S}{d(0,M)} + \sum_{k=0}^{M-1} \frac{ck}{d(k,M)}
$$
**Where :**
- The delivery date $T$ becomes $M$ **periods**
- $c(k)$ is the carrying cost per unit from $k$ to $k+1$
- $d(k,M)$ is the discount factor from $k$ to $M$
# Futures
---
Unlike forward contracts, <span style='color:#0fb9b1'>futures</span> settlement happens every day and its price changes everyday as well like in the stock market. It can be executed at any time, thus more liquid.

**Futures against Spot Price**
![[Futures vs Spot Price.png|center]]

Given the cash flow of a future contract, the sum of all entries are :
$$
S(T) - F(0)
$$
**Where :**
- $S(T)$ is the spot price at $t = T$
- $F(0)$ is the face value of the future contract.

This assumes is there is <span style='color:#f7b731'>no interest rate</span> $R = 0\%$
## Accrued Profit

Now what if there is an <span style='color:#f7b731'>interest rate</span>.
$$
\text{Total Profit } = \text{Qty } \times \sum_{i=0}^{T} (F(i) - F(i-1))R^{T-i}
$$
**Where :**
- $R^{T-i}$ is the interest rate at time $t$
- $F(i)$ is the price of the futures at time $t = i$


Just remember that the formula above given is for the <b><mark style='background:#f7b731'>long position</mark></b>.

If the position is <b><mark style='background:#f7b731'>short</mark></b>, just change $F(i) - F(i - 1)$ to be $F(i - 1) - F(i)$. Or the quantity will be negative.
---
title: Options
Date Created: 2024-04-20
Last Updated: 2025-09-27
tags:
  - QF1100
  - Math
  - Finance
---
# Options
---
Unlike futures or forwards, an <span style='color:var(--mk-color-turquoise)'>option</span> is the <span style='color:var(--mk-color-yellow)'>right but not the obligation to buy or sell</span> an asset under specified terms. And the <span style='color:var(--mk-color-yellow)'>contract does not necessary have to be exercised</span>.

There are <span style='color:var(--mk-color-orange)'>2 types of options</span> :
- <span style='color:var(--mk-color-teal)'>Call</span> option, which is **buying the rights**
- <span style='color:var(--mk-color-red)'>Put</span> option, which is to **sell the rights** (Give up)

<span style='color:var(--mk-color-yellow)'>Rights</span> are only for people with a <span style='color:var(--mk-color-teal)'>call</span> option, while for people with <span style='color:var(--mk-color-red)'>put</span> options are <span style='color:var(--mk-color-yellow)'>obliged to buy/sell</span> if the option is exercised.

This option contract has :
- **Strike price** or **exercise price**, which is the <span style='color:var(--mk-color-yellow)'>agreed upon price</span> to buy/sell an asset
- **Expiration date** or **maturity date** which is the <span style='color:var(--mk-color-yellow)'>expiry date</span> for the contract (**Don't need to exercise it on this day**).
- **Option price** or **option premium**, which is the <span style='color:var(--mk-color-yellow)'>price to buy the contract</span>

**Exercises**
>Only the <span style='color:var(--mk-color-yellow)'>buyer</span> (<span style='color:var(--mk-color-teal)'>Call</span> option) can choose to buy/sell the asset based on the contract. The seller (<span style='color:var(--mk-color-red)'>Put</span> option) has no choice

**Option region**
- American options can be <span style='color:var(--mk-color-yellow)'>exercised at any time</span>
- European options can only be <span style='color:var(--mk-color-yellow)'>exercised on the expiration date</span> (Assume to be this unless stated)

**Call vs Put**
![[Call vs Put.png|center]]

# Value from options
---
Supposed, a long <span style='color:var(--mk-color-yellow)'>call option</span>, with strike price $K$ and the price pf the asset on the expiration date is $S$, there are 2 scenarios :
1) $S \lt K$, the <span style='color:var(--mk-color-turquoise)'>option value</span> is 0 since market price is smaller than option price thus do not exercise the contract
2) $S \ge K$, the <span style='color:var(--mk-color-turquoise)'>option value</span> is $S - K$ since the shares are bought at price $K$ and sold immediately at price $S$
$$
\text{Profit} = max(0, S - K) =
\begin{cases}
S - K  & \text{if } S \ge k\\
0 & \text{if } S \lt k
\end{cases}
$$
**Where :**
- $S$ is the <span style='color:var(--mk-color-yellow)'>price of the asset in the market</span> at expiration date
- $K$ is the <span style='color:var(--mk-color-orange)'>price</span> agreed in the <span style='color:var(--mk-color-yellow)'>contract</span>

This can be denoted by $(S - K)^{+}$, the + means the <span style='color:var(--mk-color-yellow)'>value will always be positive</span>, if $S - K$ is negative then it will be 0. 

For <span style='color:var(--mk-color-orange)'>longing</span> a <span style='color:var(--mk-color-yellow)'>put option</span>, add a negative at the front or change it to $K - S$ instead.

**How to profit for options**
![[Profiting from Options.png|center]]

There is however a <span style='color:var(--mk-color-yellow)'>cost in buying the contract</span>. Therefore for **long** positions, the **graph is shifted downwards** while **short** positions are **shifted upwards**.

Thus to <span style='color:var(--mk-color-yellow)'>break even</span>, the market price $S_{T}$ must be <span style='color:var(--mk-color-yellow)'>smaller or greater</span> than the strike price (**depending on position**), to cover the cost of the option.

**For long options**
$$
\text{Profit} = (S_{T} - K)^{+} - R^{T} \times C
$$
**Where :**
- $R^{T} = (1 + r)^{T}$ which is the **interest rate**
- $C$ is the **option premium**
- $R^{T} \times C$ is the **future value** of the option premium
- $(S_{T} - K)$ is for <span style='color:var(--mk-color-teal)'>call</span> for <span style='color:var(--mk-color-red)'>puts</span> use $K - S_{T}$

**For short options**
$$
\text{Profit} = (K - S_{T})^{+} + R^{T} \times C
$$
**Where :**
- $R^{T} = (1 + r)^{T}$ which is the **interest rate**
- $C$ is the **option premium**
- $R^{T} \times C$ is the **future value** of the option premium
- $(K - S_{T})^{+} = -(S_{T} - K)^{+}$, they are interchangeable
- $(S_{T} - K)$ is for <span style='color:var(--mk-color-teal)'>call</span> for <span style='color:var(--mk-color-red)'>puts</span> use $K - S_{T}$

# How to Price an Option
---
When pricing an option, there must be no arbitrage opportunity (**No-arbitrage assumption**).

**Upper bound pricing**
1) For a <span style='color:var(--mk-color-yellow)'>call</span> option, $C \le S_{0}$
	- This is true because if not, someone can buy a stock at $S_{0}$, then **short a call** at $C$ and they will earn the difference
2) For a <span style='color:var(--mk-color-yellow)'>put</span> option $P \le K \times R$, which is the strike price and $R$ is the interest rate
	- This is true because if not, someone can **short a put** then put $P$ into the bank with interest $R$

**Lower bound pricing**
1) For a <span style='color:var(--mk-color-yellow)'>call</span> option, $C \ge max(0, S_{0} - KR)$
	- If not, someone <span style='color:var(--mk-color-yellow)'>can short</span> 1 stock at $S_{0}$ and <span style='color:var(--mk-color-yellow)'>buy the call</span> at $C$
	- The remaining amount can be <span style='color:var(--mk-color-yellow)'>placed in the bank</span> and at $T$ they will have **earned more than** $K$
	- If $S_{T} \lt K$, then just buy the stock at $S_{T}$ for a **greater profit** and close the short position
	- If $S_{T} \ge K$, then exercise the option this is the **minimum profit**

Thus if $C$ is <span style='color:var(--mk-color-orange)'>too low</span>, then the <span style='color:var(--mk-color-orange)'>profit</span> is within this <span style='color:var(--mk-color-orange)'>range</span> :
$$
(S_{0} - C) R - S_{T} \gt (S_{0} - C)R - K \gt 0
$$
**Where :**
- $R$ is the **interest rate**
- $C$ is the <span style='color:var(--mk-color-yellow)'>call option price</span>

2) For a <span style='color:var(--mk-color-yellow)'>put</span> option, $P \ge max(0, KR - S_{0})$
	- If not, someone can make a <span style='color:var(--mk-color-yellow)'>loan</span> for $S_{0} + P$  and <span style='color:var(--mk-color-yellow)'>buy the put</span> at $P$ and <span style='color:var(--mk-color-yellow)'>1 stock</span> at $S_{0}$
	- Here no matter the future value, the **repayment of loan with interest will be lower** than $S_{T}$ and $K$
	- If $S_{T} \lt K$, then just exercise the option and sell at $K$ and repay the loan at $(S_{0} + P)R$ this is the **minimum profit**
	- If $S_{T} \ge K$, then sell the stock at $S_{T}$ for a **greater profit** after paying back the loan at $(S_{0} + P)R$

Thus if $P$ is <span style='color:var(--mk-color-orange)'>too low</span>, then the <span style='color:var(--mk-color-orange)'>profit</span> is within this <span style='color:var(--mk-color-orange)'>range</span> :
$$
S_{T} - (S_{0} + P) R \ge K - (S_{0} - P)R \gt 0
$$
# Trading Strategies
---
There are many <span style='color:var(--mk-color-orange)'>strategies</span> involving options :
1) **Principle-protected notes** which can be done with a <span style='color:var(--mk-color-teal)'>zero-coupon bond</span> and a <span style='color:var(--mk-color-teal)'>European call option </span>
	>This strategy guarantees the buyer that they will <span style='color:var(--mk-color-yellow)'>at least get back their principle regardless</span>
2) **Spread trading strategy** which involves taking positions in <span style='color:var(--mk-color-yellow)'>2 or more options of the same type</span> (e.g. 2 or more puts)
	>Some <span style='color:var(--mk-color-orange)'>examples of spreads</span> are, bull, bear, box, butterfly and straddle spreads

## Butterfly Spreads

This involves positions in <span style='color:var(--mk-color-teal)'>European options</span> where :
- There are **3 different strike prices**, $K_{1} \lt K_{2}, \lt K_{3}$
- All the options bought have the **same expiration date**

This is <span style='color:var(--mk-color-orange)'>effective</span>, if an <span style='color:var(--mk-color-yellow)'>investor accurately predicts</span> that in the future the price of the <span style='color:var(--mk-color-yellow)'>stock will be around a certain price</span>. But this will <span style='color:var(--mk-color-red)'>not be profitable</span> if the <span style='color:var(--mk-color-red)'>actual stock price exceeds this range</span>.

An <span style='color:var(--mk-color-green)'>advantage</span> of this **over just buying one option** is the range of the expected price for $S_{T}$ is lower as compared to just buying 1 option.

**How to carry out this strategy**
1) **Long** a <span style='color:var(--mk-color-teal)'>call</span> with the strike price of $K_{1}$ and a <span style='color:var(--mk-color-teal)'>call</span> with strike price $K_{3}$ (<span style='color:var(--mk-color-yellow)'>This is the predicted range</span>)
2) **Short 2** <span style='color:var(--mk-color-teal)'>call</span> options with strike price $K_{2}$, usually $K_{2} = \frac{1}{2}(K_{1} + K_{2}))$

**Butterfly spread payoff scenarios**
![[Butterfly Spread Payoff Table.png|center]]

The above payoff **does not take into account the option premium**. Thus the <span style='color:var(--mk-color-red)'>cost</span> is 2 short call - 2 long calls.

**Butterfly spread payoff diagram using <b><span style='color:var(--mk-color-blue)'>calls</span></b>**
![[Butterfly Spread Payoff Diagram Using Calls.png|center]]

**Butterfly spread payoff diagram using <b><span style='color:var(--mk-color-red)'>puts</span></b>**
![[Butterfly Spread Payoff Diagram Using Puts.png|center]]

The **profit table will be different as well**. Which is just the opposite of using a <span style='color:var(--mk-color-teal)'>call</span>.

## Bull Spreads

This is <span style='color:var(--mk-color-orange)'>effective</span>, if an <span style='color:var(--mk-color-yellow)'>investor accurately predicts</span> that in the future the price of the <span style='color:var(--mk-color-yellow)'>stock will be above a certain price</span>. As long as on expiration date, if the **price is above the predicted price**, there will be a <span style='color:var(--mk-color-green)'>profit</span>.

**How to carry out this strategy**
1) **Long** a <span style='color:var(--mk-color-teal)'>call</span> with the strike price of $K_{1}$ (<span style='color:var(--mk-color-yellow)'>The price predicted by the investor</span>)
2) **Short 1** <span style='color:var(--mk-color-teal)'>call</span> options with strike price $K_{2}$, where $K_{2} \gt K_{1}$

![[Bull Spread Payoff Diagram.png|center]]

The same can be done with a <span style='color:var(--mk-color-red)'>put</span>, everything will be flipped and reversed, but this will be for a <b><mark style='background:var(--mk-color-turquoise)'>bear spread</mark></b>.
- **Long** a <span style='color:var(--mk-color-red)'>put</span> at $K_{2}$ (<span style='color:var(--mk-color-yellow)'>This is the investors predicted price</span>)
- **Short** a <span style='color:var(--mk-color-red)'>put</span> at $K_{1}$ where $K_{1} \lt K_{2}$
# Put-Call Parity
---
It is the <span style='color:var(--mk-color-yellow)'>relationship</span> between the <span style='color:var(--mk-color-yellow)'>prices</span> of a <span style='color:var(--mk-color-yellow)'>put and call option</span> with the same strike price and maturity date.

The parity sates that :
$$
C + dK = P + S_{0}
$$
**Where :**
- $d$ is the **discount factor** to maturity
- $K$ is the **strike price**
- $C$ and $P$ is the price of the <span style='color:var(--mk-color-teal)'>call</span> and <span style='color:var(--mk-color-red)'>put</span>

If the 2 prices **does not hold the equation** then there will an<span style='color:var(--mk-color-red)'> arbitrage opportunity</span>.
- Let both side of the equation be 1 portfolio 
- $A \rightarrow (C + dK)$ which is 1 call option and zero-coupon bond (A risk free interest) that provides a payoff $K$ at time $T$
- $C \rightarrow (P + S_{0})$ which is 1 put option and 1 share of a stock
- If they are not equal then
	1) If $A \gt B$ then buy $B$ and sell $A$
	2) If $A \lt B$ then buy $A$ and sell $B$

![[Put-Call Parity Portfolios Payoff.png|center]]

**If both sides are not equal, here is how to make a arbitrage opportunity**
![[Arbitrage Opportunity if Call-Put Parity is Not Equal.png|center]]
# Finding the Price for an Option
---
The approach to <span style='color:var(--mk-color-orange)'>find the price</span> for the option is using the <span style='color:var(--mk-color-teal)'>single-period binomial options theory</span>, which uses the [[Hedging#Binominal Lattice Model|binominal lattice]].

Remember that $S \times u$ means the price will go up a factor with probability $P$ and $S \times d$ means the price will drop with a probability of $1 - P$.

For there to be <span style='color:var(--mk-color-yellow)'>no arbitrage opportunity</span> : $u \gt R \gt d$

If $R \ge u \gt d$, means that the <span style='color:var(--mk-color-yellow)'>stock performs worse than a risk free asset</span> because the interest rate is better. Then just **short** the stock and **deposit the amount** into the bank for a profit of $SR - uS$ or $SR - dS$.

If $u \gt d \ge R$ then just <span style='color:var(--mk-color-yellow)'>borrow and long the stock</span> since interest rates are bad and obtain a profit of $uS - SR$ or $dS - SR$.

**Option pricing formula** for <b><mark style='background:var(--mk-color-orange)'>one period</mark></b> (t + 1) is given as :
$$
C = \frac{1}{R}(qC_{u} + (1 - q)C_{d})
$$
**Where :**
- $C$ is the price of the option
- $R$ is the interest rate
- $C_{u}$ is given by $max(uS - K, 0)$
- $C_{d}$ is given by $max(dS - K, 0)$
- $q$ is the <span style='color:var(--mk-color-turquoise)'>risk-neutral probability</span>

**Risk-neutral probability** can be calculated as such :
$$
q = \frac{R - d}{u - d}
$$
This pricing formula is <span style='color:var(--mk-color-yellow)'>independent of the probability</span> of the up and the down factor.

**Using the pricing theory for more than 1 period**
![[Multiperiod Option Pricing .png|center]]

This is for period $t = 2$, it will be the same for any $n$ period.

**Example with 5 periods**
![[Option Pricing Methods with 5 Periods.png|center]]
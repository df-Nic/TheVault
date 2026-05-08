---
title: Hedging
Date Created: 2024-04-10
Last Updated: 2025-09-27
tags:
  - QF1100
  - Math
  - Finance
---
# Margin Account
---
When investing in futures or options, a <span style='color:#0fb9b1'>margin account</span> is needed. This margin account will act as an account to collect profits as well as to<span style='color:#f7b731'> prevent people from defaulting on their obligation</span>.

Usually a <span style='color:#fa8231'>threshhold</span> is in place by around **50%** of the total investment value. And if it ever drops below, a lower bound (<span style='color:#0fb9b1'>maintenance margin level</span>) **25%**, then a <span style='color:#0fb9b1'>margin call</span> will be issued to request for a top-up

If there is <span style='color:#fa8231'>no top up</span> then the futures position will be <span style='color:#f7b731'>closed by taking out an equal and opposite position</span>.

**Scenario**
- Imagine owning a margin account with $\$4000$
- Then the price of a future contract <span style='color:#eb3b5a'>drops</span> by $\$3000$ after 1 day, the broker will deduct from the account
	- If there is no top up to meet the lower threshold, the contract will be closed, leaving a balance of $\$1000$
- If the price <span style='color:#20bf6b'>increases</span> by $\$1000$, then it will be deposited into the account

**Visualisation of a Margin Account Change**
![[Margin Account Example.png|center]]
# Hedging
---
The basis of hedging is to <span style='color:#f7b731'>use a forward contract</span> to <span style='color:#f7b731'>remove the risks of price fluctuations</span>.

Assuming there is <span style='color:#fa8231'>no hedging</span>, the profit and risk can be calculated as such :
$$
\text{Profit } = (S(t) \times \text{Amount}) - X
$$

$$
\text{Var[P] } = \text{Amount } \times (\text{Var[S(t)] } + \text{Var[X] } - 2\text{Cov(S(1),X)}) 
$$
**Where :**
- $X$ is any cost incurred
- $S(t)$ is the strike price at time $t$, which is just the market price at time $t$

However <span style='color:#fa8231'>with hedging</span>, the risk can be reduced into :
$$
\text{Var[P] } = \text{Amount } \times \text{Var[X] }
$$
The reason for this is because one $Var[S(t)] = 0$ because when longing or shorting a future contract, the price is locked in thus the <span style='color:#f7b731'>market fluctuation is not a problem</span>.

The <span style='color:#0fb9b1'>perfect hedging</span> is to <span style='color:#f7b731'>completely eliminate the risk</span> by <span style='color:#f7b731'>taking an equal and opposite position</span> in the futures market, but it is difficult to make it happen.

So by selling something, when the <span style='color:#f7b731'>price goes up it will be profitable</span>, to hedge this, <span style='color:#f7b731'>short</span> a future contract which is the opposite, if <span style='color:#f7b731'>price goes down this future contract is profitable</span>.

This will be the **opposite** when buying instead. Thus the <span style='color:#fa8231'>total profit</span> is :
$$
\text{Total Profit } = \text{Accrued Profit } + \text{Profit from selling/buying } - \text{Cost}
$$
The <span style='color:#0fb9b1'>accrued profit</span>, is the [[Forwards & Futures#Accrued Profit|profit]] from the opposite position future/forward contract. This <span style='color:#20bf6b'>minimises risk</span>.

## Minimum Variance Hedge

It is not always possible for a perfect hedge, usually hedging is done with another asset. This is known as the <span style='color:#0fb9b1'>basis</span>, which is just <span style='color:#f7b731'>another term for payoff in an imperfect hedging scenario</span>.
$$
\text{Basis } = \text{Sport Price of asset A to be hedge } - \text{Future price of contract for asset B} 
$$
**Where :**
- Our asset A is the <span style='color:#f7b731'>obligation to buy/sell</span> $W$ units at some time $T$
- $S_{A}(T)$ or $S_{T}$ is the **spot price for asset A** at time $T$
- $F_{B}(T)$ or $F_{T}$ is the future price of asset B  used as a hedge at time $T$. Remember that $F_{B}(0) = F_{0}$
- $h$ is the future position taken, how much to hedge (<span style='color:#0fb9b1'>hedge ratio</span>)
- $yT$ simply denoted as $y$ is the cash flow at $T$

Therefore the <span style='color:#fa8231'>cashflow can be calculated</span> as such :
$$
y = W\times S_{T} + (F_{T} - F_{0})\times h
$$
Take note that the formula above is if the future contract is in the **long** position, if it is **short** then swap $F_{T}$ and $F_{0}$.

Then the <span style='color:#fa8231'>variance</span> of the cash flow is :
$$
Var(y) = W^{2}Var(S_{T}) + 2W(Cov(S_{T}, F_{T}))h + Var(F_{T})h^{2}
$$
It looks complicated but, the <span style='color:#f7b731'>equation now is in terms of h</span>. Thus just need to <span style='color:#f7b731'>differentiate</span> the <span style='color:#f7b731'>equation and solve for the global minnimum</span>, then the value of $h$ will give the lowest risk.

So to <span style='color:#fa8231'>solving</span> for $h$ :
$$
h = -W\frac{Cov(S_{T}, F_{T})}{Var(F_{T})} = -W\frac{p_{S,F} \times \sigma_{S}}{\sigma_{F}}
$$
**Where :**
- $\sigma_{s}$ is the risk of asset A
- $\sigma_{F}$ is the risk of asset B
- $p_{S,F}$ is the [[Asset Comparison#Rate of Return of Assets|corelation coefficient]] whose formula was substitute in place of the $Cov(S_{T}, F_{T})$

It is possible that instead of the standard deviation the <span style='color:var(--mk-color-yellow)'>fluctuation is given</span>. Thus to get the standard deviation, it is just $\sigma = S_{0} * \text{Fluctuation}$

If $W$ is **not given** then assume to be 1.

Then sub $h$ back into $Var(y)$ :
$$
Var(y) = W^{2}Var(S_{T}) - \frac{W^{2}Cov(S_{T}, F_{T})^{2}}{Var(F_{T})} = W^{2}Var(S_{T})[1 - p^{2}_{F,S}]
$$
Then the risk is just the square root of $Var(y)$ which is :
$$
\sigma_{y} = \sqrt{1 - p^{2}_{F,S}} \times W\sigma_{s}
$$
**Where**
- $\beta = \frac{Cov(S_{T}, F_{T})}{Var(F_{T})}$ is called the <span style='color:#0fb9b1'>beta value</span>
- $\sqrt{1-p_{F,S}^{2}}$ is the factor that <span style='color:#f7b731'>measures the effectiveness of the hedging</span>

Sometimes, $h$ might <span style='color:#eb3b5a'>not be a multiple of 1 contract</span>, thus if only integer number of contracts are allowed then :
- **Determine if it is better to round up or down**
- Plug in the rounded numbers into the $Var(y)$ equation and choose the one that <b><mark style='background:#f7b731'>gives the smaller</mark></b> $Var(y)$ value.
- Or choose the one that is closer to $h$ for example $h = 5.33$ it is closer to $5$ than $6$.

**In general**
![[Scenarios to Hedge.png|center]]

# Binominal Distribution
---
Some <span style='color:#fa8231'>terminologies</span> : 
- $p$ is the probability of **success** in a single experiment
- $1 - p$ is the probability if **failure** in a single experiment
- $n$ is the total number of experiments
- $S$ is the **sample space** for all sequencies of $n$ independent experiments. All possible permutation of success and failure
- $X$ is the **number of successes**

Then the $\vert S \vert = 2^{n}$, then the $\vert X = k \vert = {n \choose k} = \frac{n!}{k!(n-k)!}$

This only works if the <b><mark style='background:#f7b731'>experiment has only 2 outcomes</mark></b>.

The <span style='color:#0fb9b1'>binominal distribution</span> of a random variable $X$, denoted by $X$ ~ $B(n,p)$, its [[Probability#Discrete Random Variable|PDF]] given as such :
$$
P(X = k)
\begin{cases}
{n \choose k}p^{k}(1-p)^{n-k}  & \text{if } 0 \le k \le n \\
0 & \text{otherwise}
\end{cases}
$$
For the binominal distribution to be 1, $1 = (p + 1 - p)^{n} = \sum^{n}_{k=0}{n \choose k}p^{k}(1-p)^{n-k}$

Therefore the <span style='color:#fa8231'>PDF</span> for an asset price $S(t)$ is as such $P(S(t) + u - (N - u) = {N \choose u}p^{u}(1-p)^{N-u}$ 
- $u$ is to increase by 1 unit
- $N-p$ is how many times it will decrease by 1 unit

The <span style='color:#fa8231'>expected value</span> (**mean**) and the <span style='color:#fa8231'>variance</span> of a <span style='color:#0fb9b1'>binominal distribution</span> is given as such :
$$
E[X] = np , Var(X) = np(1-p)
$$
## Binominal Lattice Model

Here is an **example** of a <span style='color:#0fb9b1'>binominal lattice</span> model :
![[Binominal Lattice Model.png|center]]

As <span style='color:#fa8231'>time goes to infinity</span>, it will <span style='color:#f7b731'>follow the binominal distribution</span>. And this is a multiplicative model.

### Additive Model

The additive model is simply just the <span style='color:#f7b731'>probability of a price at time</span> $\color {#f7b731} {t}$ to <span style='color:#f7b731'>increase by 1 unit</span> (**Some price**).

Now given some asset A :
1) If the price at time $t = k - 1$ <span style='color:#20bf6b'>is given</span> then
	- $S(k) = aS(k-1) + u(k-1)$
2) If the price at time $t = k - 1$ is <span style='color:#eb3b5a'>not given</span>
	- $S(k) = a^{k}S(0) + a^{k-1}u(0) + a^{k-2}u(1) + \dots + u(k-1)$

**Where :**
- $S(k)$ or $S_{k}$ is the price at period $k$
- $u(k)$ is the random variable that defines the <b><mark style='background:#f7b731'>relative difference of the prices</mark></b>
- $a$ is the contrast

**Example :**
Let $a = 1$ and $P(u(k) = 1) = p$ and $P(u(k) = -1) = 1 - p$ and let $S(k) = 100$ at time $t = 0$.

Firstly this means that, the <span style='color:#f7b731'>probability of the pricing to increase</span> by $1 is $p$. And the <span style='color:#f7b731'>probability to decrease</span> by $1 is $1-p$.

Therefore,
$$
S(1) =
\begin{cases}
S(0) + 1  & \text{With probability } p \\
S(0) - 1, & \text{With probability } 1 - p
\end{cases}
$$
One issue to <span style='color:#eb3b5a'>worry about is negative prices</span>, it is possible that this <span style='color:#0fb9b1'>additive model</span> can go below 0.

The expected value or <span style='color:#fa8231'>mean</span> using the additive model is just $E[x] = \sum^{x}_{k=0} (Price + k - (N - k)) \times P(Price + k - (N - k))$

With the mean, the variance can be calculated using $Var(x) = E[x^{2}] - E[x]^{2}$.
### Multiplicative Model

Not instead of price differences, the <span style='color:#0fb9b1'>multiplicative model</span> <span style='color:#f7b731'>handles percentage change</span>. 
$$
S(k) = S(k - 1) \times u(k - 1)
$$
But this can be <span style='color:#f7b731'>converted into a additive model</span> by taking the $ln$ on both sides.
$$
ln(S(k)) = ln(S(k) \times u(k)) = ln(u(k)) + ln(S(k))
$$
**Where :**
- $S(k)$ or $S_{k}$ is the price at period $k$
- $u(k)$ is the random variable that defines the <b><mark style='background:#f7b731'>relative change of the prices</mark></b>

**Example :**
Let $a = 1$ and $P(u(k) = u) = p$ and $P(u(k) = d) = 1 - p$, $u = 1.03$, $d = 1.2$ let $S(k) = 100$ at time $t = 0$.

This means that, the <span style='color:#f7b731'>probability of the pricing to increase</span> by a <span style='color:#f7b731'>factor</span> of $u$ is $p$. And the <span style='color:#f7b731'>probability to decrease</span> by a <span style='color:#f7b731'>factor</span> of $d$ has probability of $1 - p$.

Therefore,
$$
S(1) =
\begin{cases}
S(0) \times u  & \text{With probability } p \\
S(0) \times d, & \text{With probability } 1 - p
\end{cases}
$$
If $S(k - 1)$ was <span style='color:#eb3b5a'>not given</span>, then $ln(S(k)) = ln(S(0)) + ln(u(0)) + ln(u(1)) + \dots + ln(u(k-1))$

The <span style='color:#fa8231'>expected value</span> (**mean**) and <span style='color:#fa8231'>variance</span> is as follows :
$$
E[ln(S(k))] = ln(S(0)) + k \times v, Var(ln(S(k))) = k \times \sigma^{2}
$$

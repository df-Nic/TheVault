---
title: Probability
Date Created: 2024-02-27
Last Updated: 2025-09-27
tags:
  - QF1100
  - Math
  - Probability
---
# Terminology
---
**Sample space** - It is a set of all possible outcomes

**Sample point** - It is a element in the <span style='color:#0fb9b1'>sample space</span>

**Event** - It is a <span style='color:#f7b731'>subset</span> of a <span style='color:#0fb9b1'>sample space</span>

**Cardinality** - It is the <span style='color:#f7b731'>size</span> of the <span style='color:#0fb9b1'>sample space</span>

# Events
---
An event is just a subset of a the sample space, but the <span style='color:#f7b731'>sample space is also an event</span>. This is what is known as a <span style='color:#0fb9b1'>sure event</span>, meaning no matter what the outcome is it will be in this event.

Same goes for a <span style='color:#f7b731'>empty set</span> ($\emptyset$), this is known as a <span style='color:#0fb9b1'>null event</span>.

How about a set of <span style='color:#fa8231'>all sample points not inside a particular event</span>, this is known as a <span style='color:#0fb9b1'>compliment</span> of an event which is denoted as $E' = S \backslash A$.

An <span style='color:#0fb9b1'>intersection</span> of 2 events ($A \cap B$), is a set of <span style='color:#f7b731'>sample points present in both events</span>. And a <span style='color:#0fb9b1'>mutually exclusive event</span> is where the <span style='color:#f7b731'>interersection is a null set</span> ($A \cap B = \emptyset$).

Lastly the <span style='color:#0fb9b1'>union</span> of 2 events, is the set of <span style='color:#f7b731'>all sample points in both the events</span> ($A \cup B$).

**Example :**
- Sample space - $S = \{ (i,j) \vert 1 \le i,j \le 6\}$
- Event - $E = \{(i,j) \in S \vert i + j = 7\}$
# Probability
---
A <span style='color:#0fb9b1'>probability</span> of an event $P(E)$ is the <span style='color:#f7b731'>chance that the event will occur</span>.

**Some rules of probability**
- $P(S) = 1$, meaning no probability of an event is more than 1
- $0 \le P(E) \le 1 \forall E \subseteq S$ 
- If $E_{1}, E_{2}, \dots, E_{n}$ are <b><mark style='background:#f7b731'>all mutually exclusive events</mark></b>, then the <span style='color:#fa8231'>union of all events</span> it the <span style='color:#f7b731'>sum of all the probability</span> of each event.
- $P(A^{c}) = 1 - P(A)$, the term $A^{c}$ is called <span style='color:#0fb9b1'>A compliment</span>, which is probability of A <span style='color:#eb3b5a'>not happening</span>.
- If $A \subseteq B$ then $P(A) \le P(B)$

<span style='color:#0fb9b1'>Equally likely outcomes</span>, means that <span style='color:#f7b731'>each sample point</span> in the sample space has the <span style='color:#f7b731'>same probability</span>. Its like flipping a fair coin or a fair dice.

**To calculate probability**
$$
P(E) = \frac{\text{Number of points in E}}{\text{Number of points in S}} = \frac{\vert{E}\vert}{\vert{S}\vert}
$$
**Where :**
- $\vert{E}\vert$ is the cardinality of the set or the <span style='color:#f7b731'>size of the set</span>
- $S$ is the sample space
- $E$ is the event set

## Cumulative Distribution Function

<span style='color:#0fb9b1'>Random variable</span>, is some <span style='color:#f7b731'>real valued function on the sample space</span>. Basically some even which will happen. For example the probability that the sum of 2 dice is 6, meaning the random variable is 6.

The <span style='color:#0fb9b1'>cumulative distribution function</span> (CDF), is defined by 
$$
Fx(x) = P\{X \le x\}, x \in \Bbb{R}
$$
**Where :**
- $X$ is the random variable
- $x$ is a event in $\Bbb {R}$

The above is trying to say the <span style='color:#f7b731'>probability of something smaller than</span> $\color {#f7b731} {x}$.

**Properties of CDF**
- $Fx$ is a non-decreasing function, then if $a \lt b$ then $Fx(a) \le Fx(b)$ because $\{a \lt X \le b\} \subseteq \{X \le b\}$
- $P\{a \lt X \le b\} = P\{X \le b\} - P\{X \le a\}$ which is just $Fx(b) - Fx(a)$
- $Fx(+\infty) = 1$ as this is a **sure event**
- $Fx(-\infty) = 0$ as this is a **null event**
- $0 \le Fx(x) \le 1$

## Discrete Random Variable

A random variable is <span style='color:#0fb9b1'>discrete</span> if the <b><mark style='background:#f7b731'>possible values</mark></b> are <span style='color:#f7b731'>finite or countably infinite</span>. And its <span style='color:#0fb9b1'>probability density function</span> (PDF) is defined by :
$$
fx(x) = P\{X = x\}
$$

The difference with CDF, is that CDF can have impossible values as well as it is in the range of $\Bbb {R}$.

And having all the <span style='color:#f7b731'>probability of all possible value will give a total sum of 1</span>.

## Continuous Random Variable

Now instead of a jump in various probabilities, now the random variable is <span style='color:#0fb9b1'>continuous</span>. Meaning its CDF represents some continuous function from $(-\infty, \infty)$, <span style='color:#f7b731'>representing the probability curve</span>.

$$
P\{X \in B\} = \int_{B} fx(t) dt
$$
**Using CDF**
$$
Fx(x) = \int^{x}_{-\infty} fx(t)dt
$$

Something interesting is that this can give the <span style='color:#f7b731'>z-score from the normal distribution</span> :
$$
Fx(a) = P(X \le a) = \int^{a}_{-\infty} \frac{1}{\sqrt{2\pi}}e^{-\frac{x^{2}}{2}}
$$
To integrate this the [[Integrals#Type 1 Improper Integrals|type 1 integral]] is needed.

**Properties**
- If integrating on 1 point, the <span style='color:#f7b731'>probability is 0</span>
- The<span style='color:#f7b731'> value cannot be smaller than 0</span>, since the area under the curve cannot be negative
- If integrating from $-\infty$ to $\infty$ the <span style='color:#f7b731'>value must be 1</span>

# Expected Value
---
<span style='color:#0fb9b1'>Expected value</span>, is a <span style='color:#f7b731'>weighted average</span> of the possible values that can happen, which is denoted as $E[{X}]$

**If it is discrete :**
$$
E[{X}] = \sum (x \times P(X = x))
$$
**Where :**
- The summation is <b><mark style='background:#f7b731'>over all possible values</mark></b> of $X$

**If it is continuous :**
$$
E[{X}] = \int^{\infty}_{-\infty} xf(x)dx
$$

**Properties :**
$$
E[{aX + bY}] = aE[{X}] + bE[{X}]
$$
# Variance
---
With the <span style='color:#0fb9b1'>expected value</span>, which is the <span style='color:#f7b731'>mean</span>, the <span style='color:#0fb9b1'>variance</span> can be calculated, which is the spread or variation between the possible values of a random variable $X$.

The <span style='color:#f7b731'>larger the spread the higher the risk</span>, even though the expected values can be the same. This is because, someone can earn a lot but also can lose a lot.

$$
Var(x) = E[(X - E[x])^{2}] = E[X^{2}] - (E[X])^{2}
$$
Now with the variance, the <span style='color:#fa8231'>standard deviation can be calculated</span>, $\sigma = \sqrt{Var(x)}$.

**Properties**
- $Var[x] \ge 0$, because to get the standard deviation, there is a need for a square root
- $Var[c] = 0$ where $c$ is a constant value and not a random variable (Range)
- $Var[cX] = c^{2}Var[x]$ 

What about a <span style='color:#fa8231'>continuous random variable</span>, then integrate from $a$ to $b$ where $(a, b)$ is the range for the random variable.

## Normal Random Variable

A <span style='color:#0fb9b1'>normal random variable</span> is a normally distributed variable, with the <span style='color:#f7b731'>mean</span> ($\mu$) and <span style='color:#f7b731'>variance</span> ($\sigma^{2}$) as parameters. It function will be given as such :
$$
f(x) = \frac{e^{-\frac{(x - \mu)^{2}}{2\sigma^{2}}}}{\sigma\sqrt{2\pi}}
$$
**Where**
- $\sigma^{2}$ is the **variance**
- $\mu$ is the **population average** (mean)

## Log-normal Distribution

A random variable $X$ is <span style='color:#0fb9b1'>log-normally distributed</span> if $Y = ln(x)$.

![[PDF & CDF Graphs.png|center]]

# Join Probability
---
How to find the <span style='color:#fa8231'>probability of 2 random variables</span>. A join cumulative distribution of $X$ and $Y$ is given as :
$$
F_{X,Y}(x,y) = P\{X \le x, Y \le y\}
$$
And if $X$ and $Y$ are <span style='color:#f7b731'>independent</span>, then for any events, their probability is $P(A) \times P(B)$.

However $F_{X,Y} (x,y) = F_{X}(x)F_{Y}(y)$ might <span style='color:#f7b731'>not always be true</span> as they <span style='color:#eb3b5a'>might not be independent</span>.

This is tied to the [[#Discrete Random Variable|PDF]]. Where : 
$$
F_{x}(a) = P\{X \le a\} = P\{X \le a, Y \lt \infty \} = F_{X,Y}(a, \infty) = \lim_{b \to \infty}F_{X,Y}(a,b)
$$
Basically, if the goal is to find $X$, the set $Y$ as $\infty$ or any value.. Therefore the formula for the <span style='color:#fa8231'>PDF using join probability</span> is given as such : 
$$
f_{X}(x) = P\{X = x\} = \sum_{y} f_{x,y}(x, y)
$$
This also works for $y$. But basically $y$ in this <span style='color:#f7b731'>case is all possible values</span> of $y$ and $x$ is a <span style='color:#f7b731'>fixed value</span>.

**Continuous Random Variable :**
$$
F_{X,Y}(x,y) = \int_{-\infty}^{x}\int_{-\infty}^{y}f(s,t)dtds
$$

This uses the [[Double Integral|double integral]] for a multi variable function.

# Covariance
---
The usage of <span style='color:#0fb9b1'>covariance</span> is to measure the <span style='color:#f7b731'>relationship between 2 random variables</span>.

The <span style='color:#0fb9b1'>covariance</span> of $X$ and $Y$ is given as such :
$$
Cov(X,Y) = E[(X - EX)(Y - EY)] = E[XY] - E[X]E[Y] 
$$
**Where :**
- $E[XY]$ is the **joint PDF** of $X$ and $Y$
- $E[X]$ is the **expected value**

Now the <span style='color:#0fb9b1'>correlation coefficient</span> is given as such :
$$
p(X,Y) = \frac{Cov(X,Y)}{\sqrt{Var(X)\times Var(Y)}}
$$
**If :**
- The <span style='color:#fa8231'>value is near 1</span>, then there is a <span style='color:#f7b731'>high positive linearity</span> between $X$ and $Y$
- If the <span style='color:#fa8231'>value is near -1</span>, then there is a <span style='color:#f7b731'>high negative linearity</span> between $X$ and $Y$
- If it <span style='color:#fa8231'>is 0</span>, then there is a <span style='color:#f7b731'>week linearity</span>.

For example if the value of $p(X,Y) = 1$, then it shows that as $X$ increases $Y$ increases. While for negative values, $Y$ will decrease.

Thus, the <span style='color:#fa8231'>range of values</span> for a corelation coefficient is from -1 to 1.
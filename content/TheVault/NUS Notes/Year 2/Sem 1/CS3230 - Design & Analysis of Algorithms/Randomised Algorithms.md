---
title: Randomised Algorithms
Date Created: 2024-09-22
Last Updated: 2025-09-28
tags:
  - CS3230
  - AlgorithmDesign
---

# What are Randomised Algorithms
---
Essentially we are  inside the algorithm.

> [!note] Why Incorporate Randomness?
> When using randomness, the algorithm can be <span style='color:var(--mk-color-green)'>more efficient</span> or <span style='color:var(--mk-color-green)'>simpler</span>.
> 
> But this comes at the cost of having a <span style='color:var(--mk-color-red)'>small propability of error</span>.

Randomised complexity is <b><span style='color:var(--mk-color-yellow)'>different</span></b> from [[Average Case Analysis|average case complexity]]. For **randomised complexity**, we are trying to prove that **for every input**, it will succeed with at least some <span style='color:var(--mk-color-turquoise)'>success probability</span>.
## Success Probability Amplification

Sometimes the <span style='color:var(--mk-color-green)'>success probability</span> of a randomised algorithm can be low, but 1 way to increase the probability is to just <span style='color:var(--mk-color-yellow)'>repeat the algorithm</span>. 

If we want to <span style='color:var(--mk-color-green)'>reduce</span> the <span style='color:var(--mk-color-red)'>error probability</span> by at most $f$ then we will need to repeat the algorithm:
$$
t = \left\lceil\log{\frac{1}{f}}\right\rceil \text{times}
$$
> [!example] Example Using Freivalds' Algorithm
> Since if $AB = C$ then the it will always be correct. But now in the event that $AB \neq C$, by repeating the algorithm, if all outputs are $AB = C$, then $AB = C$, else $AB \neq C$.
> 
> This will improve the succes probability by $f$.

This method can make the <span style='color:var(--mk-color-green)'>error probability very low</span> such that it acts like a normal algorithm.

>A **useful inequality** to remember is that $1 + x \le e^{x}$.
## Types of Randomised Algorithm

There are <span style='color:var(--mk-color-orange)'>2 types</span>:
1) **Las Vegas algorithm**
	> **Output** is <span style='color:var(--mk-color-green)'>always correct</span>, but the <span style='color:var(--mk-color-red)'>time complexity is guarantee only in expectation</span> (*Not always the same*)

2) **Monte Carlo algorithm**
	> Output is <span style='color:var(--mk-color-red)'>correct with some probability</span>, but the <span style='color:var(--mk-color-green)'>time complexity is guarantee</span> with a probability of 1.

But in general the <b><span style='color:var(--mk-color-yellow)'>Las Vegas algorithm is preferred</span></b>, since we can <span style='color:var(--mk-color-yellow)'>use the Markov inequality</span> to **turn a Las Vegas algorithm into a Monte Carlo algorithm**.
<div style="page-break-after: always;"></div>

# Principle of Deferred Decision
---
It states that the probability of an **event happening when considering all the randomness involved** will be the <b><span style='color:var(--mk-color-yellow)'>same</span></b> as the probability of the <span style='color:var(--mk-color-yellow)'>event happening when only one of the choices are random</span>.
$$
Pr[\varepsilon | X = x] \ge p, \forall x \rightarrow Pr[\varepsilon] \ge p
$$
**Where:**
- $X$ is the randomise set
- $x$ is when the value is assigned to one of the values in $X$
# Union Bound
---
Assuming that $\varepsilon$ is a bad event and that $\varepsilon = \varepsilon_{1} \lor \varepsilon_{2} \lor \varepsilon_{3} \lor \dots$, then $Pr[\varepsilon] \le Pr[\varepsilon_{1}] + Pr[\varepsilon_{2}] + \dots + Pr[\varepsilon_{n}]$ .

In other words a **bad event is when one of the possible outcomes is bad**, thus the probability of a bad event is <span style='color:var(--mk-color-yellow)'>less than or equals</span> to of the <span style='color:var(--mk-color-yellow)'>sum of probability of all the bad outcomes</span>.

Thus $Pr[\varepsilon] \le f$ which it will suffice that $Pr[\varepsilon_{i}] \le \frac{f}{n}$. This can be used to **find upper bound probability**.
# Expected Value
---
Given a set $S$ with all possible values with some probability, the expected value can be computed as such:
$$
\Bbb{E}[X] = \sum_{x} x \cdot Pr[X = x]
$$
Essentially we will <span style='color:var(--mk-color-yellow)'>sum all the values</span> of $x \in S$ <span style='color:var(--mk-color-yellow)'>times its probability</span> of it getting **selected**.
## Markov Inequality

Now can we convert an expected variable into a <span style='color:var(--mk-color-yellow)'>concrete variable</span> (*Upper bound*), this is where the <span style='color:var(--mk-color-turquoise)'>Markov inequality </span>comes in and for this to work $X$ our **random variable** <b><mark style='background:var(--mk-color-red)'>cannot be negative</mark></b>.
$$
Pr[X \ge a \cdot \Bbb{E}[X]] \le \frac{1}{a}
$$
**Where:**
- $a \gt 0$ 
- $X$ **must be non negative**

The equation says that the <span style='color:var(--mk-color-yellow)'>probability</span> of $X$ to <span style='color:var(--mk-color-yellow)'>exceed some value</span> of $a$ times its expected value is <span style='color:var(--mk-color-yellow)'>upper bounded</span> by $\frac{1}{a}$.
## Linearity of Expectation

Essentially if $X = A + B$ then $\Bbb{E}[X] = \Bbb{E}[A] + \Bbb{E}[B]$.

Therefore if we can express $X$ to be the sum of a sequence of random variables, then:
$$
\Bbb{E}[X] = \sum^{n}_{i = 1} \Bbb{E}[X_{i}]
$$

<div style="page-break-after: always;"></div>

## Indicator Random variables

If we let $\varepsilon$ to be an event and if the indicator random variable happens ($1_\varepsilon$) can be defined as follows:
$$
1_\varepsilon =
\begin{cases}
1,  & \text{if $\varepsilon$ occures} \\[2ex]
0, & \text{otherwise}
\end{cases}
$$
Then $\Bbb{E}[1_\varepsilon] = Pr[\varepsilon]$ since it is just this $1 \cdot Pr[\varepsilon] + 0 \cdot Pr[\text{otherwise}]$. The <span style='color:var(--mk-color-yellow)'>second term will always be 0</span>.
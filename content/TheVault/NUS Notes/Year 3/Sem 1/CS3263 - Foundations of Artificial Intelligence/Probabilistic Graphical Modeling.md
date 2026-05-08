---
title: Probabilistic Graphical Modeling
Date Created: 2025-09-11
Last Updated: 2025-09-28
tags:
  - CS3263
  - AI
  - Graphs
  - Math/Probability
---
# Uncertainty
---
The **idea** is that sometimes we <b><span style='color:var(--mk-color-red)'>don't have all the facts</span></b> and we want to **answer a question**. This leads to uncertainty and that's where <b><span style='color:var(--mk-color-yellow)'>probability</span></b> will help.

>[!question] Why is there uncertainty?
>- **Ignorance**: Lack of knowledge
>- **Laziness**: Difficult to enumerate everything
>- **Indeterminism or physical randomness**: Events can happen randomly depending on environment
>- **Vagueness**: No concrete definition in languages

Not having all the facts can mean different things, for instance:
- Missing or unavailable
- Unreliable or ambiguous (*measurement issues*)
- Imprecise or inconsistent
- Based on defaults without considering exceptions
- Represent best guesses of experts which can be bias
# Probability Theory
---
First we need to know what is a <b><span style='color:var(--mk-color-turquoise)'>sample space</span></b>, it is denoted by $\Omega$ and it is the <b><span style='color:var(--mk-color-yellow)'>set of possible worlds that are mutually exclusive</span></b>. Then $\omega$ (*little omega*) refers to <b><span style='color:var(--mk-color-yellow)'>one possible world</span></b> in this sample space.

>[!info] Mutually exclusive means that if 1 world exist the others cannot exist at the same time

The probability that an **event** (*proposition*) is true, denoted as $\phi$ is the <b><span style='color:var(--mk-color-yellow)'>sum of probabilities of a set of worlds</span></b> where $\phi$ is <b><span style='color:var(--mk-color-green)'>true for a given world </span></b>.

Mathematically it is:
$$
P(\phi) = \sum  P(\omega) , \text{where} \{\omega \in \phi \}
$$
>[!abstract] Axioms of probability
>1) **Nonnegativity**, it states that the probability for any event must be <b><span style='color:var(--mk-color-yellow)'>greater than or equals to 0</span></b>
>2) **Normalisation**, states that the probability of the <b><span style='color:var(--mk-color-yellow)'>sample space is 1</span></b>
>3) **Additivity**, states that the probability of a **set of mutually exclusive events** is the <b><span style='color:var(--mk-color-yellow)'>sum of the probabilities</span></b>
## Conditional Probability

[[Counting & Probability#Conditional Probability|Conditional probability]] is the probability that an <b><span style='color:var(--mk-color-yellow)'>event occurs given that another event is observed</span></b>.

This can be written as $P(B \vert A) = P(A \land B) / P(A)$. Basically we need A and B to be true given that A is true.

>[!info] When we say $P(A \land B)$ we can denote this as $P(A, B)$

**Alternatively** we can write it as $P(A \land B) = P(B \vert A)  \times P(A) = P(A \vert B) \times P(B)$.

It also follows the rule of probability where everything sums to 1, $P(+ve \vert A) = 1 - P(-ve\vert A)$.

>[!abstract] Chain rule
>We can **repeatedly substitute** using the formula above. For example:
>
>$P(A_{1} \land \dots \land A_{n}) = P(A_{n} \vert A_{1} \land \dots \land A_{n - 1}) \times P(A_{1} \land \dots \land A_{n - 1})$
>
>Then repeat the same process for $P(A_{1} \land \dots \land A_{n - 1})$ until  we are left with $P(A_{1})$.
>
>Same for conditional probabilities, $P(A, B, C \vert D, E) = P(A \vert B, C, D, E) \times P(B \vert C, D, E) \times P(C \vert D, E)$

If we know $P(A \vert B)$ but need to find $P(B \vert A)$, then we can use [[Counting & Probability#Bayes Theorem|Baye's theorem]]. Which just states that $P(A \vert B) = P(B \vert A)P(A) \backslash P(B)$ .

>[!tldr] Law of total probability
>It states that $P(A) = \sum_{i} P(b_{i}) \times P(A \vert b_{i})$

### Marginalisation

Assuming we want to calculate the conditional probability of $P(X \vert Y)$, then by definition we will need to compute $P(X, Y) \backslash P(Y)$. However what if we <b><span style='color:var(--mk-color-red)'>only have P(X, Y, Z)</span></b>?

**Marginalisation** says that we <b><span style='color:var(--mk-color-green)'>can still compute it even with additional variables</span></b>. The formula for $P(X, Y)$ will be $\sum_{i} P(X, Y, Z = z_{i})$, which is the <b><span style='color:var(--mk-color-yellow)'>summation of probabilities for all values of Z</span></b>.

Same goes for $P(Y) = \sum_{i} \sum_{k} P(X = x_{i}, Y, Z = z_{j})$. Essentially for any additional variable we will need to try all possible combinations.

As for **conditional probabilities**, if we want to find $P(X \vert Y) = \sum_{i} P(X , z_{i} \vert Y)$.

>[!fail] Space & computation scales exponentially with the number of extra variables

>[!fail] Hard to specify data and learn from data
# Probabilistic Graphical Modeling
---
**Overview of a Probabilistic Agent**
![[Overview of a Probabilistic Agent.png|center|400]]

The key idea is to **exploit** <b><span style='color:var(--mk-color-turquoise)'>independence</span></b> properties among a large number of variables. And **representing it as a graph**.
<div style="page-break-after: always;"></div>

## Independence

If 2 events are **independent**, then the probability that both events occur is $P(A) \times P(B)$.

>[!warning] Do not confuse with mutually exclusive
><b><span style='color:var(--mk-color-turquoise)'>Mutually exclusive</span></b> means that for 2 events, they <b><span style='color:var(--mk-color-red)'>cannot exist at the same time</span></b>. Meaning if one event happens the other event cannot happen. Thus $P(A \land B) = 0$.
>
>And if **2 mutually exclusive events have positive probability** then they <b><span style='color:var(--mk-color-yellow)'>must be dependent</span></b>.

Given $P(A \vert B)$ and  is <b><span style='color: var(--mk-color-yellow)'>independent of  then we can drop B</span></b> and get $P(A)$.
### Conditional Independence

Given 3 events, $A$, $B$ & $C$. If given $C$, $A$ & $B$ are **conditionally independent** if $P(A \land B \vert C) = P(A \vert C) \times P(B \vert C)$.

Equivalently, $P(A \vert B \land C) = P(A \vert C)$ or $P(B \vert A \land C) = P(B \vert C)$, but this <b><span style='color:var(--mk-color-yellow)'>only holds if A and B are conditionally independent</span></b>.

>[!important] Independence implies conditional independence but not the other way round

Thus if given $C$ and $A$ and $B$ are conditionally independent then we can denote this as $A \perp B \vert C$.

>[!question] Why is finding conditional independence important?
>
>For instance if we have $P(A \vert B)$ is it the same as $P(A \vert B, C)$? If we can prove that given $B$ it makes $A \perp C$ then the **probability is the same** since <b><span style='color: var(--mk-color-yellow)'>adding C will bring no additional information</span></b>.
>
>For conditional probabilities with more variables we can consider the [[Probabilistic Graphical Modeling#Markov Blanket|Markov blanket]].
# Bayesian Networks
---
>[!success] Tries and solves the issues with the direct way of computing conditional probability
>
>For instance if we want to find the $P(A, B, C, D, E)$ (*full joint probability distribution*) we need to specify $2^{5} - 1$ (*1 variable can take on 2 values*) probability values (*minus 1 cause the last probability can be derrived*). But in a Bayesian network we only need 11 (*see the image below*), saving a lot of space.

**Example of a Bayesian network in a graphical form**:
![[Example of a Bayesian Network Graph.png|center|500]]
<div style="page-break-after: always;"></div>

The formula you see is the **product from the chain rule** and is also known as the <b><span style='color: var(--mk-color-turquoise)'>factorised distribution</span></b> of the **Bayesian network**. However you can notice some differences. For instance $P(C \vert L)$, could be $P(C \vert B, F, H, L)$. but based on [[Probabilistic Graphical Modeling#Conditional Independence|conditional independence]]we can reduce it as such.

>[!info] A fully connected Bayesian network is able to represent any distribution

We can <b><span style='color:var(--mk-color-green)'>easily tell from the graph</span></b> that lets say $L$ is true, then we know what $F$, $B$ and $H$ are conditionally independent of $C$. Why because <b><span style='color:var(--mk-color-yellow)'>they are no neighbours to C</span></b>.

>[!note] From the graph you can easily write the conditional probability as shown in the image

To read the tables, lets look at node $B$, essentially if $H$ takes the first value (*row 1*) then the numbers are the probability of $B$ taking values 1 or 2 (*true or false*).

The **edges** are based on <b><span style='color:var(--mk-color-yellow)'>causality knowledge</span></b> of the world.
## Bayesian Network Semantics

We can view this network in 2 ways:
1) **Factorisation** - A compact, <b><span style='color:var(--mk-color-yellow)'>factorised representation</span></b> of a joint probability distribution
2) **Independence-Map** (*I-Map*) - A compact representation of <b><span style='color:var(--mk-color-yellow)'>conditional independence assumptions</span></b> that hold in the joint probability distribution

>[!info] Joint probability distribution
>
>It is just the <b><span style='color:var(--mk-color-yellow)'>probability of 2 or more random variables happening at the same time</span></b> (*some set of assigned values*).
>

>[!note] It can be visualised as a [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs#Directed Acyclic Graph|directed acyclic graph]]
### Bayesian Network Definition

Let $P$ be a joint probability distribution of a set of random variables ($X_{1}, \dots, X_{n}$) in a set of vertices $V$ and $G = (V, E)$ be a DAG, then $B = (G, P)$ <b><span style='color:var(--mk-color-yellow)'>is a Bayesian network if it</span></b> $(G, P$) <b><span style='color:var(--mk-color-yellow)'>satisfies the Markov condition</span></b>.

>[!abstract] Markov condition
>
>1) $P$ <b><span style='color:var(--mk-color-yellow)'>factorises over</span></b> $G$, meaning $P(X_{1}, \dots X_{n}) = \prod^{n}_{i = 1} P(X_{i} \vert PA_{x_{i}})$, where $PA_{x_{i}}$ is the **parent** of the variable $X_{i}$ (*parent of node i*). **This is the factorised distribution of the Bayesian network.** This is just the chain rule $P(A, B) = P(A | B)P(B)$
>2) $G$ encodes the set of <b><span style='color:var(--mk-color-yellow)'>conditional independence assumptions</span></b> for all $X \in V$. This means that $X \perp ND_{x} \vert PA_{x}$, where $ND_{x}$ is the **non-descendance** of $X$. So given A -> B -> C then $C \perp A \vert B$
# D-Separation
---
D-separation is a method to **know** from the Bayesian network **which variables are independent given some which are observed**.

Let $G$ be an independence map or I-map for **a set of conditional independence** $I(P)$, if $I(G) \subseteq I(P)$, where $I(G)$ is the set of [[Probabilistic Graphical Modeling#Bayesian Network Definition|conditional independencies in the graph]].

Here $P$ is the **distribution over a set of variables**.

So any dependencies that $G$ assets <b><span style='color:var(--mk-color-yellow)'>must also hold</span></b> for $P$. $P$ can have additional dependencies that are not in $G$.

So let $X$, $Y$, $Z$ be 3 mutually disjoint subsets of $V$, $X$ & $Y$ are <b><span style='color:var(--mk-color-yellow)'>d-separated </span></b> given $Z$ is denoted as $d-sep(X, Y \vert Z)$.

>[!important] This is true if there is no active trail between any nodes assigned to $X$ and $Y$ given $Z$
>When we say no active trail, it means it must <b><span style='color:var(--mk-color-yellow)'>adhere to all 3 structures</span></b>.
## Independence Structures

If <b><span style='color:var(--mk-color-green)'>there is a trail</span></b> from $X$ to $Y$ given $Z$, then $X$ and $Y$ are <b><span style='color: var(--mk-color-yellow)'>dependent</span></b>, unless the trail is blocked.

If <b><span style='color:var(--mk-color-red)'>there is no trail</span></b>, then $X$ and $Y$ are <b><span style='color:var(--mk-color-yellow)'>conditional independent</span></b>.

>[!info] When a variable is observed, in the graph it means that node is now a blocker/barrier
<div style="page-break-after: always;"></div>

### Casual & Evidential Trail

![[Causal & Evidential Trail Example.png|center|250]]

Also known as a <b><span style='color:var(--mk-color-turquoise)'>linear connection</span></b>.

If $Z$ is **observed** (*denoted by the orange circle*), that means that <b><span style='color:var(--mk-color-red)'>X cannot go to Y</span></b> and thus it is <b><span style='color:var(--mk-color-yellow)'>conditionally independent</span></b>.

>[!note] The image is a causal trail, just flip the direction of the edges for a evidential trail
### Common Cause

![[Common Cause Structure Example.png|center|100]]

Also known as a <b><span style='color:var(--mk-color-turquoise)'>diverging connection</span></b>.

If $Z$ is **observed** (*denoted by the orange circle*), that means that <b><span style='color:var(--mk-color-red)'>X cannot go to Y</span></b> and thus it is <b><span style='color:var(--mk-color-yellow)'>conditionally independent</span></b>.
### Common Effect

![[Common Effect Structure Example.png|center|150]]

Also known as a <b><span style='color:var(--mk-color-turquoise)'>converging connection</span></b>.

It is different that what we observed from the previous 2. If $Z$ is **observed** (*denoted by the green circle*), that means that <b><span style='color:var(--mk-color-green)'>X can go to Y</span></b> and thus it is <b><span style='color:var(--mk-color-yellow)'>dependent</span></b>.

>[!important] If $Z$ or any of its descendants is observed then the path is not blocked causing $X$ & $Y$ to be dependent
## Markov Blanket

A Markov blanket ($M_{x}$) of $X$ is a **set of variables** (*what we observed*) such that $X$ <b><span style='color:var(--mk-color-yellow)'>is conditionally independent of all other variables</span></b>, given $M_{x}$, this can be written as $(\{ X \} \perp V - (M_{x} \cup \{X\}) \vert M_{x})$.

So given a graph this Markov Blanket consist of a set of **in order of**:
1) **Parents** of $X$
2) **Children** of $X$
3) **Parents of the children** of $X$

>[!info] This Markov blanket d-separates a variable from all other variables

>[!important] So essentially by finding a set of variables which makes some variable $X$ conditionally independent, allows us to know that adding any other additional variables not in the set in our conditional probability, it will not affect the probability
>
>So if we know for $X$ the Markov blanket contains $A$ and $B$. Then if we have $P(X \vert A, B, C) = P(X \vert A, B)$ 


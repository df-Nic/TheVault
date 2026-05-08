---
title: Probabilistic Inference & Causal Reasoning
Date Created: 2025-08-17
Last Updated: 2025-09-28
tags:
  - CS3263
  - AI
  - Math/Probability
---
# Bayesian Network Inference 
---
>[!cite] We have covered the [[Probabilistic Graphical Modeling#Bayesian Networks|basics of Bayesian networks]] previously

Inference in is the <b><span style='color: var(--mk-color-yellow)'>calculation of conditional distributions</span></b>, for instance $P(b_{1} \vert a_{1}, f_{2})$. Which is just [[Probabilistic Graphical Modeling#Conditional Probability|conditional probability]].

By calculating the **distribution** we are essentially calculating <b><span style='color: var(--mk-color-turquoise)'>posterior distribution</span></b> (*prior*). For example $P(X \vert Y_{1}, Z_{2})$ we are tying to <b><span style='color: var(--mk-color-yellow)'>compute the probability for all values of X given a set of observed values</span></b>.

Now if we are interested in the **most probable values** then we are finding the <b><span style='color: var(--mk-color-turquoise)'>maximum a posteriori</span></b> (*MAP*) or <b><span style='color: var(--mk-color-turquoise)'>most probable explanation</span></b> (*MAE*).

>[!info] MAP & MAE
>**MAP** is the <b><span style='color: var(--mk-color-yellow)'>largest probability</span></b> of a given posterior distribution ($argmax_{Y} P(Y \vert e)$).  But if you find MAP you can find MAE
>
>**MAE** on the other hand is the <b><span style='color: var(--mk-color-yellow)'>assignment of all variables which gives the largest probability</span></b> in the distribution.

With the **joint probability distribution** we <b><span style='color: var(--mk-color-green)'>can answer all questions</span></b>.

>[!example] Example of marginal probability, conditional distributions & MAP
>Assume we have the **joint probability distribution** of $P(x_{1}, \dots, x_{n})$. It is essentially the <b><span style='color: var(--mk-color-yellow)'>probabilities of all permutation of variables</span></b> $x_{1}$ to $x_{n}$.
>
>**Marginal probability**: $P(X_{1})$, $P(X_{5})$, $P(X_{1}, X_{7})$ and so on
>
>**Conditional distribution** (*predictions*): $P(X_{1} \vert X_{2}, X_{3}, X_{4})$
>
>**MAP**: The max of $P(X_{1} = x_{1}, X_{3} = x_{3} \vert X_{2}, X_{4})$, here we don't know $x_{1}$ and $x_{3}$ which we are trying to find out in MAP
## Inference by Enumeration

When computing the conditional distribution, our first method to approach this is to do <b><span style='color: var(--mk-color-red)'>brute force</span></b> by [[Probabilistic Graphical Modeling#Marginalisation|marginalisation]].

$$
P(X \vert a) = \frac{P(X, a)}{P(a)} = \alpha P(X, a) = \alpha \sum\limits_{y}P(X, a, y)
$$
**Where**:
- $y$ is the set of **all other variables** in the joint distribution that is not in a

So given $P(X_{i} \vert Y)$ After computing the probabilities for all possible values of $X_{i}$ we need to <b><span style='color: var(--mk-color-turquoise)'>normalise</span></b>.

>[!info] Normalising
>It is essentially taking all the computed probabilities and <b><span style='color: var(--mk-color-yellow)'>refitting them into a range between 0 and 1</span></b>.
>
>So take the probability divide it by the sum of all other probabilities.

If you recall the $P(X \vert Y) = P(X, Y) \backslash P(Y)$ our $P(Y)$ is a constant. To <b><span style='color: var(--mk-color-green)'>speed up computation we can ignore</span></b> $P(Y)$ because when we **normalise**, it will **cancel out**.

>[!success] Easy to compute, just need to read of the joint distribution table

>[!fail] Brute forcing is not efficient when the number of variables increase
>
>By doing the normal brute force method we will need to sum over $\color{red}{k^{n}}$ where:
>- $k$ is the number of possible values for a variable
>- $n$ is the number of variables
## Variable Elimination

The key idea to speed things up is to <b><span style='color: var(--mk-color-yellow)'>remove the probabilities which does not involve the summation</span></b>.

![[Example of Variable Elimination.png|center|300]]

>[!important] When marginalising over some variables, the order of submission does not matter for correctness

Lets look at the **red part**:
![[How a Variable Gets Eliminated.png|center]]

We are essentially <b><span style='color: var(--mk-color-yellow)'>summing up all the probability of a particular value</span></b> of $b$ for all values of $a$ (*marginalisation*). Which will result in a function of b denoted as $\phi_{1}(b)$, this is known as a <b><span style='color: var(--mk-color-turquoise)'>factor</span></b>.

Here we do 2 steps:
1) **Multiplication** is called <b><span style='color: var(--mk-color-turquoise)'>factor multiplication</span></b>
2) **Summation** is called <b><span style='color: var(--mk-color-turquoise)'>factor marginalisation</span></b>

We will then **repeat the same process** for the remining submissions but we replace it with $\phi$. For example after step 1 we will get $\dots \sum\limits_{b} P(c, \vert b)  \times \phi_{1}(b)$

>[!important] We do not eliminate the variables in our query, eliminate everything else but those

Sometimes you will see $\sum_{c} \phi_{c} (a, b, c)$. This is the <b><span style='color: var(--mk-color-yellow)'>domain or the scope</span></b> of the factor ($\phi$). Which is the **same** as writing the sum of all the conditional probabilities with variable $c$.

The time complexity is still $k^{n}$ but now it is only $2^{2}$, and if we repeat this we will get $a \times k^{n}$ where: 
- $a$ is the number of times we eliminate a variable
- $k$ is the number of values that the variable can have
- $n$ is the number of variables during an elimination of a factor

>[!important] The elimination ordering will determine the time & space complexity
>$n$ is <b><span style='color: var(--mk-color-yellow)'>bounded by the number of unique variables in a factor</span></b>. So if we are eliminating $A$ and we have $P(B \vert A)$, $P(A)$, $P(y+ \vert Z, A)$, there are 4 variables for a total of $2 \times 2 \times 2 \times 1 = 8$ entries (*pre-submation*).
>
>Our **output size** will be $2 \times 2 \times 1 = 4 entries$, because we eliminated $A$ (*post-summation*).
>
>So take note of their domain, if its $a+$ where the value is determined the domain size is 1.
>
>We can <b><span style='color: var(--mk-color-green)'>greedily select the factor</span></b> with the smallest number of variables, it works well but <b><span style='color: var(--mk-color-red)'>not always optimal </span></b>.

>[!success] It is generally faster if the graph structure helps since it is a form of dynamic programming with memoization

**Algorithm for variable elimination**:
```cpp
string  eliminationAsk (X, e, bn) {
	// Here X is the query, e is the observed values for variables E, bn is the bayesian network
	factors = [];
	for (V : order(vars)) { // Order vars just set some ordering for the elimination except X
		factors = [makeFactor(V, e)] + factors;
		if (V is a hidden) { // Hidden means not observed (in marginalisation you add the variable in)
			factors = sumOut(V, factors); // Do the prod and sum for V (basically marginalisation)
			// This will remove all the factors which includes V
		}
	}
	return normalize(pointWiseProduct(factors)) // This final factors does not sum to one
}
```

>[!example] Example of the variable elimination algorithm
>Lets say we have variables A, B , C, D where B and C is dependent on A and D is dependent on C. Our query is $P(B \vert A = True)$
>1) $P(B \vert A) = \alpha P(A, B) = \alpha \sum_{C} \sum_{D} P(A, B, C, D)$ (*Marginalisation step*)
>2) From our Bayesian network we get $\alpha  P(A, B, C, D) = \alpha P(A)P(B \vert A) \sum_{C} P(C \vert A) \sum_{D}P(D \vert C)$
>3) Assuming our ordering is A, B, D then C
>4) For steps A & B we only do `makeFactors` which gives us $\alpha \phi_{A}(a) \phi_{B}(b, a) \sum_{C} P(C \vert A) \sum_{D}P(D \vert C)$
>5) For D & C, they are hidden variables so we do the `sumOut` as well. So lets start with D we will get $\alpha \phi_{A}(a) \phi_{B}(b, a) \sum_{C} P(C \vert A) \sum_{D} \phi_{D}(D, C)$. So this is the `makeFactors` part. Then we get $\alpha \phi_{A}(a) \phi_{B}(b, a) \sum_{C} P(C \vert A) \phi_{1}(C)$ this is the `sumOut` portion
>6) Then we do the same for C we will get $\alpha \phi_{A}(a) \phi_{B}(b, a) \phi_{2}(A)$ Where $\phi_{2}(A) = \sum_{C} \phi_{C}(C, A)\phi_{1}(C)$ after `makeFactors`
>7) Lastly we normalise, which is just take the final table and taking the probability of B = true or false divide by the sum of B = true and B = false
# Causal Reasoning
---
>[!warning] High probability does not mean causality

Given a Bayesian network, $P(Smoke, Fire) = P(Smoke \vert Fire) P(Fire) = P(Fire \vert Smoke)P(Smoke)$. However we know that fire causes smoke and not the other way round.

So far in our Bayesian networks we <b><span style='color: var(--mk-color-yellow)'>keep the node ordering compatible with the direction of causation</span></b>. This make it <b><span style='color: var(--mk-color-green)'>easier to assess conditional probabilities</span></b>, compact network structures and causal analysis.

But if we **want to make causal assumptions** then we need to have a <b><span style='color: var(--mk-color-turquoise)'>causal Bayesian network</span></b>.

>[!abstract] Causal Bayesian network
>A restricted class of Bayesian networks that <b><span style='color: var(--mk-color-red)'>forbids all but causally compatible orderings</span></b>.
## Structural Equation

A structural equation <b><span style='color: var(--mk-color-yellow)'>describes a causal relation among variables</span></b> in a causal network.

It has the following form, $X_{i} = f_{i}(OtherVariables)$. It means that for some causal assumption ($X_{i}$), there is a deterministic function ($f_{i}$) of <b><span style='color: var(--mk-color-yellow)'>all other variables it depends on and unobservable independent noise</span></b>. We denote this noise as $U_{i}$.

>[!example] Example of $X_{i}$
>Assuming in our causal Bayesian network we have rain is caused by the sky being cloudy.
>
>So $X_{i} = rain = f_{rain}(cloudy, U_{rain})$. As for cloudy it is just $cloudy = f_{cloudy}(U_{cloudy})$ since there are no "parents".

The $U$ variables represent <b><span style='color: var(--mk-color-turquoise)'>unmodeled variables</span></b> (*error terms or disturbances*). Thus it is essentially our <b><span style='color: var(--mk-color-yellow)'>Bayesian network but with noise</span></b> for each variable.

>[!important] With a set of structural equations we will have a causal network

>[!success] With a system of structural equations we can predict interventions
>
>Interventions are things which **you control** and how it affects the whole system.
## Intervention Or Do-Operator

We denote a **intervention** as $do(variable = value)$. So $Variable = f_{variable}(Parents_{variable}, U_{variable})$ will just be $Variable = value$ after intervention. 

>[!question] What is an intervention
>Lets say we have 2 variables Hot and on air con. If it is hot the air con will be on and thus is dependent on it. **An intervention** would be to turn on the air con <b><span style='color: var(--mk-color-yellow)'>regardless</span></b> of whether it is hot or not.

<b><span style='color: var(--mk-color-yellow)'>Conditional distribution is different from interventional distribution</span></b>. By adding this intervention, we are essentially removing the dependencies of the variable since we force it to be some value (*in a graphical standpoint the edges from the parents will be removed*). 

Thus it does not matter what values the dependencies are since we force it to be some value.

**Example of a do-operator**:
![[Do-Operator Effect Example.png|center]]

In a **general casual network** (*left*), $P(x_{1}, \dots x_{n}) = \prod_{i = 1}^{n} P(x_{i} \vert parents(X_{i}))$ (*This is just based on the Bayesian network graph*).

However **with a do-operator**, lets say $X_{j} = x_{jk}$, then our new joint distribution **post-intervention** will be the following:
$$
P_{x_{jk}}(x_{1}, \dots x_{n})  = 
\begin{cases}
\prod^{n}_{i = 1 \text{ \& }  i \neq j}  P(x_{i} \vert Parents(x_{i})) = \frac{P(x_{1}, \dots, x_{n})}{P(x_{j}) \vert Parents(x_{j})} & \text{if $x_{j = x_{jk}}$} \\
0 & \text{if $x_{j \neq x_{jk}}$}
\end{cases}
$$
Where:
- $n$ is the number of variables
- $P$ is the original joint probability distribution pre-intervention
- $P_{x_{jk}}$ is the joint probability distribution after the intervention of variable $x_{j} = k$

The in the pre-intervention, the <b><span style='color: var(--mk-color-yellow)'>event can either happen or not</span></b>. And if we intervene and it doesn't then the probability will be 0, making everything to be 0 ($x \neq x_{k}$).

So linking this with [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Probabilistic Graphical Modeling.md#Marginalisation|marginalisation]], lets say we want to compute $P(Y \vert X = x_{k})$ We can marginalise $Z$ our to get $\sum_{Z} P(Z) \times P(Y \vert Z, X = x_{k})$.

We **do not need to divide by** $P(X)$ because now $X$ is <b><span style='color: var(--mk-color-yellow)'>no longer random</span></b> thus the probability is just 1.

>[!note] If our conditional probability has been intervein then replace all variables with the intervention
>For example $P(z) \times P(y \vert z, x_{k})$. But we know that $x$ is being intervened so we can replace all $x$ with $x_{k}$.

>[!warning] Simpson's paradox
> A statistical phenomenon where a trend that appears in several different groups of data reverses or <b><span style='color: var(--mk-color-red)'>disappears when the groups are combined</span></b>.


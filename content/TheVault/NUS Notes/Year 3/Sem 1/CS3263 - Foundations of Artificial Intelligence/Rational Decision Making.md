---
title: Rational Decision Making
Date Created: 2025-10-11
Last Updated: 2025-10-11
tags:
  - CS3263
  - AI/DecisionMaking
---
# Utility Theory
---
So what does it mean to make a rational decision? Lets look from it in a **axiomatic** approach.

When **stating a preference** between 2 outcomes, there can be 3 possible outcomes:
1) A person prefers option A over option B ($A \succ B$)
2) A person is indifference (*no preference*) between option A & option B ($A \sim B$)
3) A person prefers option A over option B or is indifferent ($A \succsim B$)
## Axioms For Preferences

Here are some rules which holds in order to agents to make rational decisions.

1) **Orderability or Completeness**
Given any 2 outcomes or choices <b><span style='color: #F0E68C'>only one of the 3 possible outcomes can be true</span></b> at that time.

So only **ONE** of $(A \succ B)$ or $(A \sim B)$ or $(A \succsim B)$ can be true.

2) **Transitivity**
Given that a person <b><span style='color: #F0E68C'>prefers A to B and B to C then the person must prefer A to C</span></b>. This is the same for in different ($\sim$).

$$
(A \succ B) \land (B \succ C) \implies A \succ C
$$
>[!warning] If this does not hold then we will enter a cycle
>For example A is chosen over B but C is chosen over A and B is chosen over C which brings us back to A, thus the <b><span style='color: var(--mk-color-red)'>agent can never decide</span></b>.
### Consequences of Axioms For Preferences

And because of transitivity, there is a function $U$ such that for any 2 outcomes $U(A) \gt U(B) \iff A \succ B$ and $U(A) = U(B) \iff A \sim B$.

Here $U$ is a **utility function** which returns us the utility value (*larger values are more preferred*).

>[!note] We can think of $U$ as a function which plots preferences on the number line
>
>Thus there is a [[Year 1/Sem 1/CS1231S - Discrete Structures/Relations.md#Total Order|total ordering]] of the options.

The function $U$ is <b><span style='color: #F0E68C'>not unique</span></b>, we can map any option to a utility value as long as it is a <b><span style='color: #F0E68C'>monotonically increasing transformation</span></b>.
## Lotteries

Most of the time the outcomes or **choices are uncertain and will have some sort of probability**.

A <b><span style='color: #B0E0E6'>lottery</span></b> is a <b><span style='color: #F0E68C'>list of outcomes which occur with probabilities</span></b> denoted as $L = [p_1 , S_1 ; p_2 , S_2; \dots p_n, S_n]$. Where $S$ is the outcome & $p$ is the probability.
### Axioms From Lotteries

Now with lotteries there is now **2 more axioms** which are:
<div style="page-break-after: always;"></div>

3) **Continuity**
If $B$ is between $A$ and $C$ in preference, there must be a $p$ such that the <b><span style='color: #F0E68C'>agent is indifferent</span></b> to getting $A$ with probability $p$ and $B$ with probability of $(1 - P)$.

$$
A \succ B \succ C \implies \exists p [p, A; 1 - p, C] \sim B
$$

In simple terms, there is some probability $p$ where the <b><span style='color: #F0E68C'>preference of you choosing the lottery is the same as choosing the safer option</span></b> $B$ (*either risk it to get A or take B*).

>[!example] Example of continuity
>For example, if we have 3 choices of getting 1 million dollars, 0 dollars or failing the exam then there is some $p$ where taking the lottery of 1 million or failing is indifferent from just winning $0.

4) **Substitutability**
If an agent is indifferent between two lotteries $A$ & $B$, then by introducing a lottery $C$ the agent is <b><span style='color: #F0E68C'>indifferent to two complex lotteries that are the same</span></b>, except B is substituted for A.

$$
A \sim B \implies [p, A; 1 - p, C] \sim [p, B; 1- p, C]
$$
>[!note] This also holds if $\succ$ is substituted for $\sim$ 

#### Consequences of Axioms For Lotteries

From the 2 axioms, the following properties are implied.

1) **Monotonicity**
Suppose we have 2 lotteries with the same outcomes $A$ and $B$. If an **agent prefers A** then it <b><span style='color: #F0E68C'>must have a higher probability</span></b> than $B$.

Let $p$ and $q$ be some probability value, then:
$$
A \succ B \implies ((p \gt q) \iff [p, A; 1 - p, B] \succ [q,A; 1 - q, B])
$$
2) **Decomposability**
<b><span style='color: #F0E68C'>Compounded lotteries can be reduced to simpler ones</span></b> using the laws of probability.

$$
[p, A; 1 - p, [q, B; 1 - q, C]] \sim [p, A; (1 - p)q, B; (1 - p)(1 - q), C]
$$

**Visualisation of decomposability**:
![[Decomposability Visualisation.png|center|200]]
### Von Neumann & Morgenstern Utility Theorem

With the **existence of the utility function**, between 2 lotteries if $U(A) \gt U(B) \iff A \succ B$ this is the same if they are indifferent.

So how do we calculate the utility value of a lottery, well since there are probabilities we can just computed the [[Year 1/Sem 1/CS1231S - Discrete Structures/Counting & Probability.md#Expected Value|expected value]], this is known as the **expected utility of a lottery**.

$$
U([p_1, S_1; \dots ; p_n, S_n]) = \sum_i p_iU(S_i)
$$
To simplify things this is just the <b><span style='color: #F0E68C'>summation of the probability times the utility of that outcome</span></b>.

>[!info] Principle of maximum expected utility
>An agent is rational if they choose an action that <b><span style='color: #F0E68C'>maximises</span></b> the expected utility.

>[!important] With probabilities, the utility representation is uniquely determined up to multiplication of a positive constant and a addition of a scalar
>
>Essentially when dealing with probabilities our <b><span style='color: #F0E68C'>transformation of one utility function to another</span></b> is at most $U'(S) = \alpha U(S) + b$ where $a \gt 0$.
## Preference Elicitation

Now how do we get these utility functions? <b><span style='color: var(--mk-color-red)'>Not everyone will have the same utility</span></b>. One may prefer this outcome over another person.

One way is to just **ask the person about their utility** and based on their responses a utility function is created, this is called <b><span style='color: #F0E68C'>preference elicitation</span></b>.

So how can we do this:
1) Fix 2 outcomes to establish a scale $u_\perp = 0$ to be the <b><span style='color: var(--mk-color-red)'>worst possible outcome</span></b> and $u_\top = 1$ to be the <b><span style='color: #98FB98'>best possible outcome</span></b>
2) Then we access the utility for outcome $S$ by choosing between $S$ and the lottery $[p, u_\perp; 1 - p , u_\top]$
3) Then <b><span style='color: #F0E68C'>adjust the probability until they are indifferent</span></b>

>[!note] The value $p$ will be the utility values for outcome $S$
## Human Irrationality

A **descriptive theory** describes <b><span style='color: #F0E68C'>how humans actually act</span></b>. And with this we can tell if a person is acting irrationally (*when the axioms of utility theory contradict*).

**Decision theory** on the other hand <b><span style='color: #F0E68C'>describe how a rational agent should act</span></b> and is a **normative theory**.

>[!info] Allias paradox
>If we have the following choices of lotteries between 1 and 2 and between 3 and 4 as:
>1) 80% chance of winning $4000
>2) 100% chance of winning $3000
>3) 20% chance of winning $4000
>4) 25% chance of winning $3000
>   
> People <b><span style='color: #F0E68C'>tend to take a guarantee outcome</span></b> with a lower EMV and they will <b><span style='color: #F0E68C'>pick 3 over 4</span></b> (*taking higher EMV*).

We can actually prove that <b><span style='color: var(--mk-color-red)'>there are no utility functions</span></b> for the Allias paradox, using normative analysis. Assuming that $U(\$0) = 0$:
1) The first lottery we get $0.8 \times U(\$4000) \lt U(\$3000)$ using the expected utility formula
2) Then second lottery we get $0.2 \times U(\$4000) \gt 0.25 \times U(\$3000)$
3) If we take the 2nd inequality and times 4, we will get $0.8 \times U(\$4000) \gt U(\$3000)$ 
4) And this <b><span style='color: var(--mk-color-red)'>contradicts the the first inequality</span></b>

For a human the utility of money is the proportional to the log of the amount.
<div style="page-break-after: always;"></div>

>[!info] Certainty effect
>Kahneman and Tversky argue that <b><span style='color: #F0E68C'>people are strongly attracted to gains that are certain</span></b>.
>
>Why is this so there are some possible reasons:
>- Reduce computational burden
>- Do not trust probabilities and will go for the sure thing
>- People might experience regret if they gambled and lost

>[!abstract] Other scenarios where people act irrational
>- **Ambiguity aversion**: People <b><span style='color: #F0E68C'>prefer known probabilities</span></b> to unknown ones
>- **Framing effect**: The exact working of choices has a big impact
>- **Anchoring effect**: People <b><span style='color: #F0E68C'>make utility judgements to absolute ones</span></b> because they rely too much on initial information
# Representing & Solving Decision Problems
---
## Decision Tree

![[Decision Tree Example.png|center|500]]

When ever there is a fork (*arcs*) it denotes a **decision alternative or chance outcomes**, where:
- **Squares** denotes that only <b><span style='color: #F0E68C'>one option can be chosen</span></b>, these are known as <b><span style='color: #B0E0E6'>decision nodes</span></b>.
- **Circles** denotes a <b><span style='color: #B0E0E6'>chance node</span></b> where it has a set of mutually exclusive and collectively exhaustive outcomes. Basically there is <b><span style='color: #F0E68C'>some probability that this outcome happens</span></b>

Note that <b><span style='color: #F0E68C'>circles down the tree represent conditional probability</span></b>. So for example solar power -> failure -> success, this $0.8 = P(success \vert failure)$

A fully drawn decision tree will <b><span style='color: #F0E68C'>represent all possible paths through time</span></b>. And time flows from left to right.

At the end the **triangles** (*at the most right*) us known as the <b><span style='color: #B0E0E6'>utility node</span></b> (*or terminal node*), it represents the <b><span style='color: #F0E68C'>conditional utility associated with the path</span></b> of action-alternative-chance-outcome combinations.
<div style="page-break-after: always;"></div>

### Solving A Decision Tree

![[Solving A Decision Tree Example.png|center|400]]

For **decision nodes** we will <b><span style='color: #F0E68C'>take the maximum utility between all decisions</span></b> so in our example it will be do not invest (*this decision node has a utility of 0.1 now*).

For **chance nodes** we will <b><span style='color: #F0E68C'>compute the expected utility</span></b> based on the possible outcomes. For example if we take the investment branch, $EU(Invest) = 0.2 \times 10 + -0.8 \times -6 = -2.8$.

>[!note] An easier way to solve this is by rolling or folding back the tree
>
>Essentially just <b><span style='color: #F0E68C'>begin at the end points</span></b> of the branches (*far right*) then work your way to the left.
## Influence Diagram / Decision Network

Sometimes our <b><span style='color: var(--mk-color-red)'>decision tree might get too big</span></b> and **decision networks** is a <b><span style='color: #98FB98'>more compact</span></b> solution (*like our [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Probabilistic Graphical Modeling.md#Bayesian Networks|Bayesian networks]]*).

![[Decision Network Example.png|center|350]]

A decision network must be a [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs.md#Directed Acyclic Graph|directed acyclic graph]] (*DAG*), where a **rectangle** is a <b><span style='color: #F0E68C'>set of possible decisions</span></b>.

Then the **ovals** are <b><span style='color: #F0E68C'>associated with the conditional distribution</span></b> of the variable given its parents.

Then the **diamonds** are the <b><span style='color: #F0E68C'>utility nodes</span></b>. They have no children and is associated with the utility function of its parents.

With this graph we can also **model dependencies**, for the example given above a "New unit decision" is dependent on the "decision of the exploration tool" and the "outcome of the initial design".
### Solving A Decision Network

We can **transform** the decision network into a <b><span style='color: #F0E68C'>decision tree</span></b>. Recall that a decision network is a DAG so we can use [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs.md#Kahn's Algorithm|topological sort]] to get the nodes in some ordering.

So the parent nodes will be to the left then the children nodes will be to the right.

>[!success] There are faster ways through variable elimination
> However it is more complex than the [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Probabilistic Inference & Causal Reasoning.md#Variable Elimination|variable elimination algorithm for Bayesian networks]]. 


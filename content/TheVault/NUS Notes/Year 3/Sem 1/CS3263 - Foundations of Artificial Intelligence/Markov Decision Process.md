---
title: Markov Decision Process
Date Created: 2025-10-18
Last Updated: 2025-10-31
tags:
  - CS3263
---
# Introduction to Markov Decision Process
---
A <b>MDP</b>, is a type of <b><span style='color: #87CEEB'>sequential decision model</span></b>. Essentially the **utility** of the agent depends on the <b><span style='color: #F0E68C'>sequence of decisions made</span></b>.

There are other decision models as well such as:
- Partially observable Markov decision process (*POMDP*)
- [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Reinforcement Learning.md|Reinforcement learning]]

**Example of a sequential decision model**:
![[Sequential Decision Model Example.png|center]]

To move to a new state at time $t + 1$, it needs an:
- **Action** at time $t$, denoted by the <b><span style='color: #FFE4B5'>yellow boxes</span></b>
- The **state** at time $t$, denoted by the <b><span style='color: #98FB98'>green ovals</span></b>

At <b><span style='color: #F0E68C'>each state there is a reward or utility</span></b> which is denoted by the <b><span style='color: #87CEEB'>blue triangle</span></b>. And sometimes the <b><span style='color: #F0E68C'>state might not be visible but you might get some observation</span></b> denoted by the <b><span style='color: #E6E6FA'>grey ovals</span></b>.

>[!note] Because of reward and observations, in incorporates preference, uncertainty & sensing

>[!example] Example of a unobservable state
>For instance if the state is the location of some object, but instead of the actual location you might get a GPS location which can be noisy.

These problems can be either:
1) **Myopic**: Only considers the current situation and maximising the utility
2) **Non-myopic**: Maximises immediate and also future expected rewards
## Model Formulation

In a MDP it consist of a few components:
- States
- Actions
- Transition function
- Reward function
- Discount factor

![[MDP Model Example.png|center|300]]

Lets use this **fully observable example** to illustrate the different components.

1) **States**
For our **states** ($S$), they are <b><span style='color: #F0E68C'>how we model the world</span></b>. In our example it is the grid positions (*excluding the blue box*).

2) **Actions**
The **actions** ($A$) are <b><span style='color: #F0E68C'>what the agent can do at a given state</span></b>. In our example it can be to move either up, down, left or right.

3) **Transition function**
The **transition function** is the <b><span style='color: #F0E68C'>probability of moving from one state to another given an action</span></b>. It is denoted as $P(s' \vert s, a)$ or $P(s, a, s')$.

Why probability? It is because our <b><span style='color: #F0E68C'>actions might be stochastic</span></b>, meaning there is some probability that it might succeed or not. Obviously **we can also have deterministic actions**.

In our example, there is a probability of 0.8 that it goes in the right direction and 0.1 chance of going either right or left of the given action. Just not if it hits a wall it will remain in the same state.

>[!important] This transition function must follow the Markov property
>Which states that $P(s' \vert s_{t}, a_{t}, a_{t - 1}, \dots) = P(s' \vert s_{t}, a_{t})$.
>
>It means that the **probability** of moving to another state <b><span style='color: #F0E68C'>only depends on the current state</span></b> and <b><span style='color: var(--mk-color-red)'>not the history of the earlier states</span></b>.
>
>But to model this in the real world problems is **just an assumption and it is all about domain knowledge**.

4) **Reward function**
The **reward function** states <b><span style='color: #F0E68C'>how preferred it is</span></b> to be in a:
- Certain state $R(s)$
- To take a certain action $R(s, a)$
- To take a certain action and reach this next state $R(s, a, s')$

This is defined as the numbers you see in the example in each grid (*this is the reward for being at that state*).

>[!fail] It is hard to construct reward functions
>Especially with multiple attributes, there <b><span style='color: #F0E68C'>needs to be a consideration between risk and reward</span></b>. 
>
>And if done wrongly it can lead to problems or undesired outcomes.

5) **Discount factor**
And lastly a **discount factor** ($\gamma$) which has a value of ranges between 0 to 1 (*used in infinite horizon*).

Discounting <b><span style='color: #98FB98'>leads to a well defined solutions</span></b> by bounding the penalty an agent can incur. 

A **large** discount factor means that <b><span style='color: #F0E68C'>immediate actions is preferred over making more long term actions</span></b> and vice versa for a smaller discount factor.

So with our model we can define a <b><span style='color: #B0E0E6'>policy</span></b> which is our <b><span style='color: #F0E68C'>solution</span></b>, which is essentially what is the best action to take. It is denoted as $\pi: S \rightarrow A$.

>[!info] A solution involves carefully balancing risk and reward
## MDP Policies

Given a policy (*solution*), we want to <b><span style='color: #F0E68C'>know how good this solution is</span></b>. This is known as the <b><span style='color: #B0E0E6'>quality</span></b> of the policy $\pi$.

The **quality of a policy** is <b><span style='color: #F0E68C'>measured by the expected utility</span></b> of possible state sequences generated by the policy.

Here <b><span style='color: #B0E0E6'>utility of a sequence</span></b> is just the <b><span style='color: #F0E68C'>sum of all the rewards</span></b> over this sequence.

>[!info] Optimal policy
>It is denoted as $\pi^{*}$ and it is the policy that <b><span style='color: #98FB98'>generated the highest expected utility</span></b>.
>
>And it is <b><span style='color: var(--mk-color-red)'>not unique</span></b>.

So an MDP agent will take this policy and then since it is a **function**, it will **input the current state and get an action** to do ($a = \pi(s)$).

If this **policy is optimal** then it <b><span style='color: #F0E68C'>represents the agent function explicitly</span></b> (*how it should behave*).

>[!note] Depending on the reward function we might get different optimal policies.
>
>![[Examples of Different Policies.png|center|450]]

We also need to know the **type of problem**.
### Finite Horizon

**Finite horizon**, there is a fixed time to terminate

>[!note] For an optimal action in a given state can change over time
>
>Why this is because we have a time limit, thus we <b><span style='color: #F0E68C'>want to maximise what to do within this time</span></b>.
>
>A optimal policy in this case is known as a <b><span style='color: #B0E0E6'>nonstationary optimal policy</span></b> ($\pi_{t}^{*}$), as it <b><span style='color: #F0E68C'>depends on time and the state</span></b>.
### Infinite Horizon

**Infinite horizon**, which can execute forever

>[!note] Will always behave the same regardless of time
>
>Unlike finite horizon, there is <b><span style='color: #F0E68C'>no deadline</span></b> so it will just make the best possible move without having to care that it is running out of time.
>
>A optimal policy in this case is known as a <b><span style='color: #B0E0E6'>stationary optimal policy</span></b> ($\pi^{*}$), as it <b><span style='color: #F0E68C'>only depends the state</span></b>.
#### Additive Discounted Rewards

The main problem is that we have to <b><span style='color: var(--mk-color-red)'>deal with infinities</span></b> (*sum to infinity is infinity or we take an infinite number of horizons and never stop*). What we can do is to <b><span style='color: #F0E68C'>use the discount rewards</span></b> ($\gamma$).

>[!info] This discount must to be strictly between 0 and 1

So our utility will be $R(s_{0}, a_{0}, s_{1}) + \gamma R(s_{1}, a_{1}, s_{2}) + \gamma^{2}  R(s_{2}, a_{2}, s_{3}) + \gamma^{3}R(s_{3}, a_{3}, s_{4}) + \dots$ and so on.

Notice that the <b><span style='color: #F0E68C'>later values as it reaches infinity it will become smaller</span></b>. So discounted rewards with $\gamma \lt 1$ and rewards bounded by $\pm R_{max}$, the <b><span style='color: #F0E68C'>utility will always be finite</span></b> based on the [[Year 1/Sem 1/MA1521 - Calculus for Computing/Sequences & Series.md#Geometric Series|geometric series]].

In a mathematical formula:
$$
\sum^{\infty}_{t = 0} \gamma^{t} R(s_{t}, a_{t}, s_{t + 1}) \le \sum^{\infty}_{t = 0} \gamma^{t}R_{max} = \frac{R_{max}}{1 - \gamma}
$$
Where:
- $R_{max}$ is the largest reward you can have at any step
## Utility of State & Optimal Policy

So we know that the **utility of sequence** (*return*) is the sum of the discounted rewards obtained during the sequence.

A <b><span style='color: #B0E0E6'>utility of state</span></b> (*value of state or value function*) defined as $V(s)$ is the <b><span style='color: #F0E68C'>expected value of executing the optimal policy</span></b> of from that state <b><span style='color: #F0E68C'>given the immediate and future rewards</span></b>.

$$
U(s) = V(s) =  max_{a \in A(s)} \sum_{s'} P(s' \vert s, a) [R(s, a, s') + \gamma U(s')]
$$
The formula above is also known as the **Bellman Optimality Equation** and it is saying that maximum (*best action*) of the expected value of all possible next states and the future rewards

>[!info] If you can see the function is a recursive function

This leads us to the **optimal policy** ($\pi^{*}$) which <b><span style='color: #98FB98'>returns the action that maximises</span></b> $V(s)$.

$$
\pi^{*}=  argmax_{a \in A(s)} \sum_{s'} P(s' \vert s, a) [R(s, a, s') + \gamma U(s')]
$$

>[!question] What if we were to use the reward function of just bring at state state?
>
>See that $V(s)$ uses $R(s, a, s')$. If were were to use $R(s)$ then the <b><span style='color: #98FB98'>formula will be simpler</span></b>.
>
>This will just be:
>$$
>U(s) = V(s) = R(s) + \gamma \ max_{a \in A(s)} \sum_{s'}P(s' \vert s, a) U(s')
>$$
>
>Same for $R(s, a)$
>$$
>U(s) = V(s) =\ max_{a \in A(s)}  [R(s, a) + \gamma \sum_{s'}P(s' \vert s, a) U(s')]
>$$

>[!note] The bellman equation always give a unique solution
### Q-Functions

This is known as a <b><span style='color: #B0E0E6'>action utility function</span></b>. It tells us how <b><span style='color: #F0E68C'>good is it to be in a particular state and take a particular action</span></b> ($Q(s, a)$).

It is related to our utility of state where $U(s) = V(s) = max_{a} Q(s, a)$ and for our optimal policy, it will be $\pi^{*}(s) = argmax_{a} Q(s, a)$.

This can also be linked to the bellman equation:
$$
Q(s, a) =  \sum_{s'} P(s' \vert s, a) [R(s, a, s') + \gamma max_{a'}Q(s', a')]
$$
<div style="page-break-after: always;"></div>

# Solving MDP
---
## Value Iteration

This is a **fixed point method**, where we use the <b><span style='color: #F0E68C'>utility at timestamp i to get the utility at timestamp i + 1</span></b>.

>[!info] Fixed point method
>It is a iterative algorithm which approximates the solution by applying the function until it converges (*the value doesn't change*).

Thus we have $\vert S \vert$ nonlinear equations (*because we are taking the max so it cannot be a linear system*) and $\vert S \vert$ unknowns (*all the utility of states*).

>[!success] It is guarantee to reach an equilibrium through convergence
> Basically it will always converge. This is because it will terminate when it yields little to no change in utility per step.

>[!success] The final utility values are unique solutions
>When using the Bellman equation, no matter how we initialise the initial utility, <b><span style='color: #F0E68C'>the final converged utility values will be the same</span></b>.

>[!success] After convergence, the policy will be optimal
>**In practice** the policy at $\pi_{i}$ will become <b><span style='color: #F0E68C'>optimal long before convergence</span></b>.

**Value Iteration Algorithm Pseudocode**
```cpp
// it will return a function, and takes in a mdp and epsilon a terminating condition
function value_iteration(mdp, epsilon) {
	// We can initilise U to be 0 and U` is U prime
	table U, U` = "2 tables for the utility of all states at timestamp i and i + 1";

	while (true) {
		U = U`;
		delta = 0;
		for (state s : S) {
			// Here is the bellman equation where we take the max of all actions
			U`[s] = max(QValue(mdp, s, a, U));
			if (U`[s] - U[s] > delta) {
				delta = U`[s] - U[s];
			}
		}
		// When our update is too small then terminate
		if (delta <= epsilon(1 - gamma) / gamma) {
			break;
		}
	}
	return U;
}
```
<div style="page-break-after: always;"></div>

**A visual example with the state shown earlier**:
![[Value Iteration Algorithm Example.png|center|550]]
## Policy Iteration

Essentially we begin with some random initial policy (*might be lucky and is already optimal*), which we denote as $\pi_{0}$.

Afterwards we will **iterate between 2 actions**:
1) Policy evaluation
2) Policy improvement

<b><span style='color: #F0E68C'>Policy iteration is one of a few special cases of generalised policy iteration</span></b> (*also value iteration & asynchronous policy iteration*), which essentially just takes the utility based on the policy and update the policy with respect to the utility function

>[!note] After many iterations $\pi_{i}$ will eventually converge to give the optimal policy
>There is a finite number of variables, there is a finite number of policies, thus it <b><span style='color: #F0E68C'>will terminate</span></b>.
>
>This means that $U$ will be a **fixed point in the bellman update**, thus it is a solution meaning it <b><span style='color: #98FB98'>must be an optimal policy</span></b>.
>
>In practice $\pi_{i}$ <b><span style='color: #F0E68C'>becomes optimal way faster</span></b> than $U_{i}$ converges.

First <b><span style='color: #B0E0E6'>policy evaluation</span></b>, is given a policy just compute the <b><span style='color: #F0E68C'>utility of the sate as if the policy was executed</span></b> (*just do what the policy says*).

So essentially using the formula for utility of a state:
$$
U(s) = V(s) =  \sum_{s'} P(s' \vert s, \pi_{i}(s)) [R(s, \pi_{i}(s), s') + \gamma U(s')]
$$
Here we have essentially $\vert S \vert$ number of **linear equations** and unknowns which can be **solved** in <b><span style='color: #F0E68C'>O(n<sup>3</sup>)</span></b> time.

>[!note] Basically each state will have a $U(s)$ equation which we need to solve using linear equations

<b><span style='color: #B0E0E6'>Policy improvement</span></b> on the other hand, is to **calculate the new policy** ($\pi_{i+1}$) using a <b><span style='color: #F0E68C'>one-step look ahead</span></b> based on $U_{i}$ (*finding a better action to take*) using the bellman equation.

>[!note] Or we can use [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Markov Decision Process.md#Monte Carlo Tree Search|MCTS]] to look at a bigger range instead of 1 step.

**Policy Iteration Algorithm Pseudocode**
```cpp
// Retruns a policy
policy policyIteration(mdp) {
	pi = initialiseRandomPolicy() // At this state do what action;
	U = A vector of utility of state values initially 0;
	bool unchanged = false;
	do {
		U = policyEvaluation(pi, U, mdp);
		for (State s: S) {
			// Policy Improvement
			bestOneStepAction = argmax Q-Value(mdp, s, a, U) // Our bellman equation to get best action
			if (Q-value(mdp, s, bestOneStepAction, U) > Q-Value(mdp, s, pi[s], U)) {
				pi[s] = bestOneStepAction;
				unchanged = true;
			}
		}
	} while (unchanged);
	return pi;
}
```

For **large state space** it will be better to <b><span style='color: #98FB98'>use iterative methods</span></b>.

>[!info] Asynchronous policy iteration
>We can do our updates asynchronously by only <b><span style='color: #F0E68C'>picking a subset of states</span></b> for policy improvement or evaluation.
>
>It **converges** as long as <b><span style='color: #F0E68C'>all states are updated</span></b> (*for all subsets it must contains all states when combined*).
## Monte Carlo Tree Search

Usually when our **state space is large** we <b><span style='color: var(--mk-color-red)'>cannot iterate over all states</span></b>. Usually there are a few ways to handle this:
1) **Function approximation**: <b><span style='color: #F0E68C'>Learn a function over a subset of states</span></b> and hope it generalises over everything else (*interpolation*).
2) **Limiting search**: <b><span style='color: #F0E68C'>Search until we hit the time limit</span></b> then we get the best action (*Monte Carlo tree search*)

>[!fail] Cuse of dimensionality
>It is when our <b><span style='color: var(--mk-color-red)'>state space grows exponentially</span></b> with the number of variables.
>
>Ways to handle this are:
>- Function approximation & machine learning
>- Online search, possibly with sampling (*which is MCTS*)

**MCTS Algorithm Pseudocode**:
```cpp
// Usually this state is the initial state
action MCTS(state) {
	tree = Node(state)
	while (isTimeRemaining()) {
		leaf = select(tree); // Select actions until a leaf node is reach
		child  = expand(leaf); // Take the action at the leaf to create new leaf nodes
		result = simulate(child); // Follow some heuristic to reach the goal
		// Sends this reward back to the root and maybe sum the rewards as it goes back up
		backPropagate(result, child); 
	}
	return bestAction(state); // Return the best action seen so far
}
```

![[Monte Carlo Tree Search Example.png|center|550]]

>[!info] The example given shows a deterministic search
>If it is a **MDP**, then an <b><span style='color: #F0E68C'>action is linked to multiple state nodes</span></b> (*instead of just 1 state there can be multiple*).
>
>Then for things like **2 player games** we can do the same like in the [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Local & Adversarial Search.md#Minimax|minimax]], where each level in the tree corresponds to a player.

If we visualise the tree, the **leaves** are usually the <b><span style='color: #F0E68C'>actions that can be taken</span></b>. And for **expansion** we <b><span style='color: #F0E68C'>only expand once</span></b>, afterward we carry out the rollout policy.

For **selection policy** (*on state nodes*) some commonly used policies are:
- Upper confidence bounds applied to trees (*UCT*)
- Upper confidence bounds 1 (*UCB1*)

$$
\text{UCB1}(a) = \frac{U(a)}{N(a)} + C \sqrt{\frac{ln (N (Parent(a)))}{N(a)}}
$$
**Where**:
- $U(a)$ is the total reward accumulated through the action node (*a*)
- $N(a)$ is the total number of times the action node has been visited
- $N(Parent(a))$ is the total number of times that the parent of the action node has been visited (*basically the parent is the state before taking the action*)

>[!question] What does it mean by visited?
>It is basically how many times this <b><span style='color: #F0E68C'>node has been selected during the selection policy throughout the execution</span></b> of the MCTS.

So $U(a) / N(a)$ is our <b><span style='color: #B0E0E6'>exploitation term</span></b> which <b><span style='color: #F0E68C'>selects the best action</span></b> with the data that we have.

But we also want some exploration (*maybe the current best gives a local optima*), then $C \times \sqrt{ln(N(Paret(a)))/N(a)}$ is our <b><span style='color: #B0E0E6'>exploration term</span></b>. Which is a <b><span style='color: #F0E68C'>confidence interval</span></b> that is high when it has not been thoroughly evaluated yet. 

>[!info] Confidence interval meaning in MCTS
>We want to <b><span style='color: #F0E68C'>encourage exploration</span></b> as well as maybe what we have discovered thus far rewards 1 action higher than the other but in reality the other action might be better.
>
>So the **lower this confidence interval** is, it just means that the <b><span style='color: #F0E68C'>exploitation term is almost at a convergence since it has been visited many times</span></b>.

Lastly, $C$ is our **hyperparameter**, it <b><span style='color: #F0E68C'>balances exploration and exploitation</span></b>. The higher this value is the more incline the search is to do exploration (*it is usually square root of 2*).

For **rollout policy** some commonly used policies are:
- Random walk or selection
- Follow a heuristic (*the better the heuristic the better the results*)

Our **backwards propagation** will just be an <b><span style='color: #F0E68C'>summation of the existing utility + the utility from the rollout</span></b>.

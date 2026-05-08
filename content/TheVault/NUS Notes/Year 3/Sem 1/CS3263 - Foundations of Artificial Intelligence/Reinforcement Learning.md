---
title: Reinforcement Learning
Date Created: 2025-11-03
Last Updated: 2025-11-17
tags:
  - CS3263
  - AI/ReinforcementLearning
---
# Reinforcement Learning
---
Consider teaching an agent on how to drive around a circuit, it has its own set of actions and transition states. However often <b><span style='color: var(--mk-color-red)'>it does not get feedback on how well it has done</span></b> until the end of its execution.

This <b><span style='color: #F0E68C'>feedback</span></b> on whether something good or bad happens is called a <b><span style='color: #B0E0E6'>reward</span></b> or <b><span style='color: #B0E0E6'>reinforcement</span></b>.

>[!info] Reinforcement learning is a very general machine learning paradigm which can be used in various scenarios

<b><span style='color: #F0E68C'>Rewards are part of the input perception</span></b> (*something external*) which the agent must recognise that it is a reward rather than some other input. 

![[Overview of Reinforcement Learning.png|center|250]]

>[!note] Usually in reinforcement learning, we don't know the transition or reward model and we want to use reinforcement learning to find these.
## Model Based Reinforcement Learning

So in model based reinforcement learning, lets <b><span style='color: #F0E68C'>learn the transition function</span></b> ($T$) as well as the <b><span style='color: #F0E68C'>reward function</span></b> ($R$) and use what we learn to <b><span style='color: #F0E68C'>solve</span></b> the [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Markov Decision Process.md|MDP]].

>[!info] All this is through empirical experience
>Meaning that the data that the <b><span style='color: #F0E68C'>model learns on is based on its own exploration</span></b>.

If our **states are small and discrete** (*finite*), our **transition function** in the form of $T(s, a, s')$ can be as simple as <b><span style='color: #F0E68C'>counting the action outcomes for each state and action</span></b>, to get the probability of going to the next state given the current state and the action.

Then our **reward** is just looking into the data and <b><span style='color: #F0E68C'>summing up the values and getting the average</span></b>. For example for $R(s, a, s')$ if we see $s \rightarrow s'$ given the action twice then just sum of the values and divide by 2.

Then with this 2 run the MDP solver and you can get your policy.

>[!example] Example of learning the transition & reward function
>![[Example Trajectory for RL.png|center|500]]
>
>For the **transition function** $P(s' = (3, 2) \vert s = (3, 3), a = Right) = 1/3$. This is because we see state (3, 3) 3 times and only 1 of those times we reached (3,2).
>
>For the **reward function** $R(s, a, s')$ where $s = (1, 1)$, $a = up$ and $s' = (1, 2)$. So the reward is, $1/2(-0.04 + -0.04)$. Because we see (1, 1) -> (1, 2) twice, both reward at state (1, 1) to be -0.04.
<div style="page-break-after: always;"></div>

>[!warning] The reward and transition function only depends on the data observed
>It <b><span style='color: var(--mk-color-red)'>might not cover all possible state action outcomes</span></b>.
## Model Free Reinforcement Learning

A **model free reinforcement learning** is where it <b><span style='color: #F0E68C'>directly comes up with a policy or value function</span></b> from the observed data.

>[!question] What is a model?
>A model in this case is learning the transition and reward functions to derive a policy.

![[Model-Free Reinforcement Learning Overview.png|center|150]]

It is similar to [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Markov Decision Process.md#Policy Iteration|policy iteration]]we have a policy and trajectories (*observed data*) we will use something called a <b><span style='color: #B0E0E6'>Q-function</span></b> which we learn from the observed data. Then use the Q function ($Q(s, a)$) to <b><span style='color: #F0E68C'>get the max argument and improve our policy</span></b>.
### Learning The Q-Function
#### Monte Carlo Learning

First lets **learn the value function** ($U(s)$). We do not have the transition and the reward function (*if we do then do [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Markov Decision Process.md#Policy Iteration|policy evaluation]]*) but we do have a <b><span style='color: #F0E68C'>initial policy which we can execute to get data</span></b>.

To recap the utility function is the expected total reward from that state onwards. This is **also known as expected reward-to-go or expected return**.

It is also known as the <b><span style='color: #B0E0E6'>direct utility estimation</span></b>. And <b><span style='color: #F0E68C'>getting the data we can do supervised learning</span></b> to <b><span style='color: #F0E68C'>get an unbiased estimate</span></b> of the utility function.

The **formula** is given as such:
$$
U^{\pi}(s) = \Bbb{E} [\sum^{\infty}_{t = 0} \gamma^{t} R(S_{t}) \vert S_{0} = s]  = R(s) + \gamma \sum_{s'} P(s' \vert s, \pi(s))U^{\pi}(s')
$$
Where:
- $U^{\pi}(s)$ is the utility function associated with the given policy $\pi$
- $\gamma$ is the discount at time $t$
- $R(s_{t})$ is the reward for state $s$ at time $t$

We can <b><span style='color: #F0E68C'>get the transition function using the model free method</span></b>.
<div style="page-break-after: always;"></div>

>[!example] Example of calculating the utility
>![[Example Trajectory for RL.png|center|500]]
>
>Assume that $\gamma = 1$.
>
>For (1, 1) in each trajectory (*line*) we compute the return, so we will get 0.72, 0.72 and -1.24. Then $U^{\pi}((1, 1)) = (0.72 + 0.72 - 1.24) / 3 =0.006$
>
>Lets do it for (1, 2), the first trajectory we see 2 of them, so we just calculate the return starting at that point so we will get 0.76 and 0.84 for the first line and the second line we will get 0.76. Doing the same as above we will get 0.79

So this function is essentially keeping <b><span style='color: #F0E68C'>track of all the rewards when we enter at that current time and then just take the average</span></b> (*running average*).

>[!info] It will converge after running infinitely many trials
>The value will converge to the true expected value
>

>[!note] First visit vs Every visit
>The number of visits can be treated differently. For **first** visit just take the <b><span style='color: #F0E68C'>first return and ignore the rest</span></b> as for **every** visit is to <b><span style='color: #F0E68C'>consider all visits to the state</span></b>. **Both** will <b><span style='color: #98FB98'>converge to the true expected value in the limit</span></b>.

>[!failure] Slow to converge
>Learning only begins at the <b><span style='color: var(--mk-color-red)'>end of the episode</span></b> (*when it terminates or at the goal state*).
>
>Also we are <b><span style='color: var(--mk-color-red)'>not exploiting the properties of the MDP</span></b>, because our utility function should satisfy (*equal*) to the [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Markov Decision Process.md#Utility of State & Optimal Policy|bellman equation]].
#### Temporal Difference Learning

Also referred to as **TD learning**. So instead of taking the running average, <b><span style='color: #F0E68C'>use the previously estimated value to get the next value</span></b>.

>[!example] Example of TD learning
>![[Example Trajectory for RL.png|center|500]]
>
>Assume that $\gamma = 1$. For (1, 3) the first trajectory we can do the same as before so we will get $(0.8 + 0.88) / 2 = 0.84$ and for (2, 3) we will get 0.92
>
>For the second trajectory we can to update $U^{\pi} (1, 3)$ we will get the immediate reward at that state which is -0.4 then the utility of the next state which is $U^{\pi}(2, 3)$ which we previously computed to be 0.92 adding them together, we will get 0.88.
>
>Then average the 2 values (0.88 and 0.84) or use a weighted average.

With **more than 1 estimate** for a state we can either do a <b><span style='color: #F0E68C'>average</span></b> or a <b><span style='color: #F0E68C'>weighted average</span></b>. This is to <b><span style='color: #98FB98'>incorporate what we have previously learned</span></b>.

For **transitioning from one state to another**, TD does:
$$
U^{\pi}(s) = U^{\pi}(s) + \alpha[R(s, \pi(s), s') + \gamma U^{\pi}(s') - U^{\pi}(s)]
$$
Where:
- $\alpha$ is the learning rate
- $R(s, \pi(s), s') + \gamma U^{\pi}(s')$ is known as the <b><span style='color: #B0E0E6'>TD target</span></b>
- $R(s, \pi(s), s') + \gamma U^{\pi}(s') - U^{\pi}(s)$ is known as the <b><span style='color: #B0E0E6'>TD term or error</span></b>.

We can replace the reward function with $R(S)$ or $R(S, A)$.

We can also re-write this using **weighted average**:
$$
U^{\pi}(s) = (1 - \alpha)U^{\pi}(s) + \alpha[R(s, \pi(s), s') + \gamma U^{\pi}(s') - U^{\pi}(s)]
$$

>[!note] The formula is now like a ML model where it updates based on the loss value
>
>If our target is larger than the previous estimate (*meaning our error is large*) then the updated estimate will increase, else it will decrease.
>
>So $R(s, \pi(s), s') + \gamma U^{\pi}(s')$ is the utility from the new trajectory which we deduct from $U^{\pi}(s)$ which was the previously estimated utility for state $s$.

Similar to our bellman equations again we will do the following <b><span style='color: #F0E68C'>update on all the observed successors</span></b> ($s \rightarrow s'$). So if our sequence is $AAB$ then we update from $A \rightarrow A$ then $A \rightarrow B$.

>[!important] For the utility function to converge we need to set the correct $\alpha$
> It will converge if $\alpha$ is a <b><span style='color: #F0E68C'>decreasing function of the increasing number of visits</span></b> to a state.
> 
> So the more we visited a state the smaller alpha becomes. For example $\alpha(n) = 1 / n$.
#### Q-Learning

We learnt that the [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Markov Decision Process.md#Q-Functions|Q-function]] can help get the best action however the Q-function we need to have the <b><span style='color: var(--mk-color-red)'>transition model which makes it not model free</span></b>.

So why not just learn the Q-function, making it model free as we do not need the knowledge of the model or the transition function.

The algorithm for <b><span style='color: #F0E68C'>Q-learning is the same as TD learning</span></b>:
$$
Q(s, a) = Q(s, a) + \alpha[R(s, a, s')  + \gamma max_{a'} Q(s', a') - Q(s, a)]
$$
Where:
- $max_{a'} Q(s', a')$, is the value of the best action to take at the next state

So after many rounded of updating it with the data, we will get a $Q$ function which will tell us at which state take what action.
<div style="page-break-after: always;"></div>

## Greedy Model Based RL

The issue with model and model free learning is that we can be <b><span style='color: var(--mk-color-red)'>missing some of the state action pairs</span></b> depending on the policy that was given.

Thus we will need to include <b><span style='color: #F0E68C'>exploration to learn from missing state action pairs</span></b>.

>[!warning] Need to have a tradeoff between exploration and exploitation
>**Exploitation** is essentially <b><span style='color: #F0E68C'>taking the action which we already know its the best</span></b> while **exploration** is to try to <b><span style='color: #F0E68C'>take a new action</span></b> to see if it gives a better reward.
>
>So when a agent in a **model does an action** it can either <b><span style='color: #F0E68C'>do exploration or exploitation but not both</span></b> thus we need a tradeoff.

A simple way to do exploration is to <b><span style='color: #F0E68C'>take a random action</span></b>. Then <b><span style='color: #F0E68C'>after some time become greedy</span></b> (*exploitation*). This is known as <b><span style='color: #B0E0E6'>greedy in the limit of infinite exploration</span></b>.

How this works is that:
1) To start <b><span style='color: #F0E68C'>try each action in each state</span></b> an unbounded number of times. 
2) The **longer** this runs the <b><span style='color: #98FB98'>lower the probability of missing</span></b> an optimal action (*or a state action pair*).
3) Then once we **run enough number of times**, it <b><span style='color: #F0E68C'>becomes greedy</span></b> and will take the optimal option with respect to the true model.

>[!question] How do we make it greedy after awhile?
> Why not <b><span style='color: #F0E68C'>set a probability</span></b> of being greedy ($1 - \epsilon$) or to explore ($\epsilon$).
> 
> Then <b><span style='color: #F0E68C'>as we run we can lower the value</span></b> of$\epsilon$ ($\epsilon = 1/t$) which eventually will cause the model to be greedy. This is to <b><span style='color: #98FB98'>ensure it converges</span></b>, however it is <b><span style='color: var(--mk-color-red)'>slow to converge</span></b>.

So we can use an <b><span style='color: #B0E0E6'>optimistic estimate</span></b> of the utility function $U^{+} s$. This means that the agent will be <b><span style='color: #F0E68C'>more optimistic about exploration</span></b>.

To construct $U^+{s}$ is to use an **exploration function** ($f(u, n$)) using the following update:
$$
U^{+}(s) = max_{a} f (\sum_{s'} P(s' \vert s, a)[R(s, a, s') + \gamma U^{+}(s')], N(s, a))
$$
Where:
- $N(s, a)$, is the number of times we see this action being taken from that state
- $u$ is essentially this part, $\sum_{s'} P(s' \vert s, a)[R(s, a, s') + \gamma U^{+}(s')$
- $n$ is essentially this part $N(s, a)$

For our $f$ function, we will <b><span style='color: #F0E68C'>set a threshold</span></b> on how many times we need to see $N(s, a)$ **in order to be optimistic**. If it is **below** the threshold ($N_{e}$) then <b><span style='color: #F0E68C'>return a large value</span></b> ($R^{+}$).

If it is **above** the threshold, then our model <b><span style='color: #F0E68C'>gets the best reward based on what it has seen</span></b> so far (*it is just the bellman equation to get max value*).
### Q-Learning With Exploration

We can incorporate Q-learning with an exploration function.
<div style="page-break-after: always;"></div>

**Q-learning with exploration pseudocode**:
```cpp
action QLearningAgent(sPrime, r) {
	Q = stateActionValues(); // Is persistent, initially 0
	Nsa = frequenciesStateActionPair(); // Is persistent, initially 0
	s, a = null; // Previous state and action, initially null
	if (s is not null) {
		Nsa[s, a] += 1; // Increment the visited
		Q[s, a] = Q[s, a] + alpha(Nsa[s, a])(r + gamma maxAPrime(Q[sPrime, aPrime] - Q[s, a]));
	}
	s, a = sPrime, argmaxOfaPrime f(Q[sPrime, aPrime], Nsa[sPrime, aPrime]); // Exploration fn
	return a;
}
```

So initially there is <b><span style='color: #F0E68C'>no previous state thus we will get a random action to take</span></b>. So the model does the action and is now in a new state which our RL will then <b><span style='color: #F0E68C'>feedback back to this function and repeat</span></b>.

It will take our previous state and action to <b><span style='color: #F0E68C'>update the Q-function</span></b> that is being learnt. Then we will use the <b><span style='color: #F0E68C'>exploration function to give us a new action or an known best action</span></b>.
# Function Approximation in RL
---
Using tabular states can be a bad thing for large states as the <b><span style='color: var(--mk-color-red)'>space used grows exponentially</span></b> with the number of variables. This is known as the <b><span style='color: #B0E0E6'>curse of dimensionality</span></b>.

Instead of having all the states, we use <b><span style='color: #F0E68C'>function approximation to represent utility & Q-functions</span></b>.

>[!note] Some examples of function approximators are linear function of features or neural networks
>
>But in general it uses $n$ parameters each with a <b><span style='color: #F0E68C'>hyperparameter</span></b> denoted as $\theta$ and it uses <b><span style='color: #F0E68C'>reinforcement to learn</span></b> $\theta$ to approximate the value of the function. 

When using [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Reinforcement Learning.md#Monte Carlo Learning|Monte Carlo learning]] we can get essentially a pair of state, actual utility tuple with a estimated utility. So essentially it is a [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Introduction to Machine Learning & Decision Trees.md#Supervised Learning|supervised learning problem]]. And to get the <b><span style='color: #F0E68C'>best estimate we aim to minimise the error</span></b>.

Another option is to minimise the loss function using <b><span style='color: #F0E68C'>online learning</span></b> which is [[Year 2/Sem 1/CS2109S - Introduction to AI & Machine Learning/Introduction to Neural Networks.md#Gradient Descent on Neural Network|gradient descent]].

>[!info] Online learning 
>It is <b><span style='color: #F0E68C'>essentially for continuous learning</span></b>, updating the model one example at a time as new data arrives, so basically doing something at time $t$ to get the data at time $t+1$

>[!example] Example of gradient descent
>Assuming our loss function is the Q-function (*we can use the [[Year 3/Sem 1/CS3263 - Foundations of Artificial Intelligence/Reinforcement Learning.md#Temporal Difference Learning|temporal difference loss]] as well*).
>**Q-learning**:
>To update $\theta_{i} = \theta_{i} + \alpha(R(s)  + \gamma max_{a'} Q_{\theta}(s', a') - Q_{\theta}(s, a)) \times \frac{\partial U_{\theta}(s)} {\partial (\theta{i})}$.
>
>**TD**
>To update $\theta_{i} = \theta_{i} + \alpha(R(s)  + \gamma U_{\theta}(s') - U_{\theta}(s)) \times \frac{\partial U_{\theta}(s)} {\partial (\theta{i})}$.
<div style="page-break-after: always;"></div>

# Policy Search in RL
---
In a regular policy it maps some state with an action. But in RL, our <b><span style='color: #F0E68C'>policy is an equation of parameters</span></b> ($\theta$). We can take a collection of Q-functions (*one for each action*) and take the action of the highest value.

Now our policy search instead of updating utility and the best action it now<b> <span style='color: #F0E68C'>adjusts</span></b> $\theta$ <b><span style='color: #F0E68C'>to improve the policy</span></b>.

>[!example] Example of a Q function parameterised by $\theta$
>$Q_{\theta}(s, a) = \theta_{0}(s) + \theta_{1}(a)$.
>
>This is just a very simple example.

>[!failure] This it is not continuous
>The issue is because we are taking the argmax and thus we cannot use gradient descent.

To **make our policy stochastic**, we can <b><span style='color: #F0E68C'>use the SoftMax function</span></b>.
$$
\pi_{\theta}(s_{0}, a) = \frac{e^{Q_{\theta}(s_{0}, a)}}{\sum_{a'} e^{Q_{\theta} (s_{0}, a')}}
$$
Where:
- The denominator is the sum of all possible actions

So now our policy is shows the probability of being at this state and taking this action. Now <b><span style='color: #F0E68C'>to optimise this we want to maximise the expected reward</span></b>.
$$
p(\theta, s_{0}) = \sum_{a} \pi_{\theta}(s_{0}, a)R(s_{0}, a)
$$
So with this we can just **do gradient descent on the above expected reward function**.
$$
\nabla_{\theta}p(\theta, s_{0}) = \sum_{a}  (\nabla_{\theta}\pi_{\theta}(s_{0}, a))R(s_{0}, a) = \sum_{a} \pi_{\theta}(s_{0}, a)  \frac{(\nabla_{\theta}\pi_{\theta}(s_{0}, a))R(s_{0}, a)}{\pi_{\theta}(s_{0}, a)}
$$
However with a very **large action space**, it will be <b><span style='color: var(--mk-color-red)'>very computationally expensive to sum over all actions</span></b>.

>[!success] The solution to this is to sample a subset of actions to approximate the gradient
>So using the gradient function above:
>$$
>\approx \frac{1}{N} \sum^{N}_{j = 1} \frac{(\nabla_{\theta}\pi_{\theta}(s_{0}, a))R(s_{0}, a)}{\pi_{\theta}(s_{0}, a)} = \frac{1}{N} \sum^{N}_{j = 1} \nabla_{\theta} (ln\pi_{\theta}(s_{0}, a))R(s_{0}, a)
>$$

So in an online update we essentially **get the reinforced algorithm** which is:
$$
\theta_{j + 1} = \theta_{j}  + \alpha \times   ln\pi_{\theta}(s_{0}, a)R(s_{0}, a)
$$
Note:
- You can replace $R(s_{0}, a)$ with the Q function as well

However in practice, most of the time the <b><span style='color: #B0E0E6'>advantage function</span></b> is often used instead.
$$
A_{\pi_{\theta}} = Q_{\pi_{\theta}}(s, a) - V_{\pi_{\theta}}(s) = E [r + \gamma V_{\pi_{\theta}}(s')] - V_{\pi_{\theta}}(s)
$$
Where:
- $E [r + \gamma V_{\pi_{\theta}}(s')] - V_{\pi_{\theta}}(s)$ is the TD loss function

>[!question] Why is the advantage function used more often?
>The advantage function has a <b><span style='color: #98FB98'>lower variance</span> </b> while <b><span style='color: #98FB98'>providing an unbiased estimate</span></b>.

So finally using the advantage function in our reinforced algorithm online update, we thus convert it to a <b><span style='color: #B0E0E6'>actor-critic method</span></b>.
$$
\theta_{j + 1} = \theta_{j}  + \alpha \times   ln\pi_{\theta}(s_{0}, a) (r_{j} + \gamma V_{\pi_{\theta}}(s_{j + 1}, w) - V_{\pi_{\theta}}(s_{j}, w))
$$
Where:
- $w$ is a set of hyperparameters similar to $\theta$, to estimate the value of the state

>[!info] Actor-critic method
>The actor $\pi_{\theta}$ is the actor that takes action.
>
>And at the same time, learn a value function $V(s, w)$ that is used for evaluation (*critic*).


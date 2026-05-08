---
title: Designing an AI
Date Created: 2024-08-12
Last Updated: 2025-09-28
tags:
  - CS2109S
  - AI
---
# PEAS
---
A broad visualisation of an **intelligent agent** :
![[How an Intelligent Agent Functions.png|center|400]]

**Environment** - <span style='color:var(--mk-color-yellow)'>Where</span> this agent gets its data from (*Example : In a game, real life, financial market*)
**Sensors** - <span style='color:var(--mk-color-yellow)'>Retrieval & processing</span> of data
**Functions** - Allows the agent to <span style='color:var(--mk-color-yellow)'>make decisions</span> based on data
**Actuators** - The movable <span style='color:var(--mk-color-yellow)'>parts</span> of the agent (*Example : Moving a chess piece, Engine, Breaks*)

<span style='color:#FF8348'>PEAS</span> is a framework used to determine the agent:
>[!info]+ 
>The full term for <span style='color:#FF8348'>PEAS</span> is :
>- Performance Measure
>- Environment
>- Actuators
>- Sensors

When **deciding on a performance measure** to access performance, it is good to consider the following :
- Target audience
- What to optimise
- Information accessibility
- Unintended effects
- Costs

A <span style='color:var(--mk-color-turquoise)'>rational agent</span> is an agent that will <span style='color:var(--mk-color-green)'>maximise performance measures</span>.
## Environment

An environment can be <span style='color:var(--mk-color-orange)'>fully observable or partially observable</span>
>It is the agents **field of view**, can it see the whole environment (*Chess board*) or partially (*Self driving cars*).

An environment can be <span style='color:var(--mk-color-orange)'>deterministic or stochastic</span>
>For it to be **deterministic**, the next state is **determined by the current state and the action taken**, there must be <b><span style='color:var(--mk-color-red)'>no randomness</span></b>, unlike stochastic.

> [!important]+ Things to Note
> There is also an <span style='color:var(--mk-color-orange)'>strategic</span> environment where the agent itself is **deterministic but actions by other agents are not**.
> 
> An example is 2 bots playing chess!

An environment can be <span style='color:var(--mk-color-orange)'>episodic or sequential</span>
>For it to be episodic, the agent's actions is **solely depends on the current state** and not based on decisions made in the past.

An environment can be <span style='color:var(--mk-color-orange)'>static or dynamic</span>
>Static means that so long as the **agent does not do anything**, the **environment will not change**.

> [!important]+ Things to Note
> It can also by semi-dynamic, where the environment does not change, but **other factors** (*like time*) **can affect the environment**.
> 
> An example is like playing chess, but when the <span style='color:var(--mk-color-red)'>time is up, you lose</span>

An environment can be <span style='color:var(--mk-color-orange)'>discrete or continuous</span>
>If there is a **finite number of possible states** for an environment, it is considered as discrete.

An environment can be <span style='color:var(--mk-color-orange)'>single agent or multi agent</span>
>If there are **other agents in play**, then it is a multi agent environment.

# Agent Structures
---
When designing an agent, its <span style='color:var(--mk-color-blue)'>function</span> will **fully specify** what agent it is.

It is also good to take into account <span style='color:var(--mk-color-orange)'>exploration</span> (*Gather more data*) vs <span style='color:var(--mk-color-orange)'>exploitation</span> (*Maximise gain based on current knowledge*).
## Types of Agent Structures

1. **Simple Reflex Agent** 
>It only <span style='color:var(--mk-color-yellow)'>follows a set of instructions</span> strictly and has **no feedback loop**.

2. **Model-based Agent**
>It has a <span style='color:var(--mk-color-yellow)'>sense</span> (*Simulation*) <span style='color:var(--mk-color-yellow)'>of its environment</span> and will make decisions based on the environment.

3. **Goal-based Agent**
>It has a <span style='color:var(--mk-color-green)'>goal</span> and will <span style='color:var(--mk-color-yellow)'>simulate combination of actions</span> till it reaches the goal. Once reached it will trace back and <span style='color:var(--mk-color-yellow)'>made the decision that leads to that goal</span>.

4. **Utility-based Agent**
>This agent has a <span style='color:var(--mk-color-blue)'>utility function</span> which **assigns scores to various states**. Afterwards it will <span style='color:var(--mk-color-yellow)'>simulate</span> like a goal-based agent to <span style='color:var(--mk-color-green)'>maximise its utility</span>.

5. **Learning Agent**
>This agent basically has a **feedback loop** which <span style='color:var(--mk-color-yellow)'>tells</span> itself if doing a <span style='color:var(--mk-color-yellow)'>specific action is desirable or not</span>. This is then collected as data and <span style='color:var(--mk-color-yellow)'>makes its own intuition</span>.




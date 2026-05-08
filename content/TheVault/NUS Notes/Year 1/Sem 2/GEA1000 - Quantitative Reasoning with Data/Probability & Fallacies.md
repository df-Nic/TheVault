---
title: Probability & Fallacies
Date Created: 2024-04-23
Last Updated: 2025-09-27
tags:
  - GEA1000
  - Statistics
  - Probability
  - Math
---
# Probability
---
**Probability experiment**
>Unlike normal experiments, this type of experiment can be <span style='color:var(--mk-color-yellow)'>repeated as many times</span> as possible and <span style='color:var(--mk-color-yellow)'>all outcomes can be listed out</span>

Some <span style='color:var(--mk-color-orange)'>terminologies</span> :
- **Sample space** - The set of all possible outcomes from the experiment
- **Event** - It is some subset of the sample space (Outcomes)
- **Probability** - The likelihood the event will occur

Then the probability of an event, denoted as $P(E)$ <span style='color:var(--mk-color-yellow)'>can only have a range of 0 to 1</span>. The probability can also be known as <span style='color:var(--mk-color-turquoise)'>proportion</span>.

This probability is <span style='color:var(--mk-color-red)'>not the true probability</span> since it is just an estimate.

**Rules of probability**
- $1 \le P(E) \le 1$
- $P(\text{Sample Space}) = 1$
- If $A$ and $B$ are <span style='color:var(--mk-color-yellow)'>mutually exclusive</span> (non-overlapping), then $P(A \cup B) = P(A) + P(B)$
- The <span style='color:var(--mk-color-yellow)'>sum of the probability of all events</span> in the sample space is 1

If <span style='color:var(--mk-color-yellow)'>every event has the same probability</span> then this is known as <span style='color:var(--mk-color-turquoise)'>uniform probability</span> where $P(E) = \frac{1}{n}$.
## Conditional Probability

This type of probability is given as $P(A \vert B)$, which can be translated as <span style='color:var(--mk-color-yellow)'>probability of event A given B</span>.

In mathematical terms the <span style='color:var(--mk-color-orange)'>conditional probability can be calculated</span> as such :
$$
P(A \vert B) = \frac{P(A \cap B)}{P(B)}
$$
If $P(B) = 0$ then $P(A \vert B) = 0$.

There are some <span style='color:var(--mk-color-orange)'>terms</span> to know for conditional probability :
- If asked for <span style='color:var(--mk-color-turquoise)'>sensitivity</span>, it is asking $P(+ \vert A)$ (**probability of positive, given something**), this called the true positive rate
- If asked for <span style='color:var(--mk-color-turquoise)'>specificity</span>, it is asking $P(- \vert A)$ (**probability of negative, given something**), this called the true negative rate

**Prosecutor's fallacy**
>It states that $P(A \vert B) \neq P(B \vert A)$

But the $P(A \vert B) = 1 - P(A' \vert B)$.
## Independence of Events

For <span style='color:var(--mk-color-yellow)'>2 events to be independent</span>, $P(A) = P(A \vert B)$

From this equation, the following can be obtained :
$$
P(A) \times P(B) = P(A \vert B)
$$
Therefore if this is true, $P(A) = P(A \vert B)$, then <span style='color:var(--mk-color-yellow)'>there is no association</span> between $A$ and $B$. In addition they can also be considered as independent variables / events.

There is also <span style='color:var(--mk-color-turquoise)'>conditional independence</span> :
$$
P(A \cap B \vert C) = P(A \vert C) \times P(B \vert C)
$$
This can be read as $A$ and $B$ are conditionally independent given C with $P(C) \gt 0$.
## Law of Total Probability

It states that If, $B_{1}, B_{2}, \dots, B_{n}$ forms a partition of the sample space S , then we can calculate the probability of event A as:
$$
P(A) = P(A \vert B_{1}) \times P(B_{1}) + P(A \vert B_{2}) \times P(B_{2}) + \dots + P(A \vert B_{n}) \times P(B_{n})
$$
**Conjunction fallacy**
>It is the <span style='color:var(--mk-color-yellow)'>assumption</span> that the <span style='color:var(--mk-color-yellow)'>probability of 2 things happening is greater than only 1</span> thing happening

Thus $P(A \cup B) \le P(A)$ and <span style='color:var(--mk-color-red)'>NOT</span> $P(A \cup B) \gt P(A)$ or $P(A \cup B) \lt P(B)$

**Base rate fallacy**
>Information about the <span style='color:var(--mk-color-yellow)'>rate of occurrence of some trait</span> in a population (the base rate information) <span style='color:var(--mk-color-yellow)'>is ignored</span> or not given appropriate weight.

**Example :**
- Given a breathalyser that has a 100% success rate for drunk people but a 5% will be positive even if they are not
- Then 1 out of 1000 people drink drives to say that the $P(drunk \vert +) = \frac{1}{1000}$ is the <span style='color:var(--mk-color-red)'>base rate fallacy</span>
## Random Variable

A <span style='color:var(--mk-color-turquoise)'>random variable </span>is defined as any <span style='color:var(--mk-color-yellow)'>numerical value</span> of a outcome that is <span style='color:var(--mk-color-yellow)'>assigned a probability over all possible values</span>.

There are <span style='color:var(--mk-color-orange)'>2 types of random variables</span> :
1) **Discrete random variable** - It has a <span style='color:var(--mk-color-yellow)'>finite</span> number of possible values
2) **Continuous random variable** - It has a <span style='color:var(--mk-color-yellow)'>infinite</span> possible number of values
	>It is not a distinct value but rather <span style='color:var(--mk-color-yellow)'>values over a particular range</span>. And when calculating **probability** between the range it is <span style='color:var(--mk-color-yellow)'>calculating the area under the curve</span>.


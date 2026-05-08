---
title: Categorical Data Analysis
Date Created: 2024-04-23
Last Updated: 2025-09-27
tags:
  - GEA1000
  - Statistics
---
# PPDAC Cycle
---
1) **Problem**
	>The <span style='color:var(--mk-color-yellow)'>question</span> or <span style='color:var(--mk-color-yellow)'>problem</span> that the researcher wants the data provide an answer to

2) **Plan**
	>Planning and conducting the <span style='color:var(--mk-color-yellow)'>experiment</span>

3) **Data**
	><span style='color:var(--mk-color-yellow)'>Measure</span> the outcome variable or <span style='color:var(--mk-color-yellow)'>dependent variable</span>. See if it is "successful" or not. Collect data

4) **Analysis**
	>Use <span style='color:var(--mk-color-yellow)'>visualisation tools and data analysis</span>

5) **Conclusion**
	>**Based on the analysis** what is the <span style='color:var(--mk-color-yellow)'>conclusion to the problem</span>. If this conclusion give rise to mare question, then repeat the cycle 

# Analysing Categorical Data
---
## Using a Plot

For categorical data one <span style='color:var(--mk-color-yellow)'>good plot to use will be a bar chart</span>. It clearly <span style='color:var(--mk-color-yellow)'>shows the distribution</span> of the various categories.

But it is preferable for binary categories

**Example of a bar chart**
![[Bar Chart Example.png|center]]

The example above uses **absolute numbers** but, their <span style='color:var(--mk-color-yellow)'>percentages can also be used</span> (Proportion) and this type of bar plot is called the <span style='color:var(--mk-color-turquoise)'>100% stacked bar plot</span>. Keep in mind the $y$-axis <b><mark style='background:var(--mk-color-yellow)'>must be normalised to be from 0 to 100%</mark></b>.

This can also be done with <span style='color:var(--mk-color-yellow)'>2 variables or more</span>.

**Example with 2 variables**
![[100 Percent Stacked Bar Plot with 2 Variables.png|center]]

For <span style='color:var(--mk-color-orange)'>3 or more variables</span> use a <span style='color:var(--mk-color-turquoise)'>sliced bar graph</span>.
## Using a Table

This can be <span style='color:var(--mk-color-yellow)'>done for 1 variable or 2</span> and what it does is that it summarises the data from the 2 variables into a table or also known as a <span style='color:var(--mk-color-turquoise)'>contingency table</span>.

**Example of a 2 variable table:**
![[Using a Table to Analyse Data.png|center]]
The table can also **include row and column percentages**, which is a form or normalisation.

1) **Marginal**
One of which is called the **marginal rates / proportions/ percentages/ probability**. It <span style='color:var(--mk-color-yellow)'>primarily asks for a percentage out of a specific category </span>

For **example**, the proportion of people with a failed treatment will be $219 / 1050$.

2) **Conditional**
Another value will be the **conditional rates / proportions/ percentages/ probability**. It will still ask a percentage out of a specific category but now it has a <span style='color:var(--mk-color-yellow)'>stricter condition</span>.

It is denoted by $P(A \vert B)$ which is read as the rate / probability of $A$ given $B$. The <span style='color:var(--mk-color-yellow)'>condition is that B has already happen</span>.

For **example**, to find $P(\text{Treatment X} \vert Success) = 542 / 831$.

3) **Joint**
These are just asking for the <span style='color:var(--mk-color-yellow)'>rate given a specific event</span>. This is <span style='color:var(--mk-color-red)'>not a conditional rate</span>.

For example, find the **rate of treatment Y AND success**, this will have 289 entries and a probability of $289 / 1050$.

**Purpose of these statistical values :**
- Firstly, the total count can be different between 2 categories and this <span style='color:var(--mk-color-yellow)'>gives a form or normalisation</span>
- This eliminates the unfair bias from a group with a larger number of people

# Association Between Categorical Data
---
Conditional probability is a good way to determine an event $A$ given $B$.

**Outcomes :**
- $P(A \vert B) = P(A \vert B')$, then there is <span style='color:var(--mk-color-yellow)'>no association</span> ($B'$ means not $B$)
- $P(A \vert B) \gt P(A \vert B')$ means that there is a <span style='color:var(--mk-color-green)'>positive association</span> between $A$ and $B$
- $P(A \vert B) \lt P(A \vert B')$ means that there is a <span style='color:var(--mk-color-red)'>negative association</span> between $A$ and $B$

Here the term association is used because <b><mark style='background:var(--mk-color-yellow)'>causation is different from association</mark></b>.

**Establish association**
![[Establishing Association.png|center]]
## Symmetry Rule

**This rule states that :**
![[Symmetry Rule.png|center]]

One observation is that take for example $P(A \vert B) \gt P(A \vert B')$. It means that $A$ is more likely to happen when $B$ happens. This also implies that with more $B$, $A$ happens more therefore $P(B \vert A) \gt P(B \vert A')$.

Therefore to <span style='color:var(--mk-color-orange)'>check for association</span>, check for either of the following :
1) $P(A \vert B) \neq P(A \vert B')$
2) $P(B \vert A) \neq P(B \vert A')$
## Basic rule on rates

This rule states that given $P(A \vert B)$ and $P(A \vert B')$, then the $P(A)$ <span style='color:var(--mk-color-yellow)'>will be between these 2 conditional probabilities</span>.

Mathematically, $P(A \vert B) \le P(A) \le P(A \vert B')$ **OR** $P(A \vert B') \le P(A) \le P(A \vert B)$

**With this then :**
1) $P(B)$ is <span style='color:var(--mk-color-yellow)'>close to 100%</span>, then $P(A)$ <span style='color:var(--mk-color-yellow)'>will be closer to</span> the $P(A \vert B)$ compared to $P(A \vert B')$
2) If $P(B) = 50\%$ exactly, then $P(A) = (P(A \vert B) + P(A \vert B')) / 2)$
3) If $P(A \vert B) = P(A \vert B')$ then $P(A) = P(A \vert B) = P(A \vert B')$

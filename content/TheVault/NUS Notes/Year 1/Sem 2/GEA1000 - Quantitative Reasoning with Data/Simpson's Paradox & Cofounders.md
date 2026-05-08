---
title: Simpson's Paradox & Cofounders
Date Created: 2024-04-23
Last Updated: 2025-09-27
tags:
  - GEA1000
  - Statistics
---
# Simpson's Paradox
---
When comparing associations between 2 variables usually the <span style='color:var(--mk-color-yellow)'>overall population will be analysed</span>. But lets say now the researchers focus on a particular variable against these 2 variables.

For **example**, finding the effectiveness of 2 different treatments but only focusing on males or females only
- Now assume that overall, regardless of gender **treatment $X$ is more effective**
- Now when only focusing on **data for males**, suddenly <span style='color:var(--mk-color-yellow)'>treatment Y is more effective</span>
- And only focusing on **data for females**, <span style='color:var(--mk-color-yellow)'>treatment Y is more effective</span>

This change in observation is known as the <span style='color:var(--mk-color-turquoise)'>Simpson's paradox</span>. Where a <span style='color:var(--mk-color-yellow)'>trend appears in majority of the different groups</span> of data (Groups like, gender, age, demographic). But <span style='color:var(--mk-color-yellow)'>when combined</span> together for the overall association, the <span style='color:var(--mk-color-yellow)'>result is different</span>.

**Example of Simpson's paradox**
![[Simpson's Paradox Example.png|center]]

## Analysing Simpson's Paradox using Slicing

![[Simpson's Paradox Slicing Analysis.png|center]]

Using this image as an example here are <span style='color:var(--mk-color-orange)'>some observations</span> :
- For treatment $X$, the total number of patients with large stones is more than small stones. Therefore the overall average ([[Basics of Statistics#Summary Statistics|Weighted average]]) will be closer to the success rate of the larger sub group (72.4% to 77.4%)
- This is the same for treatment $Y$
- Looking at the <span style='color:var(--mk-color-orange)'>success rates for both types of stones</span>. This shows that the smaller stones are easier to cure than the bigger ones

Thus it can be said that treatment $X$ is <span style='color:var(--mk-color-yellow)'>better</span> but because majority of the <span style='color:var(--mk-color-yellow)'>testes are done on large stones</span> it has <span style='color:var(--mk-color-yellow)'>lower its success rate overall</span>.

Thus in this case the <span style='color:var(--mk-color-yellow)'>stone size should be taken into account</span> in the analysis of treatment effectiveness.
# Cofounder
---
If <span style='color:var(--mk-color-yellow)'>there is a Simpson's paradox, there there will be a cofounder</span>. But the <span style='color:var(--mk-color-red)'>converse is not true</span>, if there is a cofounder it does not mean there is a Simpson's paradox.

This is the **reason why**, <span style='color:var(--mk-color-yellow)'>not everything is a causation</span>, there can be <span style='color:var(--mk-color-yellow)'>other factors that can have an impact at the outcome</span>.

**If there is a Simpson's paradox**, then to find a <span style='color:var(--mk-color-yellow)'>cofounder</span>, it must <span style='color:var(--mk-color-yellow)'>have some association with</span> both the <span style='color:var(--mk-color-yellow)'>dependent</span> and <span style='color:var(--mk-color-yellow)'>independent variable</span> and the association <b><mark style='background:var(--mk-color-yellow)'>must be opposite</mark></b>.

Therefore <span style='color:var(--mk-color-orange)'>should these variables be removed</span>? No as it <span style='color:var(--mk-color-yellow)'>might led researchers to believe that their observations are accurate</span> but in reality there are other cofounders affected the dependent variable.

Inversely, **collecting all the data to find cofounders** is just <span style='color:var(--mk-color-red)'>costly</span> and the <span style='color:var(--mk-color-red)'>processing</span> will be <span style='color:var(--mk-color-red)'>difficult</span>.

The <span style='color:var(--mk-color-red)'>issue</span> of cofounders is strongly present in [[Unit Design#Observational Study|non-randomised studies]] :
- Unsure if all cofounders are controlled due to non-randomised control and treatment group allocation
- Limited Conclusion
- Provides only evidence of association not causation

One way to <span style='color:var(--mk-color-orange)'>control cofounders</span> is <span style='color:var(--mk-color-yellow)'>equal allocation</span> of participants in each variable (Other than dependent and independent). Thus there will be <span style='color:var(--mk-color-yellow)'>no association</span>. Thus <span style='color:var(--mk-color-yellow)'>random assignment does help</span> in even distribution, but it is not always possible due to ethical reasons.
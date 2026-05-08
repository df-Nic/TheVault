---
title: Statistical Inference
Date Created: 2024-04-24
Last Updated: 2025-09-27
tags:
  - GEA1000
  - Statistics
---
# What is Statistical Inference
---
Currently, the [[Basics of Statistics#Exploratory Data Analysis|EDA]], is on the sample level. And now is it possible <span style='color:var(--mk-color-yellow)'>generalise the conclusions</span> of the sample to the entire <span style='color:var(--mk-color-yellow)'>population</span>, which is the purpose of <span style='color:var(--mk-color-turquoise)'>statistical inference</span>.

Our goa is to ensure the <span style='color:var(--mk-color-yellow)'>sample statistic is as close as possible to the population parameter</span>.

Sample statistic = Population parameter + Random error + Bias
- To **remove bias**, there are many ways to do so like using probability based sampling
- **Random error** arises from any probability based sampling

# Types of Statistical Inference
---
## Confidence Intervals

A <span style='color:var(--mk-color-turquoise)'>confidence interval</span> is an <span style='color:var(--mk-color-yellow)'>interval</span> of values computed from sample data that is likely to <span style='color:var(--mk-color-yellow)'>include the unknown value of a population parameter</span>.

It <span style='color:var(--mk-color-yellow)'>quantifies the variation</span> occurred from the <span style='color:var(--mk-color-yellow)'>random errors</span>.

A confidence interval <span style='color:var(--mk-color-orange)'>consists of 2 things</span> :
1) The **confidence level** (95%, 90%, 85%)
2) The **interval itself**, which is <span style='color:var(--mk-color-yellow)'>constructed</span> from the <span style='color:var(--mk-color-yellow)'>sample statistic</span> and the <span style='color:var(--mk-color-yellow)'>confidence level</span>

This <span style='color:var(--mk-color-turquoise)'>confidence level</span>, states that, it is 95% (example) **confident that the population lies in the confidence interval.**

The <span style='color:var(--mk-color-orange)'>general formula for a confidence interval</span> is :
$$
\text{Sample Statistic} \pm \text{Multuplier} \times \text{Standard Error}
$$

**Construction of confidence intervals**
1) Confidence intervals for population proportion

**Based on the general formula**
- $\text{Multuplier} \times \text{Standard Error}$ is called the <span style='color:var(--mk-color-turquoise)'>margin of error</span>
- The **multiplier** is based on the <span style='color:var(--mk-color-yellow)'>confidence interval</span> and its value determined by the <span style='color:var(--mk-color-yellow)'>standard normal distribution</span> (Z - score)
- **Standard error** is the <span style='color:var(--mk-color-yellow)'>standard deviation</span> of the sample statistic

**Standard error** can be <span style='color:var(--mk-color-orange)'>calculated</span> as such :
$$
\sqrt{\frac{p \times (1 - p)}{n}}
$$
**Where :**
- $p$ is the **sample statistic** which is just the <span style='color:var(--mk-color-yellow)'>proportion of a specific outcome</span>
- $n$ is the **sample size**

Based on the above formulas, the <span style='color:var(--mk-color-orange)'>confidence interval can be calculated a such</span> :
$$
p \pm \text{z-score} \times \sqrt{\frac{p \times (1 - p)}{n}}
$$
If the **population portion lies with in this range**, then it is said that the <span style='color:var(--mk-color-yellow)'>sample's confidence interval contains the population parameter</span>. Else, that means that it does not contain the population parameter

2) Confidence intervals for population mean

Unlike population proportion now the <span style='color:var(--mk-color-yellow)'>mean will be used instead</span> and the population parameter will be the population mean.

**Based on the general formula**
- $\text{Multuplier} \times \text{Standard Error}$ is called the <span style='color:var(--mk-color-turquoise)'>margin of error</span>
- The **multiplier** is based on the <span style='color:var(--mk-color-yellow)'>confidence interval</span> and its value determined by the <span style='color:var(--mk-color-turquoise)'>student's t distribution</span>
- **Standard error** is the <span style='color:var(--mk-color-yellow)'>standard deviation</span> of the sample statistic

**Standard error** can be <span style='color:var(--mk-color-orange)'>calculated</span> as such :
$$
\frac{s}{\sqrt{n}}
$$
**Where :**
- $s$ is the **standard deviation**
- $n$ is the sample size

Based on the above formulas, the <span style='color:var(--mk-color-orange)'>confidence interval can be calculated a such</span> :
$$
\bar{x} \pm \text{t-score} \times \frac{s}{\sqrt{n}}
$$
### Properties of Confidence Intervals

1) **Changes in confidence intervals**

For the **same sample**, if there is any <span style='color:var(--mk-color-yellow)'>change in the confidence interval</span>, it will <span style='color:var(--mk-color-yellow)'>change</span> the <span style='color:var(--mk-color-yellow)'>range</span> of the interval.

**Example of the effects of confidence level changes**
![[How Confidence Level Affects Confidence Interval.png|center]]

The <span style='color:var(--mk-color-red)'>lower</span> the level, the <span style='color:var(--mk-color-yellow)'>smaller the interval</span>, the <span style='color:var(--mk-color-green)'>larger</span> the level, the <span style='color:var(--mk-color-green)'>larger the inteval</span>.

2) **Changes in sample size**

With the same confidence interval, and 2 samples are of different sizes then, the sample with the <span style='color:var(--mk-color-yellow)'>larger size will have a smaller confidence interval</span> than the smaller one.

**Example of the effects of sample size changes**
![[Effects of Sample Size on Confidence Interval.png]]
# Hypothesis Test
---
A <span style='color:var(--mk-color-turquoise)'>hypothesis test</span> is a **statistical inference method** used to decide if the data from a random sample is <span style='color:var(--mk-color-yellow)'>sufficient to reject a particular hypothesis about a population</span>.

A **hypothesis can be** :
1) A population parameter, be it the mean or proportion
2) Weather 2 variables are associated with one another

Hypothesis test and confidence interval are almost similar.

**Idea of hypothesis test**
![[Idea of a Hypothesis Test.png|center]]
The **larger the gap**, the <span style='color:var(--mk-color-yellow)'>less likely</span> it is that the observation is due to <span style='color:var(--mk-color-yellow)'>random chance</span>.

**How to carry out hypothesis testing**
1) **Determine** the <span style='color:var(--mk-color-turquoise)'>null</span> and <span style='color:var(--mk-color-turquoise)'>alternative hypothesis</span>
2) Set the **significance level** (Typically 5%)
3) Find the relevant sample statistic
4) Calculate the p-value
5) Conclude the test

**Null hypothesis**
>Corresponds to the case where our observation can be <span style='color:var(--mk-color-yellow)'>explained by chance variation</span>. It is denoted by $H_{0}$

**Alternative hypothesis**
> Corresponds to the case where our observation is <span style='color:var(--mk-color-yellow)'>NOT due</span> to random chance. It is denoted by $H_{1}$

There are <span style='color:var(--mk-color-orange)'>3 types of hypothesis tests</span> :
1) Hypothesis test for population proportion
2) Hypothesis test for population mean (t-test)
3) Hypothesis test for Association (Chi-squared test for association)
## Hypothesis test for Population Proportion

This test will be done using the population proportion.

**Significance level**
>it is the <span style='color:var(--mk-color-yellow)'>value</span> that when small enough for the p-value to <span style='color:var(--mk-color-yellow)'>reject the null hypothesis</span>

**P-value**
>The p value is the probability of obtaining a result as extreme or more extreme than our observation in the direction of the alternative hypothesis, assuming that the null is true.

As long as the **P-value is smaller than the significance level**, then the <span style='color:var(--mk-color-yellow)'>null hypothesis can be safely rejected.</span>

If it is greater than, the <span style='color:var(--mk-color-yellow)'>null hypothesis cannot be rejected</span> and the <span style='color:var(--mk-color-yellow)'>test is inconclusive</span>. In this sense, the <span style='color:var(--mk-color-red)'>null hypothesis will never get accepted</span>.
## Hypothesis test for Population Mean

This test will be done using the population and sample mean.

While the rest stays the same as using population proportion,

## Hypothesis test for Chi Square Test

The hypothesis is now different :
1)  Null hypothesis should be, <span style='color:var(--mk-color-yellow)'>there is no association</span> between categorical variable A and categorical variable B at the population level.
2) Alternative hypothesis should be <span style='color:var(--mk-color-yellow)'>there is an association</span> between categorical variable A and categorical variable B at the population level.

The rest of the steps are the same as above.
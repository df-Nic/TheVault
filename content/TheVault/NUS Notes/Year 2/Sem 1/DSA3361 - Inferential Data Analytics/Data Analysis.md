---
title: Data Analysis
Date Created: 2024-08-13
Last Updated: 2025-09-28
tags:
  - DSA3361
  - Statistics
---
# Central Limit Theorem
---
This theorem (**CLT**) states that, the <span style='color:var(--mk-color-yellow)'>sampling distribution of the mean will always be normally distributed</span> as long as the <span style='color:var(--mk-color-yellow)'>sample size is large enough</span>.

<span style='color:var(--mk-color-turquoise)'>Sampling distribution</span> is the process of taking a <span style='color:var(--mk-color-yellow)'>sample</span> and <span style='color:var(--mk-color-yellow)'>calculate the test statistic</span>. And **repeat this over a few times**. 

This holds <span style='color:var(--mk-color-green)'>true</span> **regardless of the population distribution**.

> [!attention] CLT Conditions
> For CLT to work:
> 1) The samples must be **independent**
> 2) The number of observations are **large**

Given the **mean** ($\mu$) and the **standard deviation** of the **population** ($\sigma$), by <span style='color:var(--mk-color-turquoise)'>CLT</span>:
1) The **sample mean** ($\bar{X}$) is just $\mu$
2) The **sample standard deviation** or <span style='color:var(--mk-color-turquoise)'>standard error</span> (*s*) = $\sigma / \sqrt{n}$

As the **sample size gets bigger**, the sample variable will <span style='color:var(--mk-color-yellow)'>approximates the normal distribution</span>.

<span style='color:var(--mk-color-turquoise)'>Normality</span> indicates that the distribution follows the **bell curve**. As long as the **population distribution is normal**, the <span style='color:var(--mk-color-yellow)'>sample size need not be large</span> to CLT to be valid.
## Best Sampling Size

The **different samples size** can <span style='color:var(--mk-color-yellow)'>affect the shape</span> of the sampling distribution.

**Example:**
![[How Sample Size Affects the Sample Distribution Curve.png|center]]

But what is a <span style='color:var(--mk-color-orange)'>good sampling size</span>. It <span style='color:var(--mk-color-yellow)'>depends on the distribution</span> of the original data, for **heavily skewed distributions a large sample size is needed**.

But in general the <b><mark style='background:var(--mk-color-green)'>larger the sample size the better</mark></b>.
<div style="page-break-after: always;"></div>

# Confidence Intervals
---
CLT is what is needed to compute the **normal-based confidence intervals**.

<span style='color:var(--mk-color-turquoise)'>Confidence intervals</span> are range of plausible values which we are certain contains the true population parameter.

The standard, <span style='color:var(--mk-color-orange)'>confidence interval formula</span> is: $\text{Point Estimate} \pm \text{(Margin of Error)}$.
><span style='color:var(--mk-color-turquoise)'>Point estimate</span> is the **mean difference of the 2 groups** (*Or what is stated in the question*).

The formula to <span style='color:var(--mk-color-orange)'>calculate margin of error</span> is:
$$
\text{Margin of Error} = Z_{\text{Confidence interval}} \times \frac{\sigma}{\sqrt{n}}
$$
**Where:**
- $Z$ is the **z-score** based on the **confidence interval**
- $\sigma$ is the standard deviation

In general confidence interval is $\text{Point estimate} \pm \text{Critical value} * \text{Standard error}$

**To do this in R studio**:
```R
# Example to compute a 90% confidence interval
n <- length (X) # Get the number of entries
lower_limit <- mean (X) + qnorm (0.05)* sd(X)/ sqrt (n)
upper_limit <- mean (X) - qnorm (0.05)* sd(X)/ sqrt (n)
```

The **larger the confidence interval**, the <span style='color:var(--mk-color-yellow)'>larger the margin</span>, since the bigger the range the higher the probability the true value will fall within the range.

> [!fail] Drawbacks to Confidence Intervals
> Similar to p-value it depends on the distribution of the population data. If it is <span style='color:var(--mk-color-yellow)'>not normal or sample size is small</span> the validity is questionable. And like p-value, <span style='color:var(--mk-color-green)'>permutation testing solves this limitation</span>.
> 
> Another issue is that intervals are symmetric. Intervals from <span style='color:var(--mk-color-yellow)'>skewed distributions is not appropriate</span> or that the population mean is likely a larger value

For <span style='color:var(--mk-color-orange)'>non-normal distributions</span>, to **calculate the confidence interval,** it is <span style='color:var(--mk-color-yellow)'>good to use the percentile instead</span>. This is called bootstrap percentile.
<div style="page-break-after: always;"></div>

# Testing Methods
---
## Hypothesis Testing

Here is a recap on how to <span style='color:var(--mk-color-orange)'>carry out hypothesis testing</span>:
1) State the **null** ($H_{0}$) and **alternative** hypothesis ($H_{1}$)

> [!info] What to put for Null Hypothesis
> Follow this phrase, *"Innocent until proven guilty"*. 
> 
> Thus the null hypothesis should be the **opposite** of what the subject matter is

2) Pick a **level of significance** ($\alpha$), usually it is 0.05
3) Calculate the **test statistic** (*Something that can be calculated from the dataset*) & **P-value**
$$
\text{Test Statistic} = \frac{\text{Observed Difference}}{\text{Standard Error (SE)}}
$$
4) **Compare** P-value with level of significance
5) Interpret the decision
6) Check for assumptions
	- **Numerical Scale** - Outcome must be **numerical**
	- **Independence** - Observations are **independent** between the groups
	- **Normality** - Population data must follow the **normal distribution**

If the <span style='color:var(--mk-color-red)'>distribution is not normal</span> (*long tails*), it is good to <span style='color:var(--mk-color-yellow)'>use median or trimmed mean</span>, which is the mean after removing extreme values.

> [!summary] T-Distribution
> It consist of only 1 parameter which is called <span style='color:var(--mk-color-turquoise)'>degree of freedom</span>, which is the <span style='color:var(--mk-color-yellow)'>number of observations minus nnumber of groups</span>.

**T-test graph example**
![[T-test Graph Example.png|center|400]]

As long as the **test statistic is far from the null hypothesis**, then we can <span style='color:var(--mk-color-yellow)'>reject the null hypothesis</span>.
### Issues with Hypothesis Testing

**It is difficult to know the distribution of any test statistic**
> Given a test statistic, we <span style='color:var(--mk-color-red)'>might not know what type of distribution it follows</span>. It can be Z or T distribution.

**Assumptions might not be fully satisfied**
> If not all of the <span style='color:var(--mk-color-orange)'>3 assumptions</span> are satisfied, it can <span style='color:var(--mk-color-red)'>affect the accuracy of the p-value</span>. Other tests with **less assumptions** can be better.

**Interpretation of p-value is purely dichotomous**
> Given 2 p-values, 0.0499 and 0.0501. A <span style='color:var(--mk-color-red)'>small variation can lead to opposite conclusions</span> (*Reject or accept the null hypothesis*).

**P-value tells statistical significance**
> P-value tells if there is an effect but practical significance tells that the effect is meaningful in the real world. Thus <span style='color:var(--mk-color-red)'>p-value should not be the sole citron for decision making</span>. **Confidence intervals** provides a range of values for decision making.

**Type 1 and 2 errors**
> Type 1, is when the null hypothesis is true but it was rejected. For type 2, is when the null hypothesis is accepted but false in the population.
## Permutation Test

The goal of <span style='color:var(--mk-color-turquoise)'>permutation test </span>is to estimate how <span style='color:var(--mk-color-yellow)'>easily pure random chance</span> would produce a difference this large (*Check if chance is at play*).

Similar to hypothesis testing, but it <span style='color:var(--mk-color-green)'>does not require the test statistic distribution and has less assumptions</span>.
> The only assumption is **exchangeability**, defined as labels in the dataset <span style='color:var(--mk-color-yellow)'>can be reordered and not affecting the underlying joint distribution</span>.

The **assumption** is <span style='color:var(--mk-color-orange)'>naturally satisfied</span> if:
1) It is a randomised experiment
2) A random sample with no replacement

Carrying out <span style='color:var(--mk-color-orange)'>many permutations</span> will **normalise** the curve.

Here the assumption of a particular family of distributions for the population is not required. In particular **this test works well** when <span style='color:var(--mk-color-yellow)'>small sample size</span> or when the <span style='color:var(--mk-color-yellow)'>population does not follow normal distribution</span>. 

**Idea of permutation test**
1) Calculate the **original test statistic** (*based on the question*) 
2) Shuffle the groupings within the dataset
3) Without altering the order of the variables, copy them over and sort by groupings
4) Now the data has been jumbled up, calculate the test statistic and repeat the process
5) Using the **original test statistic** from the original dataset, find the p-value

The <span style='color:var(--mk-color-orange)'>p-value can be calculated</span> as such:
```R
pvalue <- mean(abs(perm_dist) >= abs(original))

# Note that perm_dist is a list of permuated test statistics
mean(abs(perm_dist) >= abs(original)) # Returns a list of true false values
```

To summarise, the code above calculates the <span style='color:var(--mk-color-turquoise)'>permutation threshold</span> which is just the <span style='color:var(--mk-color-yellow)'>mean of the original dataset</span>.  Then after the permutation testing, the <span style='color:var(--mk-color-orange)'>p-value</span> will be:
$$
\frac{\text{Number of entries above the permutation threshold}}{\text{Total number of entries}}
$$

Other than the permutation test, a <span style='color:var(--mk-color-turquoise)'>chi square test</span> can also be used if the **2 variables are categorical**.
# Bootstrapping
---
The idea of bootstrapping is to combat repeating experiments, <span style='color:var(--mk-color-red)'>replicating experiments can be expensive</span>.

Given a dataset of $N$ entries, sample $N$ number with replacements to create a <span style='color:var(--mk-color-turquoise)'>bootstrapped dataset</span>. Once done <span style='color:var(--mk-color-yellow)'>calculate the test statistic</span> and repeat. <b><mark style='background:var(--mk-color-yellow)'>This works for every statistic</mark></b>.

Visualising the mean values can give us a sense of <span style='color:var(--mk-color-yellow)'>how the mean will change if the experiment was repeated</span> a bunch of times. Thus <span style='color:var(--mk-color-green)'>no need to redo the experiment many times</span>.

And to <span style='color:var(--mk-color-orange)'>get the standard error</span>, just <span style='color:var(--mk-color-yellow)'>calculate the standard deviation</span> of the distribution of means from bootstrapping.
## Bootstrap Distribution

After caring out bootstrap many times, the test statistics calculated will show a <span style='color:var(--mk-color-turquoise)'>bootstrap distribution</span>.

**Uses of bootstrap distribution**
- The centre of <span style='color:var(--mk-color-orange)'>bootstrap distribution</span> for $\bar{X}$ is centred at approximately $\bar{X}$, the <span style='color:var(--mk-color-yellow)'>mean of the sample</span>
- The spread of the <span style='color:var(--mk-color-orange)'>bootstrap distribution </span>does reflect the spread of the <span style='color:var(--mk-color-yellow)'>sampling distribution</span>
- The bootstrap estimate does <span style='color:var(--mk-color-yellow)'>reflect the bias of the sampling distribution</span>. Bias occurs if a sampling distribution is not centred at the parameter (*Bias = Bootstrap mean - Sample mean*)

There is also something called <span style='color:var(--mk-color-turquoise)'>bootstrap standard error</span>, which is the <span style='color:var(--mk-color-yellow)'>bootstrap standard deviation</span>.

**Bootstrap percentile interval**
> A <span style='color:var(--mk-color-yellow)'>confidence interval of the true population mean</span>.

Bootstrap sampling is <span style='color:var(--mk-color-green)'>useful to quantifying the behaviour of a parameter estimate</span> such as the standard error, bias or for calculating confidence interval.

Bootstrap <span style='color:var(--mk-color-red)'>does not create new data</span>.
---
title: Dealing with Numerical Data
Date Created: 2024-04-23
Last Updated: 2025-09-27
tags:
  - GEA1000
  - Statistics
---
# Histograms
---
Unlike categorical data, numerical data tends to have an infinite range of possible values. Plotting the <span style='color:var(--mk-color-yellow)'>distribution</span> of numerical values in a <span style='color:var(--mk-color-yellow)'>table can be very long and difficult to understand</span>.

This is where a <span style='color:var(--mk-color-turquoise)'>historgram</span> is useful :
- It graphically displays a distribution
- Quick and easy to see trends
- Useful for large datasets

Before creating a histogram, first decide on the number of <span style='color:var(--mk-color-turquoise)'>bins</span> for the graph.
>A bin is a <span style='color:var(--mk-color-yellow)'>equal size intervals</span>. Can think of these as buckets where all data in range will be in this bin

The <span style='color:var(--mk-color-orange)'>size of the bin matters</span>
- Avoid histograms with <span style='color:var(--mk-color-yellow)'>large bin widths</span> that group data into only a <span style='color:var(--mk-color-yellow)'>few bins</span>.
- Avoid histograms with <span style='color:var(--mk-color-yellow)'>very small bin widths</span> that group data into <span style='color:var(--mk-color-yellow)'>too many bins</span>.

Construct histograms with different bin sizes to see which one is the most useful for our purpose.

**Histogram example**
![[Histogram Example.png|center]]

## Describing Distributions on Histograms

### Shape

The shape of the histogram has 2 categories, one is called <span style='color:var(--mk-color-turquoise)'>peaks</span> and the other is <span style='color:var(--mk-color-turquoise)'>skewness</span>.

For <span style='color:var(--mk-color-orange)'>peaks</span> of a histogram :
- If there is **only 1 distinct peak** it is called a <span style='color:var(--mk-color-turquoise)'>unimodal distribution</span>
- However if there are **more than 1 distinct peak**, it is called a <span style='color:var(--mk-color-turquoise)'>multimodal distribution</span> (Shown in the example above)

However with a <span style='color:var(--mk-color-orange)'>unimodal distribution</span> it can be further categorised into <span style='color:var(--mk-color-turquoise)'>symmetrical</span> or <span style='color:var(--mk-color-turquoise)'>skwed</span>.

**Unimodal distribution classification**
![[Unimodal Distribution Shape Classification.png]]

If given a <span style='color:var(--mk-color-orange)'>histogram that is rectangular</span>, then it is called a <span style='color:var(--mk-color-turquoise)'>uniform distribution</span>.

The symmetrical histogram is the normal distribution curve or bell curve.

The <span style='color:var(--mk-color-orange)'>characteristics of a histogram</span> can be described using the [[Basics of Statistics#Summary Statistics|measure of central tendency]].
![[Characteristics of Different Skewedness.png|center]]
### Spread

As discussed, the standard deviation is a good way to describe spread of data. However with histograms a naive way to understanding <span style='color:var(--mk-color-yellow)'>spread is through the range</span> which is $\text{max value} - \text{min value}$, but it <span style='color:var(--mk-color-red)'>can be misleading </span>without knowing the actual distribution
### Outliers

**Outliers**
>Observations that <span style='color:var(--mk-color-yellow)'>fall well above or well below </span>the overall bulk of data

**Histogram outlier example**
![[Histogram Outlier Example.png|center]]

Histograms that are **heavily skewed** or with **outliers** <span style='color:var(--mk-color-yellow)'>can affect the central tendency</span>
- Outliers can drastically increase or decrease the **mean**
- This is the same for the **standard deviation**

# Box Plot
---
The box plot consists of the <mark style='background:var(--mk-color-turquoise)'>5 number summary</mark> :
1) Minimum
2) Quartile 1 (25th percentile)
3) Median (50th percentile, **IQR**)
4) Quartile 3 (75 percentile)
5) Maximum

**Classification of outliers**
- If the value is **greater** than $\text{Q3} + 1.5 \times \text{IQR}$ 
- If the value is **smaller** than $\text{Q1} - 1.5 \times \text{IQR}$ 

**Box plot example :**
![[Bot Plot Example.png|center]]

The X refers to the **mean**, the bubbles at the top are **outliers** and the <span style='color:var(--mk-color-yellow)'>IQR gives an idea of the spread </span>for the middle 50% of the dataset.

**Some observations**
- The green box plot is **skewed to the right** because the <span style='color:var(--mk-color-yellow)'>lower half has less variability</span>
- The price overall has increased

**Box plot compared to Histograms**
![[Box Plot vs Histograms.png|center]]

# Bivariate Data
---
<span style='color:var(--mk-color-turquoise)'>Bivariate data</span> is just <span style='color:var(--mk-color-yellow)'>data on 2 specific variables</span> that are of interest / being analysed on.

If <span style='color:var(--mk-color-orange)'>2 variables are deterministic</span>
> They have a <span style='color:var(--mk-color-turquoise)'>deterministic relationship</span> as <span style='color:var(--mk-color-yellow)'>one variable can be determined with the knowledge of the other variable</span>. 

They are just straight line graphs, an example will be degree and Fahrenheit, knowing one can get the other.

However <span style='color:var(--mk-color-orange)'>most variables are not deterministic</span> but rather they can have a <span style='color:var(--mk-color-turquoise)'>statistical relationship</span>.

This means that there are <span style='color:var(--mk-color-yellow)'>variability between the 2 variables</span>. And to find this association, the **average value of one variable can be described given the value of the other variable**.

## Bivariate Data Analysis

One good visualisation tool to use is a <span style='color:var(--mk-color-turquoise)'>scatterplot</span> which can help <span style='color:var(--mk-color-yellow)'>give an idea of a trend or pattern</span>. 

Before plotting, **determine the 2 variables** to be used (Independent & Dependent variables)

**Scatterplot example**
![[Scatterplot Example.png|center]]

Then to <span style='color:var(--mk-color-orange)'>interpret</span> the scatterplot there are a <span style='color:var(--mk-color-orange)'>few ways</span> :

![[Direction of a Scatterplot.png|center]]

![[Form of a Scatterplot.png|center]]

![[Strength of a Scatterplot.png|center|600]]

![[Scatterplot Outliers.png|center]]
## Measurement of Association

Just by observation of the scatter plot the association can be observed but can this be<span style='color:var(--mk-color-yellow)'> numerically quantified</span>.
### Corelation Coefficient

It is the <span style='color:var(--mk-color-yellow)'>measure of the linear association</span> and it also summarises the <span style='color:var(--mk-color-yellow)'>direction</span> and the <span style='color:var(--mk-color-yellow)'>strength</span> of the association.

The <span style='color:var(--mk-color-yellow)'>range</span> of the <span style='color:var(--mk-color-turquoise)'>corelation coefficient</span> is between 1 and -1.

The <span style='color:var(--mk-color-orange)'>quantification of corelation coefficient</span> is called the<span style='color:var(--mk-color-turquoise)'> R-value</span> :
- $r \lt 0$, means there is a <span style='color:var(--mk-color-red)'>negative</span> linear association
- $r \gt 0$, means there is a <span style='color:var(--mk-color-green)'>positive</span> linear association
- $r = 1$, means there is a **perfect** <span style='color:var(--mk-color-green)'>positive</span> linear association
- $r = -1$, means there is a **perfect** <span style='color:var(--mk-color-red)'>negative</span> linear association
- $r = 0$, means there is <span style='color:var(--mk-color-yellow)'>no linear association</span>, but it **does not mean there is no association**

For **non linear graphs** it is <span style='color:var(--mk-color-yellow)'>better to look at the histogram</span> rather than the creation coefficient.

Having a <span style='color:var(--mk-color-yellow)'>strong corelation does not mean causation</span> as other variables might have some effect.

**Determining the strength of the linear association**
![[Strength of Linear Association.png|center]]

As the R-value gets closer to 1 or -1, then the data will fall more closely to a straight line in the scatter plot.

One thing about the R-value is that :
- It is <span style='color:var(--mk-color-yellow)'>not affected</span> if the $x$ and $y$ **axis interchange**
- It is <span style='color:var(--mk-color-yellow)'>not affected</span> by **adding a constant to all values**
- it is <span style='color:var(--mk-color-yellow)'>not affected</span> by **multiplying a constant to all values**

However if the data has <span style='color:var(--mk-color-red)'>outliers</span>, the <span style='color:var(--mk-color-yellow)'>strength</span> of the correlation may <span style='color:var(--mk-color-yellow)'>increase or decrease</span>.

**How to calculate correlation coefficient**

Firstly, convert each $x$ and $y$ value into its <span style='color:var(--mk-color-yellow)'>standard unit</span> (SU).
$$
SU_{x}  =\frac{x - \bar{x}}{S_{x}} 
$$
$$
SU_{y}  =\frac{y - \bar{y}}{S_{y}} 
$$
**Where :**
$\bar{x}$ and $\bar{y}$ are the mean or **average for the x and y variable**
$S_{x}$ and $S_{y}$ is the **standard deviation for the x and y variable**

To <span style='color:var(--mk-color-orange)'>calculate the R-value</span> :
$$
r = \frac{\sum{SU_{x} \times SU_{y}}}{n - 1}
$$
**Where :**
- The numerator is to take each (x, y) pairs standard unit and multiply them together then afterwards summing it up.
### Ecological Correlation

The idea of <span style='color:var(--mk-color-turquoise)'>ecological correlation</span> is to <span style='color:var(--mk-color-yellow)'>group people by ethnicity, race, nationality, high / low income</span> (Any form of grouping conditions). This is implies <span style='color:var(--mk-color-yellow)'>relationships observe at the aggregate level based on group characteristics</span>.

This <span style='color:var(--mk-color-yellow)'>corelation is based on the aggregate</span> of groups rather than on a individual level such as using group averages or group rates.

**Ecological Fallacy**
> States that corelations observed at a aggregate level is <span style='color:var(--mk-color-yellow)'>not the same</span> as individual level

**Ecological fallacy example**
![[Ecological Fallacy Example.png|center|500]]
- Based on the different **aggregate groups and their average values**, it <span style='color:var(--mk-color-yellow)'>yields a positive linear association</span> (<span style='color:var(--mk-color-teal)'>blue line</span>)
- One might think it will hold for **each aggregate group**, however each group is a <span style='color:var(--mk-color-yellow)'>negative linear association</span> (<span style='color:var(--mk-color-red)'>red line</span>)

**Atomistic Fallacy :**
> It is the **opposite of ecological fallacy**, where the <span style='color:var(--mk-color-yellow)'>corelation based on individuals is used to generalise for aggregate-level correlation</span>
# Linear Regression
---
The idea of <span style='color:var(--mk-color-turquoise)'>linear regression</span> is <span style='color:var(--mk-color-yellow)'>based on the corelation</span> of the data, is there a way to generalise the <span style='color:var(--mk-color-yellow)'>prediction</span> of a new value.

The model has a relationship of a straight line which is $y = mx + c$
- $m$ is the gradient or <span style='color:var(--mk-color-yellow)'>the amount of change</span> in $y$ <span style='color:var(--mk-color-yellow)'>for every 1 unit increment</span> of $x$

In maths, $x$ can be in terms of $y$ but in a <span style='color:var(--mk-color-red)'>linear regression it cannot work</span>. It cannot use $y$ to predict a value of $x$.

In any scatterplot, the <span style='color:var(--mk-color-yellow)'>best fit line will be the linear regression model</span> but to get this best fit line the <span style='color:var(--mk-color-turquoise)'>least squares method </span>is used.

One thing to take note of when estimating is <span style='color:var(--mk-color-turquoise)'>extrapolation</span> which is estimating something by <span style='color:var(--mk-color-yellow)'>assuming that existing trends will continue out of the observed range</span>. For example if the model is built in range X$[1, 10]$, then predicting $y$ with an $x$ value of 20 might <span style='color:var(--mk-color-red)'>not be accurate</span>.

Using a **linear regression on a non linear histogram** <span style='color:var(--mk-color-red)'>might be inaccurate</span>
## Least Squares Method

The **best fit line** <span style='color:var(--mk-color-yellow)'>aims to minimise the sum square of the error</span> for every single data point. An <span style='color:var(--mk-color-turquoise)'>error</span> is the <span style='color:var(--mk-color-yellow)'>difference between the observed data point and the predicted data point</span>.

![[Example of the Best Fit Line.png|center]]

This minimisation is <span style='color:var(--mk-color-yellow)'>done for all of the data points</span>.

This can be quite tedious, thus there is a <span style='color:var(--mk-color-orange)'>relationship between the R-value and the slope/gradient</span> which  is given as such :
$$
m = \frac{S_{y}}{S_{x}} \times r
$$
**Where :**
- $S_{x}$ and $S_{y}$ is the **standard deviation**
- $r$ is the R-value or the **corelation coefficient**

Do not get confused as $m \neq r$ in general.

If the **graph is exponential**, then the <span style='color:var(--mk-color-yellow)'>natural logarithm can be use</span> to fit the linear regression model.
- Given $y = ab^{x}$
- Then $\ln{y} = \ln{ab^{t}} = \ln{a} + \ln{b^{x}} = \ln{a} + x\ln{b}$ 
- Then it is very <span style='color:var(--mk-color-yellow)'>similar to the linear equation</span> $y = mx + c$. $\ln{b} = m$ and $\ln {a} = c$
- Here the l<span style='color:var(--mk-color-yellow)'>inear regression values</span> of $m$ and $c$ can be <span style='color:var(--mk-color-yellow)'>used in the above formula</span>
- Which will result in $\ln {y} = e^{m}x + e^{c}$
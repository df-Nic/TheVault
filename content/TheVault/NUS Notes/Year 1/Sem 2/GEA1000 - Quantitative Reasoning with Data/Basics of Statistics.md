---
title: Basics of Statistics
Date Created: 2024-02-01
Last Updated: 2025-09-27
tags:
  - GEA1000
  - Statistics
---
# Population & Sample
---
<mark style='background:#0fb9b1'>Population</mark> - Is an <span style='color:#f7b731'>entire group of individuals</span> or objects that <span style='color:#f7b731'>are of interest</span>.

<mark style='background:var(--mk-color-turquoise)'>Population Parameter</mark> - It is a <span style='color:var(--mk-color-yellow)'>numerical fact about a population</span>, which are usually constants

<mark style='background:#0fb9b1'>Sample</mark> - Unlike a population a sample is a <span style='color:#f7b731'>smaller subgroup</span> of the intended population.

<mark style='background:var(--mk-color-turquoise)'>Estimate</mark> - It is a <span style='color:var(--mk-color-yellow)'>numerical fact derived from the sample</span>, to **represent the population** 

Most of the time, if a census is not carried out, <span style='color:#eb3b5a'>it can be difficult to get the population</span>.
# Research Question
---
A <span style='color:#0fb9b1'>research question</span> is one that seeks to <span style='color:#f7b731'>investigate</span> some sort of <span style='color:#f7b731'>characteristics from a population</span>.

**For example** : Number of people in Singapore who own a car.
## Types of Research Questions

There are <span style='color:#fa8231'>different types of questions</span> based on the researches goal or aim :
1) Making an <span style='color:#f7b731'>estimate</span> on the population (Average, Proportion)
2) <span style='color:#f7b731'>Test a claim</span> about the population
3) <span style='color:#f7b731'>Compare</span> two different groups in a population
4) Investigate a <span style='color:#f7b731'>relationship between two groups</span> in a population
# Exploratory Data Analysis
---
Currently **data** consists of <span style='color:var(--mk-color-yellow)'>many variables</span> and not just one. And to understand the data, <span style='color:var(--mk-color-turquoise)'>EDA</span> is used to explore the raw data.

With this <span style='color:var(--mk-color-orange)'>data can be summarised</span> by using :
- **Graphs**
- **Numerical values** like percentages

**Steps in EDA**
1) To <span style='color:var(--mk-color-yellow)'>start generate some questions</span> to answer with the existing data set given
2) **Understand data** using <span style='color:var(--mk-color-yellow)'>visualisation</span> tools to <span style='color:var(--mk-color-yellow)'>observe key trends</span> and carry out <span style='color:var(--mk-color-yellow)'>data modeling</span> like linear regression
3) Then finally **does the analysis answer** the questions set
4) Now either refine the question or ask new ones and repeat the process

Some questions might not get answered but the <span style='color:var(--mk-color-orange)'>goal</span> is to <span style='color:var(--mk-color-yellow)'>get some useful questions answered</span>.

# Sampling
---
**Sampling frame**
>The <span style='color:var(--mk-color-yellow)'>method</span> or a <span style='color:var(--mk-color-yellow)'>list of criteria</span> in which to obtain the samples (Phone numbers, emails, age)

**Target population**
>It is the group of people in which the observation is interested in (NUS students who take public transport)

It will be <span style='color:var(--mk-color-yellow)'>ideal</span> to have the <span style='color:var(--mk-color-yellow)'>sampling frame completely overlap the target population</span>. This means that the sample is the population, but however this is not the case

Some <span style='color:var(--mk-color-orange)'>issues</span> that can arise from the **choice of sampling frame** :
- Sometimes the sampling frame might <span style='color:var(--mk-color-yellow)'>exclude certain people from the terget population</span>
- And conversely it can also <span style='color:var(--mk-color-yellow)'>include people outside the target population</span>

Getting a perfect coverage can be difficult, but as long as the <span style='color:var(--mk-color-yellow)'>data obtained</span> from the sample is <span style='color:var(--mk-color-turquoise)'>generalisable</span> to a bigger group of people preferably the <span style='color:var(--mk-color-yellow)'>target population</span> then the sample is good.

A <span style='color:var(--mk-color-orange)'>criteria for generalisability</span> is
>The sampling frame must be <span style='color:var(--mk-color-yellow)'>bigger or equals</span> to the target population. If it is <span style='color:var(--mk-color-yellow)'>smaller then</span> some members in the population will be left out and it <span style='color:var(--mk-color-red)'>cannot be generalised</span>
- Good sampling frame
- Probability based sampling
- Large sample size
- Minimise non-response bias
## Census vs Sample

**Census**
>It is the attempt to reach out to the <span style='color:var(--mk-color-yellow)'>whole population</span>

However in most cases (Unless government surveys) a <span style='color:var(--mk-color-orange)'>sample is preferred</span> because :
1) It is <span style='color:var(--mk-color-green)'>less costly</span> administratively 
2) It is <span style='color:var(--mk-color-green)'>faster to process data</span> from a sample than from a census since there are less data entries
## Sampling Biases

When sampling there are <span style='color:var(--mk-color-orange)'>2 types of biases</span> :
1) **Selection bias**
<span style='color:var(--mk-color-turquoise)'>Selection bias</span> occurs when certain people from the <span style='color:var(--mk-color-yellow)'>target population</span> are <span style='color:var(--mk-color-yellow)'>not part of the sampling frame</span> (**Imperfect sampling frame**).

Another reason is because of **non-probability sampling**, it means that the <span style='color:var(--mk-color-yellow)'>choice of participants are not by chance</span>. This can cause <span style='color:var(--mk-color-yellow)'>skewed missunderstanding</span> as a group can be left out.

2) **Non-response bias**
Some reason for this is through participants that are <span style='color:var(--mk-color-yellow)'>not interested</span> or they might <span style='color:var(--mk-color-yellow)'>not show up</span> because of reasons or <span style='color:var(--mk-color-yellow)'>does not want to reveal information</span>.

This can <span style='color:var(--mk-color-red)'>distort the understanding</span> of the population in any **study**, and it can happen any time. 
## Sampling Techniques
### Probability Sampling

The idea of <span style='color:var(--mk-color-turquoise)'>probability based sampling</span> is to implement an element of <span style='color:var(--mk-color-yellow)'>randomness</span> to <span style='color:var(--mk-color-yellow)'>prevent selection biases</span> from people.

The **randomised mechanism** is <span style='color:var(--mk-color-yellow)'>known</span> and the <span style='color:var(--mk-color-yellow)'>selection probability can be different</span> throughout all units of the sampling frame.

There are <span style='color:var(--mk-color-orange)'>4 types of probability sampling</span> :
1) Simple Random Sampling
The idea behind this is to <span style='color:var(--mk-color-yellow)'>randomly select</span> people in the sampling frame <span style='color:var(--mk-color-yellow)'>without replacement</span>. A random number generator can be used to do the selection.

The **random generator** must have an <span style='color:var(--mk-color-yellow)'>equal probability in selecting</span> one person in the entire sample to ensure results do not change haphazardly between samples.

|         <span style='color:var(--mk-color-green)'>Advantages</span>          | <span style='color:var(--mk-color-red)'>Disadvantages</span> |
| :--------------------------------------------------------------------------: | :----------------------------------------------------------: |
| Samples are a good representation of the population<br>because of randomness |               Non-response biases is a problem               |
|                              Easy to carry out                               |         Accessabiliy to participants can be an issue         |

2) **Systematic Sampling**
The idea is to <span style='color:var(--mk-color-yellow)'>apply a selection interval</span> $K$, and <span style='color:var(--mk-color-yellow)'>random starting point </span>from first interval.

Basically given a sample: 
- Partition into groups of $K$ 
- Using a random number generator, from 0 to $K$ lets call this number $x$
- The $x$ person from each partition will be selected

| <span style='color:var(--mk-color-green)'>Advantages</span> |                        <span style='color:var(--mk-color-red)'>Disadvantages</span>                        |
| :---------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------: |
| The selection process is simpler since it is <br>systematic | It is possible that the sample selected does not represent<br>the population if the list is not randomised |
|        There is no need to know the population size         |                                                                                                            |

3) Stratified Random Sampling
The idea is that <span style='color:var(--mk-color-yellow)'>people who have similar characteristic</span> are group together known as <span style='color:var(--mk-color-turquoise)'>strata</span>. And the characteristics vary between strata.

The size is not a must to be the same. Once done, it will use a <span style='color:var(--mk-color-yellow)'>simple random sampling in each stratum</span>.

|                        <span style='color:var(--mk-color-green)'>Advantages</span>                        | <span style='color:var(--mk-color-red)'>Disadvantages</span> |
| :-------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------: |
| If done correctly, the selection will be a good representation if the stratum is similar to the interests |    Process of grouping and random sampling can be tedious    |
|                                                                                                           |    Needs information about the sampling frame and strata     |
4) **Cluster Sampling**
The idea is to just <span style='color:var(--mk-color-yellow)'>group</span> the sample into <span style='color:var(--mk-color-yellow)'>same sized clusters</span>. Then randomly <span style='color:var(--mk-color-yellow)'>choose</span> a fixed number of <span style='color:var(--mk-color-yellow)'>clusters</span>.

| <span style='color:var(--mk-color-green)'>Advantages</span> |                                 <span style='color:var(--mk-color-red)'>Disadvantages</span>                                 |
| :---------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------: |
|        If It is less costly and less time consuming         | Not effective if there are too little clusters or <br>if they are not similar to each other. This can cause high variability |
### Non-Probability Sampling

These types of sampling <span style='color:var(--mk-color-yellow)'>does not include any element of randomness</span>.

There are <span style='color:var(--mk-color-orange)'>2 types of non probability sampling</span> :
1) **Convenience sampling**
The selection process is based on <span style='color:var(--mk-color-yellow)'>proximity and availability</span>. For example surveys done in a mall.

However this leads to a few <span style='color:var(--mk-color-red)'>issues</span> :
1) **Selection bias**, because getting whoever is available does not necessary mean it represent the population
2) **Non-repones bias**, people can choose not to participate

2) **Volunteer Sampling**
Instead of approaching other, <span style='color:var(--mk-color-yellow)'>researches seek volunteers</span> to participate in the research.

However this leads to a few <span style='color:var(--mk-color-red)'>issues</span> :
1) **Selection bias**, for example study on the essential of electronics for studies, might only attract the rich to participate
2) **Non-repones bias**, same example, poor people might not feel comfortable disclosing their financial instability

# Variables
---
**Variable**
>An attribute that can be measured or labelled

There are <span style='color:var(--mk-color-orange)'>2 sets of variables</span>
1) **Independent variable**
	>A variable that is <span style='color:var(--mk-color-yellow)'>subjected to manipulation</span> (deliberately or spontaneously) in a study

2) **Dependent variable**
	>A <span style='color:var(--mk-color-yellow)'>variable which is hypothesised to change</span> depending on how the **independent variable is manipulated** in a study

## Types of Variables

<span style='color:var(--mk-color-orange)'>Knowing the type of variable</span> is important as different types <span style='color:var(--mk-color-yellow)'>decides what visualisation tool to use</span> to examine the data.

There are <span style='color:var(--mk-color-orange)'>2 types of variables</span> :
1) **Categorical variable**
	>They are **label values** which are <span style='color:var(--mk-color-yellow)'>mutually exclusive</span>. Data entries of categorical data <span style='color:var(--mk-color-yellow)'>can only have one</span> of these labels

It can be further categorised into <span style='color:var(--mk-color-turquoise)'>ordinal</span> and <span style='color:var(--mk-color-turquoise)'>nominal</span>. 

**Ordinal categorial variable** has some <span style='color:var(--mk-color-yellow)'>natural ordering</span> to it and is often represented by numbers.

**Nominal categorical variable** has <span style='color:var(--mk-color-yellow)'>no ordering</span>, basically all other cases.

2) **Numerical variable**
	>They are **numerical values** where <span style='color:var(--mk-color-yellow)'>arithmetic operation can be</span> done and it makes sense.

It can be further categorised into <span style='color:var(--mk-color-turquoise)'>discrete</span> and <span style='color:var(--mk-color-turquoise)'>continuous</span>. 

**Discrete numerical variable** is possible values that form a set with **gaps**, basically <span style='color:var(--mk-color-yellow)'>whole numbers</span>.

**Continuous categorical variable** are variables that can <span style='color:var(--mk-color-yellow)'>take any possible value</span> given a range or interval.

# Summary Statistics
---
The key point of this is to <span style='color:var(--mk-color-yellow)'>summarise quantitative data </span>, which simple data visualisation cannot achieve.

<span style='color:var(--mk-color-turquoise)'>Summary statistics</span> focuses on <span style='color:var(--mk-color-orange)'>2 main ideas</span> :
1) **Measures of central tendency** (Center of the collection of values)

**Mean**
>It is the <span style='color:var(--mk-color-yellow)'>average value</span> within a collection of data points. It is denoted by $\bar x$

<span style='color:var(--mk-color-yellow)'>Adding a constant</span> value to all values, will <span style='color:var(--mk-color-yellow)'>increase the mean by that constant</span>, same goes for **multiplication**.

The **mean** can give us the <span style='color:var(--mk-color-yellow)'>total amount</span> for a given period but it <span style='color:var(--mk-color-red)'>does not tell the distribution</span>.

**Weighted average**
>Given 2 subgroup means, the <span style='color:var(--mk-color-yellow)'>average of these 2 sub groups</span> is called the weighted average

How to <span style='color:var(--mk-color-orange)'>calculate</span> the <span style='color:var(--mk-color-orange)'>weighted average</span>
- Given 2 sub groups $A$ with a total of 349 people and a average of $32.21$
-  $B$ with a total of 46 people and a average of $30.72$
$$
\text{Weighted average} = \frac{349}{395} \times 32.21 + \frac{46}{395} \times 30.72 = 32.04 
$$

<span style='color:var(--mk-color-red)'>Cannot sum the 2 means and divide by 2</span>, because the <span style='color:var(--mk-color-yellow)'>proportion is different</span>. Only if they are the same then this will work.

Calculating **proportion** (%) is also a<span style='color:var(--mk-color-yellow)'> form of mean</span>, for example 100 out of 1000 people are happy, then the proportion 0.1 is considered as a mean. This <span style='color:var(--mk-color-turquoise)'>weighted mean</span> will be closer to the larger subgroup.

**Median**
>Defined as the <span style='color:var(--mk-color-yellow)'>middle value</span> of a variable after sorting in ascending/descending order

<span style='color:var(--mk-color-yellow)'>Adding a constant</span> value to all values, will <span style='color:var(--mk-color-yellow)'>increase the median by that constant</span>, same goes for **multiplication**.

And the <span style='color:var(--mk-color-yellow)'>median between 2 subgroups does not tell anything</span> other than that it must be between the median of the 2 sub groups.

**Mode**
>The <span style='color:var(--mk-color-yellow)'>value</span> that appears the <span style='color:var(--mk-color-yellow)'>most frequently</span>. This can be considered as the **peak of a distribution**

2) **Measures of dispersion** (Spread)

**Standard Deviation**
>This is one of the ways to quantify the <span style='color:var(--mk-color-yellow)'>spread of the data about the mean</span>, and this is derived from the variance

$$
\text{Sample Variance} = \frac{(x_{1} - \bar{x})^{2} + (x_{2} - \bar{x})^{2} + \dots + (x_{n} - \bar{x})^{2}}{n - 1}
$$
$$
\text{Standard Deviation} = S_{x} = \sqrt{\text{Variance}}
$$
Even though, <span style='color:var(--mk-color-yellow)'>SD</span> tells the spread, it <span style='color:var(--mk-color-yellow)'>only applies on average</span>, it does not mean the max value is mean + SD.

<span style='color:var(--mk-color-yellow)'>Adding a constant</span> value to all values, will <span style='color:var(--mk-color-yellow)'>will not change the standard deviation</span>, as it is just shifting all point by the same amount.

However it is **not the same for multiplication**, by multiplying a constant $C$, the <span style='color:var(--mk-color-yellow)'>SD will be multiplied by</span> $\vert C \vert$. Because multiplication does not evenly shit all points.

**Coefficient of variation**
><span style='color:var(--mk-color-yellow)'>Comparing 2 SD does not work</span> because the <span style='color:var(--mk-color-yellow)'>means can be different</span>,  Thus this coefficient provides a way of quantifying the spread relative to the mean

$$
\text{Coefficient of Variation} = \frac{S_{x}}{\bar{x}}
$$
**Where :**
- $\bar{x}$ or the mean cannot be 0

**Interquartile range**
The <span style='color:var(--mk-color-turquoise)'>first quartile</span> usually denoted by Q1 is the <span style='color:var(--mk-color-yellow)'>25th percentile</span> of the data values.
The <span style='color:var(--mk-color-turquoise)'>third quartile</span>, usually denoted by Q3 is the <span style='color:var(--mk-color-yellow)'>75th percentile</span> of the data values.
The <span style='color:var(--mk-color-turquoise)'>second quartile</span> or **median** denoted by Q2 is the <span style='color:var(--mk-color-yellow)'>50th percentile</span> of the data values.

The <span style='color:var(--mk-color-turquoise)'>inter quartile range</span> is the <span style='color:var(--mk-color-yellow)'>difference</span> between Q3 and Q1
- The **larger** the value the bigger the spread
- The **smaller** the value the smaller the spread

**How to find Q1 or Q3**
- First **find the median** (Q2)
- Secondly, get all points that are $\lt$ the median
- Now with this <span style='color:var(--mk-color-yellow)'>new set find the median value</span> and this will be Q1
- Repeat the same for $\gt$ median for Q3

<span style='color:var(--mk-color-yellow)'>Adding a constant</span> value to all values, will <span style='color:var(--mk-color-yellow)'>will not change the standard deviation</span>, but multiplying by a constant  $C$, the <span style='color:var(--mk-color-yellow)'>SD will be multiplied by</span> $\vert C \vert$.
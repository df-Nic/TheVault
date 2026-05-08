---
title: Average Case Analysis
Date Created: 2024-09-07
Last Updated: 2025-09-28
tags:
  - CS3230
  - AlgorithmAnalysis
---
# Why Take the Average?
---
In some cases, the <span style='color:var(--mk-color-red)'>worst case</span> possible time happens for some <b><span style='color:var(--mk-color-red)'>very small number of inputs</span></b>. And for the **majority**, it will <span style='color:var(--mk-color-green)'>run significantly better</span>. Therefore it will be <span style='color:var(--mk-color-green)'>better to show the average time complexity</span> of this algorithm.

Therefore the **expected running time** should be the **same as the average running time**, when the <b><span style='color:var(--mk-color-yellow)'>permutation of the inputs is chosen uniformly at random</span></b>.

Algorithms will be **deterministic**.

The **average time complexity** in general can be <span style='color:var(--mk-color-orange)'>computed</span> as such:
$$
A(n) = \sum_{\pi} \frac{1}{n!} \times (\text{Running time of the algorithm with input } \pi)
$$
**Where:**
- $\pi$ is a set of <span style='color:var(--mk-color-yellow)'>all possible permutations</span> of the input size $n$
- $1 / n!$ is the <span style='color:var(--mk-color-yellow)'>probability of a permutation</span> is selected and <span style='color:var(--mk-color-red)'>not average</span>


# Quicksort Analysis
---
[[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Sorting#Quicksort|Quicksort]] is one the few algorithms who's **runtime depends on the pivot that was selected**.

> [!abstract] Importance of the Pivot
> The pivot selected is important as the **recurrence of quicksort** is as follows:
> $$
> T(n) = T(j - 1) + T(n - j) + cn
> $$
> **Where:**
> - $j$ is the pivot point who is the <span style='color:var(--mk-color-yellow)'>jth smallest element</span>.
> 
> The worst case is when the pivot is the <b><span style='color:var(--mk-color-red)'>smallest or the biggest element</span></b>. Which will give a recurrence of $T(n) = T(0) + T(n-1) + cn \in \Theta(n^{2})$.

The **probability** of getting a bad pivot is $\frac{2}{n}$ this shows that the <span style='color:var(--mk-color-yellow)'>majority of the pivot is a better choice</span>.

Now notice that the **time complexity** depends on the <b><mark style='background:var(--mk-color-yellow)'>permutation of the array</mark></b> and not the values itself. This is because the **pivot** only shifts the numbers left or right which **gives a new permutation for the next step**.

The <span style='color:var(--mk-color-orange)'>average case for quicksort</span> will be as such:
$$
A(n) = \frac{1}{n} \sum^{n}_{i = 1} (T(j - 1) + T(n - j) + cn)
$$
**Where:**
- $1 / n$ is the <span style='color:var(--mk-color-yellow)'>probability</span> of a element being chosen at random for the **pivot**
- $cn$ is just the **cost of merging and splitting**.

Since the **initial permutation of the input is uniformly random**, then after partitioning, the <span style='color:var(--mk-color-yellow)'>2 sides will also be uniformly at random</span> as well.

# How to tackle avg case Questions

1) Define **indicator random variables**

2) Find the expected value of the IRV (Probability)

Possibly find all permutations of input size of $n$.

Linearity of expectation and expected value
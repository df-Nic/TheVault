---
title: Algorithm Analysis
Date Created: 2023-06-20
tags:
  - CS2040
  - TimeComplexity
---
# Table of Contents
---
- [[#Algorithms|Algorithms]]
	- [[#Algorithms#Properties|Properties]]
	- [[#Algorithms#Calculating Efficiency|Calculating Efficiency]]
- [[#Big O Notation|Big O Notation]]
	- [[#Big O Notation#Asymptotic Analysis|Asymptotic Analysis]]
	- [[#Big O Notation#Analysis Of Cases|Analysis Of Cases]]
---

# Algorithms
---

## Properties

1. Exact
Each step in the algorithm cannot be ambiguous
2. Terminate
It must stop eventually
3. Effective
In terms of time complexity. The complexity of the algorithm
4. General
It must work for all possible inputs

**Pseudocode**
>Its to write code in detail in terms of code be it in English.

## Calculating Efficiency

Efficiency of an algorithm means the <b><span style='color:#3867d6'>complexity</span></b> of it. More specifically, the <b><span style='color:#3867d6'>time and space complexity</span></b>.

<b><span style='color:#f7b731'>Run time is not time complexity</span></b>, because run time as it depends on the compiler and other factors. It should be determined by the number of primitive operations or the number of statements executed.

**Growth Rate**
> How many operations executed grows as N (input) increases in size

N has to be large to see the effect of the growth rate as small input size will not have a significant impact.

# Big O Notation
---

## Asymptotic Analysis

It is used to analyze problems of large input sizes and considering only the <b><span style='color:#3867d6'>leading term</span></b>  and <b><span style='color:#3867d6'>ignoring coefficients</span></b>. 

An upper bound is any bound that is greater than f(n). However we want the <b><span style='color:#3867d6'>tightest bound</span></b> to f(n).

**Note**
> Any base for log will be simplified to just log n as we can change bases.

![[Comparison of growth-rates.png]]

## Analysis Of Cases

- <b><span style='color:#eb3b5a'>Worst Case</span></b>
The worst case is what interest people the most.

It determines the <mark class="hltr-yellow">maximum</mark> time needed to solve a problem for a input of size N.

- <b><span style='color:#20bf6b'>Best Case</span></b>
The fastest time an algorithm needs, however it is not useful.

- <b><span style='color:#2d98da'>Average Case</span></b>
Determine the time needs to solve an average input of N.

Average is determined by the probability distribution of inputs.

- <b><span style='color:#4b6584'>Expected Case</span></b>
It is used for algorithms that employ randomness in it.

- <b><span style='color:#3867d6'>Amortized Analysis</span></b>
Within a large sample of runs, not every run will induce the worst case behavior, sometimes it can be better.

Thus this analysis determins the total time complexity required for a series of runs.




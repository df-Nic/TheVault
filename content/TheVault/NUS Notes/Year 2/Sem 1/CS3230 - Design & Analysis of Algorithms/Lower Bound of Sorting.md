---
title: Lower Bound of Sorting
Date Created: 2024-09-07
Last Updated: 2025-09-28
tags:
  - CS3230
  - AlgorithmAnalysis
  - Sorting
---
# Brief Recap on Sorting
---
Given an array ($A$) that **contains random elements**, **arrange** it in such a way that all elements in $A$ are in a **non-decreasing order** (*Or increasing depending on the situation*).

> [!example] 
> Here are some of the [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Sorting|sorting algorithms]] with the <span style='color:var(--mk-color-red)'>worst case</span> time complexities.
> 1) **Insertion Sort** - O($n^{2}$) in the worst case
> 2) **Selection Sort** - O($n^{2}$) in the worst case
> 3) **Merge Sort** - O($n \log n$) in the worst case
> 4) **Heap Sort** - O($n \log n$) in the worst case
> 5) **Quick Sort** - O($n^{2}$) in the worst case

All of these are <span style='color:var(--mk-color-turquoise)'>comparison based</span> sorting algorithms where <span style='color:var(--mk-color-yellow)'>only comparisons</span> between each other <span style='color:var(--mk-color-green)'>are allowed</span>, `< or <= or == or > or >=`.
# Can We Do Better?
---
The claim is that <span style='color:var(--mk-color-orange)'>any comparison base sorting algorithm</span> <b>will be at best</b>, $\Omega(n \log n)$.

Lets use a **decision tree**:
![[Visualising Sorting with a Decision Tree.png|center|500]]

> [!question] How does it Work?
> A **comparison based algorithm** can be <span style='color:var(--mk-color-orange)'>modeled</span> as such:
> - A **comparison between 2 elements** will be made (*This is the <span style='color:var(--mk-color-yellow)'>node</span>*)
> - The **state is determined by the result of the comparision** (*<span style='color:var(--mk-color-yellow)'>Chosen child</span> depends on the result*)
> - The **order of the elements** at the end of the algorithm (*Done at the <span style='color:var(--mk-color-yellow)'>leaf</span>*)
> 
> Therefore the **leaves** contains <span style='color:var(--mk-color-yellow)'>all possible permutations</span> of the input array.

By observation, the <span style='color:var(--mk-color-red)'>worst case</span> will be to **traverse the maximum height** of the tree.

The **total number of permutations** is $n!$ and with a decision tree the **height** will be, $\log (n!)$, and by using <span style='color:var(--mk-color-blue)'>Stirling's approximation</span>, it will be $n \log n$.
# Non-Comparison Sorting
---
Is there a way to <span style='color:var(--mk-color-orange)'>break this lower bound</span>? It is possible but we <span style='color:var(--mk-color-red)'>cannot do it entirely with comparison</span> and other conventions are required.

One such sorting algorithm is called <span style='color:var(--mk-color-teal)'>radix sort</span> or <span style='color:var(--mk-color-teal)'>bin sorting</span>. Which runs with a time complexity of <b><mark style='background:var(--mk-color-green)'>O(n + k)</mark></b>. Where $k$ is the <span style='color:var(--mk-color-yellow)'>largest element in the array</span>.

> [!question] How does Radix Sort Work?
> Firstly, inorder to use <span style='color:var(--mk-color-teal)'>radix sort</span>, first we need to know the values in the array **fall within a range from 0 to k**, where <span style='color:var(--mk-color-yellow)'>k is the maximum element</span>.
> 
> Then we will **just do the following**:
> - Have an a**rray of size** $k$
> - For each number from 0 to k, <span style='color:var(--mk-color-yellow)'>count how many instances</span> that appears in the input array
> - Lastly **iterate through the array in order** and <span style='color:var(--mk-color-yellow)'>append the count of each instance</span> into an output array
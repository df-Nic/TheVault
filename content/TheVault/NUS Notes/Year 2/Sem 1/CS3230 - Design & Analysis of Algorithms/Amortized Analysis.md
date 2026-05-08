---
title: Amortized Analysis
Date Created: 2024-10-14
Last Updated: 2025-09-28
tags:
  - CS3230
  - AlgorithmAnalysis
---

# What is Amortized Analysis
---
<span style='color:var(--mk-color-turquoise)'>Amortized analysis</span>, guarantees the **average performance** of each operation <b><mark style='background:var(--mk-color-yellow)'>in the worse case</mark></b>. This is different from [[Average Case Analysis|average-case analysis]] as there is no probability involved as we are <span style='color:var(--mk-color-yellow)'>analysing a sequence of function calls</span>.

This is important as sometimes the <span style='color:var(--mk-color-green)'>cost of operations is small</span>, but for a <span style='color:var(--mk-color-red)'>few operations it can be very expensive</span>. This can lead us into believing that the time complexity is larger than what it really is.
# Types of Amortized Analysis
---
## Aggregate Method

The idea of this is to <span style='color:var(--mk-color-yellow)'>sum all costs</span> of $n$ operations and then <span style='color:var(--mk-color-yellow)'>divide</span> it by $n$ to get the average.

Using a **binary counter** as an example, which is to count numbers using binary:
- Given $3$ bits, 0 -> 0000, 1 -> 0001, 2 -> 0010
- Observe that as we increase by 1 we need to do multiple flip operations $0 -> 1$ or $1 -> 0$. Which on its own is $O(1)$ 
- But if we were to do this $k$ times in 1 increment then it will take $O(k)$ time.

![[Amortized Analysis of Bit Counter with Aggregate Method.png|center|400]]

Here we can see that the sum of all $n$ operations will be less than $2n$, which means on average $T(n) / n = 1$, thus to increment the counter by 1 will be <span style='color:var(--mk-color-blue)'>amortized</span> $O(1)$. 

> [!warning] Issues with Aggregate Method
> While this method is <span style='color:var(--mk-color-green)'>simple</span>, it however <span style='color:var(--mk-color-red)'>lacks the precision</span> as **compared to the next 2 methods**.
> 
> The **other 2 methods** are more suited to more general problems and thus it is <span style='color:var(--mk-color-green)'>more flexable</span>.
<div style="page-break-after: always;"></div>

## Accounting Method

The idea of this method is to <span style='color:var(--mk-color-red)'>charge more</span> on **cheap and frequent operations** (*Pay the cost and put some in the bank*) but when a **costly operation is required**, the <span style='color:var(--mk-color-green)'>cost can be paid by the "money" saved in the bank</span>.

If at any point the <span style='color:var(--mk-color-red)'>bank account goes negative</span> (*Not enough*), then our amortized analysis is incorrect. Else the **sum of all amortized costs** is an <span style='color:var(--mk-color-yellow)'>upper bound</span> to the **sum of true costs**.

> [!info] Observations of the Binary Counter
> So how do we charge more for the binary counter if we are **only doing 1 operation** which is to flip.
> 
> Lets see when the counter is 101111, we can see that the **more consecutive 1s** there are the <span style='color:var(--mk-color-yellow)'>more flips we need</span> to call at that iteration.
> 
> Thus we can <span style='color:var(--mk-color-orange)'>charge</span> as such:
> - For any bit from 0 -> 1, charge $2
> - For any bit from 1 -> 0. we take from the bank

Using the <span style='color:var(--mk-color-purple)'>binary counter</span> example,
- Every time we flip a bit from 0 -> 1, the amount in the bank is $1 and spend $1 if 1-> 0
- Thus the **amount of money** in the bank is <span style='color:var(--mk-color-yellow)'>equal to the number of 1's</span> in the binary representation of $i$
- Therefore the **amount in the bank** is <span style='color:var(--mk-color-green)'>never negative</span>, thus $2 $\in O(2) \in O(1)$.
## Potential Method

Let $\phi$ be the <span style='color:var(--mk-color-turquoise)'>potential function</span> and $\phi(i)$ is the <span style='color:var(--mk-color-yellow)'>potential at the end of the ith operation </span>.

For something to be a <span style='color:var(--mk-color-turquoise)'>potential function</span> ($\phi(i)$), it must <span style='color:var(--mk-color-orange)'>fulfil these 2 conditions</span>:
1) $\phi(0) = 0$ - At the beginning the potential must be 0
2) $\phi(i) \ge 0, \forall i$ - The potential <b><mark style='background:var(--mk-color-red)'>cannot be negative</mark></b>

For the **ith operation**, the amortized cost is, the true cost + $(\phi(i) - \phi(i - 1))$. This part ($(\phi(i) - \phi(i - 1))$), is known as the <span style='color:var(--mk-color-turquoise)'>potential difference</span>, which is denoted as $\Delta\phi(i)$,

The the **amortized cost** of $n$ operations can be calculated with:
$$
\sum^{n}_{0} \text{Actual cost of n operations} + \phi(i) - \phi(0)
$$

This is because of <span style='color:var(--mk-color-yellow)'>telescoping during the summation</span> which cancels the $\phi$ terms.

>A tip to **start finding a potential function** is to **look** at the **function** who is the <span style='color:var(--mk-color-red)'>most expensive</span>. And find something that <span style='color:var(--mk-color-red)'>decreases after next execution</span>.

Using a <span style='color:var(--mk-color-purple)'>dynamic table</span> as an example:
- Our potential function $\phi(i)$ to be $2i - \text{size}(T')$.
- Thus in the case when it is full, $\phi(i) = 2i - 2(i-1) = 2$.
- $\phi(i - 1) = 2i - (i - 1) = i - 1$
- Thus the $\Delta\phi(i) = 3 - i$, thus $i + 3 - 1 = 3 \in O(1)$

The important part is to know that at any $i$, the <span style='color:var(--mk-color-yellow)'>array will always be at most half full</span>.
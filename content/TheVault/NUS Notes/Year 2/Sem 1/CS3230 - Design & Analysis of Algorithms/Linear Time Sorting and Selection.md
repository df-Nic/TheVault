---
title: Linear Time Sorting and Selection
Date Created: 2024-11-11
Last Updated: 2025-09-28
tags:
  - CS3230
  - AlgorithmDesign
  - Algorithms
  - Sorting
  - Searching
---
# Lower Bound?
---
As mentioned [[Lower Bound of Sorting|previously]], the lower bound of sorting is $\Omega(n \log n)$. However that is if you do **some sort of comparison**. 

Can we do better if we use other conventions to do sorting?
# Counting Sort
---
Given an array with integers from $0$ to $k$ can we sort them faster than $\Omega(n \log n)$? We can do it in <span style='color:var(--mk-color-yellow)'>linear time</span> using <span style='color:var(--mk-color-turquoise)'>counting sort</span>.

> [!question] How does counting sort work?
> Since we <span style='color:var(--mk-color-yellow)'>know what is the maximum value</span> is, $k$. Then we first create a frequency table of size $k$ with all **values initialized to 0**.
> 
> Then we will <span style='color:var(--mk-color-orange)'>need 2 passes</span> through the input array:
> 1) For each element <span style='color:var(--mk-color-yellow)'>increment the count</span> of the number in the frequency table by 1
> 2) From 0 to $k$, <span style='color:var(--mk-color-yellow)'>add the numbers back based on the count</span>

We will do 2<span style='color:var(--mk-color-yellow)'> passes in order to sort the entire array</span> and this will take $O(n + n + k) = O(n + k)$.

Now for this to be in <span style='color:var(--mk-color-green)'>linear time</span> is if $k$ is **small**, more specifically if $k \in O(n)$. We <span style='color:var(--mk-color-yellow)'>traded memory for increased time</span>. But $k$ cannot be too big if not we <span style='color:var(--mk-color-red)'>use too much memory and cannot run</span> <span style='color:var(--mk-color-teal)'>counting sort</span>.
## Stable Counting Sort

Another issue with the <span style='color:var(--mk-color-teal)'>proposed counting sort algorithm</span> above is that it is <span style='color:var(--mk-color-red)'>not stable</span>.

> [!summary] 
> To make it stable the **first pass will be exactly the same**.
> 
> However the second pass we will do a <span style='color:var(--mk-color-yellow)'>prefix sum on the frequencies</span> in the frequency table.
> 
> Now the **value in the frequency table** represents the <span style='color:var(--mk-color-yellow)'>last index the number is supposed to be in</span> the original array.
> 
> Now we need **1 last pass** but start from the <span style='color:var(--mk-color-yellow)'>back of the frequency table</span>. As we add we decrease value by 1 (*Do not add values if they are not in the original array*).
<div style="page-break-after: always;"></div>

# Radix Sort
---
<span style='color:var(--mk-color-turquoise)'>Radix sort</span> is a <span style='color:var(--mk-color-yellow)'>iterative counting sort</span>, where it will repeat counting sort <span style='color:var(--mk-color-yellow)'>based on the number of digits</span> of the largest value (*i.e. if our largest number $k = 152$ then we repeat 3 times*).

We will start with <span style='color:var(--mk-color-yellow)'>10 buckets</span> (*An array of size 10 since in decimal or base 10 there is only numbers 0 to 9*) and we will sort the numbers from the<span style='color:var(--mk-color-yellow)'> least significant digit </span>(LSD) <span style='color:var(--mk-color-yellow)'>to the most significant digit </span>(MSD), essentially right to left.

<span style='color:var(--mk-color-orange)'>One prerequisite</span> is that **sorting of digits** <b><mark style='background:var(--mk-color-yellow)'>requires a fast and stable sort.</mark></b>. This is why radix sort works because of the stability property.

> [!faq] How does radix sort work?
> Same as <span style='color:var(--mk-color-teal)'>stable counting sort</span> but we will do digit by digit.
> 
> Have an **array of size 10** and <span style='color:var(--mk-color-yellow)'>sort the numbers based on the right most digit first</span>. We can use a **stack for each digit 0 to 9 to preserve stability**.
> 
> Then like <span style='color:var(--mk-color-teal)'>stable counting sort</span> start from digit 9 and add the numbers in sequence.
> 
> **Repeat for all digits** (*If there are values with less digits just append 0*)

Now the <span style='color:var(--mk-color-orange)'>time complexity</span> will be $O(d \cdot (n + k))$, where $d$ is the number of digits. But $k = 10$, therefore it will be $O(d \cdot (n + 10))$.

But we can do <span style='color:var(--mk-color-green)'>better by changing the base</span>. If we have a b-bit word and it can be broken down in $\frac{b}{r}$ groups of r-bit words then:
- $d = \frac{b}{r}$
- Each pass will be $O(n + 2^{r})$ since $k = 2^{r}$
- Thus the total time will be $O(\frac{b}{r} (n + 2^{r}))$

<span style='color:var(--mk-color-orange)'>For example</span> if we convert base 10 of a 32 bit integer into base 16 (*Hexadecimal*), then $r = 4$, $d = 8$, thus the time complexity is $O(8 \cdot (n + 16))$.

**Proving radix sort is in linear time:**
![[Proving Radix Sort is in Linear Time.png|center|450]]
<div style="page-break-after: always;"></div>

# Order Statistics
---
This is a simple problem of get the<span style='color:var(--mk-color-yellow)'> smallest k integer</span> or <span style='color:var(--mk-color-yellow)'>retrieve an integer of rank k</span>. If there are duplicates we can always transform the input into `(A[i], i)` where $i$ is the index.

> [!abstract] Naive solutions
> An $O(i \cdot n)$ algorithm will be to just <span style='color:var(--mk-color-yellow)'>1 pass find the minimum and mark it out</span>, then decrease $i$ by 1 and repreat until $i = 0$. At worst $i = n/2$ which is the median.
> 
> Or a $O(n \log n)$ solution and just <span style='color:var(--mk-color-yellow)'>sort the array</span> and retrieve $i$-th smallest element in $\Theta(1)$.
## Quickselect

Can we do better than $O(n \log n)$? If we just want to find the minimum or maximum, then we can do it in $\Theta(n)$. But what about the $i$-th element.

> [!question] How does quickselect work?
> Like <span style='color:var(--mk-color-teal)'>quicksort</span>, pick a random number in the array as our pivot, then as usual we will <span style='color:var(--mk-color-yellow)'>do the partitioning</span>.
> 
> Now **depending on the index of the pivot** ($k$) after the partitioning we will <span style='color:var(--mk-color-yellow)'>check on one of the halves but not both</span>.
> 
> If $k == i$, then we are done, if $k < i$ check on the right, if $k > i$ then check on the left.

At <span style='color:var(--mk-color-red)'>worst case</span> it will run in $O(n^{2})$ if the **pivot selected is either the maximum or minimum element** (*some say between 25th and 75th percentile*) else it will be <span style='color:var(--mk-color-green)'>faster</span> and run in $O(n)$ (*This is expected not actual run time*).
## Median of Medians

This helps solve 1 issue that <span style='color:var(--mk-color-teal)'>quickselect</span> has which is to<span style='color:var(--mk-color-yellow)'> find a good pivot</span>.

> [!question] How does it work?
> ![[Median of Medians Visualisation.png|center|300]]
> 
> 1) We can <span style='color:var(--mk-color-yellow)'>group our input array</span> into groups of 5 (*Not all numbers work for example groups of 3*).
> 2) For each group <span style='color:var(--mk-color-yellow)'>find the median value</span>
> 3) Of all the medians of each group <span style='color:var(--mk-color-yellow)'>find the median again based on all the medians</span>
> 4) The **value found in step 3** will be our <span style='color:var(--mk-color-yellow)'>pivot</span> for the <span style='color:var(--mk-color-teal)'>quickselect</span> algorithm.

We can observe that the <span style='color:var(--mk-color-orange)'>median of medians</span> will be <span style='color:var(--mk-color-yellow)'>greater than at most half of the other medians</span>. From the example above it will be $\frac{n}{5} \cdot \frac{1}{2} = \frac{n}{10}$.

It **will also be greater than** $3 \cdot \frac{n}{10}$ <span style='color:var(--mk-color-yellow)'>elements in the array</span>. Similarly it will be **smaller than** $3 \cdot \lfloor\frac{n}{10}\rfloor$ of the elements.
>*Since is a group of 5 thus the median is the 3rd elements therefore is 3, it can be different depending on the group*.

**Analysis of median of medians:**
![[Analysis of Median of Medians.png|center|300]]

> [!question] So is this better?
> Well <span style='color:var(--mk-color-red)'>no it is not</span>, you are <span style='color:var(--mk-color-green)'>better of running quickselect</span>. This is because we need a very large $c$ as well as a large $n$.
> 
> But for **small** $n$, median of median is $\Theta(1)$.
> 
> The worst-case linear-time selection is only good in theory. In practice, this algorithm is <span style='color:var(--mk-color-red)'>a bit slow due to the constant c</span> of c · n is large.
> 
> However unlike <span style='color:var(--mk-color-teal)'>quickselect</span>, this will run in $\Theta(n)$ instead of expected $\Theta(n)$.
# Dynamic Order Statistics
---
In reality, data will get deleted or removed or edited and what not and this will <span style='color:var(--mk-color-yellow)'>change the order of the elements</span>. Thus the $i$-th digit might be **different after added more values**.

We can handle this by using a <span style='color:var(--mk-color-turquoise)'>order statistics tree</span> (*is just a [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Trees#Finding the $k$-th Element|balanced binary tree]]*). It will have **1 augmentation**, where each node will have a <span style='color:var(--mk-color-yellow)'>variable called rank</span> which stores the **size of left subtree plus 1**.

And with this we can find the $i$-th digit in $O(\log n)$ time which is <span style='color:var(--mk-color-green)'>faster than linear time</span>!

> [!faq] How to find the i-th element in a bBST?
> <span style='color:var(--mk-color-yellow)'>Start from the root node</span> and lets have its rank set to $k$.
> 
> There will be <span style='color:var(--mk-color-orange)'>3 outcomes</span>:
> 
> 1) If $i = k$ then return the number.
> 2) If $i < k$ we will <span style='color:var(--mk-color-yellow)'>move to the left subtree</span>.
> 3) If $k < i$ we will <span style='color:var(--mk-color-yellow)'>move to the right subtree</span>, and we will reduce $i$ by $k$ ($i - k$).
> 
> If its outcome 2 or 3, repreat until outcome 1 is met.

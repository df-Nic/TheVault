---
title: Proof of Correctness
Date Created: 2024-08-31
Last Updated: 2025-09-28
tags:
  - CS3230
  - AlgorithmAnalysis
---
# Iterative Functions
---
There are <span style='color:var(--mk-color-orange)'>4 steps to prove the correctness</span> of **iterative algorithms**:
1) **Loop invariant** - <span style='color:var(--mk-color-yellow)'>Conditions</span> that must be <span style='color:var(--mk-color-green)'>satisfied</span> at the <span style='color:var(--mk-color-yellow)'>start of each iteration</span>
2) **Initialization** - The loop invariant is <span style='color:var(--mk-color-green)'>true</span> at the **start of the first iteration**
3) **Maintenance** - The loop invariant is <span style='color:var(--mk-color-green)'>satisfied</span> at the **start of the current and the next iteration**
4) **Termination** - At the end of the last iteration, the <span style='color:var(--mk-color-green)'>algorithm outputs the correct answer</span>

> [!question] What is a Strong Loop Invariant
> Lets look at some loop invariants for [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Sorting#Selection Sort|selection sort]].
> 
> 1. $A$ is sorted
> > It <span style='color:var(--mk-color-red)'>fails initialization</span> because $A$ might not be sorted at the start.
> 
> 2. $A[i,\dots,j - 1]$ is sorted
> > It <span style='color:var(--mk-color-red)'>fails maintenance</span> if the element at $j - 1$ is larger than the smallest element in $j$ to $n$.
> 
> 3. $x \le y$, $\forall x \in A[i, \dots, j - 1]$ and $y \in A[j, \dots, n]$
> > This does pass all 3 but for **termination** the final $j$ to $n$ array will be null making th estatement vacuously true, thus is not a strong invariant.
> 
> 5. **Both** points 2 and 3
> > When combined is a good loop invariant and it <span style='color:var(--mk-color-green)'>passes initialization, maintenance and termination</span>.
# Recursive Functions
---
Essentially for **recursive algorithms** there are only <span style='color:var(--mk-color-orange)'>2 points to prove for correctness</span>:
1) **Base case** - Just show that for the **base case** the algorithm is <span style='color:var(--mk-color-green)'>correct</span>.
2) **Inductive step** - First **assume** that any <span style='color:var(--mk-color-yellow)'>input size smaller than n is correct</span>, then prove that the algorithm is <span style='color:var(--mk-color-green)'>correct</span> for input size of $n$.

**Example binary search**

```Java
public boolean binarySearch (arr,low,high,target) {
	if (high < low) {
		return false;
	} else {
		mid = low + (high - low) / 2;
		if (arr[mid] == target) {
			return true;
		} else if  (target > arr[mid]) {
			binarySearch(arr, mid + 1, high, target);
		} else {
			binarySearch(arr, low, mid - 1, target);
		}
	} 
}
```

**Base case**
For binary search the base case when `low > high`. In which case the <span style='color:var(--mk-color-red)'>algorithm returns false</span>. This is correct because the scenario just means a <span style='color:var(--mk-color-yellow)'>empty array</span>, which definitely will not contain the target.

**Inductive step**
Lets <span style='color:var(--mk-color-orange)'>analyse the 3 cases</span>.

If `A[mid] == target`, then the output must be <span style='color:var(--mk-color-green)'>true</span>, which is what the algorithm does.

If `A[mid] < target`, then the target can be in the array **if and only if** it is in $Arr[mid + 1 \colon high]$, this is the <span style='color:var(--mk-color-yellow)'>array is initially sorted</span>. Thus the answer must be `binarySearch(arr, mid + 1, high, target)`.

Then for the last case `A[mid] > target` is similar to the case before.
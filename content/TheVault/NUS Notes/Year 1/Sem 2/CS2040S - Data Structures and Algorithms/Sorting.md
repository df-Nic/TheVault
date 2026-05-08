---
title: Sorting
Date Created: 2024-02-13
Last Updated: 2025-10-20
tags:
  - CS2040S
  - Algorithms/Sorting
---

# Sorting Algorithm Properties
---
## In-place

An <span style='color:#0fb9b1'>in-place</span> sort is any sorting algorithm what <span style='color:#f7b731'>requires constant space</span> or <b><span style='color: var(--mk-color-green)'>O(1)</span></b>. Another definition is that no additional arrays created and all the <span style='color:#f7b731'>sorting is done on the input array</span> itself.
## Stability

A sorting algorithm is stable if the <span style='color:#f7b731'>relative order</span> of elements with the same key value <span style='color:#f7b731'>is preserved</span>. Basically similar values should not change positions with each other, given the original sequence.

The importance of <span style='color:#0fb9b1'>stability</span>, can be <span style='color:#f7b731'>used when chaining sorting conditions</span>. This will not give a correctly sorted array, if the second sort onwards is unstable.
# Bubble Sort
---
## Idea of Bubble Sort
- Loop through each element in the array
- Examine the `ith` and `ith + 1` term, and <span style='color: var(--mk-color-yellow)'>swap if the ith term is bigger</span>
- <span style='color:#f7b731'>Repeat</span> this $n$ times where $n$ is the <span style='color:#f7b731'>number of elements in the array</span>

With the above implementation, the <span style='color:#fa8231'>best & worst case</span> is <b><span style='color: var(--mk-color-red)'>O(n<sup>2</sup>)</span></b>. There are redundant iterations as it <span style='color:#eb3b5a'>continues even when it is sorted</span>! 

<span style='color:#20bf6b'>One optimisation</span> is to have a <span style='color:#3867d6'>Boolean flag</span>, to <span style='color:#f7b731'>keep track if any swaps are made</span> during the iteration, if no stop the loop.

A <span style='color:#eb3b5a'>bad input</span>, is when the smallest element is in the back while the rest is sorted, `[2,3,4,5,6,7,8,1]`.

**Bubble Sort Loop Invariant** :
>After `i` iterations, then <span style='color:#f7b731'>biggest</span> `i` <span style='color:#f7b731'>items will be correctly sorted</span> at the back `i` positions in the array. Which means after `n` iterations, it will be sorted
<div style="break-after: page;"></div>

**Implementation**
```Java
import java.util.*;
public class BubbleSort{

	public static void bubblesort(int[] arr){
		for (int i = 1; i < arr.length; i++){
			boolean isSorted = true;
			for (int j = 0; j < a.length - i; j++){ //Loop through unsorted items 
				if (a[j] > a[j+1]){
					int temp = a[j]; // Do the swap
					a[j] = a[j+1];
					a[j+1] = temp;
					isSorted = false;
				}
			}
			if (isSorted) return; // Exit when it is done
		}
	}
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(n)</span></b>
**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-red)'>O(n<sup>2</sup>)</span></b>
**Space Complexity** : <b><span style='color: var(--mk-color-green)'>O(1)</span></b>
**In-place** : <b><span style='color: var(--mk-color-green)'>Yes</span></b>
**Stable** : <b><span style='color: var(--mk-color-green)'>Yes</span></b>
# Selection Sort
---
## Idea of Selection Sort
- Loop through each element in the array from `j` to `n - 1`, where it <span style='color:#f7b731'>starts from</span> `j = 1`
- <span style='color:#f7b731'>Find</span> the `j` <span style='color:#f7b731'>smallest element</span> in `j` to `n`.
- Wherever the smallest element is, <span style='color:#f7b731'>swap positions</span> with `j`
- <span style='color:#f7b731'>Repeat</span> this $n$ times where $n$ is the <span style='color:#f7b731'>number of elements in the array</span>

A <span style='color:#eb3b5a'>bad input</span>, is when the only 2 elements is out of order, `[2,3,4,6,5,7,8,1]`.

**Selection Sort Loop Invariant** :
>After `i` iterations, then <span style='color:#f7b731'>smallest</span> `i` <span style='color:#f7b731'>items will be correctly sorted</span> at the first `i` positions in the array. Which means after `n` iterations, it will be sorted
<div style="break-after: page;"></div>

**Implementation**
```Java
import java.util.*;
public class SelectionSort{
	private static void swap(int[] arr, int j, int k) {
		int temp = arr[j];
		arr[j] = arr[k];
		arr[k] = temp;
	}
	public static void selectionsort(int[] arr){
		for (int i = 0; i < arr.length; i++){
			int index = i;
			for (int j = i + 1 ; j < arr.length; j++){
				if(arr[j] < arr[index])
				index = j;
			}
			swap(arr, i, index);
		}
	}
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-red)'>O(n<sup>2</sup>)</span></b>
**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-red)'>O(n<sup>2</sup>)</span></b>
**Space Complexity** : <b><span style='color: var(--mk-color-green)'>O(1)</span></b>
**In-place** : <b><span style='color: var(--mk-color-green)'>Yes</span></b>
**Stable** : <b><span style='color: var(--mk-color-red)'>No</span></b>
# Insertion Sort 
---
## Idea of Insertion Sort
- Loop through each element in the array from `i` to `n - 1`, where it <span style='color:#f7b731'>starts from</span> `i = 1`
- For each `ith` element, <span style='color:#f7b731'>push</span> the element into its <span style='color:#f7b731'>correct position on the left</span>
- <span style='color:#eb3b5a'>Stop pushing</span> when the <span style='color:#f7b731'>element on the left</span> is $\le$

A <span style='color:#eb3b5a'>bad input</span>, is when the array is sorted but in reverse order, `[8,7,6,5,4,3,2,1]`.

**Insertion Sort Loop Invariant** :
>After every `i` iteration, <span style='color:#f7b731'>all elements from</span> 0 to `i` <span style='color:#f7b731'>will be in order</span>
<div style="break-after: page;"></div>

**Implementation**
```Java
import java.util.*;
public class InsertionSort{

	public static void insertionsort(int[] arr){
		for (int i = 1; i < arr.length; i++){
			int temp = a[i];
			
			// j has to be declared here to remember the index to insert the number into
			int j;
			// The for loop as a condition, it will iterate when true
			for (j = i-1; j >= 0 && a[j] > temp; j--){ // This condition makes it stable, ie >
				a[j+1] = a[j];
			}
			a[j+1] = temp;
		}
	}
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(n)</span></b>
**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-red)'>O(n<sup>2</sup>)</span></b>
**Space Complexity** : <b><span style='color: var(--mk-color-green)'>O(1)</span></b>
**In-place** : <b><span style='color: var(--mk-color-green)'>Yes</span></b>
**Stable** : <b><span style='color: var(--mk-color-green)'>Yes</span></b>
# Merge Sort 
---
It uses the <span style='color:#0fb9b1'>divide and conquer</span> strategy :
- Divide the problem into sub-problems
- Recursively solve the sub-problems
- Combine the results
## Idea of Merge Sort
- Spilt the array into <span style='color:#f7b731'>2 halves</span>
- <span style='color:#f7b731'>Recursively sort</span> the 2 halves
- <span style='color:#f7b731'>Merge</span> the results into 1 array
- If the <span style='color:#f7b731'>array is of length 1</span>, then return that array since it is<span style='color:#f7b731'> considered sorted</span>

Merge Sort is <span style='color:#eb3b5a'>slower</span> for <span style='color:#f7b731'>small number of items to sort</span>. Since splitting into 2 will be less beneficial.

<span style='color:#20bf6b'>One optimisation</span> is to have a <span style='color:#3867d6'>alternate between 2 arrays</span>, to save on space. The idea is to have 2 arrays, and alternate between which is to be used to hold the stored array.

**Implementation**
```Java
import java.util.*;
public class MergeSort{

	// If this is stable, then merge sort is stable
	public static void merge(int[] a, int i, int mid, int j){
		int [] temp = new int[j-i + 1];
		int left = i, right = mid + 1, idx = 0;
		
		// Add either side until one array runs out
		while (left <= mid && right <=j){
			if (a[left] <= a[right])
				temp[idx++] = a[left++];
			else
				temp[idx++] = a[right++];
		}
		// Add the remainding items
		while (left <= mid){
			temp[idx++] = a[left++];
		}
		while (right <= j){
			temp[idx++] = a[right++];
		}
		// Copy back the result into the array
		for (int k = 0; k < temp.length; k++){
			a[i+k] = temp[k];
		}
	}
	
	public static void mergesort(int[] a, int i, int j){
		if (i < j) {
			int mid = (i + j)/2;
			mergesort(a, i, mid);
			mergesort(a, mid+1,j);
			merge(a, i, mid, j); // O(n) time
		}
	}
}
```

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(n log n)</span></b>
**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-green)'>O(n log n)</span></b>
**Space Complexity** : <b><span style='color: var(--mk-color-red)'>O(n log n)</span></b>
**In-place** : <b><span style='color: var(--mk-color-red)'>No</span></b>
**Stable** : <b><span style='color: var(--mk-color-green)'>Yes</span></b>  (If <span style='color:#3867d6'>merge</span> is stable)
# Quicksort 
---
## Idea of Quicksort
- Choose a <span style='color:#0fb9b1'>partition</span> any partition (A index in the array)
- Using the value of the partition, move all the numbers <span style='color:#f7b731'>smaller to the left, bigger to the right</span>
- Afterwards <span style='color:#f7b731'>recursively sort, the left and the right half</span>

A <span style='color:#eb3b5a'>bad input</span>, is when the pivot chosen does not spilt the array into 2 even segments or `[1,1,1,1,1,1,1]`.

**Implementation**
```Java
import java.util.*;
public class QuickSort{
	
	public static void quicksort(int [] arr, int start, int end){
		if (start %3E= end){
			return;
		}
		
		int pivot = arr[end];
		int to_swap = start;
		
		for (int i = start; i %3C= end; i++){
			if (arr[i] < pivot){
				int temp = arr[to_swap];
				arr[to_swap] = arr[i];
				arr[i] = temp;
				to_swap += 1;
			}
		}
		
		int temp = arr[to_swap];
		arr[to_swap] = arr[end];
		arr[end] = temp;
		
		quicksort(arr, start, to_swap - 1);
		quicksort(arr, to_swap + 1, end);
	}
}
```
<div style="break-after: page;"></div>

**Time Complexity** (<span style='color:#fa8231'>Best Case</span>) : <b><span style='color: var(--mk-color-green)'>O(n log n)</span></b>
**Time Complexity** (<span style='color:#fa8231'>Worst Case</span>) : <b><span style='color: var(--mk-color-red)'>O(n<sup>2</sup>)</span></b>
**Space Complexity** : <b><span style='color: var(--mk-color-green)'>O(1)</span></b>
**In-place** : <b><span style='color: var(--mk-color-green)'>Yes</span></b> (If <span style='color:#3867d6'>partition</span> is in-place)
**Stable** : <b><span style='color: var(--mk-color-green)'>Yes</span></b> (If <span style='color:#3867d6'>partition</span> is stable)

Another algorithm arises from quicksort and that is <span style='color:#3867d6'>quickselect</span> which helps to <span style='color:#f7b731'>find some element</span>. This runs on  <b><span style='color: var(--mk-color-green)'>O(n)</span></b> time as the <span style='color:#f7b731'>recursion will go either left or right depending on the pivot</span>.
## How to Partition

Firstly, let the <span style='color:#fa8231'>first element</span> at index 0 be the <span style='color:#fa8231'>pivot</span>. Afterwards, have 2 pointers `low` & `high`, which points to index 1 and the last element of the array.

<span style='color: var(--mk-color-yellow)'>Increment</span> `low` by 1 if the <span style='color:#f7b731'>number if smaller than pivot</span>, else, <span style='color: var(--mk-color-yellow)'>decrement</span> the `high` until it is <span style='color:#f7b731'>smaller than the pivot</span> and once done, <span style='color:#3867d6'>swap</span> the 2 elements in `low` and `high`.

This <b><span style='color: var(--mk-color-yellow)'>stops when the 2 points meet</span></b>, before terminating, swap the pivot with the element at `low - 1`.

**Partition Loop Invariant** :
>Safely at the end of each iteration, `arr[high] > pivot`. When exiting the loop `low >= high`, if high was decremented that means that `high` is larger than pivot. If not then it will swap with `low`. And <span style='color:#f7b731'>at the end, everything to the left is smaller and to the right bigger</span>
### Choosing the Pivot

A <span style='color:#eb3b5a'>bad pivot</span> can make this sorting algorithm slow, <span style='color:#fa8231'>like the one suggested above</span>, in fact it will make it <b><span style='color: var(--mk-color-red)'>O(n<sup>2</sup>)</span></b> time as the <span style='color:#f7b731'>pivot does not partition into 2 even segments</span>.

What about <span style='color:#fa8231'>choosing the median</span> value in the array, since the median element will spilt the array into 2 evenly segments and this works and will give us a running time of <b><span style='color: var(--mk-color-green)'>O(n log n)</span></b>.

What about partition such that the 2 segments will have a ratio of $\frac{1}{10} : \frac{9}{10}$? Basically the larger segment will be about 9 times bigger. Well this is also <b><span style='color: var(--mk-color-green)'>O(n log n)</span></b>.

Why not choose the <span style='color:#fa8231'>pivot at random</span>, where it will <span style='color:#f7b731'>end up with the above segmentation</span> and sometimes better.
- **Paranoid Quicksort**, where the pivot gets chosen again if it gives a bad partitioning which is <span style='color:#f7b731'>expected to repeat 2 times</span>
<div style="break-after: page;"></div>

### Duplicates

Now a issue with the above solution is that duplicates might be <span style='color:#f7b731'>delt with multiple times</span>. Since it can be a pivot in the recursive stack which will accomplish nothing. A solution to this is to do a <span style='color:#3867d6'>3-way partitioning</span>.

**Implementation 1**
- Do a regular partition
- Pack duplicates together

The difference is that <b>it needs 1 more pass through the array</b> and if a <span style='color:#fa8231'>duplicate is found</span>, <span style='color:#f7b731'>decrement the pivot pointer</span> until a non duplicate is found, then swap the 2 positions.

**Implementation 2**
- Instead of 2 passes it will be one pass
- Maintain <span style='color:#f7b731'>4 regions of the array</span>

The idea is to have <span style='color:#fa8231'>4 segments</span> :
1) One for less than pivot
2) One for more than pivot
3) One for equals to pivot
4) The last is elements that have not been processed

## Base Case

Consider the following <span style='color:#fa8231'>base cases for quick sort</span> :
- **Recurse all the way** as per usual
- Switch to **Insertion Sort** when the **array size meets some threshold**
- **Stop the recursion** early and then do one **Insertion Sort on the entire array**

The fastest one will be point 3. Since as the recursion continue the <span style='color:#f7b731'>elements will be segmented into partitions</span>. And once its terminated, the whole array will be almost sorted and <span style='color:#0fb9b1'>Insertion Sort</span> works best for almost sorted arrays.
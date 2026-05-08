---
title: Sorting
Date Created: 2023-06-26
tags:
  - CS2040
  - Sorting
---

# Table of Contents
---
- [[#In-place|In-place]]
- [[#Stable|Stable]]
- [[#Types of Sorting|Types of Sorting]]
	- [[#Types of Sorting#Selection Sort|Selection Sort]]
		- [[#Selection Sort#Idea of Selection Sort|Idea of Selection Sort]]
	- [[#Types of Sorting#Bubble Sort|Bubble Sort]]
		- [[#Bubble Sort#Idea of Bubble Sort|Idea of Bubble Sort]]
		- [[#Bubble Sort#Can this be improved?|Can this be improved?]]
	- [[#Types of Sorting#Insertion Sort|Insertion Sort]]
		- [[#Insertion Sort#Idea of Insertion Sort|Idea of Insertion Sort]]
	- [[#Types of Sorting#Merge Sort|Merge Sort]]
		- [[#Merge Sort#Idea of Merge Sort|Idea of Merge Sort]]
	- [[#Types of Sorting#Quick Sort|Quick Sort]]
		- [[#Quick Sort#Idea of Quick Sort|Idea of Quick Sort]]
	- [[#Types of Sorting#Radix Sort|Radix Sort]]
		- [[#Radix Sort#Idea of Radix Sort|Idea of Radix Sort]]
- [[#Comparator|Comparator]]
		- [[#Radix Sort#What is it?|What is it?]]
		- [[#Radix Sort#Implementing Comparator|Implementing Comparator]]
- [[#Sorting Algorithm Characteristics|Sorting Algorithm Characteristics]]
---

# In-place
---

An in-place sort is any sorting algorithm what <span style='color:#0fb9b1'>requires constant space O(1)</span>.

Another definition is that <span style='color:#0fb9b1'>no additional arrays</span> created to complete the sort.

# Stable
---

A sorting algorithm is stable if the <span style='color:#0fb9b1'>relative order of elements with the same key value is preserved</span>.

Similar values should not change positions with each other.

# Types of Sorting
---

## Selection Sort
---

### Idea of Selection Sort

1. Find the <span style='color:#20bf6b'>largest/smallest</span> item
2. Swap it with the item at the <span style='color:#20bf6b'>end/start</span> of the array
3. Repeat step 1 and <span style='color:#20bf6b'>exclude the item that was swapped</span>

Time Complexity: <b><mark class="hltr-red">O(n<sup>2</sup>)</mark></b>
Space Complexity: <b><mark class="hltr-red">O(1)</mark></b>

Example:
```Java
import java.util.*;
public class SelectionSort{

	public static void selectionsort(int[] a){
		for (int i = a.length - 1; i >= 1; i--){
			int index = i;
			
			for (int j = 0 ; j < i; j++){
				if(a[j] > a[index])
				index = j;
			}
			
			int temp = a[index];
			a[index] = a[i];
			a[i] = temp;
		}
	}

	public static void main(String[] args){
		int[] a = {10,12,5,1,8,9,4,7};
		selectionsort(a);
		System.out.println(Arrays.toString(a));
	}
}
```

## Bubble Sort
---

### Idea of Bubble Sort

1. Do the sort in passes, where the <span style='color:#20bf6b'>largest item will be passed to the end</span> of the array in each iteration
2. Examine the <span style='color:#20bf6b'>i-th and (i + 1)-th term</span> and swap them if incorrect

Time Complexity: <b><mark class="hltr-red">O(n<sup>2</sup>)</mark></b>
Space Complexity: <b><mark class="hltr-red">O(1)</mark></b>

Example:
```Java
import java.util.*;
public class BubbleSort{

	public static void bubblesort(int[] a){
		for (int i = 1; i < a.length; i++){
			for (int j = 0; j < a.length - i; j++){ //Loop through unsorted items 
				if (a[j] > a[j+1]){
					int temp = a[j];
					a[j] = a[j+1];
					a[j+1] = temp;
				}
			}
		}
	}

	public static void main(String[] args){
		int[] a = {10,12,5,1,8,9,4,7};
		bubblesort(a);
		System.out.println(Arrays.toString(a));
	}
}
```

### Can this be improved?

Yes, as the sort above does not check if the input has been sorted. Thus a <span style='color:#3867d6'>flag</span> can be used to <span style='color:#3867d6'>break the iterative loop once it is sorted</span>.

Improvement:
```Java
import java.util.*;
public class BubbleSort{

	public static void bubblesort(int[] a){
		for (int i = 1; i < a.length; i++){
			boolean isSorted = true;
			for (int j = 0; j < a.length - i; j++){ //Loop through unsorted items 
				if (a[j] > a[j+1]){
					int temp = a[j];
					a[j] = a[j+1];
					a[j+1] = temp;
					isSorted = false;
				}
			}
			if (isSorted) return;
		}
	}

	public static void main(String[] args){
		int[] a = {10,12,5,1,8,9,4,7};
		bubblesort(a);
		System.out.println(Arrays.toString(a));
	}
}
```

This however <mark class="hltr-orange">does not change the worse case</mark> time complexity. As long as the smallest item is at the back it will take the full <b><mark class="hltr-red">O(n<sup>2</sup>)</mark></b>.

## Insertion Sort
---

### Idea of Insertion Sort

1. Start with a pile
2. Take a number and <span style='color:#20bf6b'>insert</span> it into its <span style='color:#20bf6b'>proper sorted order</span>
3. <span style='color:#20bf6b'>Repeat</span> until it is sorted

Time Complexity: <b><mark class="hltr-red">O(n<sup>2</sup>)</mark></b>
Space Complexity: <b><mark class="hltr-red">O(1)</mark></b>

Example:
```Java
import java.util.*;
public class InsertionSort{

	public static void insertionsort(int[] a){
		for (int i = 1; i < a.length; i++){
			int temp = a[i];
			
			// j has to be declared here to remember the index to insert the number into
			int j;
			 
			// The for loop as a condition, it will iterate when true
			for (j = i-1; j >= 0 && a[j] > temp; j--){
				a[j+1] = a[j];
			}
			
			a[j+1] = temp;
		}
	}

	public static void main(String[] args){
		int[] a = {10,12,5,1,8,9,4,7};
		insertionsort(a);
		System.out.println(Arrays.toString(a));
	}
}
```

## Merge Sort
---

### Idea of Merge Sort

1. It uses the divide and conquer method by <span style='color:#20bf6b'>dividing up larger problems into smaller ones</span>
2. <span style='color:#20bf6b'>Recursively</span> solve the smaller problems
3. <span style='color:#20bf6b'>Combine the results</span> of the smaller problems to product the result

Time Complexity: <b><mark class="hltr-red">O(n log n)</mark></b>
Space Complexity: <b><mark class="hltr-red">O(n)</mark></b>

Example:
```Java
import java.util.*;
public class MergeSort{
	
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
			merge(a, i, mid, j);
		}
	}
	
	public static void main(String[] args){
		int[] a = {10,12,5,1,8,9,4,7};
		mergesort(a, 0, a.length - 1);
		System.out.println(Arrays.toString(a));
	}
}
```

## Quick Sort
---

### Idea of Quick Sort

1. It uses the divide and conquer method, choose a <span style='color:#20bf6b'>pivot</span> p and <span style='color:#20bf6b'>partition the items into 2 parts</span>
2. <span style='color:#20bf6b'>Recursively</span> sort the 2 parts

Time Complexity: <b><mark class="hltr-red">O(n<sup>2</sup>)</mark></b>
Space Complexity: <b><mark class="hltr-red">O(1)</mark></b>

Example:
```Java
import java.util.*;
public class QuickSort{
	
	public static void quicksort(int [] arr, int start, int end){
		if (start >= end){
			return;
		}
		
		int pivot = arr[end];
		int to_swap = start;
		
		for (int i = start; i <= end; i++){
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
	
	public static void main(String[] args){
		int[] a = {10,12,5,1,8,9,4,7};
		quicksort(a, 0, a.length - 1);
		System.out.println(Arrays.toString(a));
	}
}
```

## Radix Sort
---

### Idea of Radix Sort

1. Treats each data as a <span style='color:#20bf6b'>character string</span>
2. No comparison is needed, thus it is a <span style='color:#20bf6b'>non-comparison based sort</span>
3. Each iteration, organize the data into groups according to the next <span style='color:#20bf6b'>character</span> in each data

Time Complexity: <b><mark class="hltr-red">O(dn)</mark></b> or <b><mark class="hltr-red">O(n)</mark></b> if <span style='color:#fa8231'>d is fixed</span>
Space Complexity: <b><mark class="hltr-red">O(1)</mark></b>

Example (Pseudocode):
```Java
import java.util.*;
public class RadixSort{
	
	public static void radixsort(int [] a, int n, int d){
	// Sorts n d-digit numeric strings in the array
	for (i = d down to 1)
		initalize 10 groups of queues to empty

		for (i = 0 through n-1){
			k = jth digit of array[i]
		}
		replace array with all items in group 0, followed by all items in group 1 and so on
	}
	
	public static void main(String[] args){
		int[] a = {10,12,5,1,8,9,4,7};
		radixsort(a, 0, a.length - 1);
		System.out.println(Arrays.toString(a));
	}
}
```

# Comparator
---

### What is it?

It is used for classes to enable java to sort an iterable of a specific class. <span style='color:#f7b731'>Without this, Java will sort it based on the memory address</span>.

### Implementing Comparator

```Java
import java.util.Comparator;

// This is a comparator class
class AgeComparator implements Comparator<Person>{
	public int compare(Person p1, Person P2){
		// Compare base on age
		// If its equal it MUST be 0
		// If Obj 1 is smaller than Obj 2 it MUST return a negative number
		// If Obj 1 is bigger than Obj 2 it MUSt return a positive number
		
		// For String we can use the function .compareTo() function
		
		return p1.getAge() = p2.getAge();
	}
	// Just Copy this
	public boolean equals(Object obj){
		return this == obj;
	}
}

Public class Runner{
	public static void main(String[] args){
		// How to use the comparator
		AgeComparator Agecomp = new AgeComparator();
		Collections.sort(List, Agecomp)
	}
}
```

# Sorting Algorithm Characteristics
---

![[Sorting Algorithm Characteristics.png]]
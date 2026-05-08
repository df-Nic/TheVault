---
Title: Searching & Sorting
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - Algorithms/Sorting
  - Algorithms/Searching
---
## Table of Contents
- [[#Purpose of Searching & Sorting|Purpose of Searching & Sorting]]
- [[#Searching|Searching]]
	- [[#Searching#Types of Searches|Types of Searches]]
- [[#Sorting|Sorting]]
	- [[#Sorting#Types of Sorting|Types of Sorting]]
---

## Purpose of Searching & Sorting
---
In terms of big data, people will need to search and sort through the data to retrieve relevant data.

For sorting and searching in Python, lists are ideal compared to tuples as lists are mutable.

## Searching
---
The idea is to go through every element in an sequence and find the specific element.

### Types of Searches
---
**Linear Search**

A linier search goes through every item in a sequence and finds the item
**Time Complexity** : O(n)
```Python
def linear_search(value, lst):
	for item in lst:
		if i == value:
			return value # Or you can return True
	return None # Or return false if the value is not in the sequence
```
<div style="page-break-after: always;"></div>

**Binary Search**

Assuming that the elements are sorted, the algorithm does not need to go through every item to find a specific value. 

If we pick a k<sup>th</sup> element, if its bigger than the value, we need to only look at indices < k. The problem size gets reduced by half every iteration.

**Time Complexity** : O(log n)
```Python
# This binary search finds an item in a sequence
def binary_search(value, seq): # Seq has to be sorted

	def helper(low, high):
		if low > high:
			return False
		mid = (low + high) // 2
		if value == seq[mid]:
			return True
		elif (value < seq[mid]):
			return helper(low, mid-1)
		else:
			return helper(mid+1, high)
	return helper(0, len(seq) - 1)

# This binary search searches where to insert an element into a sorted list
def binary_search_input(x, seq):
    low, mid, max = 0, len(seq) // 2, len(seq)
    while (low < max):
        if (x <= seq[mid]):
            max = mid
            mid = (low + max) // 2
        else:
            low = mid + 1
            mid = (low + max) // 2
    
    return (low)
```
<div style="page-break-after: always;"></div>

## Sorting
---
The idea is to create a function which produces an ordering on the objects in a sequence.

**Stability**

A stable sorting algorithm will maintain the relative positions of elements in the event that they have the same value.

For example merge sort does not reorder similar valued elements.

**In-Place Algorithms**

In place algorithms are sorting algorithms which does not require extra space to sort a sequence. 

For example bubble sort can use the same list to sort without the need of an external list.

### Types of Sorting
---

**Selection Sort**

Loop though the sequence and find the smallest number. At the end of the loop add it in to another sequence to store the ordered elements.

**Time Complexity** : O(n<sup>2</sup>)
```Python
lst = [4,11,3,12,9,7,6]

def selection_sort(lst):
	sorted_lst = []
	length = len(lst)

	while lst:
		smallest = 9999999
		for element in lst:
			if element < smallest:
				smallest =element
		lst.remove(smallest)
		sorted_lst.append(smallest)
	return sorted_lst

print(selection_sort(lst))

# In-Place selection sort
def selection_sort(lst):
	length = len(lst)
	for index in range(length):
		swap_index = None
		for next in range(index,length):
			if lst[index] > lst[next]:
				swap_index = next
		if swap_index:
	            lst[index], lst[swap_index] = lst[swap_index], lst[index]
    return lst
```

**Merge Sort**

Using the concept of divide and conquer. The sequence can be spilt into 2 halves to be sorted. Once done, combine both of them together to get back the original sequence.

**Time Complexity** : O(n logn)
```Python
lst = [4,11,3,12,9,7,6]

def merge_sort(lst):

	if len(lst) < 2:
		return lst
	left = merge_sort(lst[:len(lst)//2])
	right = merge_sort(lst[len(lst)//2:])
	return merge(left, right)

def merge(left,right):

	result = []
	while left and right:
		if left[0] < right[0]:
			result.append(left[0])
			left.remove(left[0])
		else:
			result.append(right[0])
			right.remove(right[0])
	result.extend(left)
	result.extend(right)
	return result

print(merge_sort(lst))
```
<div style="page-break-after: always;"></div>

**Bubble Sort**

Each element will be swapped with the next index element if it is bigger/smaller depending on the outcome of the sorting algorithm. Swapping until it reaches the last element.

**Time Complexity** : O(n<sup>2</sup>)
```Python
# In-Place Bubble sort
def bubble_sort(lst):
    length = len(lst)
    for index in range(length):
        for next in range(index,length):
            if lst[index] > lst[next]:
                value = lst[index]
  
                lst[index] = lst[next]
                lst[next] = value
    return lst
```

**Quick Sort**

We will have a <span style='color:#2d98da'>pivot</span> which acts as the number to compare to. It is usually the middle most element, the first or the last.

Swap elements such that it divides the list into 2 piles, one smaller than the pivot, the other greater than or equal to.

Afterwards repeat until the list is sorted.

**Time Complexity** : O(n<sup>2</sup>) worse case, O(n log n) best case.

```Python
lst = [1,3,5,2,8,9,4]

def quicksort(lst):
	def helper(start, end):
	
		if start >= end:
			return
		pivot = lst[end] # Take the last element as the pivot
		to_swap = start
		
		for index in range(start, end):
			if lst[index] < pivot:
				lst[index], lst[to_swap] = lst[to_swap], lst[index]
				to_swap += 1
			
		lst[to_swap], lst[end] = lst[end], lst[to_swap]
		helper(start, to_swap - 1)
		helper(to_swap + 1, end)
		
	return helper(0, len(lst) - 1)
	
quicksort(lst)
print(lst)
```

**Java Code**

```Java
public static int[] quicksort(int [] arr, int start, int end){
	if (start >= end){
		return arr;
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
	
	arr = quicksort(arr, start, to_swap - 1);
	arr = quicksort(arr, to_swap + 1, end);
	return arr;
}
```
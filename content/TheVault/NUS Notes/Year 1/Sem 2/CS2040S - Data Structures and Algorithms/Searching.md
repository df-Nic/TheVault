---
title: Searching
Date Created: 2024-01-25
Last Updated: 2025-10-20
tags:
  - CS2040S
  - Algorithms/Searching
---
# Thinking Process when Coding Functions
---
Before coding any function, there are a <span style='color:#fa8231'>few characteristics to consider to code correctly</span> :
- **Specifications / Functionality**
>What does the function <span style='color:#f7b731'>do</span>, what does it <span style='color:#f7b731'>return</span>
- **Precondition**
><span style='color:#f7b731'>Something that has to be true</span> for a function to work correctly <span style='color:#f7b731'>when it begins</span>
- **Postcondition**
><span style='color:#f7b731'>Something that has to be true</span> for a function to show that it has correctly done its computation <span style='color:#f7b731'>when it ends</span>
- **Invariant / Loop invariant**
>A <span style='color:#f7b731'>relationship</span> between variables or each iteration of a loop that is <span style='color:#f7b731'>always true</span>. Or is some fact that is true throughout execution.

# Binary Search
---
A <span style='color:#0fb9b1'>binary search</span> is a <span style='color:#f7b731'>reduce and conquer algorithm</span> which searches through an array and checks if an element $k$ is in it.

**How it works**
1) The <b><span style='color: var(--mk-color-yellow)'>array has to be sorted</span></b>
2) Check the element in the middle, $n/2$
3) If it is not $k$, then check if it is bigger or smaller than $k$
	1) If It is bigger than $k$, recurse to the <span style='color:#f7b731'>left</span>
	2) If it is smaller than $k$, recurse to the <span style='color:#f7b731'>right</span>
4) <span style='color:#f7b731'>Repeat steps 2 and 3</span> until $k$ is found or 1 element is left. 
5) If $k$ is found return $k$, if not return $-1$
<div style="break-after: page;"></div>

My <span style='color:#fa8231'>implementation of binary search</span> :
```java
public class BinarySearch {
	// Doing this iterativly
	public static int binarySearch(int[] arr, int key) {
		int begin = 0, end = arr.length, mid;
		
		while (begin < end){
			mid = begin + (end - begin) / 2; // Set mid per iteration, no overflow error
			if (arr[mid] == key) { // Nice we found the key
				return arr[mid];
			} else { // If we didnt find the key at mid
				if (arr[mid] > key) { // If the mid value is bigger go left
					end = mid;
				} else { // If the mid value is smaller go right
					begin = mid + 1;
				}
			}
		}
		// Nooo cannot find the element
		return -1;
	}
	
	public static void main(String[] args) {
		int [] arr = {2,4,4,5,6,7,8,9,10,13,16,17,20,21};
		int result = binarySearch(arr, 10);
		System.out.println(result);
	}
}
```

<span style='color:#fa8231'>Time complexity</span> for <span style='color:#0fb9b1'>binary search</span> is : <b><span style='color: var(--mk-color-green)'>O(log n)</span></b>.
## Uses of Binary Search

A binary search can not only be used to search something in an array ;
- It can be used as an <span style='color:#f7b731'>optimisation technique</span>
- It can solved <span style='color:#0fb9b1'>monotonic problems</span>, where something is <span style='color:#f7b731'>always increasing or decreasing but never both</span>
<div style="break-after: page;"></div>

# Peak Finding
---
Lets say there is a function, and the task is to <span style='color:#fa8231'>locate the maximum value of that function</span>. Well it can be difficult to find the global maximum and thus a <span style='color:#fa8231'>local maximum can be good enough</span>.

Thus <span style='color:#0fb9b1'>peak finding</span>, is an algorithm to <b><span style='color: var(--mk-color-yellow)'>find the local maximum</span></b> which can be faster than finding the global maximum using the reduce and conquer strategy.

To <span style='color:#fa8231'>find a global maximum</span> take <b><span style='color: var(--mk-color-yellow)'>O(n)</span></b> time at best.

**How it works**
1) Check the element in the middle, $n/2$
2) If it is a peak, the its <span style='color:#f7b731'>left and right neighbours are smaller</span> than the middle element
	1) If the left is bigger than the middle element, recurse to the <span style='color:#f7b731'>left</span>
	2) If the right is bigger than the middle element, recurse to the <span style='color:#f7b731'>right</span>
3) <span style='color:#f7b731'>Repeat steps 2 and 3</span> until a peak is found or 1 element is left. 
4) If <span style='color:#f7b731'>1 element is left </span>then by <span style='color:#f7b731'>definition it is a peak</span>

We are <b><span style='color: var(--mk-color-yellow)'>guarantee</span></b> to find a peak no matter the array. This is because if `arr[mid + 1]` is bigger than `arr[mid]`, the program will recurse to the right which means <span style='color:#f7b731'>there exist a peak somewhere</span>. And continue right if there is no peak until the <b><span style='color: var(--mk-color-yellow)'>last element, which by definition is a peak</span></b>.

Thus <span style='color:#f7b731'>there is a peak</span> in `arr[start, end]` it is <span style='color:#f7b731'>also a peak in</span> `arr[0,n-1]`.

My <span style='color:#fa8231'>implementation of peak finding</span> :
```Java
public class PeakFind {
    // Doing this iterativly
    public static int peakFind(int[] arr, int start, int end) {
        int mid = start + (end - start) / 2;
        
        if (mid - 1 >= 0 && arr[mid] < arr[mid - 1]) {
            return peakFind(arr, start, mid - 1);
        } else if (mid + 1 < end && arr[mid] < arr[mid + 1]) {
            return peakFind(arr, mid + 1, end);
        } else {
            return arr[mid];
        }
    }
}
```

<span style='color:#fa8231'>Time complexity</span> for <span style='color:#0fb9b1'>peak finding</span> is : <b><span style='color: var(--mk-color-yellow)'>O(log n)</span></b>.

However, this algorithm <span style='color:#eb3b5a'>does not always find steep peaks </span>(It has to be bigger than its neighbours). <span style='color:#fa8231'>To solve this issue</span>, if they are <span style='color:#f7b731'>equal, recurse on both sides</span>. However this will become <b><span style='color: var(--mk-color-red)'>O(n^2)</span></b> time complexity. It will be better if a <span style='color:#0fb9b1'>linear search</span> is used.

## 2-Dimention Peak Finding

Now instead of a 1D array, <span style='color:#f7b731'>now there is a 2D array</span>, which represents a plane and the task is to find a peak. 

**Method 1**
One way to do is through a <span style='color:#f7b731'>scan on each column and get the maximum</span>, afterwards use the 1D algorithm to <span style='color:#f7b731'>get the peak</span>. This however is <b><span style='color: var(--mk-color-red)'>slow at O(mn + log(m))</span></b>.

**Method 2**
A faster way is through <span style='color:#0fb9b1'>lazy evaluation</span>, similar to [[#Binary Search|binary search]], 
1) Take the middle and the neighbouring columns
2) Get their max value
3) If its not a peak recurse to the left or right depending on which is bigger
4) Repeat steps 1 and 3, until a peak is found or it is the last column

This will be faster with a time complexity of <b><span style='color: var(--mk-color-red)'>O(n log m)</span></b>.

**Method 3**
A <span style='color:#fa8231'>faster approach</span> will be through a <span style='color:#f7b731'>reduce and conquer strategy</span>,
1) <span style='color:#f7b731'>Segment the array into 4 segments</span>, `m/2` and `n/2`
2) Afterwards <span style='color:#f7b731'>search</span> the cross and the boarder (A plus within the boarder) for the <span style='color:#f7b731'>max element</span>
3) If it is not the peak, <span style='color:#f7b731'>recurse into a quadrant </span>
4) Repeat steps 1 and 3

This can find a local peak within the quadrant <span style='color:#eb3b5a'>but not the whole matrix</span>. Since it does not check what is outside the boundary.

<span style='color:#fa8231'>Time complexity</span> for this version of <span style='color:#0fb9b1'>2D peak finding</span> is : <b><span style='color: var(--mk-color-red)'>O(n + m)</span></b>.


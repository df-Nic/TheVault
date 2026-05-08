---
Title: Order Of Growth
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - AlgorithmAnalysis/TimeComplexity
---
## Table Of Contents
- [[#Order of Growth|Order of Growth]]
	- [[#Order of Growth#Different Time/Space Complexity|Different Time/Space Complexity]]
	- [[#Order of Growth#Time Complexity of Python Functions|Time Complexity of Python Functions]]
	- [[#Order of Growth#Calculating Time Complexity|Calculating Time Complexity]]
---

## Order of Growth

It is to analyze the <mark style='background:#0fb9b1'>growth rate</mark> with reference to the <mark style='background:#0fb9b1'>size</mark> of the input.

**Time Complexity:** Time taken to run a program
**Space Complexity:** Memory / Space needed when running the program

### Different Time/Space Complexity

![[Time Complexity Chart.png|center]]
<div style="page-break-after: always;"></div>

### Time Complexity of Python Functions

![[Python functions time complexity.png|center]]

**Things to take note of**
-  Concatenating a new list or tuple take O(n) time
-  The space complexity for string / lists / tuples all depends on the size thus O(n). list ** 2 will be O(n<sup>2</sup>)
- A fixed list / tuple that does not get modified besides `list.pop()` takes O(1) space
- Time will never be smaller than space, as it will need x amount of time to read / write from the space
-  Space can be reused

### Calculating Time Complexity

For time complexity we need to identify the **dominant** term and ignore additive or multiplicative constants

For example:

O(4n2 + 1000n + 3) = O(n2)

N log 4 (n) = n log n (Bases is not important does not contribute much)
<div style="page-break-after: always;"></div>

## Explaining Time & Space Complexity
---

### Time

To justify time complexity of any program you have to link time complexity to the number of statements executed and the maximum depth of the program

Example 1:

```Python
def fun(n):
	if n==0:
		return 0
	elif isPower_of_2(n):
		return n + fun(n//2)
	else:
		return n + fun(n-1)
```

The above function is a recursive function. <span style='color:#2d98da'>N will recursively reduce from n to n/2</span>. This will take n/2 -1 number of executions, thus for the first part it will take O(n) time.

Once it reaches a number that is divisible by, it will be divided by 2 until 0 and will stay to a power of 2 until it reaches 0.  This will take O(log n) time.

Total time complexity is O(n) + O(log n) => O(n)

Example 2:

```Python
def fun2(n):
	result = 0
	for i in range(n):
		for j in range(1,n):
			if (j > i):
				result  += fact(j)
return result
```

The above function in the inner most loop, it will call fact which is a function that runs O(n) time. The inner loop, the value of j<span style='color:#2d98da'> will go from 1 to n-1</span>, thus it will <span style='color:#2d98da'>execute fact at most n times</span> thus the time complexity is O(n<sup>2</sup>).

The outer loop, the value of <span style='color:#2d98da'>i will iterate from 0 to n-1</span>, thus it will <span style='color:#2d98da'>execute the inner loop n times</span> as well, thus the total time complexity of the function is O(n<sup>3</sup>).

Example 3:

```Python
def fun(n, m):  
	if n==0:  
		return 0  
	elif n%m==0:  
		return n + fun((n-1)//m, m)  
	else:  
		return n + fun(n-1, m)
```

What is the time complexity where 1 < m < n:

The else statement will <span style='color:#2d98da'>execute at most (m-1)</span> times which will then reach to the `elif` branch.
The `elif` statement will divide n by m, thus it will execute at most logm n till n is 0. Therefore, we will do at most (m - 1) reduction of n until it reaches the `elif`. Therefore the time is O(m logm n).
  
**Space**

For space complexity relate it to
1.      Length of the variables
2.      Number of variables (Local variables from recursive calls)

From Example 1:

The space complexity for the function is O(n) where <span style='color:#2d98da'>n is the number of return values for a maximum recursion depth</span>. At the start there will be n recursive calls in total until n is divisible by 2 thus it will take n space O(n)

When the value is divisible by 2 it will then take O(log n) space as the value will be divided by 2 until it becomes 0. The total space complexity is O(n) + O(log n) => O(n) space

From Example 2:

The space complexity is O(1). This is because the <span style='color:#2d98da'>number of variables used is constant</span>. In addition, <span style='color:#2d98da'>each iteration of the for loops does not introduce extra memory</span> as the <span style='color:#2d98da'>variables are overwritten</span> with the new values.

Example 3:

```Python
def foo (tup):
	if (t):
		Foo(tup[:-1])
```

The space complexity of the function above is O(n<sup>2</sup>). As every <span style='color:#2d98da'>recursive call will spilt the tuple</span> (list is also the same) from length of n to length of n – 1 thus the space used of O(n). The <span style='color:#2d98da'>maximum recursion depth is n since the base case is when the tuple is empty</span>, n to 0. Since each recursive call uses O(n) space, the total space is O(n<sup>2</sup>).

If they ask for time space complexity after running a large number of times with memoization:

**Time: O(1)**  
**Space: O(n)**  

As after a while all the values will be cached and it will just be a O(1) look up. Space is linear to the inputs as the dictionary will contain previous results.
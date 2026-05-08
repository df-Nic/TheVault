---
Title: Iterative Functions
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
---
## Table Of Contents
- [[#Recursion|Recursion]]
	- [[#Recursion#Types of recursion|Types of recursion]]
- [[#Iteration|Iteration]]
	- [[#Iteration#While Loops|While Loops]]
	- [[#Iteration#For Loops|For Loops]]
---

## Recursion
---
**1.** Have a terminating condition
	Usually 0 or 1 or empty list
**2.** Figure out the recursive call
**3.** Test your code with a small input size / test case


### Types of recursion
---

1. Linear Recursion

```Python
def factoral(n):
	if (n == 1):
		return 0
	else:
		return n * factorial(n-1)
```

It is a recursive function that makes a <mark style='background:#2d98da'>single</mark> call to itself
Time Complexity: **O(n)**

2. Exponential Recursion

```Python
def fib(n):
	if (n == 0):
		return 0
	elif (n == 1):
		return 1
	else:
		return fib(n-1) + fib(n-2)

print(fib(4))
```

It is a recursive function that makes a <mark style='background:#2d98da'>exponential</mark> number of calls to itself
Time Complexity: **O(n<sup><b>2</b></sup>)**

3. Mutual Recursion

```Python
def ping(n):
	if (n == 0):
		retrun n:
	else:
		print("Ping")
		pong(n-1)

def pong(n)
	if (n == 0):
		return n
	else:
		print("Pong")
		ping(n-1)
```

It is a recursion that does not call itself, it can work with **larger groups** or in **pairs**.

4. **Tail Recursion**

It is a type of recursion where the last statement is executed by the function. This means that there is no **baggage**. For example, F(n-1) does not need F(n-2) to complete.

**Do note that python does not support tail call optimization**

```Python
def sum_n(num,n)
	if n == 0:
		return num
	else:
		num += n
		return sum_n(num, n-1)

print(sum_n(0,10)) # => 55
```

## Iteration

### While Loops
---

```Python
def print_a(n):
	while (n > 0):
		print('a')
		n -= 1

print_a(4)
```

For a while loop the expression must be true for the loop to continue

The system will manage the stack and can be expensive in terms of time and space.

### For Loops
---

```Python
def print_a(n):
	for i in range(n):
		print("a")

print_a(4)
```

For a for loop the body will be evaluated once for each increment of I (Not inclusive of end)

You have to code out the logic yourself but it can be less expensive.

>`for i in range (0,10,-1)` **won’t do anything**
>`for I in range (10, 0,-1)`will go from 10 - 1

**Keywords:**
<span style='color:#fa8231'>Pass</span>: The part of the code does nothing
<span style='color:#fa8231'>Continue</span>:  Will force the loop to begin the next iteration
<span style='color:#fa8231'>Break</span>: Will stop the loop entirely
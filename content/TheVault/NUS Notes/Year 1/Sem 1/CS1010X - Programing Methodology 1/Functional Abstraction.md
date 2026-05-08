---
Title: Functional Abstraction
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - ProgrammingLanguage/Python
---
## Table Of Contents
- [[#Functions|Functions]]
	- [[#Functions#Args & Kwargs|Args & Kwargs]]
	- [[#Functions#Forgiveness Attitude|Forgiveness Attitude]]
- [[#Lambda Functions|Lambda Functions]]
	- [[#Lambda Functions#Nested Lambda Functions|Nested Lambda Functions]]
	- [[#Lambda Functions#Accessing Lambda Function in a tuple/list|Accessing Lambda Function in a tuple/list]]
---

## Functions

```Python
# Example of a function in python
def add_2 (number):
	number += 2
	return number
```

We can nest function calls like so `add_2(add_2(1))`. The inner most function will be called first. The result will be 5.

Take note, `Print(add_2` or `x = add_2`, without the (), it will just be a function variable at storage address

Take note that any function call or self define if statements as inputs will be executed or evaluated first before calling the function.
```Python
def new_if(pred, then_clause, else_clause):
	if pred:
		then_clause
	else:
		else_clause

def p(x):
	if x>20:
		print(x)
	else:
	# x > 5 will become T/F, print(x) will print x first and the input will be None, 
	# p(2*x) will execute p recursively again before executing new_if
		new_if(x>5, print(x), p(2*x))
p(4) # 4 8 16 32
```

### Args & Kwargs
---
Args and Kwargs are denoted by * and ** respectively and are used for a unknown amount of inputs in a function.

It can be used as inputs for a specific function.

```Python
def helper(op, args):
	return op(*args) # *args as a input will treat each item in a iterable as a individual input if the input for the function is *args as well

# *args => (1,2,3) # Each element is a input
# args => ((1,2,3),) # The whole tuple is ONE input

print(helper(lambda x : x * x, (2,)))
print(helper(lambda x, y : x * y,(2,1)))
```

Take note that if a tuple is an input for args, the function will treat it as one input and therefore, args will be a nested tuple. `Input = (1,2,3), args = ((1,2,3),)`.

Thus a get around is to put a * or a ** when using an input.
```Python
def add_one(*args):
	return tuple(map(lambda x : x + 1, args))

x = (1,2,3)
print(add_one(*x))
print(add_one(x)) # Type error as args = ((1,2,3),)
```

**Args**
> Args will be in the form of a tuple

**Kwargs**
> Kwargs will be in a dictionary, where the user denotes the keys and the values

```Python
fn(a = "Real" , b = "Python", c = "Is", d = "Great", e = "!")
```
<div style="page-break-after: always;"></div>

### Forgiveness Attitude
---
If the variable cannot be found on the left-hand side it can be found in global. If the variable is referenced in the function, it will cause an error. To get around this you can use **GLOBAL** beside the variable name.

```Python
x = 10

def add_2():
	#Global x (To fix the issue add in this line)
	x += 2 
	return x

# => Error local variable x referenced before assignment

def add_2():
	return x + 2

add_2() # => 12
```

## Lambda Functions

```Python
# Simple Lambda Function
fn_1 = lambda x : x + 1

print(fn_1(10))

# Lambda function with if/else
fn_2 = lambda x : x + 1 if True else x - 1

print(fn_2(10))

# Returning a lambda function
def function(x):
	return lambda x: x + 1

print(function(1)) # This will print the lambda function
```

Lambdas are special function that are assigned to a variable
<div style="page-break-after: always;"></div>

### Nested Lambda Functions
---
```Python
def twice(f):
	return lambda x : f(f(x))

def thrice(f):
	return lambda x : f(f(f(x)))

# print(thrice(twice(twice))(lambda x : x +1)(0)) # -> Add 1 will run (2*2) ** 3
# print(twice(thrice)(twice)(lambda x : x +1)(0)) # -> Add 1 will run 2 ** (3**2) times 
# print(twice(thrice)(twice(lambda x : x +1))(0)) # Add 1 will run (3**2) * 2 times
```


### Accessing Lambda Function in a tuple/list
---
```Python
f = lambda f,g : (f,(g))
g = lambda g : g(g, g)

print(g(f)[0](4,2))
```

You can also store lambdas inside tuples/lists and call them with the index notation.

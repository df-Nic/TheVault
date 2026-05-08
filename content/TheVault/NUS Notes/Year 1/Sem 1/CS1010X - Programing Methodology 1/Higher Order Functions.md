---
Title: Higher Order Functions
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - ProgrammingLanguage/Python
---
## Table Of Contents
- [[#What are Higher Order Function (HOF)|What are Higher Order Function (HOF)]]
	- [[#What are Higher Order Function (HOF)#Examples of Other HOF|Examples of Other HOF]]
---

## What are Higher Order Function (HOF)
---

```Python
def accumulate(op, base, n, next, term):
	if (a == 0):
		return base
	else:
		return op(term(n), accumulate(op, base, next(n), next, term))

'''
OP and Term are abstracts of the parameters in higher order functions.

OP: Usually the combiner / generic operator
Base: Is the base case for the recursion
Next: Is how n will be changed which will lead to the base case
Term: Is the function which will be carried out
N: Is the input for the function
'''
```

They are functions which can be used with other functions to return the same result. 

With the example above, we can simulate the `map` function in python with any function to be used on each element in a iterable object.

For higher order functions we need to be warry of the operator, for instance fold **NEEDS** to start from f(0) unlike for instance sum as addition in any order will yield the same result, same goes for something simple like multiplication and division.

### Examples of Other HOF

```Python

#### Fold Left ####
def fold_left(fn, initial, seq):
	if seq == ():
		return initial
	else:
		return fn(fold_left(fn, initial,seq[:-1]), seq[-1])
'''
op = function of the operator used to combine the sequence
base = base value of the sequence
seq = str,list,tuple,dict,set
'''

#### Fold ####
def fold(op, f, n):
	if n == 0:
		return f(0)
	else:
		return op(f(n), fold(op, f, n-1))
'''
Returns a value by combining the value created by term on each sequence of n based on the op function
op = function of the operator used to combine the sequence
term = function of the pattern
n = number of sequences
'''

#### Fold2 ####
def fold2(op, term, a, next, b, base):
	if a > b:
		return base
	else:
		return op(term(a), fold2(op, term, next(a), next, b, base))

'''
Returns a value by combining the value created by term on each sequence from a to b based on the op function
op = function of the operator used to combine the sequence
term = function of the pattern
a = starting sequence
next = function for the increase from a to b
b = ending sequence
base = base value of the sequence
'''

#### Sum ####
def sum(term, a, next, b):
	if a > b:
		return 0
	else:
		return term(a) + sum(term, next(a), next, b)

'''
Returns the sum by adding all the term function on a to b
term = function of the pattern
a = starting sequence
next = function for the increase from a to b
b = ending sequence
'''

#### Product ####
def sum(term, a, next, b):
	if a > b:
		return 0
	else:
		return term(a) * sum(term, next(a), next, b)

'''
Returns the product by multiplying all the term function on a to b
term = function of the pattern
a = starting sequence
next = function for the increase from a to b
b = ending sequence
'''
```

---
Title: Generic Operators
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - ProgrammingLanguage/Python
---
## Table of Contents
- [[#What is it|What is it]]
- [[#Challenges|Challenges]]
- [[#Generic Abstraction Layer|Generic Abstraction Layer]]
	- [[#Generic Abstraction Layer#Ways to Build an Abstraction Layer|Ways to Build an Abstraction Layer]]
		- [[#Ways to Build an Abstraction Layer#Dispatching on Type|Dispatching on Type]]
		- [[#Ways to Build an Abstraction Layer#Data-directed Programming|Data-directed Programming]]
		- [[#Ways to Build an Abstraction Layer#Message Passing|Message Passing]]
---

## What is it
---
Using similar functions we can operate on different representations of data or data structures to return similar results.

Different representations might have slightly different accuracy due to internal representation. However we can reuse codes even though it is different due to **data abstraction**.
<div style="page-break-after: always;"></div>

## Challenges
---
1.  Match representations to its respective operations

One solution is to **tag** the data to explicitly indicate the representation type.

```Python
# Rectangular (<rectangular data>)
# Polar (<polar data>)

def attach_tag(type_tag, contents):
	return (type_tag,) + contents

def type_tag(datum): # Will return the type_tag
	if type(datum) == tuple and len(datum) == 3:
		return datum[0]
	else:
		raise
		Exception("Bad tagged datum -- type_tag" + str(datum))

def contents(datum): # Will return the type_tag
	if type(datum) == tuple and len(datum) == 3:
		return datum[1:]
	else:
		raise
		Exception("Bad tagged datum -- type_tag" + str(datum))
```

Therefore with tagging, we can check the type tag on the data structure to decide which function we will use. To implement this just call the `attach_tag()` function inside the constructors. 

```Python
# Rectangular form constructors
def make_from_real_imag(x,y):
	return attach_tag('rectangular',(x,y))

# Polar form constructors
def make_from_real_imag(x,y):
	return attach_tag("polar", (math.hypot(x,y), math.atan(y/x)))
```
<div style="page-break-after: always;"></div>

2.  Naming conflicts

Even with tagging, there is still an issue with naming as shown above. One way to bypass this issue is to also end the function name with the data tag.

```Python
# Rectangular form constructors
def make_from_real_imag_rectangular(x,y):
	return attach_tag('rectangular',(x,y))

# Polar form constructors
def make_from_real_imag_polar(x,y):
	return attach_tag("polar", (math.hypot(x,y), math.atan(y/x)))
```

## Generic Abstraction Layer
---
Have functions that will handle the different data representations to use the correct functions or return the correct data representation.

### Ways to Build an Abstraction Layer
---

#### Dispatching on Type

The way to accomplish this is to check the data type and call the appropriate function, this is called dispatching on type.

Generic operators work on data that could take on multiple forms, also known as polymorphic data.

```Python
def real_part(z): # This selector is now generic
	if is_rectangular(z):
		return real_part_rectangular(contents(z))
	elif is_polar(z):
		return real_part_polar(contents(z))
	else:
		raise Exception("Unknown type -- real_part" + z)
```

Some issues with this is that:
- Need to know all the different data types available
- Adding a new type requires a change in all generic operators
- Does not resolve naming conflicts

#### Data-directed Programming

The generic operators can use lookup tables to find the correct operation based on the data tag.

This method address the problem of naming conflicts and allows for easy extension by adding more entries to the table.

**Accessing the tables**

There will be 2 functions to manipulate the table, one is `get()`, the other is `put()`.

Note that the <b><span style='color:#f7b731'>Table</span></b> should be a global variable to be accessed.

```Python
table {}

def put(op, data_type, fn) # Op is a function name in strings ie "Add", "Subtract" etc
	if op not in table:
		table[op] = {}
	table[op][data_type] = fn

def get(op, types):
	return table[op][types] # This will return the specfic function
```

To populate the table we can define functions that when called will add the functions into the table.
<div style="page-break-after: always;"></div>

Example:
```Python
from math import *

def install_rectangular_package():

	## Function for this data type ##
	def make_from_real_imag(x,y):
		return attach_tag('rectangular',(x,y))

	def real_part(z):
		return z[1]

	def image_part(z):
		return z[2] # Because 0 is the data tag

	def angle(z):
		return math.hypot(real_part(z), imag_part(z))

	def magnitude(z):
		return math.atan(real_part(z) / imag_part(z))

	def make_from_mag_ang(r,a):
		return make_from_real_imag(r * math.cos(a), r * math.sin(a))

	## Putting the functions above into the table ##

	def tag(x):
		return attach_tag('rectangular',x)

	put('real_part', ("rectangular",), real_part) # The function will be index with the op and the data type
	put('imag_part', ("rectangular",), imag_part)
	put('magnitude', ("rectangular",), magnitude)
	put('angle', ("rectangular",), angle)
	put('make_from_real_imag', "rectangular", make_from_real_imag)
	put('make_from_real_imag', "rectangular", make_from_real_imag)

	return "Done"
```
<div style="page-break-after: always;"></div>

Using the following function, we can fetch the specific data type function to operate one.

```Python
def apply_generic(op, *args):
	type_tags = tuple(map(type_tag,args)) # Contains a table of all the data tags inside args
	fn = get(op, type_tags) # based on the op and the tags, get the correct function in the table
	return fn(*args)

# Note that type tag is definded above

# To carry execute a function
def real_part(z):
	return apply_generic('real_part', z)
def imag_part(z):
	return apply_generic('imag_part', z)
```

#### Message Passing

This methods makes the data <span style='color:#f7b731'>"intelligent"</span>. Meaning, the user will just need to tell the data what you want and they will act on themselves.

It accepts an input and performs the necessary action based on the input. This is the basis of <span style='color:#f7b731'>object-oriented programming</span>. 

```Python
def make_from_real_imag(x,y):
	def dispatch(op):
		if op == 'real_part':
			return x
		elif op == 'imag_part':
			return y
		elif op == 'magnitude':
			return math.hypot(x,y)
		elif op == 'angle':
			return math.atan(y/n)
		else:
			raise Exception("Unknown op -- make_from_real_imag" + op)
	return dispatch
```
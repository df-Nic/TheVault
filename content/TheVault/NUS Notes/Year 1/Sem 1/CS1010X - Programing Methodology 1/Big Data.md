---
Title: Big Data
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - ProgrammingLanguage/Python
---
## Table of Contents
- [[#Processing Big Data|Processing Big Data]]
- [[#Functions to Handle Data|Functions to Handle Data]]
- [[#Working with CSV Files|Working with CSV Files]]
---

## Processing Big Data
---
There are 5 steps in processing big data:
1. Filtering
2. Accumulating
3. Searching
4. Sorting
5. Mapping

## Functions to Handle Data
---
**Accumulate (HOF)**

```Python
def accumulate(fn, initial, seq):
	if seq == ():
		return initial
	else:
		return fn(seq[0], accumulate(fn, initial, seq[1:]))
```

It will execute a function in a sequence from right to left.

**Map**

```Python
square_fn = lambda x : x ** 2
lst = [1,2,3]

list(map(square_fn, lst)) # => [1,4,9]
# The map function returns a iterable, thus type casting to a list is needed to view the output. All iterators can be iterated using the next() function
```

The map function applies each element in a sequence. 

**Filter**

```Python
filter_fn = lambda x : x <= 10
lst = [8,9,10,11,12,13]

list(filter(filter_fn,lst)) # => [8,9,10]
# The filter function returns a iterable, thus type casting to a list is needed to view the output.
```

Filters out elements in a sequence based on a condition.

**Enumerate**

```Python
lst = [1,2,3,4]
list(enumerate(lst)) # => [(0,1), (1,2), (2,3), (3,4)]
```

The enumerate adds an index as a key to the enumerate object.

## Working with CSV Files
---
Using the csv library, we can read a CSV file and import the data into python for our use

```Python
import csv

def read_csv(filename):
    with open(filename, 'r') as f:
        lines = csv.reader(f, delimiter=',')
        return tuple(lines)[1:] # Index 0 is the header, unless the CSV has no header then there is no need to slice the tuple.
```

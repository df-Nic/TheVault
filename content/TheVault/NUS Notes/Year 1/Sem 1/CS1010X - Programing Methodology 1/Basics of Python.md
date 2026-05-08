---
Title: Basics of Python
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - ProgrammingLanguage/Python
---
## Table Of Contents
- [[#Order of Precedence|Order of Precedence]]
- [[#Logic operators|Logic operators]]
	- [[#Logic operators#Not|Not]]
	- [[#Logic operators#And|And]]
	- [[#Logic operators#Or|Or]]
	- [[#Logic operators#Boolean Values|Boolean Values]]
- [[#Comparators|Comparators]]
	- [[#Comparators#Equivalence|Equivalence]]
	- [[#Comparators#Identity|Identity]]
- [[#List/Tuple/String Slicing|List/Tuple/String Slicing]]
- [[#Generic Functions|Generic Functions]]
---

## Order of Precedence

| **Order** |                    **Operator**                     |               **Syntax**                |
| :-------: | :-------------------------------------------------: | :-------------------------------------: |
|     1     |                     Parentheses                     |                  `()`                   |
|     2     | Exponent (This operator will go from right to left) |                  `**`                   |
|     3     |  Multiplication, Division, Floor division, Modulus  |               `* / // %`                |
|     4     |                Addition, Subtraction                |                  `+ -`                  |
|     5     |                 Comparison Identity                 | `==, <=, >, !=, is, is not, in, not in` |
|     6     |                         Not                         |                  `not`                  |
|     7     |                         And                         |                  `and`                  |
|     8     |                         Or                          |                  `or`                   |

**Take note that the return value for:**
- **%**
	a % b, where a < b returns <span style="color:orange">a</span>
	a % b, where a < b returns <span style="color:orange">remainder</span>
- //
	<span style="color:orange">Rounded down</span> integer of the float

## Logic operators

### Not
---
|   **X**   | <span style="color:orange">Not</span> **X** |
|:-----:|:---------------------------------------:|
| True  |                  False                  |
| False |                  True                   |

### And
___
| X <span style = color:orange>And</span> Y | False     |   True   |
|:-----------------------------------------:| --------- |:--------:|
|                   True                    | **False** | **True** | 
|                   False                   | **False** |     **False**     |

>For **AND** if both values are true, it will return the 2nd value, if both are false it will return the 1st value.
>
>If one value is false it will return the **False** value.

### Or
___

| X <span style = color:orange>Or</span> Y | False     |   True   |
|:-----------------------------------------:| --------- |:--------:|
|                   True                    | **True** | **True** | 
|                   False                   | **False** |     **True**     |

>For **OR** if both values are true, it will return the 1st value, if both are false it will return the 2nd value.
>
>If one value is false it will return the **True value**.


<div style="page-break-after: always;"></div>

### Boolean Values
--- 

|          | <span style = color:orange>True</span> | <span style = color:orange>False</span> |
|:--------:|:--------------------------------------:|:---------------------------------------:|
| Integers |                   1                    |                    0                    |
|  Values  |          Any non-empty value           |            Null, Empty, None            |

> When doing operators with Booleans it will use its integer form.
> 
> 10 != True but 1 == True OR 1 - False = -1


## Comparators
---
### Equivalence

`==`, means that 2 objects have identical elements.

```Python
x = [1,2,3,[4,5]]
y = [1,2,3,[5,4]]
z = [1,2,3,[4,5]]

print(x == y) # => False
print(z == x) # => True
```

### Identity

The `is` keyword refers to 2 objects being the same (Reference to memory address).

```Python
x = [1,2]
y = [1,2]
z = x

print(x is y) # => False, as they are 2 different objects with different memory
print(z is x) # => True, as z is referencing to x, having the same memory address
```

<div style="page-break-after: always;"></div>

## List/Tuple/String Slicing
---
| Positive Index  | 0   | 1   | 2   | 3   | 4   |
| --------------- | --- | --- | --- | --- | --- |
| Negative Index  | -5  | -4  | -3  | -2  | -1  |
| **List/String** | [1  | 2   | 3   | 4   | 5]  |
| Positive Slice  | 0   | 1   | 2   | 3   | 4   |
| Negative Slice  | -5  | -4  | -3  | -2  | -1  |


The code for slicing is `lst[start,end,step]`, where start is inclusive and end in exclusive.

Examples:
```python
List [ : : -2] => [5, 3, 1] List [ 1:  -1] => [2, 3, 4]  List [ -1: -4 ] => []  
List [-3 : -1] => [3, 4] List [ : 20] => [1, 2, 3, 4, 5]  List [20 : ] => [ ]  
List [-2 : 10] => [4, 5]  List[3 : 0 :-2] => [4, 2]
```

You can delete items using `del(List [start : stop])`.

We can also assign variables using slicing, `List [1:3] = [1] #=>[1, 1, 4, 5]`.

<div style="page-break-after: always;"></div>


## Inner/Helper Functions
---

If a problem is difficult to solve, we can create some smaller helper functions which can help to solve parts of the problem for us to make our code simpler and reduces repeated code.

### Closing and Binding

This is for <span style='color:#3867d6'>inner functions or nested functions</span>. Any variable referenced by the nested function from the outer function will retains its access to it even after finishing execution.

Python has 2 terms <span style='color:#3867d6'>binding and closing</span>.

**Binding**: When a nested function references a variable from the outer function scope and it is a immutable data type, it can only access the value and not edit it.

**Closing**: When a nested function references a variable from the outer function scope and it is a mutable data type, it can  access tand edit values.

```Python
def counting_deep_replace(lst,a,b):

    counter = [0] # Closing
    counter_2 = 0 # Binding

    def deep_replace(lst,a,b):
        length = len(lst)

        if lst:
            for i in range(length):
                if lst[i] == a:
                    lst[i] = b
                    counter[0] += 1
                    # counter_2 += 1 Will raise an error, saying that the variable is referenced before created
                elif (isinstance(lst[i], list)):
                    deep_replace(lst[i], a, b)
  
    deep_replace(lst,a,b)

    return counter[0]
```

<div style="page-break-after: always;"></div>

## Generic Functions
---
**Abs**

Returns the absolute (positive) value of an integer.
```Python
print(abs(-1.25)) # => 1.25
print(abs(-100.59)) # => 100.59
```

**Isnumeric**

Checks if every character in the string is between 0 - 9.
Negative numbers do not count.
```Python
str_1 = "12345"
print(str_1.isnumeric()) # => True

str_2 = "1,2,3,4,5"
print(str_2.isnumeric()) # => False

str_3 = "-1.2"
print(str_3.isnumeric()) # => False
```

**Round**

Rounds a float to the nearest specified decimal point. If no decimal point was given then it will round to a whole number.

5 and above will cause the number to be rounded up.
```Python
round(9.54) # => 10
round(9.4563, 2) # => 9.46
round(9.33,1) # => 9.3
```

<div style="page-break-after: always;"></div>

**Max / Min**

Returns the largest / smallest value in the sequence
```Python
x = [1,2,3,4,5]
y = ["a","b","c","d","E"]

print(min(x)) # => 1
print(max(x)) # => 5
print(min(y)) # => E
print(max(y)) # => d

# How it works with letters is it uses the ASCII value for that letter. We can see whats its value using ORD()

print(ord("E")) # => 69
print(ord("d")) # => 100
```

**Sum**

Sum up all the values in a sequence
It will raise and error if it's not a sequence or there is a non int / float.
```Python
print(sum([1,2,3,4,5])) # => 15
print(sum([1.2,1.3,1.4])) # => 3.9
```

**Sorted**

Returns a sorted sequence. Any sequence other than a list will be converted into a list.

```Python
tup = (1,3,4,2)
sorted_seq = sorted(tup)
print(sorted_seq) # => [1,2,3,4]

sorted_seq = sorted(tup, reverse = True)
print(sorted_seq) # => [4,3,2,1]

sorted(tup, key = function) # => Will sort the list based on the function (Condition). Usually for nested list / tuples and want to sort by a specfic element
```

<div style="page-break-after: always;"></div>

**Del**

Delete / remove items from a sequence.

```Python
tup = (1,2,3,4,5)

del tup[0] # => (2,3,4,5)
del tup[1:3] # => (2,5)

dictionary = {"one" : 1, "two" : 2, "three" : 3}

del dictionary["two"] # => {"one" : 1, "three" : 3}
```

**Print**

Prints out a string

```Python

print("Hello")

print("1" + "2") # '12'
# print(1 + "2") # Error

print("Hello", str(19), "people") # 'Hello 19 people'. The , adds in a space. 

# If you use a + instead of a , you need to manually add in a plus
```

**Upper bound comparison**

The following command `float('inf')`, can be used as a upper bound when finding minimum values in python.

```python
float('inf') # this is a very large number in python and can be used as a upper bound.
```
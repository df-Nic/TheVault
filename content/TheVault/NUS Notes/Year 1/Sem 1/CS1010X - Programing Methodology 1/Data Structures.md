---
Title: Data Structures
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - ProgrammingLanguage/Python
  - DataStructures
---
## Table of Contents
- [[#Tuples|Tuples]]
	- [[#Tuples#Joining tuples|Joining tuples]]
	- [[#Tuples#Tuple Functions|Tuple Functions]]
- [[#Lists|Lists]]
	- [[#Lists#List Functions|List Functions]]
- [[#Dictionary|Dictionary]]
	- [[#Dictionary#Dictionary Functions|Dictionary Functions]]
- [[#Sets|Sets]]
	- [[#Sets#Set Functions|Set Functions]]
---
## Tuples
---
```Python
# Tuple in Python
tup = (1,2,3)
# Nested Tuple in Python
tup_nested = (1,2,3,(4,5))
````

Tuples are **immutable**, once created the contents cannot be changed. Slicing works with tuples, `tup[1:2:-1]`, however this will create a new copy.

**Tuples are hash-able** therefore, they can be used as keys in dictionaries.

### Joining tuples

`(1) + (1) = 2` , no comma means it’s not a tuple

`(1,) + (1,) = (1,1)`, `(1,) + ((1,2),) = (1,(1,2))`, for nested tuples make sure the outer most bracket has a comma as well

`Tup [:index]: + (5,) + Tup[index:]`, to insert into a tuple based on index

Combining tuples, time complexity is O(n).

Initializing tuples is O(1) time but modifying/copying it gives us O(n) time

Commas are tuple separators thus in python, `1 > 1,000,000 => (False, 0, 0)`

### Tuple Functions

**Count**

Returns the number of times the element appears in the tuple, **O(n) time**.

```Python
tup = (1,2,3,(4,5))

print(tup.count((4,5))) # => 1
```

**Index**

Returns the index of the element when it **first appears**, it takes **O(n) time**. If the element is not in the tuple it will raise an error.

```Python
tup = (1,2,3,4,3)

print(tup.index(3)) # => 2
print(tup.index(5)) # => tuple.index(x): x not in tuple
```

## Lists

---

```Python
# Lists in Python
lst = [1,2,3]
# Nested Lists in Python
lst_nested = [1,2,3,[4,5]]
```

Lists are similar to tuples however, they are immutable. Meaning the contents can be changed. `lst[0] = 10`.

Similar, to tuples, concatenating of 2 lists, the time complexity is O(n).

Lists are not hash-able therefore, they cannot be used as keys in dictionaries.

### List Functions

**Append**

Adds the elements at the back of the list, it takes **O(1) time**.  
It does not return anything and updates the list with the new element.

```Python
lst = [1,2,3]

lst.append(4) # => [1,2,3,4], return: None
```

**Clear**

Empties the list of all elements, it takes **O(n) time**.  
It does not return anything

```Python
lst = [1,2,3]

lst.clear() # => [], return None
```

**Copy**

Returns a **shallow copy** of a list, it takes **O(n) time**.

```Python
lst = [1,2,3,[4,5]]

lst_copy = lst.copy() # => lst_copy will have the contents of lst, since its a shallow copy, any changes to the inner lists will affect the original lst.
```

**Count**

Returns the number of times the element appears in the list, it takes **O(n) time**.

```Python
lst = [1,1,1,2,3,1]

lst.count(1) # => 4
lst.count(4) # => 0
```

**Extend**

Adds on elements in a list into another list or iterable, it takes **O(n) time**.  
It does not return anything and updates the list with the new elements.

```Python
lst_1 = [1,2,3]
lst_2 = [4,5,6]

str_x = "789"

lst_1.extend(lst_2) # => lst_1 will be [1,2,3,4,5,6], return None

# It also works with strings
lst_1.extend(str_x) # => lst_1 will be [1,2,3,4,5,6,'7','8','9'], return None
```

**Index**

Returns the first instance of the specified value, it takes **O(n) time**.

```Python
lst = [1,2,1,3,1,4]

print(lst.index(1)) # => 0
print(lst.index(1,1)) # => 2, here the start index is 1, the end index is last
print(lst.index(1,2,4)) # => 2, here the start index is 2 and the end is 4 
```

**Insert**

Inserts an element in a specified index, it takes **O(n) time**.  
It does not return anything and updates the list with the new element.

```Python
lst = [1,3,4]

lst.insert(1,2) # => [1,2,3,4], it will insert 2 into index 1 of the list
lst.insert(10,5) # => [1,2,3,4,5], if the index exceeds it will add the element to the back of the list

lst.insert(-1,6) # => [1,2,3,4,6,5], it works with negative indexes
```

**Pop**

Removes an element in a specified index and returns that element as well  
If an index is stated it takes **O(n) time**. If there is no index it will take **O(1) time**.

```Python
lst = [1,2,3,4,5]

element_1 = lst.pop() # => 5, since no index is stated, it will pop the last item
element_2 = lst.pop(1) # => 2, since 2 is in index 1
element_3 = lst.pop(-2) # => 3, after removing 2 elements, 3 will be in index -2

# Take note that if the index is out of range it will raise an error
```

**Remove**

Removes the first instance of the element, it takes **O(n) time**.  
It does not return anything and removes the element from the list.

```Python
lst = [1,2,3,4,5,3]

lst.remove(4) # => [1,2,3,5,3], return None
lst.remove(3) # => [1,2,5,3], return None
```

**Reverse**

Reverses the list from back to front, **O(n) time**.  
It does not return anything and updates the list.

```Python
lst = [1,2,3,4,5]

lst.reverse() # => [5,4,3,2,1], return None
```

**Sort**

It sorts the list from ascending or descending order **O(nlogn) time**.  
It does not return anything and updates the list.

```Python
lst = [1,4,6,3,8,10,2,5]

lst.sort() # => [1,2,3,4,5,6,8,10], return None
lst.sort(reverse = True) # => [10,8,6,5,4,3,2,1], return None
lst.sort(key = function) # => Will sort the list based on the function (Condition). Usually for nested list and want to sort by a specfic element in each list.
```

## Dictionary

---

```Python
# Dictonary in Python
dictionary = {"one" : 1, "two" : 2, "three" : 3, ("three", "four") : [3,4]}
dictionary_cast = dict{"one" = 1, "two" = 2, "three" = 3}

dictionary["two"] = 2
dictionary[("three", "four")] = [3,4] # We can use tuples as a key because they are hashable. Even tuples or tuples. But if there is a list in the tuple it wont work
```

Dictionaries are similar to hash tables, they take in a key value pair. They are unordered and no duplicates are allowed.

Types of keys allowed: Int, Strings, Booleans and Tuples

Note that for **Booleans**, If key of integer 1 is in the dictionary and you add the key True, it will override the value with key integer 1.

### Dictionary Functions

**Clear**

Removes everything in the dictionary, it takes **O(n) time**.  
It does not return anything and empties the dictionary.

```Python
dictionary = {"one" : 1, "two" : 2, "three" : 3}

dictionary.clear() # => {}, return: None
```

**Copy**

Returns a deep copy of the dictionary, it takes **O(n) time**.

```Python
dictionary_1 = {"one" : 1, "two" : 2, "three" : 3}

dictionary_2 = dictionary_1.copy() # => {"one" : 1, "two" : 2, "three" : 3}
```

**Get**

Returns the value of the key, it takes **O(n) time**.

```Python
dictionary = {"one" : 1, "two" : 2, "three" : 3}

print(dictionary.get("two")) # => 2
print(dictionary.get("four")) # => None
# We can also set a value if the key does not exist in the dictionary
print(dictionary.get("four", -1)) # => -1
```

**Keys**

Returns a list of the keys in the dictionary, it takes **O(n) time**.  
This returns a `dict_keys` data type.

```Python
dictionary = {"one" : 1, "two" : 2, "three" : 3}

keys = dictionary.keys()) # => ["one","two","three"]
```

**Values**

Returns a list of the values in the dictionary, it takes **O(n) time**.  
This returns a `dict_values` data type.

```Python
dictionary = {"one" : 1, "two" : 2, "three" : 3}

values = dictionary.values()) # => [1,2,3]
```

**Items**

Returns the key value pairs in the dictionary, it takes **O(n) time**.  
This returns a `dict_items` data type.

```Python
dictionary = {"one" : 1, "two" : 2, "three" : 3}

# Loop through every key value in a dictionary
for key, value in dictionary.items():
	print(key)
	print(value)
```

**Note that when iterating through a dictionary using `.keys()` or `.items()` you cannot delete the keys.**

**Update**

Updates the dictionary with a set of key value pairs  
It does not return anything but updates the dictionary

```Python
dic = {1:2, 2:3, 3:4, 4:5}

dic.update({1:1, 5:6})
print(dic) # => {1: 1, 2: 3, 3: 4, 4: 5, 5: 6}
```

**dict**

Convert a iterable with 2 items into a dictionary. The iterable must have at least 2 items.

```Python
x = ((1,2),(3,4))

y = dict(x) # {1:2, 3:4}
print(y)
```

## Sets

---

```Python
# Sets in Python
set_ = {1,1,2,3} # => {1,2,3}, all extra 1's are removed
```

Sets is a iterable that stores a single instance of a variable. They are unordered, unindexed and no duplicates are allowed.

Since a set is unindexed, the elements cannot be accessed through indexing.

### Set Functions

**Add**

Add an element into a set, it takes **O(1) time**.  
It does not return anything and updates the set.

```Python
set_ = {1,2,3}

set_.add(4) # => {1,2,3,4}, return None
set_.add(1) # => Nothing happens as 1 is already in the set
```

**Clear**

Removes everything in the set, it takes **O(n) time**.  
It does not return anything and empties the set.

```Python
set_ = {1,2,3}

set_.clear() # => {}, return: None
```

**Copy**

Returns a deep copy of the set, it takes **O(n) time**.

```Python
set_1 = {1,2,3}

set_2 = set_1.copy() # => {1,2,3}
```

**Discard**

Removes an element from the set, it will not raise an error if the item does not exist, it takes **O(n) time**.  
It does not return anything and removes the element from the set.

```Python
set_ = {1,2,3,4}

set_.discard(4) # => {1,2,3}, return None
```

**Difference**

Returns the difference between another set, it takes **O(n) time** where n is the length of the first set.

```Python
set_1 = {1,2,3}
set_2 = {3,4,5}

set_3 = set_1.difference(set_2) # => {1,2}
```

**Is-subset**

Returns a Boolean on whether all items in both sets are similar, it takes **O(n*m) time**.

```Python
set_1 = {1,2,3}
set_2 = {3,4,5}
set_3 = {1,2,3}

print(set_1.issubset(set_2)) # => False
print(set_1.issubset(set_3)) # => True
```

**Union**

Returns a set of unique elements from 2 sets, it takes **O(n*m) time**.

```Python
set_1 = {1,2,3}
set_2 = {3,4,5}

set_3 = set_1.union(set_2) # => {1,2,3,4,5}
```
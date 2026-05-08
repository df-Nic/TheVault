---
Title: Exception Handling
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - ProgrammingLanguage/Python
  - Programming/ErrorHandling
---
## Table of Contents
- [[#What is its purpose|What is its purpose]]
- [[#Type of Errors:|Type of Errors:]]
- [[#Handling Exceptions|Handling Exceptions]]
---
## What is its purpose
---
Using exception handling, we can by pass certain codes to prevent them from stopping completely when an error is raised

## Type of Errors:
---
1.  Name Error: A variable is not defined
2.  Type Error: Cannot convert int object to str implicitly
3. Zero Division Error: Cannot divide by 0
4. User made error: A class defined by the user to raise an error

## Handling Exceptions
---
One way to catch an error is the try and except block.

```Python
(x,y) = (5,0)

try: 
	z = x/y

except ZeroDivisionError:
	print("Cannot divide by zero")

except exception: # Any type of error or just use except : will do the same thing
	print("Unknown error")

else: 
	print("result is" + z)

finally:
	print("Executing Finally Clause")
```

**How does it work**
1. the `try` clause is executed
2. If can exception has occurred, skip the `try` clause and find the matching `except` clause
3. If no exception occurs, go to the `else` clause, if have
4. The `finally` clause is always executed before leaving the try statement even if the exception has occurred or not


You can also throw your own exceptions by using the `exception` keyword. `raise NameError("HiThere")`

**Making your own exceptions**

```Python
class MyError(Exception):
	def __init__(self, value):
		self.value = value
	def __str__(self):
		return repr(self.value)

try:
	raise MyError(2*2)
except MyError as e:
	print("Exception valie:", e.value) # Exception value: 4

raise MyError("oops!") # Raise an error with text oops!
```
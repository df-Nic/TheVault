---
Title: Object Oriented Programming
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1010X
  - Programming/OOP
---
## Table of Contents
- [[#Terms and Concepts|Terms and Concepts]]
- [[#Creating a Class|Creating a Class]]
	- [[#Creating a Class#Constructors|Constructors]]
	- [[#Creating a Class#Inheritance|Inheritance]]
		- [[#Inheritance#Multiple Inheritance|Multiple Inheritance]]
	- [[#Creating a Class#Polymorphism|Polymorphism]]
- [[#Other Special Methods|Other Special Methods]]
	- [[#Other Special Methods#Str|Str]]
	- [[#Other Special Methods#Add|Add]]
	- [[#Other Special Methods#Equal|Equal]]
---

## Terms and Concepts
---
1. **Classes & Instances**
Class is a blueprint that defines properties and behavior of entities, its essentially specifies the common behavior of entities.

Instances is a particular object of a given class, basically the usable object created from the blueprint (class).

2. **Methods and message passing**

3. **Inheritance**
It helps to minimize repeated code by reusing code from parent classes (Superclass)

4. **Polymorphism**

When 2 functions with similar names are in the Superclass and Subclass. The function in the subclass will be used instead. This is called overriding.
<div style="page-break-after: always;"></div>

## Creating a Class
---
To create a class in **Python**, we will use the keyword `class`. Each class will require a **constructure** which is a special function which makes an instance of the class object.

```Python
class BankAccount (object): # object referes to the class being the root class

	## Constructor ##
	def __init__ (self, initial_balance): # Self, a reference to the  object
		# State class variables here
		self.balance = initial _balance

	## Class functions ##
	def withdraw (self, amount): # All class functions must have the keyword self
		if self.balance > amount:
			self.balance -= amount
			return self.balance
		else:
			return "Money not enough"

	def deposit (self, amount):
		self.balance += amount
		return self.balance

## Creating an instance ##
account_1 = BankAccount(100)
account_1.withdraw(40) # Balance 60
account_1.deposit(100) # Balance is 160
account_1.withdraw(1000) # "Money not enough"
```

### Constructors
---
It's a special method  `__init__` , that is called when the object is first initialized. 

This allows an instance of an object to be created for any class you defined.

There are other special methods in python and they are denoted by  " __ ".
<div style="page-break-after: always;"></div>

### Inheritance
---
It is to take advantage of the similarities between different class. Thus objects with similar functionality should inherit from a base object called **superclass**.

Any class that inherits from the superclass is called a **subclass**. The subclass acts like an extension to the superclass.

```Python
## Root Class ##
class NamedObject(object): # Root classes will have the object tag
	def __init__(self, name):
		self.name = name

	def get_name(self):
		return self.name

## Subclass ##
class MobileObject(NamedObject): # Subclasses will have the roob class tag
	def __init__(self, name, location):
		super().__init__(name) # This will use the superclass init and variables
		self.location = location

	def install(self):
		self.location.add_thing(self)
```

The key word `super`, is used when we want to use something from the superclass, be it functions or variables.

If the function cannot be found in the subclass, it will check in the superclass and if it exist it will call that function. Or we can use `super().<function>`, to specifically use the super class function.

If we don't use super in some cases it will cause a recursion loop
```Python
## Function in a subclass ##
def say(self, stuff):
	say(stuff + self.phrase)

# This wont use the super class function say it will just call itself as it is the nearest function with the same name.
```
<div style="page-break-after: always;"></div>

#### Multiple Inheritance

A class can inherit from multiple classes. It will inherit every attribute from its superclass's.

```Python
class Singer(object):
	def say(self, stuff):
		print("tra-la-la --" + stuff)
	def sing(self):
		print("tra-la-la")

class Lecturer(object):
	def __init__(self , phrase):
		self.favourite_phrase = phrase

class SingingLecturer(Lecturer, Singer): # Order of the super class matters
	def __init__(self, favorite_phrase):
		super().__init__(favorite_phrase)
```

If a function is in all the superclass inherited, the subclass will search for the function in the first superclass stated, if not it will go to the next superclass.

How python determines the order to look is through Method Resolution Order. If the superclass calls super() it will search in the second superclass.

```Python
class A(Object):
	def f(self):
		Print("Im at A")
class B(A):
	def f(self):
		Print("Im at B")
		Super().f()
class C(A):
	def f(self):
		Print("Im at C")
		Super().f()
class D(B,C):

	def f(self):
		super().f()
```

If function `f`, is called, it will navigate from, D -> B -> C -> A and it will execute each `f`, in that order.

If function `f` is not in class D then it will go straight to Class B. This is because, all subclasses of that function has to be called first before the superclass function is called.
<div style="page-break-after: always;"></div>

### Polymorphism
---
It provides a convenient means for handling polymorphic functions (<span style='color:#f7b731'>Overloading</span>).

The same function can be used by different objects of different classes but handled differently to perform the proper actions based on the respective class objects (<span style='color:#f7b731'>Overriding</span>)


## Other Special Methods
---

### Str

This allows us to define the string representation of an object to python

```Python
class Duration(object):
    def __init__(self, minutes, seconds):
        
        self.minutes = minutes 
        self.seconds = seconds
    
    def __str__(self):
        
        minutes = self.get_minutes()
        
        seconds = self.get_seconds()
        if (minutes < 10):
            minutes_str = "0" + str(minutes)
        else:
            minutes_str = str(minutes)
        
        if (seconds < 10):
            seconds_str = "0" + str(seconds)
        
        else:
            seconds_str = str(seconds)
        
        return (minutes_str + ":" + seconds_str)
    
    def get_minutes(self):
        
        seconds = self.seconds
        minutes = self.minutes
        if (seconds >= 60):
            minutes += (seconds // 60)
        return (minutes)
    
    def get_seconds(self):
        
        seconds = self.seconds
        if (seconds >= 60):
            seconds -= (seconds // 60) * 60
        return (seconds)
    
    @property
    def total_seconds(self):
        minutes = self.minutes
        seconds = self.seconds
        return (seconds + (minutes * 60) )
```

### Add

The `__add__`, special function will override the + operator when used by the objects.

It is used to specify a way to add up 2 objects.

```python
# Using the same Duration class
def __add__ (self, object):
        
        d = Duration(self.minutes + object.minutes, self.seconds + object.seconds)
        
        return (d)
```

### Equal

The `__equal__`, special function will override the == operator when used by the objects.

It is used to specify a way check if 2 objects are similar.

```Python
def __eq__(self, other):
        if isinstance(other, Duration):
            if other.minutes == self.minutes and other.seconds == self.seconds:
                return True
        return False
```
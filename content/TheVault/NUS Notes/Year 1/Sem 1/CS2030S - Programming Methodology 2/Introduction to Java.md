---
title: Introduction to Java
Date Created: 2023-08-15
tags:
  - CS2023S
  - Java
---
# Table of Contents
---
- [[#Java Basics|Java Basics]]
	- [[#Java Basics#Workflow|Workflow]]
	- [[#Java Basics#Features of OO Language|Features of OO Language]]
	- [[#Java Basics#Variables|Variables]]
		- [[#Variables#Subtype|Subtype]]
			- [[#Subtype#Properties|Properties]]
			- [[#Subtype#Primitive Subtypes|Primitive Subtypes]]
		- [[#Variables#Conversions|Conversions]]
		- [[#Variables#Reference Data Types|Reference Data Types]]
			- [[#Reference Data Types#Autoboxing|Autoboxing]]
			- [[#Reference Data Types#Unboxing|Unboxing]]
	- [[#Java Basics#Conditional Statements|Conditional Statements]]
	- [[#Java Basics#Flow Control (While and For)|Flow Control (While and For)]]
	- [[#Java Basics#Array|Array]]
		- [[#Array#Creating an Array|Creating an Array]]
		- [[#Array#Looping Through an Array|Looping Through an Array]]
		- [[#Array#Array-List|Array-List]]
	- [[#Java Basics#Scanner Class|Scanner Class]]
	- [[#Java Basics#Print-f|Print-f]]
- [[#Classes|Classes]]
	- [[#Classes#Encapsulation|Encapsulation]]
	- [[#Classes#Terminologies|Terminologies]]
	- [[#Classes#Types of Methods|Types of Methods]]
	- [[#Classes#Public Classes|Public Classes]]
	- [[#Classes#Overloading & Overriding|Overloading & Overriding]]
	- [[#Classes#Accessibility|Accessibility]]
	- [[#Classes#"This"|"This"]]
	- [[#Classes#Dynamic Polymorphism|Dynamic Polymorphism]]
- [[#Abstract Data Type (ADT)|Abstract Data Type (ADT)]]
	- [[#Abstract Data Type (ADT)#Implementing an Abstract Data Type|Implementing an Abstract Data Type]]
		- [[#Implementing an Abstract Data Type#Struct|Struct]]
- [[#Stack / Heap Diagram|Stack / Heap Diagram]]
---

<div style="page-break-after: always;"></div>

# Java Basics
---
## Workflow

1) **Create / Edit**
All the coding will be done in any folder with the file type <span style='color:#8854d0'>.java</span>

2) **Compile**
To compile, execute the command in to the CMD `javac <filename>.java`.
Upon executing it will produce a <span style='color:#8854d0'>.class</span> file for all classes. This files are the <span style='color:#8854d0'>Bytecode</span> of the program.

Compiling allows Java to <mark style='background:#eb3b5a'>find errors before executing</mark> the code, saving time.

3)  **Execute**
To execute (run the program) type the command `java <classname>`.

## Features of OO Language

**Encapsulation**
-  Group data and associated functionalities into a single package
-  Hide internal details from outsider

**Inheritance**

-  A method of extending current implementation
-  Introduce logical relationship between packages
-  Functions will be searched in the subclass, followed by the superclass

**Polymorphism**

-  Behavior of the functionality changes according to the actual type of data
-  Allows the same function name to have different inputs based on the class requirements
## Variables

There are <b><span style='color:#0fb9b1'>two</span></b> types of variables:

1. **Primitive Types**
> They are your standard variable types; `int`, `double`, `float` to name a few.

2. **Reference Types**
> They are user defined classes; `Integer`, `String`, `Array` to name a few.


<b><span style='color:#8854d0'>Final</span></b>:  It is a keyword used for variables where after declaring, the value <mark style='background:#f7b731'>cannot be changed</mark>. `Final int VAL = 1000;`

<div style="page-break-after: always;"></div>

<b><font size=4>Liskov Substitution Principle</font></b>
> Objects of a superclass should be replaceable with objects of its subclasses without breaking the application
### Subtype

If a type **T** is a <span style='color:#0fb9b1'>subtype</span> of **S**, it is denoted as <b><mark class="hltr-cyan">T &lt;: S </mark></b>, this means that **S** is a <span style='color:#0fb9b1'>supertype</span> of **T**.

This is mainly important when <mark style='background:#f7b731'>implementing classes</mark> making a subtype means that code used for type **S** can also be used on variables with type **T**.
#### Properties

**Reflexive**
> T <: T

**Transitive**
> If T <: S and S <: U, then T <: U

**Anti-Symmetric**
> If T <: S and S <: T, then T = S, this cycling however is prevented by Java

#### Primitive Subtypes

In Java each primitive type is a subtype of another primitive type.

Byte <: Short <: Integer <: Long <: Float <: Double
Char <:  Integer 

![[Java Primitive Subtype Flow Diagram.png|center]]
### Conversions

**Upcasting**
>When doing arithmetic operations with different integer types, Java will convert <mark style='background:#f7b731'>lower ranged</mark> integers to higher range integers. This is also known as **widening** or **promotion**.

**Downcasting**
>Java will not however, convert higher range integers to lower ranges as it will lose precision. Thus an <mark style='background:#f7b731'>explicit type conversion is required</mark>. This is also known as **narrowing** or **demotion**. 

<div style="page-break-after: always;"></div>

### Reference Data Types

Also known as a <span style='color:#eb3b5a'>wrapper class</span>, they are donated with capital letters; `Integer`, `Double`.

Similar to classes they can be initialized through `Integer num = new Integer(10);`. 

**Automatic Garbage Collection** 
>If there is no variables pointing to the object, Java will **reclaim** the memory used by the object.

**String Interning** 
> Initializing a string using a string value directly, it will only create a <mark style='background:#f7b731'>unique instance</mark> of the object. Other objects with the same value will have the same reference to the object.

If `String s1 = new String("Hello")` and `String s2 = "Hello"` then `s1 = s2` in terms of memory address
#### Autoboxing

When assigning a <mark style='background:#f7b731'>primitive data type to a reference data type variable</mark>. Java will automatically create an object with the value and assign the reference of the object.

```Java
import java.util.*;
public class Basics {
	public static void main(String[] args){
		int x1, x2;
		Integer y;
		x1 = 10;
		x2 = 20;
		
		y = 10; // Autoboxing
		y = x1 + x2 // Autoboxing
	}
}
```

#### Unboxing

When assigning a reference data type to a primitive data type variable. Java will automatically take the value in the object and assign it to the variable.

```Java
import java.util.*;
public class Basics {
	public static void main(String[] args){
		int x;
		Integer y1, y2;
		
		y1 = 10;
		y2 = 20;
		
		x = y1 + y2; // Unboxing
	}
}
```

Autoboxing and Unboxing can be used <span style='color:#f7b731'>interchangeably</span>. 

<div style="page-break-after: always;"></div>

## Conditional Statements
---
**If & Else**
```Java
int time = 22;

if (time < 10){
	System.out.println("Good morning");
}
else if (time < 20){
	System.out.println("Good day.");
}
else{
	System.out.println("Good evening");
}

// OR

int time = 20;

String result = (time < 18) ? "Good day" : "Good evening"; // ? is like if : is like else
System.out.println(result);
```

**Switches**

Is another way to write if else statements based on a variable's value.
```Java
public static void main(string[], args){
	char Grade = "B";
	switch (Grade){
		case "A": // If Grade == A
			System.out.printLn("You are Grade A Employee: Bonus = " + 2000)
			break; # Have to use break to get out of the switch
		case "B":
			System.out.println("You are Grade A Employee: Bonus = " + 1000)
			break;
		case "C":
			System.out.println("You are Grade A Employee: Bonus = " + 500)
			break;
		case "D":
			System.out.println("You are Grade A Employee: Bonus = " + 100)
			break;
	}
}
```
<div style="page-break-after: always;"></div>

## Flow Control (While and For)
---
**While**

```Java
while (a > b) {
	// Body
}
// OR
do {
	//body
} while (a > b)

/*
Both are acceptable, however the latter will execute the code once before doing the conditional check, the former will check before executing the code
*/
```

**For**

```java
for (int i = 0; i < 10; i++){ 
// Declare loop controle variable, checking condition and incrementing loop control variable
	// Body
}
for (int i = 0; i < 10; i--){
	// Body
}
```

**Increments**

`++i`, is a pre-increment operator where it increments the value of `i` by 1 and returns the incremented value.

`i++`, is a post-increment operator which also does increment `i` by 1 but returns the original value (Pre-Incremented).

```Java
class Increment{
	public static void main(String[] args) { 
		int i = 1;
		System.out.println(i++); // 1
		System.out.println(++i); // 3
	}
}
```
<div style="page-break-after: always;"></div>

## Array
---

An array is like a list however it has a fixed length.
To change the length of the length, a new array needs to be created.

### Creating an Array

```java
// 1D Array
int [] intarray = new int[] {10,20,30,40}

// Multidiemtional array
int [][] multiintarray = new int[][] {{1,2,3,4},{5,6,7,8}}

// Creating a empty array
int [] new_array = new int[5]; // It makes a empty array of size 5
```

### Looping Through an Array

```Java
int [] intarray = new int[] {10,20,30,40}

int length = intarray.length; // Get the length of an array

// Using indexes
for (int i = 0; i < length. i++){
	System.out.println(intarray[i])
}

// Using values
for (int i : intarray){
	System.out.println(i)
}
```
<div style="page-break-after: always;"></div>

### Array-List

An array list acts like a python list where the length is not fixed.

For an array list if you don't specify the variable type stored, java will not know what inside the array list and will return a object type.

We can add an element into a undefined variable type array list, by putting it straight into the ()

```Java
import java.util.ArrayList;

public class Main {
  public static void main(String[] args) {
    ArrayList<String> cars = new ArrayList<String>();
    cars.add("Volvo");
    cars.add("BMW");
    cars.add("Ford");
    cars.add("Mazda");
    cars.set(0, "Opel"); // Set the index of the arraylist to another value
    cars.remove(0); // Remove an item based on index
    cars.size(); // Get the length of the array list
    cars.clear(); // Empty the array list
    
    System.out.println(cars.get(0)); // Get an item based on index
```
## Scanner Class
---
The scanner class is used to get inputs from users and use it in the program.

```Java
import java.util.Scanner;

class Temperature {
	public static void main(String[], args){
		double fahrenheit, celcius;
		Scanner = myScanner = new Scanner(System.in);

		// Requests an input from the user
		System.out.printLn("Enter temperature in Fahrenheit: ");
		// Sets the input into a variable
		fahrenheit = myScanner.nextDouble();

		celcius = (5.0/9) * (fahrenheit - 32)
		System.out.println("Celcius: " + celcius);
	}
}
```
<div style="page-break-after: always;"></div>

## Print-f
---
Its a method to format string outputs in Java.

```Java
public static void main(String[], args){
	System.out.printf("PI = %.6f\n", PI) // For 6 decimal points
}
```

**Different types of formatting with print-f**

| Symbol |   Type    |
|:------:|:---------:|
|   %c   | Character |
|   %d   |  Decimal  |
|   %f   |   Float   |
|   %i   |  Integer  |
|   %s   |  String   |
# Classes
---
## Encapsulation

It is the <span style='color:#f7b731'>bundling of related variables and function</span> into a <span style='color:#0fb9b1'>class</span>. Therefore, unlike <span style='color:#0fb9b1'>structs</span>, it can contains functions.

Note that all classes are a subclass to the class <span style='color:#f7b731'>Object</span>.
## Terminologies

**Methods**
> Functions inside a class

**Fields**
> Attributes inside the class

**Instances**
> Actual objects of the class

<div style="page-break-after: always;"></div>

## Types of Methods

There are <b><span style='color:#f7b731'>two</span></b> types of methods:

1. Instance Methods
> Denoted with the `static` keyword and can only be accessed by object instances.

2. Class Methods
> Does not have the `static` keyword. Accessed using the class name and cannot access class attributes

## Public Classes

They are known as the <span style='color:#2d98da'>driver class</span>. This is where the `main`, function will reside in.

This `main` class is where Java will execute your program, and the name of the class <mark style='background:#f7b731'>must be the same as the file</mark>.

```Java
import java.util.*;

class numbers {

}

public class Basics { // Java will find this class and the main method to start
	public static void main(String[] args){
		int x;
		Integer y1, y2;
		
		y1 = 10;
		y2 = 20;
		
		x = y1 + y2; // Unboxing
	}
}
```
## Overloading & Overriding

**Overloading** 
> Functions with <span style='color:#eb3b5a'>identical names</span> but they <span style='color:#eb3b5a'>differ by their inputs</span>.

**Overriding**
> Functions with the <span style='color:#eb3b5a'>same name and inputs</span>, inside classes. Used in inheritance

## Accessibility

**<span style='color:#8854d0'>Public</span>**
- Anyone can access the variable or function
- Intended for functions only
<div style="page-break-after: always;"></div>

**<span style='color:#8854d0'>Private</span>**
- Only can be access within the class or functions in the class
- This is recommended for attributes
- Static methods cannot access private objects unless an instance of the object is passed into the function.

**<span style='color:#8854d0'>Protected</span>**

- Is a more relaxed version of the private accessibility level
- Can be access by the same class, its children classes and classes in the same java package
- Recommended for things that are common in the "Family"

**<span style='color:#8854d0'>None</span>**
-  Only accessible to classes in the same Java package
-  Known as the package private visibility
## "This"

The keyword `this`, is used as a reference to call the object.

```Java
// Without using the keyword this
public void deposit (double amount) {
	
		if (amount <= 0)
			return;
			
		_balance += amount;
}

// Using the keyword this
public void deposit (double amount) {
	
		if (amount <= 0)
			return;
			
		this._balance += amount;

/*
Using the key word this is a good practice as if there are 2 objects with the same class, we will need to indicate which object attribute to access.
*/
}
```
<div style="page-break-after: always;"></div>

## Dynamic Polymorphism

A superclass reference can refer to an object of a subclass

```Java
public static void main (String[] args) {
		SavingAcct bal1 = new SavingAcct(2, 1000.0, 0.03); 
		BankAcct bal2;
		
		bal2 = bal1
		bal2.print() // Will also print out the interest rate. It will use the SavingAccct print() function.

		bal2.payInterest(); // Will raise a compilation error as BankAcct does not have a function called payInterest. This is because it does not check the variable type of the actual object.
}
```

This works because `bal2`, is a reference to an object `bal1`. When a method is called, it will find the function that is <mark style='background:#fa8231'>associated to the referenced object</mark>, `bal1`. If its not found it will search in the Superclass of `bal1`.
# Abstract Data Type (ADT)
---

It represents a collection of data together with a specification of a set of operations (<span style='color:#0fb9b1'>Functional abstraction</span>)
> Functional abstraction indicates what ADT operations do and not how to implement them
> It also does not specify how Data is to be stored

## Implementing an Abstract Data Type
---

Using <mark style='background:#f7b731'>interfaces</mark>, a class can be identified as a abstract data type.

Like an ADT Interfaces only provides the necessary method signature with <mark style='background:#f7b731'>no body</mark> and not how the data is stored.

You <mark style='background:#f7b731'>have</mark> to implement the body of every method inside the interface.

With interfaces we can use 2 different classes interchangeably. By using the <mark style='background:#f7b731'>interface</mark> reference data type.

```Java
public interface FracADT{
	public int getNum();
	public int getDenom();
	public void setNum(int num);
	public void setDenom(int denom);
	
	public FracADT add(FracADT f);
	public FracADT times(FracADT f);
	public FracADT simplify();
}
```
<div style="page-break-after: always;"></div>

**Implementing the Interface**

```Java
class Fraction impliments FracADT{
	public int num;
	public int denom;
	
	// Impliment ALL the functions in FracADT
}
```
### Struct

```Java
typedef struct{
	double x;
	double y;
	double r;
} Circle;
```

<span style='color:#0fb9b1'>Structs</span> can be used to create <span style='color:#f7b731'>user defined variables</span> into their programs
# Stack / Heap Diagram
---

![[Stack & Heap Diagram.png]]

The <span style='color:#8854d0'>stack</span> will contain all the <span style='color:#f7b731'>variables initialized</span> inside the program and the data that it is pointing towards.

The <span style='color:#8854d0'>heap</span> will contain the <span style='color:#f7b731'>object data stored</span> inside memory.
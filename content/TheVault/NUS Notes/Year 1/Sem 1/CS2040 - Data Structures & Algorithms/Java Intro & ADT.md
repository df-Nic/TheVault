---
title: Java Intro & ADT
Date Created: 2023-06-18
tags:
  - CS2040
  - Java
---
# Table Of Contents
---
- [[#Java Basics|Java Basics]]
	- [[#Java Basics#Variables|Variables]]
		- [[#Variables#Types of Variables|Types of Variables]]
		- [[#Variables#Conversions|Conversions]]
		- [[#Variables#Reference Data Types|Reference Data Types]]
			- [[#Reference Data Types#Autoboxing|Autoboxing]]
			- [[#Reference Data Types#Unboxing|Unboxing]]
	- [[#Java Basics#Scanner|Scanner]]
	- [[#Java Basics#Classes|Classes]]
		- [[#Classes#Types of Methods|Types of Methods]]
		- [[#Classes#Public Classes|Public Classes]]
		- [[#Classes#Overloading & Overriding|Overloading & Overriding]]
- [[#Abstract Data Type (ADT)|Abstract Data Type (ADT)]]
	- [[#Abstract Data Type (ADT)#Implementing an Abstract Data Type|Implementing an Abstract Data Type]]
---

# Java Basics
---

## Variables
---
### Types of Variables

There are <b><span style='color:#0fb9b1'>two</span></b> types of variables:

1. **Primitive Types**
> They are your standard variable types; `int`, `double`, `float` to name a few.

2. **Reference Types**
> They are user defined classes; `Integer`, `String`, `Array` to name a few.


<b><span style='color:#8854d0'>Final</span></b>:  It is a keyword used for variables where after declaring, the value <mark style='background:#f7b731'>cannot be changed</mark>.

### Conversions

**Upcasting**
>When doing arithmetic operations with different integer types, Java will convert <mark style='background:#f7b731'>lower ranged</mark> integers to higher range integers. This is also known as upcasting or promotion.

**Downcasting**
>Java will not however, convert higher range integers to lower ranges as it will lose precision. Thus an <mark style='background:#f7b731'>explicit type conversion is required</mark>. This is also known as narrowing or demotion. 

### Reference Data Types
---

Also known as a <span style='color:#eb3b5a'>wrapper class</span>, they are donated with capital letters; `Integer`, `Double`.

Similar to classes they can be initialized through `Integer num = new Integer(10);`. 

**Automatic Garbage Collection** 
>If there is no variables pointing to the object, Java will **reclaim** the memory used by the object.

**String Interning** 
> Initializing a string using a string value directly, it will only create a <mark style='background:#f7b731'>unique instance</mark> of the object. Other objects with the same value will have the same reference to the object.

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

Autoboxing and Unboxing can be used <span style='color:#0fb9b1'>interchangeably</span>. 

## Scanner
---
```Java
Scanner sc = new Scanner(System.in);

a = sc.nextInt(); // A next line is denoted by a space in the input
b = sc.nextInt(); // you can also use sc.nextLine();
```

## Classes
---

### Types of Methods

There are <b><span style='color:#0fb9b1'>two</span></b> types of methods:

1. Instance Methods
> Denoted with the `static` keyword and can only be accessed by object instances.

2. Class Methods
> Does not have the `static` keyword. Accessed using the class name and cannot access class attributes

### Public Classes

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

### Overloading & Overriding

**Overloading** 
> Functions with <span style='color:#eb3b5a'>identical names</span> but they <span style='color:#eb3b5a'>differ by their inputs</span>.

**Overriding**
> Functions with the <span style='color:#eb3b5a'>same name and inputs</span>, inside classes. Used in inheritance


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
	public FracADT minus(FracADT f);
	public FracADT times(FracADT f);
	public FracADT divide(FracADT f);
	public FracADT simplify();
}
```

**Implementing the Interface**

```Java
class Fraction impliments FracADT{
	public int num;
	public int denom;

	public int getNum(){
		return num;
	}
	
	public int getDenom(){
		return denom;
	}
	/*
	* Must define all functions mentioned in the interface
	*/
}
```
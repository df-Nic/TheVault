---
title: Object Oriented Programming
Date Created: 2023-08-20
tags:
  - CS2023S
  - OOP
  - Java
---
# Table of Contents
---
- [[#Information Hiding|Information Hiding]]
- [[#Constructors|Constructors]]
	- [[#Constructors#`this` Keyword|`this` Keyword]]
	- [[#Constructors#Fully Qualified Name|Fully Qualified Name]]
- [[#Accessors and Mutators|Accessors and Mutators]]
- [[#Class Fields & Methods|Class Fields & Methods]]
	- [[#Class Fields & Methods#Class Fields|Class Fields]]
		- [[#Class Fields#Static|Static]]
		- [[#Class Fields#Final|Final]]
	- [[#Class Fields & Methods#Class Methods|Class Methods]]
- [[#Composition|Composition]]
	- [[#Composition#Aliasing / Sharing References|Aliasing / Sharing References]]
- [[#Inheritance|Inheritance]]
	- [[#Inheritance#Super|Super]]
	- [[#Inheritance#Type Checking|Type Checking]]
		- [[#Type Checking#Compile-Time Type|Compile-Time Type]]
		- [[#Type Checking#Run-Time Type|Run-Time Type]]
- [[#Overriding|Overriding]]
	- [[#Overriding#Method Signature|Method Signature]]
	- [[#Overriding#Method Description|Method Description]]
	- [[#Overriding#Method Overriding|Method Overriding]]
---
<div style="page-break-after: always;"></div>

# Information Hiding
---

The main reason to restrict access is to <span style='color:#f7b731'>refrain</span> the users/clients to <span style='color:#f7b731'>modify the class fields</span>.

```Java
// Circle class version 1.0
Class Circle{
	public double x;
	public double y;
	public double r;
	
	public Circle(double x, double y, double r){
		this.x = x;
		this.y = y;
		this.r = r;
	}
}

// Circle class version 2.0 (Prefered)
Class Circle{
	private double x;
	private double y;
	private double r;
	
	public Circle(double x, double y, double r){
		this.x = x;
		this.y = y;
		this.r = r;
	}
}
```

Consider the 2 versions of class <span style='color:#2d98da'>Circle</span>. If the user wants to calculate the area, they will use the following, `area = 3.14 * this.r * this.r`, this will only work if the <span style='color:#f7b731'>fields are of public access</span>.

If the `r` field is changed to `radius`, then the users code will not work. Thus it is good to make <span style='color:#f7b731'>all class fields to be private</span>, such that it <span style='color:#f7b731'>can only be accessed within the same class</span>.

# Constructors
---

<span style='color:#2d98da'>Constructors</span> is special a function which allows users to <span style='color:#f7b731'>create objects</span> of a class, it is called when the <span style='color:#8854d0'>new</span> keyword is used.

If a <span style='color:#2d98da'>constructor</span> is not defined then a <mark class="hltr-blue">default contractor</mark> will be added by the compiler.
```Java
// Default Constructor
public <class_name>(){
}
```
<div style="page-break-after: always;"></div>

Characteristics of a <span style='color:#2d98da'>constructor</span>:
1)  <span style='color:#f7b731'>Same name</span> as the class.
2)  Can be either <span style='color:#8854d0'>public</span> or <span style='color:#8854d0'>private</span>.
3)  Can have multiple constructors with different input types (Java will use the correct one).

**When a constructor is called**
-  The memory will be allocated to store all the fields and the <span style='color:#f7b731'>location will be assigned to the keyword </span>`this`.
-  It will invoke the constructor and pass the keyword `this` implicitly, basically `this.x = x`.
-  Return the reference pointed by `this` back.
-  The <span style='color:#8854d0'>new</span> <span style='color:#f7b731'>keyword returns the reference</span> to the newly created object to the variable, therefore no need for a <span style='color:#8854d0'>return</span> statement.

## `this` Keyword

`this` is a special reference variable which <span style='color:#f7b731'>points back to itself</span>.

`Circle a1.getArea()`, `this` will be referencing to the object `a1` is pointing to.

```Java
// Circle Constructor
public Circle(double x, double y, double r) { 
	x = x; 
	y = y; 
	r = r;
}
```

The issue with the above code is that Java uses a <span style='color:#fa8231'>lexical scoping</span>. Thus x will refer to the input parameter x. Thus the code will do nothing.

However, `this` can be added ambiguity, if there is no parameter `x, y, r` then it will refer them from the <span style='color:#fa8231'>outer scope</span> which is the class fields. Therefore, the following will work.

```Java
// Circle Constructor
public Circle(double x, double y, double r) { 
	this.x = x; 
	this.y = y; 
	this.r = r;
}
```

It is always good to put the `this` reference before a instance field as it makes it easier to understand.

## Fully Qualified Name

`this.<instance_field>` might still be ambiguous and thus a <span style='color:#0fb9b1'>fully qualified name</span> (FQN) can always be used unambiguously.

- FQN starts with the class name
- Followed by the name, `this` is used if the name refers to a field else there is no need for this step.
- Followed by the actual name used.

Example: `Circle this.r`
# Accessors and Mutators
---

**Accessors / Getters**
> A function to retrieve the properties of an object, <span style='color:#f7b731'>retrieve the value of a field</span>

```Java
class Circle{
	// Variables
	
	// Constructors
	
	// Accessor
	public double get_radius(){
		return this.r;
	}
}
```

**Mutators / Setters**
> A function to modify the properties of an object, <span style='color:#f7b731'>update the value of a field</span>

```Java
class Circle{
	// Variables
	
	// Constructors
	
	// Mutatos
	public void update_radius(double r){
		this.r = r;
	}
}
```

**Tell, Don't Ask Principle**
> Instead of asking for the values for the field, ask the class to do the computation

# Class Fields & Methods
---

**Magic Numbers**
> They are constants which can vary.

<span style='color:#0fb9b1'>Magic numbers</span> should be <span style='color:#f7b731'>avoided</span> as a change in a magic number will require a change in multiple places. Therefore, one way to solve this is to assign these numbers to a variable.

These values should also be:
-  Constant for all variables
-  Cannot be reassigned

## Class Fields

An instance field is a variable who's <span style='color:#f7b731'>value is pre-defined</span> upon a creation of a object.

```Java
class Circle{
	private double x;
	private double y;
	private double r;
	private double PI = 3.14159; // Object Instance Field
}
```

However, the above is not constant for all variables as <span style='color:#f7b731'>each object will have their own instance</span> of `PI`.
### Static

<span style='color:#8854d0'>Static</span> means that there will <span style='color:#f7b731'>only be one instance</span> of a particular thing.

A <span style='color:#8854d0'>static</span> instance field, is <span style='color:#f7b731'>linked to the class</span> itself and not the object. This means that the variable is a <span style='color:#0fb9b1'>class variable / field</span>.

It helps to <span style='color:#f7b731'>save memory</span> as well by making it a class field instead of a instance field.

```Java
class Circle{
	private double x;
	private double y;
	private double r;
	private static double PI = 3.14159; // Class instance Field
}
```

However, the variable `PI` <span style='color:#f7b731'>can still be changed</span>.

### Final

<span style='color:#8854d0'>Final</span>, makes a variable / field <span style='color:#f7b731'>strictly prevents reassignments</span> to it (1st Assignment is alright). 

```Java
class Circle{
	private double x;
	private double y;
	private double r;
	private static double PI = 3.14159; // Static instance Field
	private final int id; // This Id cannot be changed once assigned
	private static int lastId = 0; // Class Instance field
	
	public Circle(double x, double y, double r){
		this.x = x;
		this.y = y;
		this.r = r;
		this.id = Circle.lastId;
		Circle.lastId++;
	}
}
```

The keyword <span style='color:#f7b731'>can also be used on classes and functions</span> as well.

If a <span style='color:#f7b731'>class</span> is <span style='color:#8854d0'>final</span>, then it <span style='color:#f7b731'>cannot be inherited</span>, while <span style='color:#f7b731'>functions cannot be overridden</span>.
## Class Methods

Same as a class field, a <span style='color:#f7b731'>class method will use the keyword</span> <span style='color:#8854d0'>static</span>. In a <span style='color:#0fb9b1'>class method</span>, the keyword `this` cannot be used, if not an error will occur because a <span style='color:#f7b731'>static method cannot access a not static field</span>.

The reason why `this` cannot be used is because in a class method, which instance is it referring to or if there is no objects created then what instance is there to refer to.

```Java
class Circle{	
	// Variables
	
	public Circle(double x, double y, double r){ // Non static
		this.x = x;
		this.y = y;
		this.r = r;
		this.id = Circle.lastId;
		Circle.lastId++;
	}
	
	public static int getNumCircle(){
		return Circle.lastId
	}
}
```

A <span style='color:#2d98da'>constructor</span> is a non static function as it can use the keyword `this`.

# Composition
---

<span style='color:#0fb9b1'>Composition</span>, captures a <span style='color:#f7b731'>"has-a" relationship</span> which helps to build complex data types. This idea is to <span style='color:#f7b731'>separate the responsibility</span> into different classes.

In theory, it is to create small subclasses to make one bigger class.

```Java
class Point{
	private double x;
	private double y;
}

class Circle{
	private Point c; // Here instead of x and y, it used the point class.
	private double r;
}
```

## Aliasing / Sharing References

This is a common issue in composition, since the class is using <span style='color:#f7b731'>reference type variable</span> (class). If multiple instance of a object uses object b when created, then <span style='color:#f7b731'>any changes</span> in b <span style='color:#f7b731'>will change every instance that was created</span> using object b.

To solve this, when creating a object, always <span style='color:#f7b731'>create a new object</span> of class b to prevent this from happening.

```Java
// Using the point and circle class above
public static void main(String args[]){
	// Aliasing will occure, if P is changed c1 and c2 will change
	Point p = new Point(1.0,1.0);
	Circle c1 = new Circle(p,5.0);
	Circle c2 = new Circle(p,4.0);

	// Alisasing will not occure, if p1 is change only c1 will be affeced
	Point p1 = new Point(1.0,1.0);
	Point p2 = new Point(1.0,1.0);
	Circle c1 = new Circle(p1,5.0);
	Circle c2 = new Circle(p2,4.0);
}
```

With the above solution the trade off will be the memory usage is not optimized.

# Inheritance
---

<span style='color:#0fb9b1'>Composition</span>, captures a <span style='color:#f7b731'>"is-a" relationship</span> which helps to build complex data types. This idea is to <span style='color:#f7b731'>extend the capability</span> of another data type.

Therefore is a class A extend class B, then A :< B.

```Java
class ColouredCircle extend Circle{
	private String colour;
	// In addition, all the fields of circle will be inherited also

	public ColouredCircle(Point p, double r, String colour){
		super(p,r); // This will call the circle constructor
		this.colour = colour;
	}
}
```

## Super

The keyword <span style='color:#8854d0'>super</span>, will call the method in the superclass / parent class.

This <span style='color:#f7b731'>removes the need to add redundant code</span>. If the code in the parent class does the same thing then just reuse it. This is to
-  Minimize errors
-  Reduce repeated code
-  Minimize the need to change code in multiple places
<div style="page-break-after: always;"></div>

Super <mark class="hltr-red">has to be used first</mark>.

```Java
class ColouredCircle extends Circle{
	// Variables Constructor
	public String to_string(){
		// Reuses the superclass function with the added feature to print the color
		System.out.println (super.to_string() + this.colour);
	}
}
```

## Type Checking

```Java
Point p = new Point(5.0,5.0);
Circle c = new ColouredCircle(p, 5.0, "Blue");
```
### Compile-Time Type

The <span style='color:#0fb9b1'>compile-time type</span> is the <span style='color:#f7b731'>type of the variable during the compiling phase</span>, for instance, the above `c` is a Circle.

The reason to use this more is because, Java will not know what the actual type of the variable will be until the code is run. Thus Java assumes that it may assume a error.
### Run-Time Type

The <span style='color:#0fb9b1'>runtime-time type</span> is the <span style='color:#f7b731'>type of the variable after the code is executed</span>, for instance, the above `c` is a Coloured Circle.

# Overriding
---
## Method Signature

Includes:
1)  Method Name
2)  Type of Arguments
3)  Order of Arguments
4)  Number of Arguments

Sometimes the class name can be added also.

Example :  `contains(int, int)` or `Circle::contains(int,int)`
## Method Description

A <span style='color:#0fb9b1'>method description</span>, is just the <span style='color:#0fb9b1'>method signature</span> + the <span style='color:#f7b731'>return type</span>

Example :  `boolean contains(int, int)`
<div style="page-break-after: always;"></div>

## Method Overriding

<span style='color:#0fb9b1'>Method overriding</span> happens when a <span style='color:#f7b731'>subclass defines an instance method with the same method descriptor</span> (as an exception, the overriding method can return the subclass) as an instance method in the superclass.

As a good practice, when overriding an instance method in superclass, annotate the method in the subclass with `@Override` annotation.

```Java
class Circle {
	private Point c;
	private double r;
	
	@Override
	public String toString() {
		return "Circle(" + this.c + ", " + this.r + ")";
		// Note that the to_string function is automatically called when printing or contaternating 
		// with Strings, thus there is no need to put this.r.toString()
	}
}
```

The return type <span style='color:#f7b731'>does not need to be the same</span> as long as Return Subclass <: Return Parent
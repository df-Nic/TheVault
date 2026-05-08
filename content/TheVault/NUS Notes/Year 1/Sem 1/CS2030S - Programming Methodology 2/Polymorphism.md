---
title: Polymorphism
Date Created: 2023-08-28
tags:
  - CS2023S
  - OOP
---
# Overloading
---

Unlike <span style='color:#0fb9b1'>overriding</span> which occurs when the same method descriptor is defined in both the super and sub class. <span style='color:#0fb9b1'>Overloading</span>, on the other hand occurs when there are <span style='color:#f7b731'>methods in the same class shares the same name</span> but with <span style='color:#f7b731'>different types, order and number of parameters</span>.

```Java
class SampleClass{
	// Variables and Constructor Omitted
	
	public int add(int x, int y) {
	  return x + y;
	}
	
	// This method is overloaded
	public int add(int x, int y, int z) {
	  return x + y + z;
	}
}
```

However, <span style='color:#f7b731'>changing the names</span> of the parameters does <span style='color:#f7b731'>not constitute overloading </span>but instead it will raise an error. Same goes for the return type.

All this also applies to <span style='color:#0fb9b1'>constructors</span>.
## Constructor Chaining

Since the <span style='color:#0fb9b1'>constructor</span> can be overloaded, it is possible to chain the calls of the constructor.

One reason why chaining the constructor is used, is because of the need to invoke another constructor.

```Java
class Circle {
  private Point c;
  private double r;

  public Circle(Point c, double r) {
    this.c = c;
    this.r = r;
  }

  // Overloaded constructor with a call to this(..)
  public Circle() {
    this(new Point(0, 0), 1);
  }
}
```

The usage of `this(..)` is the same as calling `super(..)`. Therefore it <span style='color:#f7b731'>must be used in the first line</span>. Which also results in `this` and `super`  <span style='color:#f7b731'>not being able to be used at the same time</span>.

# Equals
---

Similar to using `==`, the function <span style='color:#2d98da'>equals</span>, is used to determine if 2 reference objects are <span style='color:#f7b731'>semantically the same</span>.

```Java
public boolean equals(Object obj) { 
	if (obj instanceof Circle) { 
		Circle circle = (Circle) obj; 
		return (circle.c.equals(this.c) && circle.r == this.r); 
	} 
	return false; 
}
```

**Note :** That typecasting from a superclass to a subclass is called <span style='color:#f7b731'>narrowing</span>.

The parameter type is <span style='color:#8854d0'>object</span> instead of the class type. The reason for this is, it <span style='color:#8854d0'>object</span> wasn't used, the function will not be <span style='color:#0fb9b1'>overridden</span>. 

```Java
// Array of Object is used is because the array can store multiple different class objects
boolean contains(Object[] array, Object obj) {
  for (Object curr : array) {
    if (curr.equals(obj)) {
      return true;
    }
  }
  return false;
}
```
# Dynamic Binding
---

With the example above how does Java find the right function to use. It is through <span style='color:#0fb9b1'>dynamic binding</span>. Which can <span style='color:#f7b731'>only be used on instance methods only</span>.

The <span style='color:#0fb9b1'>dynamic binding</span> mechanism is a mechanism to <span style='color:#f7b731'>determine which instance method to be invoked according to the run-time type</span> of the target of invocation. This is a two-part process.
## Compile-Time Part

Determine the method descriptor to be invoked.

**Steps**
1) Determine the <mark class="hltr-orange">compile-time type</mark> of `obj` in `obj.method_name(arg)`. `obj` is also called the target of invocation.
2) Based on the class of `obj`, find <span style='color:#f7b731'>all methods with the same method name</span> including the superclass.
3)  Keep methods that can accept the <mark class="hltr-orange">compile-time type</mark> of `arg`
4) Find the most specific method descriptor. If there is more than 1 then there is an error.

**Most Specific** method, is where the arguments of a method M can be used in method N <span style='color:#f7b731'>but not the other way round</span>. 

Type casting only affects the type <span style='color:#f7b731'>during complication and not run time</span>.
## **Run-Time Part**	

Determine the method implementation based on the retrieved method descriptor in part 1.

**Steps**
1) Retrieve the <span style='color:#0fb9b1'>method descriptor</span> found in compile-time part
2) Determine the <mark class="hltr-orange">run-time type</mark> of `obj`
3) Start from the run-time type and select the <span style='color:#f7b731'>nearest method matching the method descriptor</span>
	1) If found execute the method
	2) If not continue the search from the superclass.

**Example**

`obj.equals(arg)` where `obj` and `arg` is a <span style='color:#f7b731'>compile-time type</span> <span style='color:#8854d0'>object</span> .

Firstly, Java will <span style='color:#f7b731'>look into the object class plus its superclass</span> (For this case there is none), and find all functions with the name `equals` and get their method descriptors. in this case is just  equals(object) -> In the object class.

Secondly, based on the <span style='color:#f7b731'>compile-time type</span> of `arg` it will filter out unusable methods based on their descriptors.

After which it will chose the most <span style='color:#0fb9b1'>specific method</span>. Based on the run-time type of `obj` lets say <span style='color:#8854d0'>circle</span>. It will look in the <span style='color:#8854d0'>circle</span> class and find the method descriptor as mentioned above. If it cannot be found go to the superclass.

Therefore the main reason why `boolean equals(Circle c)` will not work is because in the second step, Java will remove this function as the `obj` on <span style='color:#f7b731'>compile-time type</span> is of type <span style='color:#8854d0'>object</span> not type <span style='color:#8854d0'>circle</span>.

# Liskov Substitution Principle
---

It states that a property of objects of type T, should be held true for type S where S <: T

For all subclasses of a particular parent class, an <span style='color:#f7b731'>object of type parent class can be replaced by its subclasses without change the desirable property of the program</span>.

**Desirable Property**
	It is the specific specifications or test cases of the parent class.

```Java
void displayGrade(Module m, double marks) {
  char grade = m.marksToGrade(marks);
  if (grade == 'A') {
    System.out.println("well done!");
  } else if (grade == 'B') {
    System.out.println("good");
  } else if (grade == 'C') {
    System.out.println("okay");
  } else {
    System.out.println("please try again");
  }
}

class CSCUMod extends Module {
  public char marksToGrade(double mark) {
    if (mark > 50) {
      return 'S';
    } else {
      return 'U';
    }
  }
}

```

The above example breaks LSP, as the subclass function only displays S and U where the parent class is supposed to display A, B, C or F.

# Abstract Class
---

In terms on <span style='color:#0fb9b1'>dynamic binding</span>, if some other function except for `toString` and `equals` wants to be generalized, it will not work as the generic class <span style='color:#8854d0'>object</span> or its subclasses might not support these functions.

One way is to make a <span style='color:#0fb9b1'>abstract class</span> which will <span style='color:#f7b731'>contain the skeleton framework of the functions needed</span>. It is so general that it cannot and should not be instantiated.

If the class has <span style='color:#f7b731'>at least one abstract method it is declared abstract</span>. But an <span style='color:#f7b731'>abstract class may have no abstract method</span>.

```Java
abstract class Shape {
  public abstract double getArea();
  // abstract class has no method body (i.e., { .. })
  // instead, it ends with a semi-colon (i.e., ;)
}

// Calling this will raise an error
Shape s = new Shape();

// But this is alright as a shape object is not being created
Shape[] arr = new Shape[20];

// This is how to use a abstract class and all the functions must be implimented
class Circle extends Shape{
	public double getArea(){
		// Implimentation
	}
}
```
<div style="page-break-after: always;"></div>

## Properties of a Abstract Class

- Abstract class can be subclasses.
- Abstract class may have fields.
- Abstract class may have abstract methods (i.e., method without implementation).
- Abstract class may have non-abstract methods (i.e., concrete methods).
- Abstract class is not required to have abstract methods.
- If a class has an abstract method, it must be declared abstract.

Concrete methods must be <span style='color:#f7b731'>overridden</span> in any subclass.

Abstract methods <span style='color:#f7b731'>must be defined and overridden</span> if not the subclass will just be another abstract class.

<span style='color:#0fb9b1'>Dynamic Binding</span> will on abstract classes as; 
1) The compile-time type of the object must be a concrete class if not it will not be able to be instantiated. 
2) The method will have to be implemented and overridden if not it will be an abstract class again and thus it will lead to the issue in point 1  
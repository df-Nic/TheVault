---
title: Immutable & Nested Class
Date Created: 2023-10-09
tags:
  - CS2023S
  - Java
---
# Immutability
---
Immutability is the concept of <span style='color:#eb3b5a'>preventing changes from happening</span> to any created instance of an abject.

**Immutable Class**
> A class where there <mark class="hltr-orange">cannot be any visible changes</mark> outside the abstraction barrier.

In other words, any combination of its <span style='color:#f7b731'>accessible methods</span>, the behavior of the methods must be the same at all times
-  Return value
-  Print
-  Exceptions
-  Etc.

Return back to <span style='color:#0fb9b1'>aliasing</span> where objects share the same usage of other reference classes.
-  One solution is to always <span style='color:#f7b731'>create a new instance of an object</span> this is to prevent other instances using the same object to be affected
-  However this can <span style='color:#eb3b5a'>consume a lot of space</span>
-  <mark class="hltr-green">Immutability allows the aliasing </mark>

**Advantages of Bring Immutable**
1)  Ease of Understanding
2)  Ensure Safe Sharing of Objects
3)  Enabling Safe Sharing Of Internals
4)  Enabling Safe Concurrent Execution
## Making a Class Immutable

Key things to <span style='color:#f7b731'>take note</span> when making a class immutable
1)  Ensuring attributes cannot be resigned
2)  If there are modifications to the attributes, the original object should not be affected

The <span style='color:#8854d0'>final</span> keyword prevents reassigning but it <mark class="hltr-red">does not prevent the field to be mutated</mark>

To make a class immutable;
1)  Add the keyword <span style='color:#8854d0'>final</span> in the class
	Prevents <span style='color:#0fb9b1'>inheritance</span> which will <span style='color:#eb3b5a'>violate LSP</span>
2)  Add the keyword <span style='color:#8854d0'>final</span> in all attributes to prevent reassignment
3)  Remove any functions which does assignment to the fields
4)  Change any mutator from void to return a new modified instance.

```Java
// Example of a Immutable Class

final class Point {
	private final double x;
	private final double y;
	private final static Point ORIGIN = new Point(0, 0);
	
	private Point(double x, double y) {
    this.x = x;
    this.y = y;
    }
	
	// Factor Method
	public static Point of(double x, double y) {
		if (x == 0 && y == 0) {
			return ORIGIN;
		}
		return new Point(x, y);
	}
    :
}

// If Point is not immutable then Cirlce will not be immutable
final class Circle {
	private final Point c;
	private final double r;
	
	public Circle (Point c, double r) {
		this.c = c;
	    this.r = r;
	}
    :
	
	public Circle moveTo(double x, double y) {
		return new Circle(c.moveTo(x, y), this.r);
	}
}
```

### Factory Method

A <span style='color:#0fb9b1'>factory method</span> is another function that is used to create an object besides calling the constructor
-  It is a <span style='color:#8854d0'>static</span> function
-  With factory methods the constructors are <span style='color:#8854d0'>private</span>

<div style="page-break-after: always;"></div>

## Immutable Arrays

``` Java
// Example of a immutable array
final class ImmutableArray<T> {
	private final T[] array;
	private final int start;
	private final int end;

	// This is a variadic method which allows any number of inputs
	@SafeVarargs
	public static <T> ImmutableArray<T> of(T... items) {
		// Copy items to T[] arr (@SuppressWarnings!)
		return new ImmutableArray<T>(arr, 0, arr.length);
	}
	
	public ImmutableArray<T> subarray(int start, int end) {
		int newStart = this.start + start;
		int newEnd = this.start + end;
		return new ImmutableArray<T>(this.array, newStart, newEnd);
	}
}
```

**Issues with this approach**
1)  `this.array = array` makes `ImmutableArray` to be mutable
2. <span style='color:#eb3b5a'>Copying is expensive</span>
3. The array is only <span style='color:#f7b731'>immutable if T is immutable</span>.

**Varargs**
> The syntax for this is `T... items`

This allows <mark class="hltr-orange">multiple number of inputs with the same type</mark> to be passed into the function as an array.

`@SafeVarargs`
> Varargs is just an array, and array and generics do not mix well thus this is to suppress the warning that Java will display

<div style="page-break-after: always;"></div>

# Nested Class
---
The purpose of a nested class is to <span style='color:#f7b731'>group logically relevant classes together</span> which will have no use outside of the <span style='color:#0fb9b1'>container class</span> (Outer most class).

**Overall classification of nested classes**
1) Inner Class
	-  Inside another class
	-  Not inside a method
	-  Non-static context

2) Static Nested Class
	-  Inside another class
	-  Not inside a method
	-  Static context

3) Local Class
	-  Inside another class
	-  Inside a function

4) Anonymous Class
	- Has no name


A nested class can access attributes or functions of the container class even when declared as <span style='color:#8854d0'>private</span>. And similarly, it can be static or non static. Static classes is associated with the <mark class="hltr-orange">containing class not an instance</mark>.

Java will find the variable based on its<span style='color:#f7b731'> closest scope</span>.

```Java
//Nested class example
class A {
	private int x = 0;
	static int y = 1;
	
	class B {
		void foo() {
			x = 1; // accessing x in A is OK (equivalent to A.this.x)
			y = 1; // accessing y in A is OK (equivalent to A.y)
		}
	}
	
	static class C {
		void bar() {
			// x = 1; // removed because we cannot access this
			A.this.x = 1; // Can access using the fully qualified name
			y = 1; // accessing y is OK (equivalent to A.y)
		}
	}
	
	void baz() {
		B b = new B();
	    C c = new C();
	    // Line A
	}

// In the main method
	//A a = new A();
	//a.baz();
}
```

<div style="page-break-after: always;"></div>
To draw the <span style='color:#0fb9b1'>stack and heap diagram</span> for the above code;

![[Stack & Heap for Static Nested Class.png|center]]
## Local Class

Similar to a nested class, but it will be <span style='color:#f7b731'>inside a function</span>

```Java
interface C {
	void g();
}

// Example of a local class
class A {
	int x = 1;
	
	C f() {
		int y = 1; // Captured
		int z = 2; // Not Captured as it was not used in the local class B
		
		class B implements C {
			void g() {
				x = y; // accessing x and y is OK.
			}
		}
		
		B b = new B();
		return b;
	}
}
```
<div style="page-break-after: always;"></div>
## Variable Capture

After `f()` has been executed <mark class="hltr-orange">all the local variables and methods from the stack is removed</mark>. So how does it still work when `B.g()` is called.

Java will <span style='color:#f7b731'>remember the variables</span> needed for future access and this is called <span style='color:#0fb9b1'>variable capture</span>. And it will only be captured if:
1)  They are local to the method
2)  Used in the local class

What happens is that the local class makes a <span style='color:#f7b731'>copy</span> of the local variables. These are <mark class="hltr-red">not part of the fields of the class</mark> and cannot be accessed the conventional way, it can also <mark class="hltr-red">cannot be reassigned but it can be mutated</mark>.

Java only allows a local class to access variables that are<span style='color:#f7b731'> explicitly declared</span> `final` or implicitly final (_a.k.a. effectively final_, this is usualy for primitive types) 

**Example of a stack and Heap Diagram storing a local variable**

![[Stack & Heap with Local Variable 1.png|center]]

**Example of a Stack and Heap diagram when a local variable is used**

![[Stack & Heap with Local Variable 2.png|center]]

## Anonymous Class

It is a class with <span style='color:#f7b731'>no name</span>.

An anonymous class has the following format: `new X (arguments) { body }`, where:

- _X_ is a class that the <span style='color:#f7b731'>anonymous class extends or an interface that the anonymous class implements</span>. X cannot be empty. This syntax also implies an anonymous class <span style='color:#eb3b5a'>cannot extend another class and implement an interface at the same time</span>. Furthermore, an anonymous class <span style='color:#eb3b5a'>cannot implement more than one interface</span>.
    - Put it simply, you cannot have `extends` and `implements` keyword in between `X` and `(arguments)`.
- _arguments_ are the arguments that you want to pass into the constructor of the anonymous class, similar to <span style='color:#8854d0'>super</span>. If the anonymous class is extending an interface, then there is no constructor, but we still need `()`.
- _body_ is the body of the class as per normal, except that we <mark class="hltr-orange">cannot have a constructor for an anonymous class</mark>.

Just like a l<span style='color:#0fb9b1'>ocal class</span>, it captures the variables of the enclosing scope as well, the same rules to variable access as local classes applies.

```Java
// Example of a anonymous class
Comparator<String> cmp = new Comparator<String>() {
  public int compare(String s1, String s2) {
    return s1.length() - s2.length();
  }
};
names.sort(cmp);
```
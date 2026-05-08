---
title: Interface, Wrapper, and Exception
Date Created: 2025-09-27
tags:
  - CS2023S
  - OOP
  - Java
  - ErrorHandling
---

# Interfaces
---

An <span style='color:#0fb9b1'>interface</span> is an abstraction of what the type can do.

**Convention**: Java typically use the suffix "-able" to indicate that the type is an interface

It is a type of <span style='color:#0fb9b1'>abstract class</span> is a class that <span style='color:#f7b731'>cannot be instantiated</span>. It typically represents an abstract concept.

Methods declared are <span style='color:#f7b731'>abstract by default</span>. Thus an <span style='color:#0fb9b1'>interface</span> is a skeleton on what methods classes should at least have. Same as an abstract class it <span style='color:#f7b731'>cannot be in instantiated but can be casted into</span>.

```Java
interface GetAreable {
  double getArea();
}

// Since it does not have the getArea function, this class will have a public abstract double getArea()
abstract class Shape implements GetAreable {
  private int numOfAxesOfSymmetry;

  public boolean isSymmetric() {
    return numOfAxesOfSymmetry > 0;
  }
}

class Flat extends RealEstate implements GetAreable {
  //Omit Variables

  @Override
  public double getArea() {
      :
  }
}
```

As shown above <span style='color:#f7b731'>both abstract and concrete classes</span> can `impliment` an interface. However it is not the same otherwise, <span style='color:#f7b731'>interfaces can only inherit other interfaces</span>.

The concrete class has to <span style='color:#8854d0'>override</span> all of the abstract methods in the interface, if not it will become <span style='color:#0fb9b1'>abstract</span>.

Therefore, unlike <span style='color:#0fb9b1'>abstract classes</span>, it <span style='color:#f7b731'>cannot have instance fields</span> and it <span style='color:#f7b731'>cannot have non-abstract methods</span> (**Pure interface**)
<div style="page-break-after: always;"></div>

## Multiple Inheritance

Java <span style='color:#f7b731'>does not allow multiple inheritance</span> this is due to ambiguity where 2 superclass have the same method signature.

- A class can <span style='color:#8854d0'>extend</span> <mark class="hltr-orange">at most 1 class</mark>
- A class can <span style='color:#8854d0'>implement</span> <mark class="hltr-orange">0 or more interfaces</mark>
- An interface can <span style='color:#8854d0'>extend</span> <mark class="hltr-orange">0 or more interfaces</mark>

Interfaces can also be a supertype of a class, which is shown in the following code,
```Java
// Flat <: GetAreable and Flat <: RealEstate (2 Superclasses)
class Flat extends RealEstate implements GetAreable {
  //Omit Variables

  @Override
  public double getArea() {
      :
  }
}
```
## Casting an Interface

**Narrowing**
> Type casting to a <mark class="hltr-orange">supertype</mark>

**Widening**
> Type casting to a <mark class="hltr-orange">subtype</mark>

```Java
interface I {
    :
}

class A {
    :
}

class B implements I {
    :
}

I i1 = new B(); // Compiles, widening type conversion
I i2 = (I) new A(); // Compiles as well but will crash during run time
```

The reason why a object of type `A` can be type casted into `I`, as there is no certainty that it will not work. Thus java will allow it as it is explicitly done by the developer. If a <span style='color:#f7b731'>subclass</span> of `A` <span style='color:#8854d0'>implements</span> `I` then `A` can be type casted to `I`.

Thus even though `A` has no relationship with `I`, <span style='color:#f7b731'>it will still compile</span>. But it will <span style='color:#f7b731'>raise an issue during run time</span>.
<div style="page-break-after: always;"></div>

```Java
class AI extends A implements I {
    :
}
// This will allow A to be type casted into I
```

A class that has wrapper class arguments will not accept primitive type inputs
## Impure Interfaces

Interfaces are <span style='color:#f7b731'>quite static</span> as once they are defined, <span style='color:#f7b731'>any changes will affect all the classes that implements it</span>.

One way around this is to make <span style='color:#0fb9b1'>Impure Interfaces</span>. This type of interfaces contains `default` implementation of methods. Thus classes that <span style='color:#8854d0'>implement</span> it will not need to <span style='color:#8854d0'>override</span> these functions.

However, this will <span style='color:#f7b731'>cause an issue with multiple inheritance</span> even with multiple interfaces. Assuming 2 <span style='color:#0fb9b1'>impure interfaces</span> with <span style='color:#f7b731'>2 default methods</span> with the <span style='color:#f7b731'>same name</span>, then it <span style='color:#f7b731'>causes ambiguity</span> all over again.

Example of a impure interface:
```Java
interface Ordered {
  boolean lessThan(Ordered o);                     // this < o
  default boolean greaterThan(Ordered o) {         // this > o   -->  o < this
    return o.lessThan(this);
  }
  default boolean greaterThanOrEqual(Ordered o) {  // this >= o  -->  !(this < o)
    return !this.lessThan(o);
  }
  default boolean lessThanOrEqual(Ordered o) {     // this <= o  -->  !(this > o)  -->  !(o < this)
    return !o.lessThan(this);
  }
}
```

# Wrapper Class
---
**All** primitive wrapper class objects are <span style='color:#f7b731'>immutable</span>. Then when a new value is assigned, a new object will be created.

| Primitive |  Wrapper  |
|:---------:|:---------:|
|  `byte`   |  `Byte`   |
|  `short`  |  `Short`  |
|   `int`   | `Integer` |
|  `long`   |  `Long`   |
|  `float`  |  `Float`  |
| `double`  | `Double`  |
|  `char`   |  `Char`   |
| `boolean` | `Boolean` |

All of the wrapper classes that deals with Integers (numbers) are all subclasses of <span style='color:#2d98da'>Number</span>.
## Single Step Auto-Boxing

<span style='color:#0fb9b1'>Auto-boxing</span> and <span style='color:#0fb9b1'>unboxing</span> are <span style='color:#f7b731'>single step processes</span>. <span style='color:#f7b731'>Wrapper classes have no relationship with one another</span> thus, `int` can only be auto-boxed into a `Integer` and nothing else.

```Java
Double d = 2 // Error cannot convert int to Double (Single Step)

// The following is allowed
Integer x = 4; // auto-boxing
double d = x;  // auto-unboxing afterwards it will do a primitive subtyping
```
<div style="page-break-after: always;"></div>

## Performance

The performance of using a <span style='color:#0fb9b1'>wrapper class</span> instead of a <span style='color:#0fb9b1'>primitive type</span> is slower. This is because a wrapper class will behave like an object where the <span style='color:#f7b731'>variable stores the memory address</span>. Thus unlike the primitive type where the stack will contain the value. <span style='color:#f7b731'>Java will read the memory address</span> assigned to the variable in the stack and then <span style='color:#f7b731'>read the value of the object at that memory address inside the heap</span>.

So why use wrapper classes when a primitive type is just faster. Just like an array of objects, if a set of values is off different types and it must be stored in 1 array then using a wrapper class will work. Whereas `int[]` can only store primitive type integers.

# Variance
---
Let C(T) be a <span style='color:#0fb9b1'>complex type</span> based on type T. We say a complex type C is:
- Covariant
	If S <: T then it implies C(S) <: C(T)
- Contravariant
	If S <: T then it implies C(T) <: C(S)
- Invariant
	Neither covariant nor contravariant

**Complex Type**
	For now the only complex type is an array `<type> []` and it is <span style='color:#f7b731'>covariant</span>.


```Java
Integer[] intArray = new Integer[2] {
  Integer.valueOf(10), Integer.valueOf(20)
};
Object[] objArray;
objArray = intArray;
objArray[0] = "Hello!"; // <- compiles! But it will crash on run time :(
```

The above code works is because, `objArray` (_with a compile-time type of_ `Object[]`) can refer to an object with a run-time type of `Integer[]`. This is allowed since the <span style='color:#f7b731'>array is covariant</span>.

Next a `String` object is placed into the `Object` array. Since `String` <: `Object`, the compiler allows this. The compiler does not realize that at run-time, the `Object` array will refer to an array of `Integer`.

So we now have a perfectly compliable code, that will crash on us when it executes the last line. Only then would Java realize that we are trying to stuff a string into an array of integers!


We will consider 3 cases where it is _possible_ for RTT(`b`) to be a subtype of `C`. There may be other cases, so you have to think about possibilities in terms of potential new classes added in the future. `a = (C) b;`
<div style="page-break-after: always;"></div>

1. Case 1: CTT(`b`) <: `C`
    - This is simply widening and is always allowed.
    - The use of explicit type cast is unnecessary but not incorrect.
2. Case 2: `C` <: CTT(`b`)
    - This is narrowing and requires run-time checks.
    - Consider `C` <: `B`:
        - If CTT(`b`) = `B` and RTT(`b`) = `C` (_or subtype of_ `C`), then it is allowed at run-time.
        - If CTT(`b`) = `B` and RTT(`b`) = `C` (_or other subtype of_ `B` _that is not_ `C`), then it not allowed at run-time. Since there is a _possibility_, the compiler will add codes to check at run-time.
3. Case 3: `C` is an interface
    - Let RTT(`b`) = `B`. Then it may have a subclass `A` such that `A` <: `C` (_i.e., implements the interface_ `C`).
	    `class A extends B implements C { .. }`|  
    - If RTT(`b`) = `A`, then it is allowed at run-time.


## Produce / Consumer

Assume : A1 <: B and A2 <: B
### Producer

It produces a value

```Java
Object obj = objArray[0];
Object obj = f(argument);
```

**Covariant Problem**
```Java
A1[] aArr = new A1[] { new A1(), new A1() };
B[] bArr = aArr;    // assume covariant: A1[] <: B[]
bArr[0] = new A2(); // compiles because A2 <: B
// but this is a run-time error
```

### Consumer

It consumes a value

```Java
objArray[0] = value;
f(argument); // void function
```

**Contravariant Problem**
```Java
B[] bArr = new B[] { new A1(), new A2() };
A1[] aArr = bArr;   // assume contravariant: B[] <: A1[]
A1 a1 = aArr[2];    // compiles because A1 <: A1
// but this is a run-time error

// This is hypothetical as java array is not contravariant
```
<div style="page-break-after: always;"></div>

# Exception Handling
---

**Exception**
> It is an error that will be raised only on <span style='color:#f7b731'>run time</span>

**Try Catch Finally Syntax**
```Java
try {
  // do something
} catch (an exception parameter) { // Can have as many catches as you want
  // handle exception
} finally {
  // clean up code
  // regardless of there is an exception or not
}
```

The `try` statement must be used with at least one `catch` or `finally` block. It cannot just have the `try` block.

The `try` block will execute the code line by line, <span style='color:#f7b731'>once an error has occurred, all the remaining lines will not be executed</span> and the `catch` block will be executed followed by the `finally` block.

Java will go through one by one for each catch to find the catch with that specific error. When an error occurs it <span style='color:#f7b731'>will jump to the catch block which handles the error</span>.

**Check Exception**
- An error that the program has no control over (Raised during run time)
- Programmer has no control over (even if code is perfectly written).
- Checked by compiler that it is either handled or re-thrown. (It has to be handled)
- It is as subclass of `Exception` and not subclass of `RuntimeException`.
- It is good to make all exception checked

**Unchecked Exception**
- An error that is unnoticed (Raised during complication time)
- Caused by programmer's errors (should not happen if the code is perfectly written).
- Not checked by compiler and typically just let error be unrecoverable.
- Do not need to use a `try catch` block to handle the error 
- Subclass of `RuntimeException`.
<div style="page-break-after: always;"></div>


## Exception Hierarchy

**Throwable**
> Parent of all exception classes, every error can be thrown is a subtype of this

**Exception**
> All the issue that can arise from the code

**Error**
> A problem that is very severe that it cannot recover from it
## Custom Exception

**Unchecked Exception**

```Java
class InvalidCircle extends RuntimeException {
	public InvalidCircle(double r) {
		super("Invalid circle with radius: " + r); 
		// The superclass has a constructor that takes in a message
	}
}

// Usage
class Circle {
	// variables omitted
	
	public Circle(Point c, double r) {
		if (r <= 0) {
			throw new InvalidCircle(r); // Throw the exception 
		}
		// Rest of the implimentation
	}
}
```

**Checked Exception**
```Java
class InvalidCircle extends Exception { // Remember
	public InvalidCircle(double r) {
		super("Invalid circle with radius: " + r); 
		// The superclass has a constructor that takes in a message
	}
}

// Usage
class Circle {
	//varables omited
	public Circle(Point c, double r) throws InvalidCircle { // This is important, this line tells the code it may throw this exception and the caller should handle it
			if (r <= 0) {
				throw new InvalidCircle(r);
			}
		}
	}
}
```
## Catch Exceptions to Clean Up

Instead of stopping the program, if it is possible to deallocate or fix certain issues of the code and let it continue running will be better than just stopping the code all together.

```Java
public void m2() throws E2 {
  try {
    // setup resources
    m3();
  } catch (E2 e) {
    throw e;
  } finally {
    // clean up resources
  }
}
```

## Bad Practices of Exception Handling

### Do Not Use It As a Control Flow

```Java
// This will check even before executing thus it is better
if (obj != null) {
  obj.doSomething();
} else {
  doTheOtherThing();
}

// The below will try something which might not work
try {
  obj.doSomething();
} catch (NullPointerException e) {
  doTheOtherThing();
}
```

### Do Not Catch All Exception

```Java
try {
  // your code
} catch (Exception e) { // This will catch everything because everything is a subclass of exception
  System.exit(0);
}
```
### Do Not Overreact

```Java
try {
  // your code
} catch (Exception e) {
  System.exit(0); // Try and solve the problem do not just stop the program
}
```
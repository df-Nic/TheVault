---
title: Generics
Date Created: 2023-09-12
tags:
  - CS2023S
  - Java
---
# Generics
---

Java allows the usages of a <span style='color:#0fb9b1'>generic type</span>. Think of it as arguments that will take in other types.

This is useful as it allows us to make our code generic but also not scriptable to accidental type changes.

For example take a look at the `pair` class;
```Java
class Pair {
  private Object first;
  private Object second;

  public Pair(Object first, Object second) {
    this.first = first;
    this.second = second;
  }

  Object getFirst() {
    return this.first;
  }

  Object getSecond() {
    return this.second;
  }
}
```

To make the class <span style='color:#f7b731'>work for any type</span>, the class will store 2 objects. This comes as a cost of using <span style='color:#0fb9b1'>wrapper class </span>instead of <span style='color:#0fb9b1'>primitive types</span>.

Though this code is generic and is flexible, it does have its issues. If the Pair were to store a `Integer` pair but for some reason `String` was stored. This will then cause errors down the line.

**Using generic types;**
```Java
class Pair<S,T> {
  private S first;
  private T second;

  public Pair(S first, T second) {
    this.first = first;
    this.second = second;
  }

  public S getFirst() {
    return this.first;
  }
  // Rest of the methods
}
```

From the example above the <span style='color:#f7b731'>generic type is specified between</span> < and >, where `S` and `T` are the type parameters.

To initiate a class using a generic type, the user must specify the type inputs for the class like so;
`Pair<String, Integer> p = new Pair("Hello", 2030);`

It is also possible to pass a perimeter of a method to another method
```Java
class DictEntry<T> extends Pair<String,T> {
    // Functions and Attributes omitted
}
```

Here `T` will be passed in as the type argument for Pair.
## Generic Methods

Same as before, a <span style='color:#f7b731'>method can use generic types as type inputs along with arguments</span>.

```Java
class A {
  public static <T> boolean contains(T[] array, T obj) {
    for (T curr : array) {
      if (curr.equals(obj)) {
        return true;
      }
    }
    return false;
  }
}

/**
Main method
String[] strArray = new String[] { "hello", "world" };
A.<String>contains(strArray, 123); // type mismatch error
*/
```

Here the function also requires a <span style='color:#f7b731'>type as a input alongside the needed augments</span>. The reason for this is because, lets say someone wants to search for a `String` in a `int` array. It will always be false.

```Java
class Confused<T> { // T#1
  private T t;

  public <T> T getT() { // T#2
    return this.t; // Return T#1 but the function return type is T#2??
  }
}
```

The above shows that there are 1 generic type `T`, however they are <span style='color:#f7b731'>treated as 2 separate types</span>. Java as a unique numbering to distinguish both. Thus an error is raised as the return type is different from the returning value's type.

<mark class="hltr-orange">Static methods cannot use a generic type</mark> is have to use a defined type.
## Bounded Type Parameters

A generic type is too generic! This can be restricted by <span style='color:#f7b731'>putting a restraint on the generic type</span> through the keyword <span style='color:#8854d0'>extends</span>.

```Java
class A {
  public static <T extends GetAreable> T findLargest(T[] array) {
    double maxArea = 0;
    T maxObj = null;
    for (T curr : array) {
      double area = curr.getArea(); //Not all classes have this function
      if (area > maxArea) {
        maxArea = area;
        maxObj = curr;
      }
    }
    return maxObj;
  }
}
```

If `T` does not extends from `GetAreable`, Java will raise an error. This is because during compile time T will be treated as an object (Will be discussed later). The rational behind this is that <span style='color:#f7b731'>T can be any class and not all classes will have the</span> `getArea` function.

Thus with the <span style='color:#8854d0'>extends</span> `getAreable`. It restricts T to only be `getAreable` class or <span style='color:#f7b731'>any of its subtypes.</span> Which will definitely have the `getArea` function.
<div style="page-break-after: always;"></div>

# Type Erasure
---
## Code Sharing

<span style='color:#0fb9b1'>Code Sharing</span> is a code generation method of <span style='color:#f7b731'>erasing type arguments and type parameters</span> in conjunction (usually after) with type checking. This is the method used by Java.

This make it such that there is <span style='color:#f7b731'>only one representation of the generic type</span> in the generated code which encompasses all instantiated generic types. Thus it does not need to be recompiled for new types.

All the generic types are replaced with `object` however if it is bounded (upper bound) it will be replaced by the bound instead.

```Java
// Generic type is instantiated and used
Integer i = new Pair<String,Integer>("hello", 4).getSecond();
// What Java transformed it into
Integer i = (Integer) new Pair("hello", 4).getSecond();
```

## Generics & Arrays

Java generic types are <span style='color:#0fb9b1'>invariant</span> and <mark class="hltr-orange">thus it cannot be mixed with Java arrays</mark>. If a Array of generic type is created it will be invariant. If not it will violate Liskov substitution principle

After type erasure, the run time will not know about the type arguments as it would have been removed.

```Java
// create a new array of pairs
Pair[] pairArray = new Pair[2];

// pass around the array of pairs as an array of object
Object[] objArray = pairArray;

// put a pair into the array -- no ArrayStoreException!
objArray[0] = new Pair(3.14, true);
```

For example, as shown above the generic types are removed and <span style='color:#f7b731'>Java will check that an array of pairs is being put another pair inside</span>. Everything checks out. This would have caused a <span style='color:#0fb9b1'>heap pollution</span>.

**Heap Pollution**
> A variable of a parameterized type refers to an object that is not of that parameterized type.

The following lines of code will not work
```Java
Pair<String,Integer>[] pairArray = new Pair<String,Integer>[2];
new Pair<S,T>[2];
new T[2]; // If T is not given

// Basically a generic type cannot be instantiated
```
<div style="page-break-after: always;"></div>

# Unchecked Warnings
---
## Creating Arrays with Type Parameters

One way to get around this is to use an `ArrayList`. It does the <span style='color:#f7b731'>type checking during compile time</span> and since it is a generic class, it is also <span style='color:#0fb9b1'>invariant</span> unlike array. Thus there is no subtyping relationship, preventing heap pollution. 

Another way to get around Java's array is through the following
```Java
class Array<T extends Comparable<T>> {
  private T[] array;

  Array(int size) {
	@SuppressWarnings("unchecked", "rawtype")
    this.array = (T[]) new Comparable[size];
    // Why use Comparanble instead of Object, while if we use object then after type erasure, 
    // It is trying to assign Comparable = Object which is wrong if you use Object
  }

  public void set(int index, T item) {
    this.array[index] = item;
  }

  public T get(int index) {
    return this.array[index];
  }

  public T[] getArray() {
    return this.array;
  }
}
```

The array will be a new array of comparable which will be type casted into `T`.

This works because, without the type casting Java will know that not all Comparable are a subtype of T and this will not compile. In addition if it was just `T[length]` it will also raise an error as Java cannot instantiate a generic array

The above compile however, it will still raise an error as Java cannot guarantee it is safe since it does not know if Object is a subtype of T.
```Java
Array<String> array = new Array<String>(4);
Object[] objArray = array.getArray();
objArray[0] = 4;
array.get(0);  // ClassCastException
```
<div style="page-break-after: always;"></div>

If the coder is sure that it will not cause an error during run time then they can suppress the error message through `@SuppressWarnings("unchecked")`.

- `@SuppressWarnings("unchecked")` can only be <span style='color:#f7b731'>used to the most limited scope</span> to - avoid unintentionally suppressing warnings that are valid concerns from the compiler.
- Suppress a <span style='color:#f7b731'>warning only if it is certain that it will not cause a type error</span> later.
- Must always add a note (_as a comment_) to fellow programmers explaining why a warning can be safely suppressed.
- It can only be used on a declaration and not a assignment.

## Raw Types

A <span style='color:#0fb9b1'>raw type</span> is <span style='color:#f7b731'>a generic type used without type arguments</span>. This corresponds to the code after type erasure.

```Java
Array arr = new Array(4);
arr.set(0, "hello");

Array arr<Integer> x = new Array<>(4) // This is not a raw type
Array arr<Integer> x = new Array(4) // This is a raw type
```

The above will just use the generic `Array<T>` as a <span style='color:#0fb9b1'>raw type</span> array.

```Java
void populateArray(Array a) { // Raw type
  a.set(0, 1234);
}

Array<String> a = new Array<String>(4);
populateArray(a);
String s = a.get(0);

```

Consider the above code, it will give a warning as Java cannot do any type checking without any type argument. As it cannot guarantee that object :< T. Therefore raw types must not be used in code and it the warning is ignored it will cause a run time error.

The only exception is using it as an operand of `instanceof` method. Since `instanceof` checks for run-time type and type arguments have been erased, we can only use the `instanceof` operator on raw types.

`instanceof` will also return true if it is a <span style='color:#f7b731'>subclass</span>.
---
title: Wildcards & Type Inference
Date Created: 2023-09-19
tags:
  - CS2023S
  - Java
---
# Wildcards
---

Remember in the previous chapter, generics are <span style='color:#0fb9b1'>invariant</span> in Java. Therefore an array of type T and type S are not covariant even through T is a subtype of S.

To solve this Java <span style='color:#0fb9b1'>wildcards</span> can be used which is denoted as `?`. It acts like a <span style='color:#f7b731'>substitute for any type</span>, making it more flexible. 

## Upper-Bounded Wildcards

```Java
public void copyFrom(Array<? extends Shape> src) {
	int len = Math.min(this.array.length, src.array.length);
	for (int i = 0; i < len; i++) {
		this.set(i, src.get(i));
	}
}
```

Given the above code the <span style='color:#0fb9b1'>wildcard</span> `?` is <span style='color:#f7b731'>upper bounded</span> by Shape. Meaning `?` can be <span style='color:#f7b731'>substituted for any type of Shape and its subclasses</span>.
<div style="page-break-after: always;"></div>

This wild card is <mark class="hltr-orange">covariant</mark> meaning it has the following subtyping relations:
- If S <: T then `A<? extends S>` <: `A<? extends T>` (covariance)
	Whatever the LHS can accept for `?` the RHS can accept as well
- For any type `S`, `A<S>` <: `A<? extends S>`

## Lower-Bounded Wildcards

```Java
public void copyTo(Array<? super T> dest) {
	int len = Math.min(this.array.length, dest.array.length);
    for (int i = 0; i < len; i++) {
      dest.set(i, this.get(i));
	}
}
```

Given the above code the <span style='color:#0fb9b1'>wildcard</span> `?` is <span style='color:#f7b731'>lower bounded</span> by T. Meaning `?` can be <span style='color:#f7b731'>substituted for any type of T and its superclasses</span>.

This wild card is <mark class="hltr-orange">contravariant</mark> meaning it has the following subtyping relations:
- If S <: T then `A<? extends T>` <: `A<? super S>` (contravariant)
- For any type `S`, `A<S>` <: `A<? super S>`
## Unbounded Wildcards

It is just a wildcard with <span style='color:#f7b731'>no restrictions</span>. Therefore it accepts any class

This wild card is <mark class="hltr-orange">invariant</mark> meaning it has the following subtyping relations:
-  `C<S>` <: `C<?>` 
-  `C<? extends S>` <: `C<?>` 
-  `C<? super S>` <: `C<?>` 

Why so is because it will be <span style='color:#f7b731'>fully contain inside </span>of `C<?>`

Side note `new C<?>[10]` does work, however this cannot be used
```Java
new C<?>[10];
arr[0] = new C<Integer>(5);
arr[0].set(6); // compile error
Integer x = arr[0].get(); // compile error
```

If there is no lowest or highest bound then any type for `?` might cause an error.
<div style="page-break-after: always;"></div>

## PECS

This stands for
- Producer
- Extends
- Consumer
- Super

This server as a basis on when to use <span style='color:#0fb9b1'>upper-bounded</span> or <span style='color:#0fb9b1'>lower-bounded wildcards</span>

```Java
// This is a consumer as des.set uses some value of type T from this.
copyTo(Array<? super T> dst )
	dst.set(i, this.get(i))

// This is a prodicer as src.get returns some value which will be used by this 
copyFrom(Array<? extends T> src )
	this.set(i, src.get(i))
```

# Type Inference
---

If the code gets too long, it can be shorten by <span style='color:#0fb9b1'>initiating inference</span>.

## Diamond Operator

```Java
Pair<String, Integer> p = new Pair<String, Integer>();
Pair<Pair<String, Integer>, Pair<Double, Double>> p = new Pair<>();
```

Inside the `<>` of new `Pair<>()`; java will infer it to be `Pair<String, Integer>`, `Pair<Double, Double>`.
## Method Invocation

```Java
Main.<String>contains(new Array<String>(0), "CS2030S");
Main.contains(new Array<String>(0), 2030); // Inferred to what?
```
<div style="page-break-after: always;"></div>

## Inference Algorithm

**Steps**
1) Write all the <span style='color:#f7b731'>local type constraints</span> (Not all 3 might appear)
	-  **Target Type** : The return type must be the subtype of the variable it is assigned to, if there is a return type
	-  **Argument Typing** : The type of argument must be the subtype of the parameter, if there is a arguments
	-  **Type Parameter Bound** : The declaration of the generic type if there is a generic type

2) Solve the type constraint for the declared generic type using:
	-  <span style='color:#0fb9b1'>Reflexive</span> property of subtyping relationships
	- <span style='color:#0fb9b1'>Transitive</span> property of subtyping relationships
	- <span style='color:#0fb9b1'>Anti-Symmetric</span> property of subtyping relationships

3) If there are multiple possible solutions, then choose the <span style='color:#f7b731'>most specific ones</span> from the type specified in the constraints
	-  Ignore the subclasses not specified in the constraints
	- The solution may be the <span style='color:#0fb9b1'>superclass</span> of the types specified in the constraints


## Examples

### Example 1

```Java
Main.contains(cArr, shape); // cArr :: Array<Circle> & shape :: Shape

<T> boolean contains(Array<? extends T> array, T obj) { .. }
```

**Target Typing**
-  None as `main.contains...` is not being assigned to anything
 
**Argument Typing**
Based on the <span style='color:#f7b731'>input arguments</span>;
-  `Array<Circle>` <: `Array<? extends T>`
- `Shape` <: `T`

Now remember <span style='color:#f7b731'>Java generic is invariant</span>; thus 
-  `?` = `Circle`
- Therefore `Circle` <: `T`

Now there are 2 things to solve 
1) `Circle` <: `T`
2) `Shape` <: `T`

**Type Parameter Bound**
- There is nothing as T is just some generic type <span style='color:#f7b731'>not bounded</span> or it can be said as `T` <: `T`

Since if there are multiple options, choose the <span style='color:#f7b731'>most specific one</span> and therefore, T will be inferenced as `Shape`

### Example 2

```Java
Main.contains(strArr, 2030); // strArr :: String[]

<T> boolean contains(T[] array, T obj) { .. }
```

**Target Typing**
-  None as `main.contains...` is not being assigned to anything
 
**Argument Typing**
Based on the <span style='color:#f7b731'>input arguments</span>;
-  `String[]` <: `T[]`
- `Integer` <: `T`

Now remember <span style='color:#f7b731'>Java array is covariant</span>; thus (Notice the usage of `[]` instead of `<>`)
-  `String` <: `T`

Now there are 2 things to solve 
1) `String` <: `T`
2) `Integer` <: `T`

**Type Parameter Bound**
- There is nothing as T is just some generic type <span style='color:#f7b731'>not bounded</span> or it can be said as `T` <: `T`

Since if there are multiple options, choose the <span style='color:#f7b731'>most specific one</span> and therefore, T will be inferenced as `Object`
<div style="page-break-after: always;"></div>

### Example 3

```Java
Shape s = Main.findLargest(new Array<Circle>(0));

<T extends GetAreable> T findLargest(Array<? extends T> array) { .. }
```

**Target Typing**
-  `T` <: `Shape`
 
**Argument Typing**
Based on the <span style='color:#f7b731'>input arguments</span>;
-  `Array<Circle>` <: `Array<? extends T>`

Now remember <span style='color:#f7b731'>Java generic is invariant</span>; thus 
-  `?` = `Circle`
-  Thus `Circle` <: `T`

**Type Parameter Bound**
- `T` <: `GetAreable`

Here there are;
1)  `T` <: `GetAreable`
2)  `T` <: `Shape`
3) `Circle` <: `T`

Since if there are multiple options, choose the <span style='color:#f7b731'>most specific one</span> and therefore, T will be inferenced as `Circle`
<div style="page-break-after: always;"></div>

### Example 4

```Java
Main.findLargest(new Array<Circle>(0)).getColour();

<T extends GetAreable> T findLargest(Array<? super T> array) { .. }
```

**Target Typing**
-  None as `main.contains...` is not being assigned to anything
 
**Argument Typing**
Based on the <span style='color:#f7b731'>input arguments</span>;
-  `Array<Circle>` <: `Array<? super T>`

Now remember <span style='color:#f7b731'>Java generic is invariant</span>; thus 
-  `?` = `Circle`
-  Thus `T` <: `Circle` as `Circle` is a supertype of T

**Type Parameter Bound**
- `T` <: `GetAreable`

Here there is;
1)  `T` <: `GetAreable`
2)  `T` <: `Circle`

Since if there are multiple options, choose the <span style='color:#f7b731'>most specific one</span> and therefore, T will be inferenced as `Circle`. Even though `ColouredCcircle` works but the class was not mentioned at all thus it will not be used.

The above however will <span style='color:#f7b731'>not compile</span> as a Circle does not have the function `.getColour()` since T is being inferenced as of type `Circle`.
---
title: Lambda and Lazy
Date Created: 2023-10-17
tags:
  - CS2023S
  - Java
---
# Functions
---
**Pure Functions**
> Denoted by $f : x \rightarrow y$ is a mapping from the <span style='color:#f7b731'>domain</span> x to the <span style='color:#f7b731'>co-domain</span> y

Thus a pure function will be <span style='color:#f7b731'>deterministic</span>, has <span style='color:#f7b731'>no side-effect</span> and is <span style='color:#f7b731'>referentially transparent</span>

**Deterministic**
> $f(x) == y$ for all values of x

**Referentially Transparent**
> All f(x) can be replaced with y and vise versa

This means that if in the code uses y = 1 and f(x) returns 1 if x = 1, then it can be rewritten as y = f(1)

This can be an issue in arrays where if it is <span style='color:#eb3b5a'>not immutable</span> then it might not always return the same value

**No Side-effect**
> Only the value is relevant (Input arguments is relevant, `this` is not included)

Examples of Side Effects:
-  Print to the monitor
-  Write to files
-  Throw exceptions
-  Modify Fields (Reassignment / Mutation)
-  Modify the arguments (Reassignment / Mutation)

Adding new functions in classes can be complicated, however making lambda functions is easier as they can exists outside of the class to be used by the client.

```Java
// Impure function
Box<Integer> increment(Box<Integer> box) {
	return new Box<>(box.val() + this.ctx); // Impure cause this.ctx might not be a constant
}

// Pure Function
Ctx<integer> increment(Ctx<Integer> ctx) {
	return new Ctx<>(ctx.val() + ctx.ctx(), ctx.ctx());
}
```
<div style="page-break-after: always;"></div>

## Higher Order Functions

A function is a <span style='color:#0fb9b1'>higher-order function</span> or a <span style='color:#f7b731'>first class citizen</span> if F can be
1)  Assigned to another variable
2)  Can be passed into a function as an argument
3)  Can be returned from a function as a value
4)  Can be inserted into an array

However one issue in java is that there is <span style='color:#eb3b5a'>no type for a function</span>. Thus to simulate this <mark class="hltr-orange">a class can be made</mark> which mimics a function which can be passed in as a argument.

**Example**
```Java
// Here we can see that it has 2 inputs and 1 return, so depending on the number of generics
// The number of inputs can be adjusted
interface Fun<T,U,V> {
	V apply(T,U);
}
```
## Lambda Functions

In java a lambda function is called a <span style='color:#0fb9b1'>functional interface</span> where it is an <mark class="hltr-orange">interface</mark> with a <mark class="hltr-orange">single abstract method</mark> and this should be annotated with a `@Functionalinterface`

Thus it can be used as the assignment target for <span style='color:#0fb9b1'>lambda expressions</span>

**Example**
```Java
@FunctionalInterface 
interface Transformer<T, R> { 
	R transform(T t); 
}
```

**Lambda Expression**
> It is an <span style='color:#0fb9b1'>anonymous function</span>, a function with no name

**Example**
```Java
// Named Class (Used the java Function package)
class Incr impliments Function<Integer, Integer> {
	@override
	public int apply(int x) {
		return x + 1
	}
}

// Anonymous Class
Function<Integer, Integer> f = 
	new Function<>() {
		@Override
		Integer apply(Integer x) {
			return x + 1;
		}
	};

// To call our lambda function just use, this can be used if f is a functional interface
Function<Integer, Integer> f = x -> x + 1;
```

```Java
Function<Integer, Integer> f = x -> x + 1;
```

Since f is a <span style='color:#0fb9b1'>functional interface</span> the type of x and the return type can be inferred from the <T,U> in front of f.
Java will create the Function class with the respective method body and input arguments

Syntax of **Lambda Functions**,
```Java
// No parameter Lambda Function
() -> expr

// Single Parameter
param -> expr

// Multiple Parameters
(param1, param2) -> expr

// Multiple Statements
(param1, param2, param3) -> {body; return expr; }
```
### Currying

It is a technique to convert a lambda function that takes in<span style='color:#f7b731'> multiple arguments</span> into a <mark class="hltr-orange">sequence of functions that each takes in a single argument</mark>.

The goal here is to minimize the number of interfaces created with different generic types 

This can be written as `Transformer<Integer, Transformer<Integer, Integer>> add = x -> y -> (x + y);`

This works as x will be locally captured and thus when the inner function is called then the remembered value x will be used. Thus x or <mark class="hltr-orange">any object that is locally captured must be effectively final or final</mark>

<div style="page-break-after: always;"></div>
# Lazy
---

**Eger Evaluation**

This is currently the type of code that was coded, where something will be computed weather or not it is needed at that moment.

**Lazy Evaluation**

This allows a delay in the execution of code, saving them until it is needed later. This enables another powerful mechanism called <span style='color:#0fb9b1'>lazy evaluation</span>. Where a <span style='color:#f7b731'>sequence of complex computations can be built, without actually executing them, until it is need to</span>. Expressions are evaluated on demand when needed.

**Example**
```Java
class Lazy<T> {
	private T value;
	private boolean isAvailable;
	private Producer<T> producer;
	
	public Lazy(Producer<T> producer) {
		this.isAvailable = false;
	    this.value = null;
	    this.producer = producer;
	}
	
	public T get() {
		if (!isAvailable) {
			this.value = producer.produce();
			this.isAvailable = true;
		}
		return this.value;
	}
}

class Logger {
	enum LogLevel { INFO, WARNING, ERROR };
	
	public static LogLevel currLogLevel = LogLevel.WARNING;
	
	static void lazyLog(LogLevel level, Lazy<String> msg) {
		if (level.compareTo(Logger.currLogLevel) >= 0) {
			System.out.println(" [" + level + "] " + msg.get());
		}
	}
}


// To Call the function
Lazy<String> loginMessage = new Lazy(
    () -> "User " + System.getProperty("user.name") + " has logged in");

Logger.lazyLog(Logger.LogLevel.INFO, loginMessage);
```
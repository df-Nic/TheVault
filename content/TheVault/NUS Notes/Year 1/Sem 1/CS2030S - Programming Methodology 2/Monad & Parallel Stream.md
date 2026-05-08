---
title: Monad & Parallel Stream
Date Created: 2023-10-31
tags:
  - CS2023S
  - Concurrency
---
# Logging
---
<span style='color:#0fb9b1'>Category Theory</span> given 2 functions $f(x)$ and $g(x)$, both of these function are [[Lambda and Lazy#Functions|pure functions]] and thus they can be <span style='color:#f7b731'>composite</span> to give the same result as using it subsequently $f(x) -> y \ \& \ g(y) -> z = g(f(x))$. Similar there must be a <span style='color:#0fb9b1'>identity function</span> for values x y and z

A `flatmap` function which was implemented to <span style='color:#f7b731'>transform a value into a object</span>. For this to work the content of the output must be composed.

**Context**
> The context is usually used as a <span style='color:#f7b731'>description</span> of what a class will represent

For example `Lazy<T>`, the item is evaluated on demand and is evaluated once

## Logger Class

A log in general is a <span style='color:#f7b731'>record of all previous operations done</span>. Thus the logger class will record each operation done to some object or value

**Example**
```Java
// Logger Class
class Loggable<T> {
	private final T value;
	private final String log;
	
	private Loggable(T value, String log) {
		this.value = value;
		this.log = log;
	}
	
	public static <T> Loggable<T> of(T value) {
		return new Loggable<>(value, "");
	}
	
	public <R> Loggable<R> flatMap(Transformer<? super T, ? extends Loggable<? extends R>> transformer) {
	Loggable<? extends R> transformedItem = transformer.transform(this.value);
	// Below is the compose function, combines the info from the 'this' and transformedItem into 1
	return new Loggable<>(l.value, transformedItem.log + this.log); 
	
	public String toString() {
		return "value: " + this.value + ", log: " + this.log;
	}
}

// Sample transformer function to log
public Loggable<T> add_one(T x) {
	return Loggable.of(x + 1, "<- add one (" + x + ")" );
}
```

the following code above uses a `flatmap` instead of `map`. This is because if the `map` function is used, then <span style='color:#eb3b5a'>how will it store the string of past operations since it only return the value</span>. Thus the `flatmap` function is useful as it returns an object which is able to store more information

# Monad & Functor
---
## Monad

It is a <span style='color:#f7b731'>algebraic structure in category theory</span> with a structure with at least 2 methods called the `of` and `flatmap` function which <mark class="hltr-orange">must obey these three laws</mark>

1) Left Identity Law
	 $\forall x, f(x)$: `Monad.of(x).flatMap(y -> f(y))` $\equiv$ `f(x)`

This means that the `of` function cannot add necessary context <span style='color:#f7b731'>except the identity context</span> which is why the logging starts with a empty string. And that either calling the `flatmap` or `f(x)` will return the same Monad object with the same values 

2) Right Identity Law
	 $\forall$ monad: `monad.flatMap(x -> Monad.of(y))` $\equiv$ monad

Similar explanation to the left identity law

Take note $x^{y}$ there <span style='color:#f7b731'>is a right identity</span> where $y = 1$ but there is <span style='color:#eb3b5a'>no left identity</span> as nothing to the power of y which is equals to y

After calling a `flatmap` function and assigning the return to y then the return value of `y.flatmap(x -> Monad.of(y))` will be the same as y

3) Associative Law
	 $\forall$ monad, $f(x)$: `monad.flatMap(x -> f(x) ).flatMap(y -> g(y))` $\equiv$ `monad.flatMap(x -> f(x).flatMap(x -> g(x)) )` 

The above just <span style='color:#f7b731'>making a composite function</span> where the LHS is just $(C_{1} \oplus C_{2}) \oplus C_{3}$ while the RHS is just $C_{1} \oplus (C_{2} \oplus C_{3})$ 

**Example**
```Java
class Monad<T, S> {
	private final T content; // the content (value to be operated on)
	private final S context; // the context (side-information)

    :

  public <U> Monad<U, S> map(Transformer<? super T, ? extends U> transformer) {
    U content = transformer.transform(this.content);
    return new Monad(content, this.context); // preserve context
  }

  public <U> Monad<U, S> flatMap(Transformer<? super T, ? extends Monad<? extends U, ? extends S>> transformer) {
    Monad<? extends U, ? extends S>> next = transformer.transform(this.content);
    return Monad.compose(this, next);
  }

  private static <T, U, S> Monad<U, S> compose(Monad<T, S> prev, Monad<? extends U, ? extends S>> next) {
      : // code omitted
  }
}
```

## Functor

it is a design pattern inspired by the definition from category theory that allows one to <span style='color:#f7b731'>apply a function to values inside a generic type without changing the structure of the generic type</span>

It must contain at least 2 methods called the `of` and `map` function which <mark class="hltr-orange">must obey these two laws</mark>

1) Identity Law / Identity Morphism
	 $\forall$ functor: `functor.map(x -> x)` $\equiv$ functor

2) Composition Law / Composition Morphism
	 $\forall$ functor, $f(x)$, $g(x)$: `functor.map(x -> f(x) ).map(y -> g(y) )` $\equiv$ `functor.map(x -> g(f(x)))`

Even though a structure that<span style='color:#f7b731'> satisfy the three laws of Monad</span> it <mark class="hltr-red">might not not satisfy all the laws of Functor</mark>

Even though Monad and Functor are classes in java but they are basically a concept to make some classes

# Concurrent & Parallel Computing
---
## Concurrent

Currently most codes that run are sequential. Thus there are ways to run different processes <span style='color:#0fb9b1'>concurrently</span>

Something that is concurrent is when there are <span style='color:#f7b731'>multiple process running at the same time
</span>
The benefits of these are it
1) Improves utilization of the processor such that one process which is slow will not affect another process
2) Allows the programmer to separate unrelated tasks into threads and write each thread separately

## Parallelism

<span style='color:#0fb9b1'>Parallel computing</span> refers to the scenario where multiple subtasks are truly running at the same time -- either;
-  Have a processor that is capable of running multiple instructions at the same time
- Have multiple cores/processors and dispatch the instructions to the cores/processors so that they are executed at the same time

<span style='color:#eb3b5a'>All parallel programs are concurrent but not all concurrent programs are parallel</span>

However <span style='color:#f7b731'>not every process can be made parallel</span>. This is called <span style='color:#0fb9b1'>embarrassingly parallel</span> one where little or no effort is needed to separate the problem into a number of parallel tasks. This occurs when the <span style='color:#f7b731'>operation does not care about the order of the data</span>
<div style="page-break-after: always;"></div>

## Summary for the different processes

1) Sequential
	 One task must finish before the next task is carried out

2) Multi Processing
	 <span style='color:#f7b731'>Multiple CPU </span>to do multiple processes for double the output

3) Concurrent Multi-Tasking
	 2 or more tasks can be paused to execute some other process

4) Multi Threading
	 2 tasks or more are running different processes at the same time with <span style='color:#f7b731'>one CPU and with the help of the different cores</span>

## Using Streams to do Parallel Computing

[[Infinite List & Streams#Streams|Java Streams]] can be used to do parallel computing

```Java
import Java.util.stream.Streams

boolean isPrime(int x) {
  for (int i = 2; i <= x-1; i++) {
    if (x % i == 0) {
      return false;
    }
  }
  return true;
}

IntStream.range(2030000,2040000)
	.filter(x -> isPrime(x))
	.forEach(System.out::println)

// Using parallel computing
IntStream.range(2030000,2040000)
	.parallel()
	.filter(x -> isPrime(x))
	.forEach(System.out::println)
// However when each item is printed the order will be different as depending on which core finishes its process it will carry on with the next one

// Making it sequential
IntStream.range(2030000,2040000)
	.parallel()
	.sequential()
	.filter(x -> isPrime(x))
	.forEach(System.out::println)
```

There is a method `sequential()` which marks the stream to be process sequentially. If you call both `parallel()` and `sequential()` in a stream, the last call "wins"

## Interference

Since parallel computing does tasks simultaneously but what if 2 processes accessed an object and modify it at the same time. This is one <span style='color:#f7b731'>limitation</span> of using parallel computing.

This usually applies to <span style='color:#0fb9b1'>stateful</span> functions where the <span style='color:#f7b731'>result depends on any state</span> (the input) that might change during the execution of the stream. This can cause incorrect outputs.

This is called <span style='color:#0fb9b1'>atomic operations</span> which are operations that execute without interruption of any other process in between their execution phase

**Example**
```Java
List<Integer> list = new ArrayList<>(
    Arrays.asList(1,3,5,7,9,11,13,15,17,19));
    
List<Integer> result = new ArrayList<>();
list.parallelStream()
    .filter(x -> isPrime(x))
    .forEach(x -> result.add(x));
```

There are ways to solve it and it is using
1) `.collect` method
```Java
list.parallelStream()
    .filter(x -> isPrime(x))
    .collect(Collectors.toList())
```

2) Using a thread-safe data structure in the concurrent package
```Java
List<Integer> result = new CopyOnWriteArrayList<>();
list.parallelStream()
    .filter(x -> isPrime(x))
    .forEach(x -> result.add(x));
```

3) `.toList` method
```Java
list.parallelStream()
    .filter(x -> isPrime(x))
    .toList()
```

## Associativity

The `reduce` function can combine all of the items in the stream into one particular value and if it is <span style='color:#f7b731'>done in parallel, then the stream will be processed by parts </span>

Consider the following code

```Java
<U> U reduce (U e, BiFunction<U, ? super T, U> f, BinaryOperator<U> g)

// Where f is the accumulator and g is the combiner
```

The accumulator <span style='color:#f7b731'>does something to the set of elements in one block</span>, while the combiner <span style='color:#f7b731'>does something to the accumulated value from all the blocks</span>
<div style="page-break-after: always;"></div>

Therefore there are some rules to follow in order to get the correct out put
1)  `e` must be some identity, $g(e,x) = x$ for the `reduce` and `f(x)`
2)  Functions $f$ and $g$ must be a pure function
3)  Functions $f$ and $g$ <span style='color:#f7b731'>must be associative</span>, H
	 However if the above is being used then $f$ does not need to be associative unless `T reduce(T e, BinaryOperator<T> f)` is used where $f$ is <span style='color:#f7b731'>both the combiner and the accumulator</span>
4)  Functions $f$ and $g$ must be compatible, where $g(x,f(e,y)) = f(x,y)$

---
title: Infinite List & Streams
Date Created: 2023-10-25
tags:
  - CS2023S
  - Java
---
# Infinite List
---

An infinite list is a list which can <span style='color:#f7b731'>store an infinite number of values</span>, however java's array is immutable and the size is fixed. Therefore, <span style='color:#f7b731'>this list can be constructed as a class</span> with a `head`, `tail` (Which is another list) and a terminating list called `Sentinel` which is a <span style='color:#f7b731'>subtype of the class</span>.

Think of this as a linked list which is a pair of items where one is the value itself and the other points to another pair
## Eager List

This version of an infinite list evaluates all values upon creation of the list. And there are a few special functions that are implemented which are `get`, `iterate`, `generate`, `filter` and `map`

```Java
class EagerList<T> {
	private final T head;
	private final EagerList<T> tail;
	private static EagerList<?> EMPTY = new Sentinel(); 
	
	public EagerList(T head, EagerList<T> tail) {
		this.head = head;
		this.tail = tail;
	}
	
	// Other functions which will be covered later
}
```

### `get` Function

```java
public T get(int n) {
	if (n == 0) {
      return this.head();          // be careful!
    }                              //   use the methods
    return this.tail().get(n - 1); //   instead of fields
}
```

^975f17

The above implementation works is by <span style='color:#f7b731'>recursively</span> calling the `get` function to get the value of a specific index in the `EagerList` 

Also note that `tail` is also another `EagerList` which <span style='color:#f7b731'>contains the next index value</span> and therefore, it will have the method `get`
### `generate` Function

```Java
public static <T> EagerList<T> generate(T t, int size) {
	if (size == 0) {
		return empty();
    }
    return new EagerList<>(t, generate(t, size - 1));
}
```

It will create a `EagerList` of size n and each recuring `EagerList` in `tail` will have the same value

### `iterate` Function

```Java
public static <T> EagerList<T> iterate(T init, BooleanCondition<? super T> cond, 
									   Transformer<? super T, ? extends T> op) {
	
	if (!cond.test(init)) {
      return empty();
    }
    return new EagerList<>(init, iterate(op.transform(init), cond, op));
}
```

This function its a <mark class="hltr-orange">reproduction of the while / for loop in java</mark>. `init` will be the <span style='color:#f7b731'>base value</span> and <span style='color:#f7b731'>depending on the condition</span>, it will continue to create a `EagerList` with the transformed value and will <span style='color:#eb3b5a'>terminate when the condition is not fulfilled</span>

### `map` Function

```Java
public <R> EagerList<R> map(Transformer<? super T, ? extends R> mapper) {
	return new EagerList<>(mapper.transform(this.head()), this.tail().map(mapper));
}

// In the Sentinel class
@Override
public <R> EagerList<R> map(Transformer<? super Object, ? extends R> mapper) {
	return empty();
}
```

The `map` functions returns a `EagerList` with all its <span style='color:#f7b731'>values re-evaluated based on the</span> `mapper`. It <span style='color:#f7b731'>recursively calls the function</span> as the `tail` is a `EagerList` and the function also returns a `EagerList` which is good as the `tail` of the list is an `EagerList`

### `filter` Function

```Java
public EagerList<T> filter(BooleanCondition<? super T> cond) {
    if (cond.test(this.head())) {
	    return new EagerList<>(this.head(), this.tail().filter(cond));
	}
	return this.tail().filter(cond);
}

// In the Sentinel class
@Override
public EagerList<Object> filter(BooleanCondition<? super Object> cond) {
    return empty();
}
```

The `filter` function will return a new `EagerList` where the values satisfy the condition. The function will <span style='color:#f7b731'>start creating</span> a `EagerList` <span style='color:#f7b731'>once one of the value satisfy the condition</span>. If the subsequent values <span style='color:#f7b731'>do not meet the condition then it will be skipped</span>

## Lazy List

Instead of evaluating all the values in the list, there is a way to implement the [[Lambda and Lazy#Lazy|Lazy methodology]] such that it will only be computed when needed

```Java
class InfiniteList<T> {
	private final Producer<T> head;
	private final Producer<InfiniteList<T>> tail;

	public InfiniteList(Producer<T> head, Producer<InfiniteList<T>> tail) {
		this.head = head;
	    this.tail = tail;
	}
	
	public T head() {
		T h = this.head.produce();
		return h == null ? this.tail.produce().head() : h;  // If the head is null, get the next head
	}
	
	public InfiniteList<T> tail() {
		T h = this.head.produce();
		// If the head is null return the next tail
		return h == null ? this.tail.produce().tail() : this.tail.produce();  
	}
	
	public T get(int n) {
		if (n == 0) {
			return this.head();          // be careful!
		}                              //   use the methods
		return this.tail().get(n - 1); //   instead of fields
	}
	
	// Other Functions
}
```

Now instead of taking in a value, it will <span style='color:#f7b731'>take in a producer</span> which will compute the value when needed

### `generate` Function

```Java
public static <T> InfiniteList<T> generate(Producer<T> producer) {
	return new InfiniteList<T>(producer,
		() -> generate(producer));
}
```

The `generate` function will create a `InfiniteList` where the `head` will be a `producer` which will <span style='color:#f7b731'>produce the first value of the list</span>. The `tail` will be <span style='color:#f7b731'>a producer which will produce the next</span> `InfiniteList` (Block) with the current producer for `head`

However, this implementation it can be seen that the next `InfiniteList` for the `tail` is not yet produced until the `tail()` function is called. This is because `tail` <span style='color:#f7b731'>stores the producer of the next item and not the item itself</span>

### `iterate` Function

```Java
public static <T> InfiniteList<T> iterate(T init, Transformer<T, T> next) {
	return new InfiniteList<T>(() -> init,
		() -> iterate(next.transform(init), next));
}
```

Unlike the implementation in the [[#`iterate` Function|Eager List]] there is <span style='color:#20bf6b'>no need for a terminating condition</span> since the next iteration will be computed when it is needed to be evaluated.

### `map` Function

```Java
public <R> InfiniteList<R> map(Transformer<? super T, ? extends R> mapper) {
	return new InfiniteList<>(
		() -> mapper.transform(this.head()),
		() -> this.tail().map(mapper));
}
```

Similar to iterate, now the `tail` will store a producer where it will <span style='color:#f7b731'>call</span> `map` onto the `InfiniteList` that `tail` is pointed to <span style='color:#f7b731'>when it is needed</span>

### `filter` Function

```Java
public InfiniteList<T> filter(BooleanCondition<? super T> cond) {
	Producer<T> newHead = () -> cond.test(this.head()) ? this.head() : null;
    return new InfiniteList<>(newHead, () -> this.tail().filter(cond));
}
```

Unlike the `EgerList` implementation, the values are not computed yet and thus to denote that the value is been filtered off `head` will <span style='color:#f7b731'>return</span> `null` if it <span style='color:#f7b731'>does not meet the conditions of the filer</span>

# Streams
---
Streams are used like a <span style='color:#0fb9b1'>pipeline</span> which is a <span style='color:#f7b731'>single use object</span>.

Think of streams as a <mark class="hltr-orange">temporary for loop on a list</mark> which will be removed after its usage. The <span style='color:#f7b731'>data source, its a collection of values</span> and there are <span style='color:#f7b731'>operations which can be performed on these values</span>

Similar to `InfiniteList` a `Stream` is also lazy and will execute when a <span style='color:#0fb9b1'>terminating operation </span>is used

The<span style='color:#f7b731'> order of the operation matter</span>

It is <span style='color:#eb3b5a'>important that the stream does not get modified</span> (new items added) besides the usage of the `map` function

Examples of using streams
```Java
// Fnunction to determin if the value is prime or not
boolean isPrime(int x) {
  return IntStream.range(2, x)
      .noneMatch(i -> x % i == 0);
}

// Using the isPrime function to find the first 500 Prime numbers
IntStream.iterate(2, x -> x+1)
    .filter(x -> isPrime(x))
    .limit(500)
    .forEach(System.out::println);
```
## Creating the Data Source

They are also called <span style='color:#0fb9b1'>terminal operations</span>. They are operations that terminate and starts the evaluation of the stream.

```Java
// Using the .of function to manually decide the values in the stream
Stream.of(1, 2, 3).forEach(System.out::println);

// Using a loop to generate values in the stream
Stream.generate(() -> 1).forEach(System.out::println); // infinite loop which will cause an error
Stream.iterate(0, n -> n + 1).limit(10).forEach(x -> System.out.println(x)); // Will terminate at 10

// .forEach will print out every value inside the stream
```

## Intermediate Operations

There are some functions in `stream` class which <span style='color:#f7b731'>allows the manipulation of the elements </span>in the stream object which includes, `map`, `flatmap`, `filter`

```Java
Stream.of("hello\nworld", "ciao\nmondo", "Bonjour\nle monde", "Hai\ndunia")
    .map(x -> x.lines()) // returns a stream of streams

Stream.of("hello\nworld", "ciao\nmondo", "Bonjour\nle monde", "Hai\ndunia")
    .flatMap(x -> x.lines()) // return a stream of strings

Stream.of(1,2,3,4,5,6,7,8,9,10)
	.filter((x) -> x % 2 == 0) // Fiters all event numbers
```

### Stateful and Bounded Operations

Operators that are <span style='color:#0fb9b1'>stateful</span> means that the <span style='color:#f7b731'>stream must be finite</span>

Some examples of functions that are <span style='color:#0fb9b1'>stateful</span> are:
-  `sorted`
-  `distinct`

```Java
Stream.of(98,3,4,11,11,7,12,9,10)
	.sort() // Which can pass in a unique comparitor
	.distinct()
```


Operators that are <span style='color:#0fb9b1'>bounded</span> means that <span style='color:#f7b731'>a infinite list can be made finite</span>

Some examples of functions that are <span style='color:#0fb9b1'>bounded</span> are:
-  `limit`
-  `range`
-  `takeWhile`

```Java
Stream.iterate(0, n -> n + 1)
	.limit(10) // First 10 iterations

Stream.iterate(0, x -> x + 1)
	.takeWhile(x -> x < 5); // Takes all the values until the condition is not satisfied
```

### Peaking into a Stream

There is a way to check the next value in the stream without having to terminate the stream and that is through the `peak` function

```Java
Stream.iterate(0, x -> x + 1).peek(System.out::println).takeWhile(x -> x < 5).forEach(x -> {});

// Here 6 will be printed out but the ForEach will print until 5 (Meaning the stream will end at 5)
```

## Terminating Operations

There are some functions in `stream` class which <span style='color:#f7b731'>terminates the stream</span> in the stream object. In other words it <mark class="hltr-red">consumes the stream making it unusable anymore</mark>. There functions include which includes, `reduce`, `forEach` and element matching functions


For the `reduce` operation, it is also known as `fold` or `accumulate` which <span style='color:#f7b731'>repeatedly apply a lambda function onto all elements</span> in the stream and <span style='color:#f7b731'>combine them into one value</span>

```Java
Stream.of(1, 2, 3).reduce(0, (x, y) -> x + y); // Returns the sum of all values in the stream where 0 is the starting value (x)
```

For element matching there are 3 operations;
1)  `noneMatch` returns true if none of the elements pass the given predicate.
2)  `allMatch` returns true if every element passes the given predicate.
3)  `anyMatch` returns true if at least one element passes the given predicate.

---
title: Asynchronous Programming
Date Created: 2023-11-07
tags:
  - CS2023S
  - Concurrency
---
# Threads
---
As of now, most codes <span style='color:#f7b731'>run linearly</span>, meaning the program will wait for a method to complete its execution and only then will it continue 

One way to bypass this is using java Threads in the `java.lang.Thread`, which allows multi threading using Java's own threads

```Java
import java.lang.Thread
// Thread takes in a Runnable functional interface with a method run(), no input and returns void
new Thread(() -> {
  for (int i = 1; i < 100; i += 1) {
    System.out.print("_");
  }
}).start();

new Thread(() -> {
  for (int i = 2; i < 100; i += 1) {
    System.out.print("*");
  }
}).start(); // Only with start() function the tread to start running
```

These 2 threads now run on <span style='color:#f7b731'>2 separate sequence of execution</span>. Java also has an inbuild scheduler which decides which tread to run on which core. The <span style='color:#f7b731'>program exits after all threads finish executing</span>

One issue in parallel computing is <span style='color:#0fb9b1'>interleaving</span>, where the <span style='color:#f7b731'>output is unknown</span> as it is up to Java's scheduler to decide which thread to run first

There is a way to visualise how many threads are being used though the following
```Java
Stream.of(1, 2, 3, 4)
      .parallel()
      .reduce(0, (x, y) -> { 
        System.out.println(Thread.currentThread().getName()); // Print Java thread name
        return x + y; 
      });
```

Side note, there requires some <span style='color:#f7b731'>time to switch from one thread to another</span> this is called <span style='color:#0fb9b1'>context switching</span>
## Sleep

There is a way to <span style='color:#f7b731'>pause the current execution</span> of a thread is using `Thread::sleep` function. Only after the sleep timer is over, will the tread be ready to be chosen by the scheduler

```Java
while (findPrime.isAlive()) { // Check if another thread is still running
  try {
    Thread.sleep(1000);
    System.out.print(".");
  } catch (InterruptedException e) {
    System.out.print("interrupted");
  }
}
```

## Benefits

**Non-Blocking**
> For functions with long computation times, multi threading can help <span style='color:#f7b731'>speed up computation</span>

## Drawbacks

**Overheads**
> Sometimes functions that cannot be done in parallel might<span style='color:#f7b731'> increase the computation time</span>

**Some examples are :** 
1)  Starting a thread
2)  Scheduling a thread
3)  Context switching
4)  Parent must wait
5)  etc

**Exception Handling**
> There is <span style='color:#f7b731'>ambiguity</span> in where it should be handled, what <span style='color:#f7b731'>exceptions are thrown and how to handle</span> all possible cases, how to <span style='color:#f7b731'>differentiate exceptions from tasks and threads</span>

**Single Use**
> A thread <span style='color:#f7b731'>cannot be called again</span> once it is completed, besides creating a new thread again

**Information Sharing**
> Firstly, 2 or more threads <span style='color:#f7b731'>does not execute in sequence</span>, in addition there is <span style='color:#f7b731'>no return value</span> since it used a `Runnable` class

Even if, there is a shared output field;
1)  It is <span style='color:#f7b731'>effectively final</span> for primitive types
2)  For complex types it <span style='color:#f7b731'>might missed out some values</span> as a thread can stop before finishing executing, causing read data to remain as the old value (race condition) in the event another thread updates the data (Stateful operations) 
# Dependency Management
---
## Completable Future

In Java there is a `CompletableFuture` which acts like a <span style='color:#f7b731'>monadic function</span>. It allows the programmer to specify which <span style='color:#f7b731'>functions can be executed in parallel and which one cannot</span>

It encapsulates a value that is <span style='color:#f7b731'>either there or not there yet</span>

The functions in the `CompletableFuture` are;
1)  `completedFuture` or `supplyAsync` which is the `of` function
2)  `thenApplyAsync` which is the `map` function
3)  `thenComposeAsync` which is the `flatmap` function
4)  `thenCombine` which is the `combine` function

`ComparableFuture` <mark class="hltr-orange">cares about dependency and not concurrency</mark>. As it only matters when something is executed, all the prerequisites have been executed already

```Java
import java.util.concurrent.CompletableFuture
CompletableFuture<Integer> foo(int x) {
  CompletableFuture<Integer> a = CompletableFuture.completedFuture(taskA(x));
  CompletableFuture<Integer> b = a.thenComposeAsync(i -> taskB(i));
  CompletableFuture<Integer> c = a.thenComposeAsync(i -> taskC(i));
  CompletableFuture<Integer> d = a.thenComposeAsync(i -> taskD(i));
  CompletableFuture<Integer> e = b.thenCombineAsync(c, (i, j) -> taskE(i, j));
  return e;
}
```

### How to use it

**Creating a `CompletableFuture`**

1)  Use the `completedFuture` method. This method is equivalent to <span style='color:#f7b731'>creating a task that is already completed</span> and return us a value

2)  Use the `runAsync` method that takes in a `Runnable` lambda expression. `runAsync` has the return type of `CompletableFuture<Void>`. The returned `CompletableFuture` instance completes when the given lambda expression finishes

3)  Use the `supplyAsync` method that takes in a `Supplier<T>` lambda expression. `supplyAsync` has the return type of `CompletableFuture<T>`. The returned `CompletableFuture` instance completes when the given lambda expression finishes

There is also a `allOf` and `anyOf` which <span style='color:#f7b731'>completes only when all of the other</span> `CompletableFuture` given is completed

A creation of a `CompletableFuture` will immediately execute the lambda function

**Chaining a `CompletableFuture`**

There several methods that takes in `Runnable`. These methods have no analogy in our lab but it is similar to `runAsync` above.

1)  `thenRun` takes in a `Runnable`. It executes the `Runnable` after the current stage is completed
2)  `runAfterBoth` takes in another `CompletableFuture` and a `Runnable`. It executes the `Runnable` after the current stage completes and the input `CompletableFuture` are completed
3)  `runAfterEither` takes in another `CompletableFuture` and a `Runnable`. It executes the `Runnable` after the current stage completes or the input `CompletableFuture` are completed
<div style="page-break-after: always;"></div>
**Getting The Result**

1) The method `CompletableFuture::get` throws a <span style='color:#f7b731'>couple of checked exceptions</span>: `InterruptedException` and `ExecutionException`, which we need to catch and handle.
2)  The `CompletableFuture::join` is similar to `get` but it <span style='color:#eb3b5a'>does not handle exceptions</span>

**Non-Blocking**
> Functions like `theComposeAsync` and `thenCombineAsync` return immediately and the next line is executed

**Blocking**
> Functions like `join` will not execute the next line until this completes

However <span style='color:#0fb9b1'>blocking</span> operations can cause <span style='color:#eb3b5a'>deadlocks</span> where 2 threads depend on each other and thus the program will not continue
## Advantages

**Easy Multi-Threading**

If it is <span style='color:#f7b731'>possible to convert</span> a monad to a `CompletableFuture` then;
-  It is easy to perform multi-threading
-  No need to worry about order of operations and communication between threads
-  Focus only on logical order of operation and dependencies between values

## Properties

**Moadic**
> `CompletableFuture` is a **Monad**. If you know how to chain a monad, you hopefully know how to chain a `CompletableFuture`

**Super Interface**
> Some methods in `CompletableFuture` returns `CompletionStage`. `CompletionStage` is an interface implemented by `CompletableFuture`

**Overhead Reduction**
>We can reduce overhead of thread _creation_ using `ForkJoinPool` (to be discussed later). This is a form of **Thread Pool** (i.e., a collection of threads + a collection of tasks to be executed)

**Exception Handling**
> Can be done using `handle()` method
<div style="page-break-after: always;"></div>

# Fork and Join
---

The `ForkJoinPool` is a thread pool created by Java for <span style='color:#f7b731'>recursive parallel execution</span>. It uses the divide and conquer strategy, where it divides into <span style='color:#f7b731'>smaller identical problems and combine the results </span>

```Java
class Summer extends RecursiveTask<Integer> {
  private static final int FORK_THRESHOLD = 2;
  private int low;
  private int high;
  private int[] array;

  public Summer(int low, int high, int[] array) {
    this.low = low;
    this.high = high;
    this.array = array;
  }

  @Override
  protected Integer compute() {
    // stop splitting into subtask if array is already small.
    if (high - low < FORK_THRESHOLD) {
      int sum = 0;
      for (int i = low; i < high; i++) {
        sum += array[i];
      }
      return sum;
    }

    int middle = (low + high) / 2;
    Summer left = new Summer(low, middle, array);
    Summer right = new Summer(middle, high, array);
    left.fork(); // Divides the problem without blocking
    return right.compute() + left.join(); // Join combines the result, blocking the task but not necessary the thread
  }

// To run the task
Summer task = new Summer(0, array.length, array); 
int sum = task.compute();
}
```

```Java
left.fork();  // >-----------+
right.fork(); // >--------+  | should have
return right.join() // <--+  | no crossing
     + left.join(); // <-----+

left.fork();  // >-----------+
return right.compute() //    | compute in middle
     + left.join(); // <-----+
```

When coding note `join()` <mark class="hltr-orange">has to be in the reverse order</mark> of `fork()` which is called the palindromic order

Using `compute()` enables the combination of 1 `fork()` and `join()` operation in the middle
## How the Thread Pool Works

### The different Pools

There is a <span style='color:#0fb9b1'>global task queue</span> is a queue of task submitted from `fork()` by a thread that is not part of the pool
- New tasks are <span style='color:#f7b731'>inserted into the back of the queue</span>
- A thread from fork join pool may <span style='color:#f7b731'>retrieve a task from the front of the queue </span>into its <span style='color:#0fb9b1'>local task deque</span>.
- A join stack is also available to store tasks currently on hold (e.g., waiting other tasks to complete).

A <span style='color:#0fb9b1'>local task deque</span> is a <span style='color:#0fb9b1'>deque</span> (double-ended queue) of task to be executed by the thread in a fork join pool.
- On call to `fork()`, insert to the **front** of the deque (non-blocking)
- On call to `join()`, **find** the task to be executed (may need pop and push back)
- Task may be <mark class="hltr-orange">stolen from the back</mark> of the deque (Task Stealing)

A <span style='color:#0fb9b1'>ForkJoinPool</span> is a pool of threads for using `fork()` and `join()` such that
- `fork()` puts the _new_ task into the task deque (non-blocking)
- `join()` puts the _current_ task into the join stack (potentially blocking)
    - The worker thread try to find the joined task in its deque to run
### Steps

1)  Assume there are 2 threads in the pool with 0 tasks (Idle state)
2) When an external thread calls `fork()` the <span style='color:#0fb9b1'>global task queue</span> will have a task
3)  An idle thread checks its <span style='color:#0fb9b1'>deque</span> for tasks if it is empty it will <span style='color:#f7b731'>steal from the tail of the other thread</span> or it will get from the <span style='color:#0fb9b1'>global task queue</span> or it will get from its <span style='color:#0fb9b1'>duque</span>
4) Any new calls to `fork()` <span style='color:#f7b731'>inside the thread pool</span> will be added to the front of the <span style='color:#0fb9b1'>deque</span>
5) When `join()` is called if some <span style='color:#f7b731'>subtasks has not been executed</span> the `compute()` method will be called. If the subtasks is done, `join()` will return something. If the subtask has been stolen <span style='color:#f7b731'>it will find another task to do</span>
### Stealing From the Back

Stealing from the back <span style='color:#f7b731'>ensures a more balance workload</span> on a reasonable assumption.
- New tasks are inserted from the front
- Tasks are retrieved from the front
- Tasks at the back potentially create more tasks which is expensive

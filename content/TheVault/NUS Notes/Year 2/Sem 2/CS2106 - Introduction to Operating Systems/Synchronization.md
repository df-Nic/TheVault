---
title: Synchronization
Date Created: 2025-02-19
Last Updated: 2025-09-28
tags:
  - CS2106
  - Processes
  - Concurrency
---
# Race Conditions
---
Execution of concurrent processes may be <span style='color:var(--mk-color-yellow)'>non-deterministic</span>. The **order in which a shared resources is modified** determines the final result.

> [!failure] Problems with concurrent execution
> As long as **2 processes** executes in a <span style='color:var(--mk-color-yellow)'>interleaving fashion</span> (*time quantum causing a switch*) and <span style='color:var(--mk-color-yellow)'>shares some common resource</span>, it will cause <span style='color:var(--mk-color-red)'>synchronization problems</span>.
> 
> This is known as a <span style='color:var(--mk-color-turquoise)'>race condition</span>.

> [!example] Example of a race condition
> We have 2 processes that adds 10 to a variable `x = 0`. Process A loads from memory and adds 10 but **before it can write to memory, process B get preempted**.
> 
> Now B will add 10 but with `x = 0`! And it writes into memory. Now process A regains control and also write `x = 10` into memory (*overriding*) and thus the final value is 10.
# Critical Sections
---
The <span style='color:var(--mk-color-green)'>solution to have critical sections</span>, which **handles the unfavourable access or modification** to a shared resource.

> [!question] Where are the critical sections?
> As long as there is a <b><mark style='background:var(--mk-color-yellow)'>section of code that modifies a shared resource</mark></b>, it is a critical section.

Before we enter the critical section we will need to invoke a `EmterCS` and `ExitCS` function.

The idea is to **block** (*hold*) any process who enters this critical section <span style='color:var(--mk-color-yellow)'>until the currently executing process is done</span> (*mutual exclusion)* or there is <span style='color:var(--mk-color-yellow)'>no process at all</span> in CS (*progress*).

> [!note] Things to considering when handling CS
>  Besides the behavior above:
> - **Independence**: Process **not executing in critical section** should <span style='color:var(--mk-color-yellow)'>never block other processes</span>
> - **Bounded wait**: After a **process requests to enter critical section**, there should be an <span style='color:var(--mk-color-yellow)'>upper bound number of other processes that enters critical section</span> before this proves (*no fnifnite waiting time*).

> [!warning] Issues arising from incorrect synchronization
> - **Deadlocks**: It is when <span style='color:var(--mk-color-red)'>all processes are blocked</span> and therefore there is no progress, happens when <span style='color:var(--mk-color-yellow)'>2 processes access the same resource and they block each other</span>. The <span style='color:var(--mk-color-green)'>OS can detect deadlocks</span>.
> - **Livelock**: To **avoid a deadlock a process will switch to another resource**, but if <span style='color:var(--mk-color-yellow)'>2 processes switch to the same resource blocking again</span> and the process repeats, continuously blocking. The <span style='color:var(--mk-color-red)'>OS cannot detect livelocks</span> as they are not blocks but rather doing nothing.
> - **Starvation**: Where the <span style='color:var(--mk-color-yellow)'>process is blocked forever</span> and can never enter the the critical section.

The <span style='color:var(--mk-color-orange)'>properties of a correct CS implementation</span> are:
1) **Mutual exclusion**: If a process is in the CS then no other process can enter until it is done
2) **Progress**: If no one is in the CS then any process waiting should be granted
3) **Bounded wait**: When a process requests to enter CS, there should be an upper bound on the number of processes who can enter CS before this process (*no starvation*)
4) **Independence**: Process not executing in CS should never block other processes
## CS Implementations

### Assembly Level

Here we use <span style='color:var(--mk-color-yellow)'>mechanisms provided by the processes</span>. One common mechanisms is <span style='color:var(--mk-color-turquoise)'>Test And Set</span>. It takes in 2 parameters, a `Register` & a `MemoryLocation`.

However test and set is **implemented in the hardware** and it not known for programmers.

**What it does** it:
1) <span style='color:var(--mk-color-yellow)'>Loads the current content</span> from memory into the register (*returns what's inside the address*)
2) <span style='color:var(--mk-color-yellow)'>Stores a 1</span> in the memory location.

This process of loading and writing is **atomic**, meaning it <b><mark style='background:var(--mk-color-yellow)'>cannot be interrupted</mark></b>.

> [!example] Example of using `TestAndSet`
> ```C
> // Enter CS function
> void EnterCS( int* MemoryLocation) {
> 	// Block as long as someone is  in the CS
> 	while(TestAndSet(MemoryLocation) == 1); // We know TestAndSet will write a 1 to the memory location
> }
> 
> // Exit CS function
> void ExitCS( int* MemoryLocation) {
> 	*MemoryLocation = 0; // This is atomic also
> }
> ```
> > [!fail] Issues of this implementation
> > During the time quantum, the process will be **stuck in the while loop** (*busy waiting*) and <span style='color:var(--mk-color-red)'>not doing anything</span>, thus it is <span style='color:var(--mk-color-red)'>expensive</span> (*wasting CPU power*).

There are <span style='color:var(--mk-color-orange)'>other variants</span> of this:
- **Compare & exchange**
- **Atomic swap** (*used by intel, whatever is on memory will be in register and vice versa*)
- **Load link / Store conditional**
### High Level Language

Here we make <span style='color:var(--mk-color-yellow)'>use of normal programing constructs</span> (*while loops, arrays, etc.*).

Our first thought is to have a shared variable `lock` and check if `lock == 1` and do a while loop to wait before entering CS, but here there is a huge problem as `lock` **itself is shared** and <span style='color:var(--mk-color-red)'>thus prone to raised conditions</span>.

> [!question] How can this happen?
> It is possible where before setting `lock = 1`, the control is handed over and the other process bypasses the `while` loop cause both processes to be in the CS

There are some ways to work around this:
1) **Disable interrupts** before entering CS (*not recommend as no mutual exclusion*)
> This works cause by <span style='color:var(--mk-color-yellow)'>disabling interrupts there is no interleaving</span>, **but**, if we <b><mark style='background:var(--mk-color-red)'>have multiple CPU's it will not work</mark></b> as <span style='color:var(--mk-color-yellow)'>both can check lock at the same time</span> which cause a race condition. It is also bad cause if the <span style='color:var(--mk-color-red)'>process crashes before we reenable interupts it will remain disabled caused problems with I/O</span>.

2) **Denote who gets to enter the CS** (*does not progress*)
> Instead of blocking, we can <span style='color:var(--mk-color-yellow)'>denote which processes to enter CS</span>, **but** if it crashes, then the <span style='color:var(--mk-color-red)'>other processes will never get to run</span>, since `turn` will never get updated.

3) **Using an array** (*causes deadlocks*)
> Process 0 will set `want[0] = 1` when it wants to enter CS then it checks if `want[1] = 1` before entering. Same goes for process 1 but the opposite, set `want[1]` and checks `want[0]`. This however <span style='color:var(--mk-color-red)'>may causes deadlocks</span>, if we set `wait[0]` to 1 and then process swaps and now `wait[1]` is set to 1, then <span style='color:var(--mk-color-yellow)'>no one can exit the while loop</span>.
#### Peterson's Algorithm

![[Peterson's Algorithm.png|center|500]]

> The assigning of `Turn` <b><mark style='background:var(--mk-color-yellow)'>must be atomic</mark></b>.

This <span style='color:var(--mk-color-green)'>solves the issue of deadlocks</span> and it works

> [!failure] Disadvantages
> - **Busy waiting**: We are still <span style='color:var(--mk-color-yellow)'>using a while loop</span> instead of blocking the process
> - **Low level**: We are <span style='color:var(--mk-color-yellow)'>manipulating variables to do synchronisation</span>, this can lead to bugs and errors
> - **Not general**: <span style='color:var(--mk-color-yellow)'>Not easy to extend to more than 2 processes</span>
### High Level Abstractions

We <span style='color:var(--mk-color-yellow)'>implement using assembly level mechanisms</span>, but we <span style='color:var(--mk-color-yellow)'>provide a abstract mechanism</span> which provides additonal features for usability.

> [!note] Programing languages that has these synchronization mechanisms
> - <span style='color:var(--mk-color-blue)'>Java objects</span> has a built in lock (*mutex*) and synchronized method access
> - <span style='color:var(--mk-color-purple)'>Python</span> supports mutex, semaphores and conditional variables
> - <span style='color:var(--mk-color-purple)'>C++</span>, as of version 11 it supports mutex and conditional variables
#### Semaphores

A commonly known generalized synchronization mechanism is a <span style='color:var(--mk-color-turquoise)'>semaphore</span> also known as a <span style='color:var(--mk-color-turquoise)'>mutex</span> if set to 1 (*mutual exclusion*) and it has **2 main functions**:
1) `Proberen` (*in English it is decrease*) or `p` or `wait()` or `down`
2) `Verhogen` (*in English it is increase*) or `v` or `signal()` or `up`

> [!note] Only the behavior is defined
> How they are implemented is up to the developers like using other mechanisms like `sleep` or busy waiting

It requires a header file, `#include <semaphore.h>` and when compiling do `gcc file_name.c - lrt`. And it is usually **used in the context of threads**.

> [!question] Why not processes?
> Semaphores will be shared, thus if we `fork()` a process we will also <span style='color:var(--mk-color-yellow)'>duplicate the semaphore</span>.
> 
> **If you want** we can just <span style='color:var(--mk-color-yellow)'>create it in shared memory</span>.

A semaphore provides us with a way to:
- **Block** a number of processes (*these are known as <span style='color:var(--mk-color-turquoise)'>sleeping processes</span>*)
- **Unblock / wake up** one or more processes
- Can be used to sync with other processes, known as **barriers**

> [!note] Types of semaphore
> There are **2 types of semaphores**:
> 1) **General semaphore**: Where `S` can be <span style='color:var(--mk-color-yellow)'>any non-negative number</span> subjected to `MAXINT` (*counting semaphores*)
> 2) **Binary semaphore**: Where `S` can be only <span style='color:var(--mk-color-yellow)'>0 or 1</span>
##### Semaphore Functions

A semaphore it is a **integer value** (*unsigned for now*), but it is a **protected one**, meaning the <span style='color:var(--mk-color-yellow)'>operations on it are atomic</span>. It can be <span style='color:var(--mk-color-yellow)'>initialized to any non-negative value</span>.

![[Semaphore Example.png|center]]

The general idea is that is the value is <span style='color:var(--mk-color-yellow)'>greater than 0 it will decrease</span> this value, but if it is <span style='color:var(--mk-color-yellow)'>0 it wi ll block the process</span> and adds it to the list (*this list is FCFS basis*).

> [!info] `Wait (s)`
> If `s` is **smaller than or equals to 0**, the <span style='color:var(--mk-color-yellow)'>process goes to sleep</span>, **else**, <span style='color:var(--mk-color-yellow)'>decrease</span> `s` <span style='color:var(--mk-color-yellow)'>by 1</span>.

> [!info] `Signal(s)`
> It takes up one sleeping process if any and the <b><mark style='background:var(--mk-color-yellow)'>process never blocks</mark></b>.
> 
> it also <span style='color:var(--mk-color-yellow)'>increments</span> `s` by 1, but **only if there is no sleeping process** (*this is if we do not allow our semaphore to go negative*).

Thus when a process enters CS, it will call `wait(s)` decreasing the value by 1. If **another processes enters it will be put into the waiting list**. Once the process exits CS it will call `signal(s)` which will **bring a process out from the waiting list or increment by 1 if its empty**.
##### Properties of a Semaphore

We know that the **initial value of a semaphore is greater than or equals to 0**. Thus at any given point in time:
$$
S_{\text{current}} = S_{\text{initial}} + \text{number of signal calls} - \text{number of wait calls completed} 
$$
> [!abstract] Proving mutual exclusion for a semaphore
> Let $N_{CS}$ be the number of processes in the critical section. And it is defined by the number of processes who called `wait(s)` but not `signal(s)`
> $$
>  N_{CS} = \text{number of wait calls completed}  - \text{number of signal calls}
> $$
> 
> Thus $S_{current} + N_{CS} = 1$ and since $S_{current} \ge 0$, then that means our $N_{CS}$ **can only be 0 or 1**.
##### Possible Issues with Semaphores?

It is both <span style='color:var(--mk-color-green)'>deadlock* and starvation free</span>.

From the proof above $S_{current} + N_{CS} = 1$. If $S_{current} = 0$ and $N_{CS} = 0$, then <span style='color:var(--mk-color-red)'>we will have a contradiction</span>, thus it cannot happen.

> [!bug] Special case where a deadlock can occur for semaphores
> It happens when there are <span style='color:var(--mk-color-yellow)'>2 non-sharable processes in a non-cyclic fashion</span>.
> 
> ![[Special Case where a Semaphore Cause a Deadlock.png|center]]
> 
> Essentially, when `P1` calls `wait(P)` and then `P2` calls `wait(Q)`. Then when `P1` continues it will get blocked and same goes for `P2`.
> 
> This however is **quite specific** and will <span style='color:var(--mk-color-green)'>not even happen if the processes acquires the resource in the same order.</span> (*ie P first then Q for both or the other way round*) .

It is also starvation free as long as the <b><mark style='background:var(--mk-color-yellow)'>scheduling algorithm decision on who gets waken up if fair</mark></b>.
#### Other Abstractions

As of now, a semaphore is **very powerful** and there are <span style='color:var(--mk-color-green)'>no known unsolvable synchronization problem with it</span>.

However, there are <span style='color:var(--mk-color-orange)'>other high level abstractions which provide extended features</span>, such as <span style='color:var(--mk-color-turquoise)'>conditional variables</span>. It is similar to semaphores where it is initialised with a value of 0 and <span style='color:var(--mk-color-yellow)'>allows tasks to wait on it</span>.

Unlike semaphores, it can **broadcast** to all sleeping processes, meaning it can <span style='color:var(--mk-color-yellow)'>wake up all sleeping processes</span> unlike <span style='color:var(--mk-color-red)'>semaphores which can do one at a time</span>.

> [!question] Why would you want to broadcast?
> Lets say we have a bunch of processes waiting on the output of another process. With broadcasting, it <span style='color:var(--mk-color-green)'>can just signal to everyone</span> when its done.

#### `pthreads` Mutex & Conditional Variables

[[Threads#POSIX Threads|pthreads]]also allows us to use mutexes and conditional variables.

For **mutex**, the data type will be `pthread_mutex`, <b><span style='color:var(--mk-color-yellow)'>this is only a binary semaphore</span></b> and it has the following functions:
- **Lock**: `pthread_mutex_lock()`
- **Unlock**: `pthread_mutex_unlock()`

For **conditional variables** the data type will be `pthread_cond` and it has the following functions:
- **Wait**: `pthread_cond_wait()`
- **Signal**: `pthread_cond_singal()` (*wake up 1 process*)
- **Broadcast**: `pthread_cond_broadcast()`

> For conditional variables, we <span style='color:var(--mk-color-yellow)'>need to use it with mutexes</span>. As when we use `wait` we need to supply with a mutex.
# Classical Synchronization Problems
---
## Produce Consumer Problem

We have a <b><span style='color:var(--mk-color-turquoise)'>producer</span></b>, which <b><span style='color:var(--mk-color-yellow)'>produces</span></b> items and <b><span style='color:var(--mk-color-yellow)'>inserts</span></b> it into the buffer only when it is <b><span style='color:var(--mk-color-yellow)'>not full</span></b>.

We also have a <b><span style='color:var(--mk-color-turquoise)'>consumer</span></b>, which <b><span style='color:var(--mk-color-yellow)'>consumes</span></b> and <b><span style='color:var(--mk-color-yellow)'>remove</span></b> items from the buffer only when it is <b><span style='color:var(--mk-color-yellow)'>not empty</span></b>.

The problem we have here is that we will be <b><span style='color:var(--mk-color-red)'>using some shared variables</span></b> like `count` which stores the number of items in the buffer.

In addition, the <b><span style='color:var(--mk-color-red)'>producer and the consumer should wait if the buffer is full or empty</span></b> respectively. Since we will lose the item that was produced and the consumer will consume nothing. 
### Busy Waiting Solution

We can use <b><span style='color:var(--mk-color-yellow)'>1 mutex and more shared variables</span></b>.

On start up we set `canProduce` to be true since the buffer is empty. For `canConsumer` it will be false because the buffer is empty.

**Producer**
```C
while (TRUE) {
	//Produce Item;
	while(!canProduce); // If buffer is not full produce something
	wait( mutex ); // Claim the semaphore and enter CS
	if (count < K) {
		buffer[in] = item;
		in = (in+1) % K; 
		count++; // This is a shared variables
		canConsume = TRUE; // Can consume is set to true because something is in the buffer
	} else {
		canProduce = FALSE; // Buffer is full
	}
	signal( mutex );
}
```

**Consumer**
```C
while (TRUE) {
	while (!canConsume); // Buffer is not empty
	wait( mutex );
	if (count > 0) {
		item = buffer[out];
		out = (out+1) % K;
		count--; // Shared variable
		canProduce = TRUE; // Since we consume the buffer is guarantee not full
	} else {
		canConsume = FALSE; // If the buffer is empty then we cannot consume anymore
	}
	signal( mutex );
	
	// Consume Item;
}
```
### Blocking Version

Here we use <span style='color:var(--mk-color-orange)'>3 semaphores</span>:
1) `mutex` this is for the **shared variables or CS**, this is set to 1
2) `notFull`, which is a counting semaphore to **denote the number of empty spaces** in the buffer. This is set to $K$ where $K$ is the size of the buffer
3) `notEmpty`, which is to **denote the number of items** in the buffer. This is initially set to 0

**Producer**
```C
while (TRUE) {
	// Produce Item;
	wait( notFull ); // Reduce the number of free space by 1
	wait( mutex ); // Claim semaphore
	buffer[in] = item;
	in = (in+1) % K;
	count++;
	signal( mutex ); // Release semaphore
	signal( notEmpty ); // Increase notEmpty by 1 since there is an item inside
}
```

**Consumer**
```C
while (TRUE) {
	wait( notEmpty ); // Reduce the numbe of items by 1
	wait( mutex ); // Claim semaphore
	item = buffer[out];
	out = (out+1) % K;
	count--;
	signal( mutex ); // Release semaphore
	signal( notFull ); // Incase the number of free space by 1
	// Consume Item;
}
```
## Readers & Writers Problem

We have a **shared data structure**, we have <b><span style='color:var(--mk-color-turquoise)'>readers</span></b> which can <b><span style='color:var(--mk-color-yellow)'>read together</span></b>. We also have <b><span style='color:var(--mk-color-turquoise)'>writers</span></b> which <b><span style='color:var(--mk-color-yellow)'>should write alone</span></b>.

Another restriction is that when the <b><span style='color:var(--mk-color-yellow)'>writer is writing, the reader cannot read</span></b> also.
### Simple Solution

We will use <span style='color:var(--mk-color-orange)'>2 mutexs and 1 shared variable</span>:
1) `roomEmpty`, which is initialised to 1 will be to **allow either writers or readers** to the data structure
2) `mutex`, to **protect the shared variable** and is initialised to 1
3) `nReader` which is initialised to 0 is a **shared variable** to keep **track of the number of readers**

**Writers**
```C
while (TRUE) {
	wait( roomEmpty ); // Only 1 writter can enter
	// Modifies data
	signal( roomEmpty );
}
```

**Readers**
```C
while (TRUE) {
	wait( mutex ); // Since we are accessing the shared variable
	nReader++;
	if (nReader == 1)
		wait( roomEmpty ); // Block if the writter is writting
	signal( mutex );
	// Reads data
	wait( mutex );
	nReader--;
	if (nReader == 0) // No more readers
		signal( roomEmpty ); // If we did read the data then we only set the value to 1 when all the readers are done
	signal( mutex );
}
```

> [!failure] This solution will cause starvation for writers if the readers keep coming
## Dining Philosophers

The context is that there are 5 philosophers seated around a table. Between **each pair of philosophers there is a chopstick**. When the philosophers **want to eat they will pick up the left and right chopstick**.

![[Dining Philosophers Problem Visualisation.png|center]]

Our goal is to devise a <b><span style='color:var(--mk-color-green)'>deadlock-free</span></b> and <b><span style='color:var(--mk-color-green)'>starve-free</span></b> solution to allow the philosopher to eat freely.

This <b><span style='color:var(--mk-color-yellow)'>chopsticks can be modeled as a mutex</span></b>.
### Bad Solution

```C
#define N 5
#define LEFT i
#define RIGHT ((i + N - 1) % N)

// For philosopher i
while (TRUE){
	Think( );
	//hungry, need food!
	takeChpStk( LEFT ); // This is our wait function
	takeChpStk( RIGHT ); // This is out wait function
	Eat( );
	putChpStk( LEFT ); // This is our signal function
	putChpStk( RIGHT ); // This is our signal function
}
```

> [!failure] This causes deadlocks
> For each of the philosophers they can **acquire the left chopstick first before switching** to another philosopher.
> 
> Thus <b><span style='color:var(--mk-color-red)'>everyone will be blocked when picking up the right chopstick</span></b>.

So why not just <b><span style='color:var(--mk-color-yellow)'>put down the left chopstick if the right one is being used</span></b> and try again later. Then this will <b><span style='color:var(--mk-color-red)'>lead to a livelock</span></b> instead (*pick up, put down, pick up, ...*). 
### Naive Solution

A naive solution is to <b><span style='color:var(--mk-color-yellow)'>use a mutex to block anyone picking up chopsticks</span></b>.

```C
#define N 5
#define LEFT i
#define RIGHT ((i + N - 1) % N)

// For philosopher i
while (TRUE){
	Think( );
	wait(mutex);
	//hungry, need food!
	takeChpStk( LEFT ); // This is our wait function
	takeChpStk( RIGHT ); // This is out wait function
	Eat( );
	putChpStk( LEFT ); // This is our signal function
	putChpStk( RIGHT ); // This is our signal function
	signal(mutex);
}
```

> [!warning] This solution works but only one philosopher can eat at any time
### Tanenbaum Solution

We will use an **array of mutex** of size $N$ all **initialised to 0**, **1 mutex** and **1 more shared variable an array** of size $N$ to indicate the state of $N$ philosophers.

When the philosopher wants to **eat** it will call a function called `takeChopSticks()` which takes in an integer to denote which philosopher it is.

Once he is **done eating** it will call a function called `putChopSticks()` which also takes in an integer to denote which philosopher it is.

**Take chopsticks function**
```C
void takeChpStcks( int i ) {
	wait( mutex ); // Since we are accessing a shared variable state
	state[i] = HUNGRY; // Denote that the philosopher is hungry
	safeToEat( i ); // We will check the left and right philosopher if they are eating or not
	signal( mutex );
	wait( s[i] ); // Here we will wait if it is not safe to eat since the ith semaphore is 0 initially
}
```

**Safe to eat function**
```C
void safeToEat( int i ) {
	// We need to check if itself is hungry and the neighbours are not eating currently
	if( (state[i] == HUNGRY) && (state[LEFT] != EATING) && (state[RIGHT] != EATING) ) {
		// If we reach here means the left and right copsticks are not used beaucse the neighbours are not eating
		// We do noe need use a mutex here cause called will be blocking the process
		state[ i ] = EATING; // Just set the state to eating
		signal( s[i] ); // Set the ith semaphore to 1 to allow the takeChpStcks function to exit
}
```

**Put chopsticks function**
```C
void putChpStcks( int i ) {
	wait( mutex ); // Since we are accessing a shared variable state
	state[i] = THINKING; // Change the state back to thinking
	
	// Here we just signal the left and right philosopher that ONE chopstick is free
	// Currently they may be blocked by the wait() in the takeChpStcks function
	// Thus we will ask them to check the left and right again
	safeToEat( LEFT ); // Signal the left person that it is safe to eat
	safeToEat( RIGHT ); // Signal the right person that it is safe to eat
	
	signal( mutex );
}
```
### Limited Eaters

If we were to **limit the number of people** on the dining table to be $N-1$ then we will <b><mark style='background:var(--mk-color-green)'>never encounter deadlocks</mark></b>.

> [!question] Why does deadlocks not occur?
> This is because if we have at least 1 empty space, then <b><span style='color:var(--mk-color-yellow)'>by pigeon hole principle we will have 1 extra chopstick</span></b>.
> 
> If $N = 5$, then we will have 5 chopsticks between them if we limit to $N-1$ then we will have 1 person which can have 2 chopsticks.

To implement this we just **use a counting semaphore** to denote the number of seats available. We will initialise this semaphore to have a value of $N-1$.

In addition similar to the [[Synchronization#Bad Solution|bad solution]] **each chopstick is a mutex**.

```C
void philosopher( int i ){
	while (TRUE){
		Think( );
		wait( seats ); // Take a seat
		wait( chpStk[LEFT] ); // Pick the left chopstick
		wait( chpStk[RIGHT] ); // Pick the right chopstick
		Eat( );
		signal( chpStk[LEFT] ); // Put down the left chopstick
		signal( chpStk[RIGHT] ); // Put down the right chopstick
		signal( seats ); // Free up a seat
	}
}
```


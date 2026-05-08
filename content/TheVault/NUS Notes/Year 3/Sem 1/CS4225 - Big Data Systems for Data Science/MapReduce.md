---
Title: MapReduce
Date Created: 28-November-2025
Last Updated: 18-March-2026
Tags:
  - CS4225
  - BigData/MapReduce
---
# Motivation
---
With data centers containing terabytes worth of data, we need an efficient way of using it.

An efficient solution is <b><span style='color:var(--mk-color-yellow)'>parallelization</span></b> & [[Divide & Conquer|divide and conquer]].

>[!question] Some things to consider when doing divide & conquer and parallelization
>- How to assign jobs/tasks?
>- What if we have more jobs than workers?
>- What if workers need to share partial results?
>- How to aggregate partial results?
>- How to know if all workers are done?
>- What if a worker fails/die?
## Challenges

1) **Machine failures**
**Hardware** will <b><span style='color:var(--mk-color-red)'>indivertibly fail</span></b>. Thus there needs to be a system in place to handle machine failure.

>[!example] How serious this is
>
>One server roughly stays up for 10 years. Thus if you have 3650 server expect to lose 1 per day
>
>Bigger companies are worse off, Google has 2.5 million (*estimation*) servers in 2016, thus 700 failures a day.

2) **Synchronization**
When enabling parallelization, we will encounter <b><span style='color:var(--mk-color-red)'>synchronization issues</span></b>:
- Indeterministic order in which workers run
- Will workers interrupt one another (*block*)
- Communicate results with other workers

We need to have control mechanisms such as [[Synchronization#Semaphores|barriers]].

>[!question] What is a barrier?
>
>A barrier is a synchronization technique where it <b><span style='color:var(--mk-color-yellow)'>forces workers to wait for every other worker</span></b> before continuing.

3) **Programming Difficulty**
It is <b><span style='color:var(--mk-color-red)'>difficult to implement concurrency</span></b>:
- Hard to debug
- Scale of datacenters
- Interacting services

This **results in one-off solutions** (*custom code*) and it <b><span style='color:var(--mk-color-red)'>adds burden</span></b> on the programmer to manage.

>[!success] See the datacenter as a computer
>
>We should design the <b><span style='color:var(--mk-color-yellow)'>right level of abstraction</span></b> such that the unnecessary system-level details can be ignored.
>
>Users just need to specify what needs to be done (*through an API*) & the framework will handle the execution.
# Basic MapReduce
---
A typical problem will have the following processing flow:
1) Iterate over large number of records
2) Extract something of interest from each record
3) Shuffle & sort intermediate results
4) Aggregate intermediate results
5) Generate final output

**Map, shuffle, reduce** are the <b><span style='color:var(--mk-color-yellow)'>core pipeline events</span></b> (*steps 2-4*) for a MapReduce model.

We only need to **provide functional abstraction for** `map` and `reduce`, `shuffle` will be handled by a framework like Hadoop.

>[!abstract] Map
>
>It essentially uses a **user defined function** to <b><span style='color:var(--mk-color-yellow)'>map input data into a list of key value pairs</span></b>.
>
>A record is <b><span style='color:var(--mk-color-yellow)'>processed in splits</span></b> (*default is 128 MB*), this is also known as a <b><span style='color:var(--mk-color-turquoise)'>map task</span></b>.

>[!abstract] Shuffle
>
>It is done by the framework, but the <b><span style='color:var(--mk-color-yellow)'>data is partitioned and sorted by key</span></b>.
>
>Partitions are usually done based on the key.

>[!abstract] Reduce
>
>It <b><span style='color:var(--mk-color-yellow)'>aggregates the partitions</span></b> from a list of values of a particular key(s) to a list of key value pairs .
>
>The reduce function will be <b><span style='color:var(--mk-color-yellow)'>called once for every unique key</span></b>.

We can optimise the pipeline by introducing **partition & combining** functions to <b><span style='color:var(--mk-color-green)'>help reduce network traffic</span></b>.
## Partition

Users can use a **custom partition function** to help spread out the load more evenly assuming that some <b><span style='color:var(--mk-color-yellow)'>keys have much more values than other</span></b>.

However by **default** how the partitioning works is that given a key:
- It will be [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Hashing|hashed]] using a hash function
- Then we will take the mod (`%`) of the has value by the number of reducers available
<div style="page-break-after: always;"></div>

## Combiner

>[!failure] After mapping, disk writes & sending data through the network can be slow depending on the number of keys & values

We can think of combiners as **another reducer** but is done during the <b><span style='color:var(--mk-color-yellow)'>mapping stage of the pipeline</span></b>, aggregating the values of similar keys into 1 value.

>[!important] The combiner may or may not run it depends on the framework to decide
>So it must have the <b><span style='color: var(--mk-color-yellow)'>same output key-value type of the mapper and input of the reducer</span></b>.
>
>How it works is that the <b><span style='color: var(--mk-color-yellow)'>mapper has a buffer to store the intermediary results</span></b> before sending it to the local disk. Thus the combiner works on this buffer when called.

>[!important] It is the user's responsibility that the combiner does not affect the correctness of the final output
>
>The combiner can <b><span style='color:var(--mk-color-yellow)'>run multiple times</span></b> not just once.
>
>For instance lets say our combiner is the `sum` function by key.
>
>It will work for `min` and `max` queries since at the last reduce we will sum everything together. It does not matter if we add now or later the result will be the same.
>
>However it will not work for mean as, `mean(sum(1, 1), 2)` is different from `mean(1, 1, 2)`.

>[!success] Correct use of reducers as combiners
>
>Only use it if the reduction involves a <b><span style='color:var(--mk-color-yellow)'>binary operation</span></b> that is both <b><span style='color:var(--mk-color-yellow)'>[[Speaking Mathematically#Terms|associative]]</span></b> and <b><span style='color:var(--mk-color-yellow)'>[[Speaking Mathematically#Terms|commutative]]</span></b>.
# Additional Concepts of MapReduce
---
## Secondary Sort

Before the **reducing stage**, the keys arrive sorted but we can also <b><span style='color:var(--mk-color-yellow)'>sort the values</span></b>.

>[!success] This makes it more convenient to compute certain statistics or handling timestamp data
>Computing median it is faster if it was to be sorted.

>[!note] Natural Key
>
>It is the <b><span style='color:var(--mk-color-yellow)'>original key in the composite key</span></b>.
>
>The rest of the original values in the original key value pairs are called <b><span style='color: var(--mk-color-turquoise)'>natural values</span></b>.
>
>Remember this composite key will consist of the old original key and the new values to make this new key.

We will take our key-value pairing and turn it into a **composite key** (*not the map emits this composite key*). We also need a **custom comparator** to sort by key first then value.

>[!question] Is this enough, what is wrong?
>
>When we set our key to be a **composite key** then our <b><span style='color:var(--mk-color-yellow)'>assignment to the reducer will change</span></b> since it is hashed with the composite key.
>
>Therefore we will also **need a custom partitioner** to get the desired allocation.

>[!failure] We should not do secondary sort during the reducing stage
>
>It is like borrowing the **inbuilt distributed sorting process** of Hadoop to sort for us.
>
>In addition, it has to <b><span style='color:var(--mk-color-red)'>use more memory & is costly</span></b> to buffer all values for a given key before sorting.
## Preserving State

Remember that our map and reduce functions can be called multiple times and each function call is independent.

We can initialise a state variable (*through a class*) to <b><span style='color:var(--mk-color-yellow)'>store spilt results from mappers</span></b>.

This is also known as a <b><span style='color:var(--mk-color-turquoise)'>in-mapper combiner</span></b>.

>[!tldr] You can think of this state variable as a combiner with a barrier where it stores all the mappers results then emits everything is done
>It either emits using a `for` loop **after each key-value pair** or we can have a `cleanup` function which does the **emitting after 1 split**.

>[!success] With state variables you can have more complex aggregations

>[!success] Reduce data sent over the network

>[!fail] The cost is that it increases the memory working set
# Performance Guidelines for Scalability
---
## Linear Scalability

It essentially means that as the amount of work increases it should scale with the computing resources available.

When we increase the data size we should also increase the computing resources with a <b><span style='color:var(--mk-color-yellow)'>1:1 ratio</span></b>.

On the same topic, we also need to ensure that the <b><span style='color:var(--mk-color-yellow)'>work load is well balanced</span></b> across all mappers & reducers. If we **don't** then we will encounter <b><span style='color:var(--mk-color-red)'>bottlenecks</span></b>.
## Minimise Disk & Network I/O

As mentioned previously <b><span style='color:var(--mk-color-red)'>disk reads or writes are slow</span></b>. But sending data over the <b><span style='color:var(--mk-color-red)'>network is also costly due to limited bandwidth</span></b> and the <b><span style='color: var(--mk-color-red)'>memory used is the total size of all the mappers outputs</span></b>.

>[!note] Tasks on the disk dominates the MapReduce jobs

A key observation is that during the shuffle phase, the disk & network I/O is roughly the same.

Thus, [[MapReduce#Combiner|combiners]] are a good way of **reducing** the disk reads and network data transfers.

>[!success] It is more efficient to do sequential reads & writes to the disk

>[!success] It is more efficient to send data over the network in bulk
>
>There is some overhead when sending small chunks over the network.
## Reduce Memory Working Set

>[!info] Working Set
>
>It is the portion of <b><span style='color:var(--mk-color-yellow)'>memory that is actively used by the program</span></b>.

We want to <b><span style='color:var(--mk-color-green)'>minimise the memory needed</span></b> for a job to execute.

A **large working set** means high memory requirements but also an <b><span style='color:var(--mk-color-red)'>increase probability of out-of-memory errors</span></b>.

Using [[MapReduce#Preserving State|state variables]] can also <b><span style='color:var(--mk-color-red)'>add to the memory usage</span></b>, if it is required for the mapper and reducer to keep track of some internal data structure.

>[!info] Reducers does not have to store a list of values in memory!
>
>Reducers usually access it via an **iterator** which **only stores the current value** in memory and does a "lazy evaluation" to get the next value. This <b><span style='color:var(--mk-color-green)'>saves memory</span></b> as compared to loading the whole list.


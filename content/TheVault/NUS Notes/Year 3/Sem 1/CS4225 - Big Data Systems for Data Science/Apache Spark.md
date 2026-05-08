---
title: Apache Spark
Date Created: 2025-10-10
Last Updated: 2025-10-15
tags:
  - CS4225
  - ApacheSpark
---
# Introduction To Spark
---
Recall that in [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Hadoop.md#Hadoop Implementation of MapReduce|Hadoop]] a query is broken down into smaller tasks, execute a map reduce and it reads and writes data into the HDFS.

Here we can see a couple of issues with Hadoop, which is it incurs <b><span style='color: var(--mk-color-red)'>network & disk I/O cost which makes it slow</span></b>. And because of this it is <b><span style='color: var(--mk-color-red)'>not sutible for iterative processing</span></b>.

>[!info] Iterative processes
>It is a process where it <b><span style='color: #F0E68C'>repeatedly does some tasks</span></b>.
>
>For instance machine learning algorithms like backward propagation is iteratively updating its weights. 

So Spark solves this by <b><span style='color: #F0E68C'>storing most of its intermediate results in memory</span></b>. This makes it <b><span style='color: #98FB98'>faster</span></b>. However if there is <b><span style='color: var(--mk-color-red)'>not enough memory then it still spill to the disk</span></b>.

Another advantage of Spark is its <b><span style='color: #98FB98'>easy of programmability</span></b> over Hadoop.

Spark's design philosophy is:
- Speed
- Ease of use
- Modularity (*ML, graph, streaming support*)
- Extensibility (*can connect to many other databases or storage systems*)
- *and more ...*

**Components in SPARK**
![[Spark Components.png|center]]

>[!tldr] Because of spark core computation engine and spark SQL engine they can do all of the big data operations listed

**Spark** is not a database but is <b><span style='color: #F0E68C'>a processing system</span></b> which works with a database (*storage system*). It provides an interface to connect to a data storage and read data to be processed.

>[!important] This storage must be persistent
>It is because of Spark's **resiliency** due to [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Apache Spark.md#Lineage|lineage]]. If the worker goes down a new worker will use the lineage to recompute the data, if the storage is not persistent then the <b><span style='color: var(--mk-color-red)'>worker might not be able to fetch the data again</span></b>.
## Spark Architecture

![[Spark Architecutre.png|center]]

Spark consist of 3 components:
1) **Driver process**
This driver will communicate with the users and retrieve requests. It will <b><span style='color: #F0E68C'>distribute the work to executors</span></b>. Once the task is done the driver will return back the results to the user.

>[!tldr] If the driver fails then the whole spark session is restarted
>The <b><span style='color: #F0E68C'>cluster manager will restart a session with a new driver</span></b>.
>
>This is in line with Sparks' lazy philosophy.

2) **Executors**
Just like the workers in MapReduce, it will <b><span style='color: #F0E68C'>execute a small task</span></b> and it will be <b><span style='color: #F0E68C'>done in parallel</span></b> with other executors.

3) **Cluster manager**
It is responsible for the <b><span style='color: #F0E68C'>resource management and allocation</span></b> of the whole cluster. This can be Spark's standalone cluster manager or it can be others like YARN, Mesos or Kubernetes.

>[!note] For testing purposes, Spark can be deployed on the local machine when in local mode
## Evolution of Spark APIs

![[Spark API Evolution.png|center|400]]
# Working With RDDs
---
It stands for **resilient distributed datasets**. It is distributed because data or a collection of objects is distributed over different machines.

But more interestingly it is **resilient** because it <b><span style='color: #98FB98'>achieves fault tolerance</span></b> through <b><span style='color: #F0E68C'>lineages</span></b>.

>[!question] What are faults in big data?
>One major fault is when a machine fails, how can we recover the data and the actions that the machine has already applied to the initial input?

**Overview of working with RDDs**
![[Working With RDDs Example.png|center|400]]

## Distribute The Data

If you recall the driver distributes the work to the various workers. Thus essentially what it does is that RDD will <b><span style='color: #F0E68C'>partition the data</span></b>, into smaller datasets for each of the workers.

>[!example] Example of creating partitions
>Command: `sc.parallelize(data, number of partitions)`
>
>This partitions the data into the number of specified partitions.

>[!important] Once these smaller datasets are created it cannot be changed
>What this means is that the data is <b><span style='color: #F0E68C'>immutable once partitioned</span></b>.
## Transformations

The only way to **manipulate and get new the data** is by using <b><span style='color: #B0E0E6'>transformations</span></b>. You can think of it as mapping values to something else.

>[!example] Example of a transformation
>Command: `dataRDD.map(lambda s: len(s))`
>
>For each data, it will map it to its length, creating a new RDD.

However just by calling a transformation like in the example, does not mean the transformation has been executed yet. <b><span style='color: #F0E68C'>Transformations are lazy</span></b>, meaning it will only be <b><span style='color: #F0E68C'>executed once an action is called</span></b> on it.

>[!success] Advantages of being lazy
>It can be expensive to run immediately, so Spark can <b><span style='color: #F0E68C'>optimise the query plan</span></b> to <b><span style='color: #98FB98'>improve speed</span></b> (*this is also because it uses the data frame API as well*).
<div style="page-break-after: always;"></div>

## Actions

<b><span style='color: #B0E0E6'>Actions</span></b> <b><span style='color: #F0E68C'>trigger spark to compute</span></b> a result from a series of transactions.

Here are some examples of an action command:
- `collect` - This action asks Spark to retrieve all elements of the RDD to the driver node
- `show` - Print out the data
- `count` - Count the number of data points
- `save` - Save the data into a persistent storage

So only when a action function is called, the driver will then **send all the transformations to all the workers**, thus this is why everything is **done in parallel**.
# Caching In Spark
---
Sometimes we might be **frequently transforming the same set of information**, thus it will be better if this set of data is cached for <b><span style='color: #98FB98'>faster processing</span></b>.

Lets look at some sample code:
```python
lines = sc.textFile("hdfs://...")
errors = lines.filter(lambda s: s.startswith("ERROR"))
messages = errors.map(lambda s: s.split("\t")[2])
messages.cache()

messages.filter(lambda s: "mysql" in s).count()
messages.filter(lambda s: "php" in s).count()
```

So the line `messages.cache()` saves the transformed data onto the cache. Note that at this point [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Apache Spark.md#Transformations|nothing has happened yet]]. Once `count()` is executed, it will start reading, doing the transformations and caching the data.

**Without the caching**, when its time to do the second `count`, <b><span style='color: var(--mk-color-red)'>spark will read from the disk all over again incurring heavy I/O cost</span></b>.

In Spark there is also another function called `persist(options)`, which can save an RDD into memory, disk or off-heap memory (*other forms of memory*).

>[!question] When do we cache?
>
>When <b><span style='color: #F0E68C'>re-computing is expensive</span></b> and it needs to be <b><span style='color: #F0E68C'>re-used multiple times</span></b>.
>
>Also we do not cache large chunks, <b><span style='color: #F0E68C'>cache smaller chunks</span></b>, usually after an aggregation.

During the caching process if there is **not enough space in cache**, it will evict the [[Year 1/Sem 2/CS2100 - Computer Organisation/Caching.md#Block Replacement Policy|least recently used RDD]].
# Lineage
---
Lineage in Spark is like a <b><span style='color: #F0E68C'>log of all the transformations</span></b> that was executed. Spark represent this log as a [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Graphs.md#Directed Acyclic Graph|directed acyclic graph]] (*DAG*).

So when we apply a transformation, it will add on to this DAG and when an **action** is called it will <b><span style='color: #F0E68C'>trigger the computations on this DAG</span></b>.

>[!tldr] Unlike Hadoop, Spark does not use replication
> Spark will store all intermediary data in memory, so by duplicating data in <b><span style='color: var(--mk-color-red)'>memory might not be enough and adding more memory is expensive</span></b>.
## Dependencies

Each command in Spark can be 1 of 2 types of dependencies:

![[Narrow & Wide Dependency Visualisation.png|center|350]]

1) **Narrow** dependencies
Where each partition of the parent RDD, is used by <b><span style='color: #F0E68C'>at most 1</span></b> partition of the child RDD (*same if we used data frames or data sets*).

Some transformation which are narrow dependency are `map`, `flatMap`, `filter`, `contains`

2) **Wide** dependencies
Where each partition of the parent RDD, is used by <b><span style='color: #F0E68C'>more than 1</span></b> partition of the child RDD (*between servers thus its a network shuffle*).

Some transformation which are wide dependency are `reduceByKey`, `groupBy`, `orderBy`.

>[!important] Some times wide dependency transformations are actually narrow dependencies
>In some special cases when we use a wide dependency transformation, it will result in all partitions being used by 1 child partition.
>
>So it is **only wide if**, there is a <b><span style='color: #F0E68C'>shuffling of 1 partition to many other partitions</span></b>.

So linking back to lineages, <b><span style='color: #F0E68C'>all narrow dependencies are group together into a stage</span></b>. Spark performs consecutive transformations **within stages**.

Only when a **wide dependency transformation is called** then it will <b><span style='color: #F0E68C'>change to a new stage</span></b>. Thus **across stages**, it will shuffle data across partitions.

>[!success] Minimising shuffling is a good practice for improving performance

# Data Frames & Data Sets
---
## Data Frames

A **data frame** represents data in a <b><span style='color: #F0E68C'>table format</span></b>. It is similar to the data frames in pandas or in SQL.

A **data frame** is made up of <b><span style='color: #F0E68C'>row objects</span></b> (*data*) and our **functions** take in strings (*column headers*) or <b><span style='color: #F0E68C'>column objects</span></b>.

A data frame <b><span style='color: #F0E68C'>offers a higher level interface</span></b> (*transformations that resemble SQL operations*). This makes it <b><span style='color: #98FB98'>easier to work with</span></b>, while also allowing all tasks to be done while rarely using RDD functions. 

We can also <b><span style='color: #F0E68C'>use SQL queries</span></b> as a way to do **transformation**. But if we do so then we <b><span style='color: #F0E68C'>need to create a table view</span></b> before executing our query.

>[!note] However, in the end, all data frame operations are still compiled down to RDD operations

However once you use a data frame you <b><span style='color: var(--mk-color-red)'>cannot convert it to an RDD</span></b>, only to another data frame.

>[!success] Generally data frames are more efficient and easier to work with
> In **RDD** you <b><span style='color: var(--mk-color-red)'>instruct spark how to compute the query</span></b> which might be inefficient.
> 
> But in a **data frame** you <b><span style='color: #98FB98'>tell spark what you want it to do</span></b>. This makes the code simpler but also allows spark to optimise the query. 
## Data Sets

Similar to data frames but they are <b><span style='color: #F0E68C'>now type safe</span></b>. So each row in the data frame is a row object but what if the **user wants their own class** for the row?

We can <b><span style='color: #F0E68C'>define our own class for our rows</span></b> and when we do a action function, it will return the rows as our defined class and not the row object.

>[!question] Why do we need our own types?
>If your data is internal or you want your own customised object.

Just take note that data sets are <b><span style='color: var(--mk-color-red)'>not available</span></b> in <b><span style='color: #DDA0DD'>Python</span></b> and <b><span style='color: #DDA0DD'>R</span></b>, since these languages are <b><span style='color: #F0E68C'>dynamically typed</span></b> languages.
# Spark SQL Engine
---
![[Spark SQL Engine.png|center|400]]

This is the **core engine of spark** it supports all the relational operations using the:
- **Data frame API**
- <b><span style='color: #B0E0E6'>Catalyst optimiser</span></b>
- <b><span style='color: #B0E0E6'>Tungsten</span></b>

>[!question] What is a catalyst optimiser and tungsten?
>
><b><span style='color: #F0E68C'>Both are optimisers</span></b> in Spark SQL engine. However the **catalyst optimiser** is used to <b><span style='color: #98FB98'>optimise the query</span></b> (*software side*) while **tungsten** is to <b><span style='color: #98FB98'>optimise more on the hardware level</span></b>.
## Catalyst Optimiser

The catalyst optimiser will take a query and convert it into an execution plan through these **4 transformational phases**:
1) **Analysis**
2) **Logical optimisation**
3) **Physical planning**
4) **Code generation** (*using project Tungsten*)

![[Spark's Catalyst Optimiser Transformation Phases.png|center|400]]

>[!info] Because it has the logical plan, that is why catalyst optimiser is able to optimise the query for the user

So no matter what language, the **performance will be the same**.

If we were to use the **data frame** API to **generate our logical plan**, it will be <b><span style='color: #98FB98'>more efficient</span></b> as compared to using RDD.
## Project Tungsten

Its task is to <b><span style='color: #98FB98'>improve the memory and CPU efficiency</span></b> of Spark applications and push performance closer to the limits of modern hardware (*basically it works with hardware*).

And as mention previously, **Tungsten** is used to <b><span style='color: #F0E68C'>generate RDD level code & execute it</span></b>. This code generated will be efficient in:
- **Memory management**
- **Binary processing**
- **Cache-aware computation** (*will know when to cache certain data*)

>[!note] All of these improves the physical execution of the RDD code
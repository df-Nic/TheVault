---
title: Distributed Databases
Date Created: 2025-09-19
Last Updated: 2025-09-28
tags:
  - CS4225
  - Database/NoSQL
  - DatabaseDesign/DistributedDatabases
---
# Introduction to Distributed Databases
---
Here we will be **using NoSQL** systems to implement a distributed database.

>[!question] But what is a distributed database
>It is <b><span style='color: var(--mk-color-yellow)'>multiple databases working together</span></b> which can be deployed in different locations.
>
>Data is also spread out to the different systems and it <b><span style='color: var(--mk-color-green)'>will not all be in 1 place</span></b>.

But why develop a distributed database, well it does comes with its **advantages** like:

>[!success] Scalability
> Easily **scale horizontally** by simply adding more nodes.

>[!success] Availability / fault tolerance
>If 1 node fails then other nodes can still service the request.

>[!success] Latency
> Distributed databases around the world can generally reduce latency by **sending the request to the closest replica**.

When designing a distributed database we need to <b><span style='color: var(--mk-color-yellow)'>ensure data transparency</span></b>, where:
- Users should not know how the data is distributed, replicated or partitioned
- Queries that works on a single node database must work on distributed databases
## Distributed Database Architectures

![[Distributed Database Architectures.png|center|350]]

To interpret the diagram, look at the **shared everything** architecture:
- The top one is a **processor**
- The middle one is **memory**
- And the bottom one is the **disk**
<div style="page-break-after: always;"></div>

Here are some of the **usages for each of the architectures**:
1) Shared everything: single node DMBS
2) Shared memory: supercomputers (*not commonly used*)
3) Shared disk: cloud databases like oracle and snowflake
4) Shared nothing: mostly NoSQL like Redis, MongoDB, Cassandra
## Assumptions in Distributed Databases

### Failing Nodes

![[Distributed Database Failing Nodes Assumption.png|center|250]]

This assumptions means that at <b><span style='color: var(--mk-color-red)'>any time the nodes can do down</span></b>.

Thus this is the reason why many NoSQL systems have **duplicates**. This is to <b><span style='color: var(--mk-color-green)'>ensure that the system has sufficient redundancy</span></b>.
### Connection Failure

![[Distributed Database Connection Failure Assumption.png|center|200]]

It is possible that <b><span style='color: var(--mk-color-red)'>connection between 2 nodes may fail</span></b>. So when developing a distributed system its design will have this in mind.

>[!failure] And in some worse case will partition the whole system into 2

### Well-Behaved Nodes

When designing a distributed database, we need to assume that all nodes are **well-behaved**. It means that the <b><span style='color: var(--mk-color-yellow)'>protocol assigned will be strictly followed</span></b> & will not go against it or corrupt the database.

>[!info] Byzantine fault tolerant protocol
>
>It is a protocol which allows the system to <b><span style='color: var(--mk-color-yellow)'>function correctly even when some nodes behave arbitrarily</span></b>.
>
>This is widely used in blockchains where they use a decentralised ledger & various consensus mechanisms.
## CAP Theorem

**CAP** stands for:
- **Consistency**: Same as [[NoSQL#Eventually Consistency|strong consistency]] where every <b><span style='color: var(--mk-color-yellow)'>read</span></b> receives the <b><span style='color: var(--mk-color-yellow)'>most recent write or error</span></b>
- **Availability**: Every request to a node in the system must <b><span style='color: var(--mk-color-yellow)'>lead to a response</span></b>
- **Partition tolerance**: The system <b><span style='color: var(--mk-color-yellow)'>continues to operate</span></b> even when network failures causes a partition

The **consistency** in CAP is **different** than the one in [[Creating and Populating Tables with Constraints#Constraints|ACID]].

>[!warning] A distributed system cannot have all 3 properties of CAP
>![[Distributed Database CAP Tradeoffs.png|center|200]]
>
>There will always be a <b><span style='color: var(--mk-color-red)'>tradeoff necessary</span></b>. When tuning a distributed system for <b><span style='color: var(--mk-color-yellow)'>consistency you will need to tradeoff availably</span></b> (*and vice versa*).
>
>Generally **NoSQL** will <b><span style='color: var(--mk-color-yellow)'>forgo consistency</span></b> while **distributed RDBMS** will <b><span style='color: var(--mk-color-yellow)'>forgo availability</span></b> (*not always the case*).
>
>For example, if we have a partition and only 1 has the updated value. If we read from the other partition, do we return the outdated value (*no consistency*) or return an error (*no availability*).
# Data Partitioning
---
Since in distributed databases consist of multiple machines working together, we need to know how to partition to data to <b><span style='color: var(--mk-color-yellow)'>evenly spread the load to all the machines</span></b>.

>[!Warning] How we partition matters
>**Partition wrongly,** there will be <b><span style='color: var(--mk-color-red)'>imbalanced data</span></b> per partition causing a bottleneck.
>
>**Partition correctly** the <b><span style='color: var(--mk-color-green)'>work load will be balanced evenly</span></b>.
## Table Partitioning

![[Table Partitioning Example.png|center|400]]

It is a simple solution of <b><span style='color: var(--mk-color-yellow)'>putting one table or collection into one machine</span></b>. So each machine will handle data of the same table or collection.

>[!failure] Scalability issues
>We cannot spilt the data in 1 data into 2 separate machines. Thus if <b><span style='color: var(--mk-color-yellow)'>one table is too big to fit on a machine</span></b> than this approach will not work.
<div style="page-break-after: always;"></div>

## Horizontal Partitioning

![[Horizontal Partitioning Example.png|center|500]]

Also known as [[NoSQL#MongoDB|sharding]]. It is a common approach to partitioning. Here <b><span style='color: var(--mk-color-yellow)'>different data entries are stored in different nodes</span></b>.

As mentioned previously, there will be a **partition key** (*shard key*) which will <b><span style='color: var(--mk-color-yellow)'>decide which partition</span></b> the data will be stored on.

>[!question] Finding the right partition key
>This is a case by case scenario but a rule of thumb is that if our <b><span style='color: var(--mk-color-yellow)'>queries mostly revolve around filtering or doing a "group-by"</span></b>  for column(s) then it will be a suitable partition key.
### Assigning Data to Partitions

With the partition key set, **how can we specify which data goes to which partition?**
#### Range Partition

![[Range Partition Example.png|center|450]]

So given a partition key's value a <b><span style='color: var(--mk-color-yellow)'>partition can accept a range of values of this key</span></b>.

>[!success] Good if our queries are mainly ranged-based ones
>We can ignore certain partitions if it does not fit within the range.
>

>[!failure] Imbalanced shards
>
>It is possible that some ranges will have way more data than other ranges leading to an imbalanced partitions.
>
>There is a <b><span style='color: var(--mk-color-turquoise)'>balancer</span></b> which will <b><span style='color: var(--mk-color-yellow)'>redistribute by splitting the range</span></b>. This does keeps it balance but at the cost of a <b><span style='color: var(--mk-color-red)'>significant overhead</span></b>.
<div style="page-break-after: always;"></div>

#### Hash Partition

![[Hash Partition Example.png|center|500]]

So instead of using a range why not just <b><span style='color: var(--mk-color-yellow)'>hash the value with some hash function</span></b>.

If your hash function returns values exceeding some range you can <b><span style='color: var(--mk-color-yellow)'>limit the result</span></b> by using the **modulo** function.

>[!note] Most hash functions are design to ensure that the distribution of all possible has values are [[Year 1/Sem 2/CS2040S - Data Structures and Algorithms/Hashing#Hash Functions|evenly distributed]]
>
>This leads to our **partition ranges** to be <b><span style='color: var(--mk-color-green)'>evenly distributed with data as well</span></b>.
>
>But it <b><span style='color: var(--mk-color-red)'>does not guarantee that our data will be balanced between partition</span></b> as if our data mostly consist of keys which maybe have the same value will all hash to the same value thus making it imbalanced.

>[!fail] If we have a range query then we need to send to all shards
#### Consistent Hashing

It **solves some problems in range & hash partitions** where what if we want to partition over more nodes or if a node goes down (*cannot write into that partition*).

By **redoing the partition** it will be <b><span style='color: var(--mk-color-red)'>costly & inefficient</span></b> due to the data that needs to be **moved** around.

![[Consistent Hashing Example.png|center|500]]

So think of a hash function which output between a certain range, then our <b><span style='color: var(--mk-color-yellow)'>partitions can be markers along the number line</span></b>.

>[!question] So which partition does each data belong to?
>So a **data point belongs** the the <b><span style='color: var(--mk-color-yellow)'>first marker going clockwise</span></b>.
>
>In our example if our data's partition key hashed to number  5 then it belongs to partition 3.
##### Addition & Deletion of Partitions

We can see that this idea makes <b><span style='color: var(--mk-color-green)'>addition & deletion of a node to be simple</span></b>:
- When **removing** a node, we can <b><span style='color: var(--mk-color-yellow)'>just move those in node 3 to the next node moving clockwise</span></b> (*in our case is node 1*)
- When **adding** a new node, <b><span style='color: var(--mk-color-yellow)'>all data before this node until the next node moving anti-clockwise</span></b> (*if we add node 3 then move 31, 0 - 10*).

>[!success] The main advantage is we only need to move the affected data and not everything

>[!abstract] Multiple markers
>
>![[Consistent Hashing With Multiple Markers.png|center|500]]
>
>Instead of 1 marker per partition, how about **multiple markers for 1 partition**. It <b><span style='color: var(--mk-color-yellow)'>works similarly as before</span></b> just go clockwise.
>
>But if we remove a node, then <b><span style='color: var(--mk-color-yellow)'>not all the data will go into the same node</span></b>. It will be spread out making the <b><span style='color: var(--mk-color-green)'>load more balanced</span></b>.
##### Replication

We can also duplicate the data by <b><span style='color: var(--mk-color-yellow)'>simply replicate it in the next additional nodes moving clockwise</span></b> after the primary node. So if we want to duplicate data at 10:
- Node 3 is the primary
- While nodes 1 and 2 are the secondary and it will be duplicated there
# Indexing
---
Its a **method** of <b><span style='color: var(--mk-color-green)'>quickly accessing data</span></b> in the database. 

>[!example] An analogy of an index
>You can think of it as a table of contents. Where our index key is the headers then it will directly point you to the page number.

In database these indexes are implemented as <b><span style='color: var(--mk-color-purple)'>B+ trees</span></b>. They are <b><span style='color: var(--mk-color-yellow)'>balanced trees</span></b> where the <b><span style='color: var(--mk-color-yellow)'>values are stored only in the leaf nodes</span></b>.

![[B+ Tree Example.png|center|400]]

How this data structure works is that the **inner nodes will contain values** (*directions*) which <b><span style='color: var(--mk-color-yellow)'>tells you where to branch off to</span></b> given a key. So for example if our key is 8 we will head down the middle.

In addition, the **leaves are connected** to one another using a <b><span style='color: var(--mk-color-turquoise)'>sibling pointer</span></b> (*linked list*) for <b><span style='color: var(--mk-color-green)'>easy traversal</span></b>.

>[!success] With B+ trees, we can search, insert and delete in O(log n) time

>[!note] The values you see in the example are just pointers to the actual database row as storing the actual data in the tree is too large

Linking back to [[NoSQL#MongoDB|MongoDB]], <b><span style='color: var(--mk-color-yellow)'>each shard will have its own indexing</span></b>, this is known as <b><span style='color: var(--mk-color-turquoise)'>local indexing</span></b> (*global indexing is the opposite*). Where they will use it to run the query.

>[!info] `_id` column
>In MongoDB every table will have a `_id` column where <b><span style='color: var(--mk-color-yellow)'>each value is unique which is auto-generated</span></b>. It <b><span style='color: var(--mk-color-yellow)'>can then be indexed with other columns</span></b>.

Apart from indexing, a <b><span style='color: var(--mk-color-turquoise)'>query planner</span></b> is also used to make the query <b><span style='color: var(--mk-color-green)'>faster</span></b>. It <b><span style='color: var(--mk-color-yellow)'>decides the best way the query should run</span></b> using the indexes it has.


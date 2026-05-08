---
title: NoSQL
Date Created: 2025-09-15
Last Updated: 2025-09-28
tags:
  - CS4225
  - Database/NoSQL
---
# What is NoSQL
---
It refers to a <b><span style='color: var(--mk-color-turquoise)'>non-relational database</span></b>, where it <b><span style='color: var(--mk-color-yellow)'>stores data in some format</span></b> <b><span style='color: var(--mk-color-red)'>other than relational tables</span></b>.

>[!note] SQL refers to the relational databases not the querying language
>**NoSQL** systems <b><span style='color: var(--mk-color-yellow)'>can involve SQL-like querying</span></b> languages.

>[!info] Relational & non-relational DB can work with each other
>Each are used for the task they are most suited for.
>

Types of NoSQL databases:
- **Document store** : Stores data in a JSON format (*example* <b><span style='color: var(--mk-color-teal)'>mongoDB</span></b>)
- **Key-value store** Store data in key-value pairs (*example* <b><span style='color: var(--mk-color-teal)'>redis</span></b>)

>[!success] Flexible / dynamic schema
>Database items <b><span style='color: var(--mk-color-yellow)'>does not need to follow a precise schema</span></b> (*good for less well-structured data*).
>
>However there are **still ways to validate constraints**, called <b><span style='color: var(--mk-color-yellow)'>schema validation</span></b>.

>[!success] Horizontal scalability
>Due to sacrificing strong consistency. We can just deploy more databases and let eventually consistency ensure everything is in sync.
>
>If its [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/NoSQL.md#Eventually Consistency|strong consistency]] then every write will be locked which defeats the purpose of scaling.

>[!success] High performance & availability
>Due to relaxed consistency model & fast reads/writes

>[!failure] No declarative query language
>Query logic like joins may have to be handled on the application side, which can add to more code (*unsupported features which is available in a relational database*)

>[!failure] Weaker consistency guarantees
>Eventual consistency.
<div style="page-break-after: always;"></div>

>[!abstract] Schema on write & schema on read
>They are properties that the DB follows. For **relational databases** they follow the <b><span style='color: var(--mk-color-turquoise)'>schema on write</span></b>. This means than <b><span style='color: var(--mk-color-yellow)'>when data is written it must follow the schema</span></b> (*if not it will show an error*).
>
>As for **NoSQL**, the follow the <b><span style='color: var(--mk-color-turquoise)'>schema on read</span></b>. This means than <b><span style='color: var(--mk-color-yellow)'>when data is queried it will enforce a structure on the data</span></b>.

**Properties** of NoSQL systems:
- Horizontal scalability (*designed to operate in a distributed manner*)
- Replicate & distribute data over many servers (*Robustness*)
- Simple call interface
- Often weaker concurrency model than relational DBs (*outdated data*)
- Efficient use of distributed indexes & RAM
- Flexible schemas

For **NoSQL database**, we weaken the consistency constraint from [[Creating and Populating Tables with Constraints#Constraints|ACID]]to <b><span style='color: var(--mk-color-turquoise)'>BASE</span></b>.

>[!abstract] BASE
>- **Basically Available** : Basic reading & writing are available most of the time
>- **Soft state**: Without guarantees, we have some probability of knowing the state at any time (*chance you get outdated data*)
>- **Eventually consistent**: [[NoSQL#Eventually Consistency|After a period of time]] data will be synchronise

# Types of NoSQL Systems
---
There are **5 types**:
1) Key-value stores
2) Wide column databases
3) Document stores
4) [[Graphs & Page Rank#Graph Data|Graph databases]]
5) Vector databases
## Key-Value Stores

It acts like a dictionary in programming languages where it <b><span style='color: var(--mk-color-yellow)'>stores associations between keys & values</span></b>.

**Keys** are usually <b><span style='color: var(--mk-color-yellow)'>primitives</span></b> & it <b><span style='color: var(--mk-color-green)'>can be queried</span></b> while **values** can be <b><span style='color: var(--mk-color-yellow)'>both primitive & complex</span></b> & it <b><span style='color: var(--mk-color-red)'>cannot be queried</span></b>. 

>[!info] Primitives & complex types
>**Primitives** are our integers, strings, raw bytes and so on.
>
>**Complex types** are our objects, JSON, HTML fragments, BLOB (*basic large object*) and so on.

These key-value stores can be <b><span style='color: var(--mk-color-yellow)'>persistent</span></b> (*data is stored in disk*) or <b><span style='color: var(--mk-color-yellow)'>non-persistent</span></b> (*big in-memory hash table*).
<div style="page-break-after: always;"></div>

Applications which uses key-values stores are:
- Storing user sessions
- Caches
- User data that is processed individually (*by key*)

They have 2 simple API **operations** which is just to `Get` (*value by key*) and to `Put` (*Set value associated with key*). 

We can extend these 2 basic operations to have a `multi-get`, `multi-put` & range queries (*fetch keys between a certain range*).

>[!success] Suitable for small continuous reads & writes

>[!fail] Only applicable for basic information
>
>Basic information is information where <b><span style='color: var(--mk-color-yellow)'>complex queries are not required</span></b>.
>
>We can only query by key, if we need to store customer information like address, name, collection of items then this is not sutible.
## Document Stores

A **document** is a <b><span style='color: var(--mk-color-yellow)'>JSON-like object</span></b> which has its **own fields & values** (*can be nested i.e. another JSON object*).

These databases stores contains a <b><span style='color: var(--mk-color-turquoise)'>collection</span></b> and a **document**.

>[!info] Collection
>A collection can be thought of as a folder which will <b><span style='color: var(--mk-color-yellow)'>contain a bunch of documents</span></b>.

Useful if our queries are **suitable** for queries <b><span style='color: var(--mk-color-yellow)'>based on the fields of a documents</span></b>.

>[!success] Allows for a flexible schema

>[!success] Suitable to store structured objects
>
>If it comes to **unstructured objects then there is no advantage** over key value stores.

**Example document**
```JavaScript
{
/* This is a collection which is like our tables*/
"user" : [
	/* This is a document which is like our rows*/
	{
		"userId" : 1, /* The field is the columns*/
		"name" : "Jane Doe",
		"hobbies" : ["cooking", "running"]
	},
]
}
```
<div style="page-break-after: always;"></div>

### CRUD

**Querying** in a document store is all based on the <b><span style='color: var(--mk-color-yellow)'>content of the document</span></b>. And similar to relational databases these queries can be categorised as **CRUD**.

>[!question] What is CRUD?
>
>It is an abbreviation for create, read, update & delete.

**Examples of CRUD queries**

>[!note] These examples follows the MongoDB syntax

1) **Create**

```MongoDB
db.users.insert ( <-- Collection is users
	-- Starting here is a document --
	{
		name: "John", <-- field : value
		age: 26,
		status: "Healthy"
	}
)
```

2) **Read**

```MongoDB
db.users.find ( 
	{ age: { $gt: 18}}, <-- Condition
	{name : 1, address : 1} <-- projection, which is just selecting a specific set of fields
).limit(5) <- Only the first 5 results
```

>[!note] If the document does not contain the field, we will not return the document 

3) **Update**

```MongoDB
db.users.update ( 
	{ age: { $gt: 18}}, <-- Condition to update
	{ $set: {status: "Sick"}}, <-- Updated value or action
	{multi : true} <-- Update multiple items
).
```

3) **Delete**

```MongoDB
db.users.delete ( 
	{ status : "Sick"} <-- Condition to delete
).
```
<div style="page-break-after: always;"></div>

### MongoDB

![[MongoDB Architecture.png|center|450]]

The image above, shows the **architecture** of the <b><span style='color: var(--mk-color-teal)'>MongoDB</span></b>. It consist of 3 main components:
1) **Routers** (*mongos*): <b><span style='color: var(--mk-color-yellow)'>Handles requests</span></b> from applications & <b><span style='color: var(--mk-color-yellow)'>route queries</span></b> to the correct shards (*like the* [[Hadoop#Hadoop Implementation of MapReduce|master worker]])
2) **Config server**: <b><span style='color: var(--mk-color-yellow)'>Stores the metadata</span></b> (*for query handling*), in particular which shard the data is stored in
3) **Shards**: In 1 shard, there are <b><span style='color: var(--mk-color-yellow)'>multiple machines storing the same data</span></b> (*redundancy*) 

>[!info] Shards
> We can think of this as <b><span style='color: var(--mk-color-yellow)'>separate storages</span></b>.
> 
> Now who decides **what data goes into which shard**, that is handled by the <b><span style='color: var(--mk-color-turquoise)'>partition key</span></b> (*shard key*). So the <b><span style='color: var(--mk-color-yellow)'>value one of the keys in the document will be used for partitioning</span></b>.
> 
> This results in <b><span style='color: var(--mk-color-green)'>same values for a key to be in the same shard</span></b>.

>[!important] Shards and replica sets are 2 different concepts
>A **shard** is responsible for <b><span style='color: var(--mk-color-yellow)'>segregating data</span></b> into different machines.
>
>While a **replica set** is tasked for redundancy by <b><span style='color: var(--mk-color-yellow)'>storing duplicates of the same data</span></b>.

So here is a **general flow for a query** in MongoDB:
1) The query will be sent to one of the routers
2) It will interact with the config server to determine which shards to query (*scatter phase*)
3) Query is sent to the relevant shards ([[NoSQL#Partition Pruning|partition pruning]])
4) Shards search for the data and rerun it back to the router (*gather phase*)
5) The router will then combine the results and return the data to the user
#### Partition Pruning

Sending a **query to all the shards** can be <b><span style='color: var(--mk-color-red)'>expensive & inefficient</span></b>. If possible we want to <b><span style='color: var(--mk-color-yellow)'>send the query to the relevant shards</span></b> & this is what partition pruning does.

Recall that **data is stored based on a partition key**, so if our **query only has the partition key** then we can <b><span style='color: var(--mk-color-green)'>safely send it to the relevant shards</span></b> by just taking the value.

**If not** (*query is some value not the partition key*) then we cannot guarantee that it will be in a set of shards thus we have to <b><span style='color: var(--mk-color-red)'>send it to all shards</span></b>.

>[!note] This only applies to read, update & delete queries
>
>For **insert** queries it is special. When inserting a new document the <b><span style='color: var(--mk-color-yellow)'>query must have the partition key</span></b>. If the query does <b><span style='color: var(--mk-color-red)'>not have it then it will throw an error</span></b>.
>
>Thus the insert query will always be sent to the one relevant shard.

>[!warning] We need to carefully set our partition keys
>
>If we do not set it correctly, we might have <b><span style='color: var(--mk-color-red)'>imbalanced partitions</span></b>, <b><span style='color: var(--mk-color-red)'>high maintenance</span></b> (*updated data and we need to move it to a new partition*) & <b><span style='color: var(--mk-color-red)'>low cardinality affecting scalability</span></b> (*low number of partitions*).
>
>Sometimes a <b><span style='color: var(--mk-color-turquoise)'>composite partition key</span></b> (*more than 1 key*) will solve some of these problems.
#### Replication

![[Standard Shard Framework.png|center|300]]

In MongoDB the standard configuration in a shard will consist of **1 primary and 2 secondaries**.

When a **write** query is sent, the primary will <b><span style='color: var(--mk-color-yellow)'>update the data</span></b>  & write this change to its <b><span style='color: var(--mk-color-turquoise)'>operation log</span></b> (*a log on all the queries*)

The **secondaries** will <b><span style='color: var(--mk-color-yellow)'>replicate this log and apply it to their own data copy</span></b>, then acknowledge the operation. This then <b><span style='color: var(--mk-color-green)'>ensures data is synchronised</span></b>.

>[!important] There is no delay when writing to primary thus reading from primary will always be the most updated data

The **order** in which the operation log is bring written will <b><span style='color: var(--mk-color-yellow)'>follow when the secondary reads it</span></b>.

>[!note] For reads and writes it will always be done on primary
>However the user **can choose to read from secondary**. This <b><span style='color: var(--mk-color-green)'>decreases latency & distribute load</span></b> (*improve throughput*).
>
>However there is a <b><span style='color: var(--mk-color-red)'>risk that the user is reading stale data</span></b> (*outdated*). This is known as <b><span style='color: var(--mk-color-turquoise)'>eventual consistency</span></b>.
<div style="page-break-after: always;"></div>

## Wide Column Stores

![[Wide Column Stores Example.png|center]]

These types of DBs are <b><span style='color: var(--mk-color-yellow)'>designed for massive-scale data</span></b>, which requires <b><span style='color: var(--mk-color-yellow)'>fast writes</span></b>.

>[!info] This DB is very suitable for time-ordered data
>
>Examples: Logs, metrics, sensor data etc.

The **rows** are our entities like on a relational DB. The **columns** which are our fields.

It might look like a relational database however it has some **differences**:
- There is a **column families** which <b><span style='color: var(--mk-color-yellow)'>groups related columns</span></b>
- **Sparsity**, which is when a <b><span style='color: var(--mk-color-yellow)'>column is not used then it does not use space</span></b> (*in a relational DB it will be NULL*)

>[!note] Sparsity can also be applied to document stores since if the field has no value it will not be in the document

>[!success] Efficiently operate on columns or a subset of columns
## Graph Databases

![[Graph Database Example.png|center|280]]

Essentially we have entities which we will map with **edges** if they have a <b><span style='color: var(--mk-color-yellow)'>relationship</span></b>.
## Vector Databases

Unlike other databases, vector databases <b><span style='color: var(--mk-color-yellow)'>stores vectors</span></b> where each row in the vector is a point in the d-dimension space.

These vectors are usually dense, numerical & high-dimensional.

Features of a vector database:
- Scalability
- Real-time updates
- Replication

>[!success] Allow fast similarity search
>
>Given a query it can retrieve similar neighbours from the database (*locality-sensitive hashing*).

>[!abstract] Popular in AI , ML & vision models
>Since texts are converted into embeddings which are just vectors.

# NoSQL Key Concepts
---
## Eventually Consistency

It is a concept where **files become consistent** assuming devices are <b><span style='color: var(--mk-color-yellow)'>connected to the internet for a sufficiently long time</span></b>.

Essentially you can think of many sources of the same data and through the network, over a period of time it will all be synchronised (*so long the system / DB / connection is working*).

In NoSQL we **trade off** <b><span style='color: var(--mk-color-green)'>availability</span></b> over a <b><span style='color: var(--mk-color-red)'>much weaker consistency guarantee</span></b> (*all this depends on the application you are building*).

>[!warning] Out of sync data
>This happens when there is a <b><span style='color: var(--mk-color-red)'>loss of connectivity</span></b> (*internet*), or when the data is just received and there is <b><span style='color: var(--mk-color-red)'>latency</span></b> involved.
>
>It will <b><span style='color: var(--mk-color-yellow)'>need time to synchronise</span></b> the data in other sources and thus users might fetch outdated information.

>[!abstract] Strong consistency
>![[Strong Consistency Example.png|center|400]]
>
>**Strong consistency** is the strictest form of consistency where any reads immediately after an update <b><span style='color: var(--mk-color-yellow)'>must give the same result for all observers</span></b> (*must be the most updated one*).
>
>It uses <b><span style='color: var(--mk-color-turquoise)'>locks</span></b>, will be used to <b><span style='color: var(--mk-color-yellow)'>prevent any query on the database</span></b> until the value has been updated. But this <b><span style='color: var(--mk-color-red)'>affects the availability</span></b> of the system / DB.
<div style="page-break-after: always;"></div>

## Duplication

In relational database we can join 2 tables into 1. But for NoSQL, how can we accomplish this? One way is to use support `join` operations by the database (*later versions of MongoDB*).

However a more <b><span style='color: var(--mk-color-green)'>efficient</span></b> way is <b><span style='color: var(--mk-color-yellow)'>duplication or denormalization</span></b>. The idea is to store the same data twice (*storage is cheap*), which is essentially merging the 2 together (*take all the fields and put it together*). Then to <b><span style='color: var(--mk-color-green)'>query it can be done in 1 single query on the newly merged table</span></b>.

>[!note] These tables should be designed around queries we expect to receive

>[!fail] Difficult to deal with updates
>
>If a value is changes it needs to be propagated to the merged tables as well.


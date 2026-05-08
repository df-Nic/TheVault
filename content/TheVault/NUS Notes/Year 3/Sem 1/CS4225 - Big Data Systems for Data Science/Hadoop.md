---
Title: Hadoop
Date Created: 28-November-2025
Last Updated: 18-March-2026
Tags: 
title: Hadoop
tags:
  - CS4225
  - Hadoop
---
# Introduction to Hadoop
---
![[Hadoop Architecture Overview.png|center]]

In the olden days, **storage** nodes (*just databases*) and **compute** nodes (*does the computation*) are **segregated**. This means that there is <b><span style='color:var(--mk-color-red)'>high traffic when moving data which is costly & time consuming</span></b>.

Thus Hadoop combines the <b><span style='color:var(--mk-color-yellow)'>storage nodes and compute nodes to be on the same machine</span></b>, which enables <b><span style='color:var(--mk-color-green)'>locality for better performance</span></b>.

Hadoop is a framework which handles:
- Scheduling (*Assign tasks to workers*)
- Shuffle Phase (*Data is shuffled & sorted in between maps*)
- Synchronisation (*Output is as expected*)
- Faults (*Detects worker failure and restarts*)

Each slave node <b><span style='color:var(--mk-color-yellow)'>double up as a data node and a worker node</span></b>.

>[!attention]  In Hadoop, the HDFS and the MapReduce is a separate system
# Hadoop Implementation of MapReduce
---
We will combine the basic flow of MapReduce and describe it with how Hadoop implements it.

![[Images/CS4225 Images/Hadoop's MapReduce.png|center]]

1) **Submit**
This is where the user **interacts** with Hadoop, they will pass in certain parameters:
- A function for `map` (*or a class with the map function*)
- A function for `reduce` (*or a class with the reduce function*)
- A partition function (*Not required*)
- Number of reduce workers (*reduce tasks*)
- Number of map workers

2) **Schedule**
There is a **"master worker"** which is tasked to <b><span style='color:var(--mk-color-yellow)'>schedule resources</span></b> for the map and reduce tasks (*allocate workers*).

>[!info] A worker is a component of the cluster that performs storage & processing tasks

3) **Map task**
  The input files or <span style='color:var(--mk-color-yellow)'>documents will then be spilt into 128MB chunks</span>. Each of these chunks (*map task*) will be sent to a map worker.

>[!important] Map tasks are not input key value pairs
>The number of map tasks is equal to the number of input splits.
>
>1 split can have multiple input key value pairs.

>[!info] Map workers work on 1 map task at a time & when completed they pick up any remaining unassigned map task

>[!important] The spilt size matters
>Initially as you increase the job size performance improves because parallelism utilises more machines.
>
>If its too **large** there ill be <b><span style='color:var(--mk-color-red)'>limited parallelism</span></b> (*not all  mappers will be utilised*). And it can be <b><span style='color: var(--mk-color-red)'>limited to the networks bandwidth</span></b>.
>
>If its too **small**, then there will be a <b><span style='color:var(--mk-color-red)'>high overhead of map tasks</span></b> (*overwhelm the master worker*).
<div style="page-break-after: always;"></div>

4) **Map phase**

>[!important] Don't take 1 split or map task as 1 giant text, it is possible that inside 1 split can have multiple key value pairs
>
>So the number of `map` function calls is the number of input splits.

A map worker will <b><span style='color:var(--mk-color-yellow)'>iterate over each key value</span></b> tuple in its spilt, call the `map` function & <b><span style='color:var(--mk-color-yellow)'>output a list of new key value pairs</span></b>. 

>[!note] The initial key the map functions receives is based on the input format
>
> For example, with a `TextInputFormat`, the initial key value pair will be the byte offset and the value is the actual text.
> 
> What new key value it maps the input value is up to the function. 

Afterwards it <b><span style='color:var(--mk-color-yellow)'>takes the list and partitions it</span></b> based on the partitioner (*done between map & partition phases*).

It will then <b><span style='color:var(--mk-color-yellow)'>sort each partition based on the key</span></b> (*merge sort*). Then it will combine the data & will be <b><span style='color:var(--mk-color-yellow)'>saved into a local disk</span></b> own by the worker.

>[!warning] This is why the combiner can be useful
>
>Since if there are a lot of key value pairs then we need to do a lot of writing to the disk.
>
>It is <b><span style='color:var(--mk-color-green)'>better to do 1 big tasks </span></b> than many small tasks when dealing with the disk.

5) **Remote Read**
Each reduce worker will be <b><span style='color:var(--mk-color-yellow)'>in charge of a specific set of keys</span></b>, which is all defined by the partitioner.

>[!note] Shuffle phase
>
>It is comprised of the <b><span style='color:var(--mk-color-yellow)'>local write by the mapper and the remote read by the reducer</span></b>.

>[!info] There is a barrier for the reduce workers
>
>The reduce workers are <b><span style='color:var(--mk-color-green)'>allowed to read from the mappers local disk</span></b>, however they <b><span style='color:var(--mk-color-red)'>cannot operate on the data</span></b> until the mapping phase is complete.
>
>If there is no barrier it might compute wrongly.

After fetching the data from all the mappers local disk <b><span style='color:var(--mk-color-yellow)'>over the network</span></b>, the reducer will do a <b><span style='color:var(--mk-color-yellow)'>merge sort based on the keys</span></b>, before grouping the <b><span style='color:var(--mk-color-yellow)'>tuples with the same key into a list</span></b> (*<key, list of values>*).

>[!success] Merge sort is used to improve efficiency

6) **Reduce phase**
The reducer will then call the `reduce` function for the list of values on every unique key.
  
7) **Write**
The output of the reducer will be <b><span style='color:var(--mk-color-yellow)'>written into a HDFS</span></b> which is a distributed file system.
<div style="page-break-after: always;"></div>

# Hadoop Distributed File System
---
Also known as <b><span style='color:var(--mk-color-turquoise)'>HDFS</span></b>.

>[!info] Distributed
>
> It means taking the **data** and </b><span style='color:var(--mk-color-yellow)'>segregating it into chunks and storing them</span></b>.

>[!note] HDFS is stand alone, thus it can be used by itself or with other software

In HDFS:
- Files are <b><span style='color:var(--mk-color-yellow)'>stored as chunks</span></b> over a set of data nodes (*default is 128MB*)
- It has a single <b><span style='color:var(--mk-color-turquoise)'>name node</span></b> (*master node*)
- It also <b><span style='color:var(--mk-color-green)'>replicates data for fault tolerance</span></b> (*default is 3*) for redundancy
- Reads & writes data locally first

>[!abstract] Name node
>
>It is a master node which coordinates access to other nodes and keeps track of metadata.
>
>It does the following things:
>- Holds file/directory structure
>- Metadata
>- File-to-block mapping
>- Access permissions
>- etc
>- Periodic communication with data nodes (*Heartbeat & re-duplicate the lost files*)
>- Block rebalancing (*Evenly distribute data*)
>  
>  If the **name node data is lost**, then <b><span style='color:var(--mk-color-red)'>all data is lost</span></b> as there is no way to reconstruct them since the metadata is lost.
>  
>  There are methods to ensure resilience through backups & checkpointing.

**Assumptions** in HDFS
- Commodity hardware is used instead of "exotic" hardware for scaling out
- These machines have high component failure rates (*it should be resilient against hardware failures*)
- Quite a number of huge files
- Large sequential reads instead of random access

Its interface is similar to regular file systems.

>[!success] Optimised for high throughput access to data

>[!success] Suited for large datasets requiring batch processing

>[!failure] HDFS does not support file modification
>
>It is designed for write-once, read many
<div style="page-break-after: always;"></div>

## Writing Data

When a request is sent to write a file, the **name node** will first <b><span style='color:var(--mk-color-yellow)'>create the metadata</span></b> for the file, then it will <b><span style='color:var(--mk-color-yellow)'>tell the client where to store it</span></b>.

>[!question] Why does the name node not store the file itself?
>
>It is <b><span style='color:var(--mk-color-red)'>expensive to send the file to the name node</span></b> then straight to the data node.

It will inform the client of **3 data nodes** (*default is 3*):
1) On the **client's node** (*The local node closest to the user*)
2) On a **different node** but on the **same rack**
3) On a **different rack**

>[!success] This ordering balances locality & fault tolerance

Afterwards the client (*not you but is part of Hadoop*) will then **send each block**, to the <b><span style='color:var(--mk-color-yellow)'>first data node, which will then stream to the remaining 2 data nodes</span></b>.

>[!example] Example of the transferring process
>
>Lets say our file has 1 block and it was assigned to data nodes, 1, 4, 7.
>
>The client will just stream the block to data node 1, then data node 1 will stream to 4 then 4 will stream to 7.
## Reading Data

When asking to read data from a file, the name node will check in its directory if the file exist.

Then it will tell the client node which <b><span style='color:var(--mk-color-yellow)'>data nodes each block is being stored in</span></b>.

The client will then <b><span style='color:var(--mk-color-yellow)'>communicate with the closest data node</span></b>. In the event the data node is down or the block is corrupted it will move to the next closest data node.

>[!important] This is why the data nodes are assigned this way
>
>Having **3** (*or more*) **data nodes** to store 1 block ensures <b><span style='color:var(--mk-color-green)'>redundancy & fault tolerance</span></b>, in case of data corruption or failure of the data node.
>
>And the **way the data node is assigned**, enables <b><span style='color:var(--mk-color-green)'>locality</span></b>, by storing it as close to the client as possible.


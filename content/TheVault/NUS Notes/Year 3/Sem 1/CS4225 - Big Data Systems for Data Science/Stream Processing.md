---
title: Stream Processing
Date Created: 2025-10-17
Last Updated: 2025-11-01
tags:
  - CS4225
  - ApacheSpark/StreamProcessing
---
# Streams
---
In some cases **data** does not **arrive** all at once but <b><span style='color: #F0E68C'>over time</span></b> and in <b><span style='color: #F0E68C'>high volume</span></b>.

So in a **streaming approach** it is designed to <b><span style='color: #F0E68C'>process the input as it received</span></b>, which is different from offline or batch approaches that operate on the full data at once.

**Data enters** at a rapid rate from something called a <b><span style='color: #B0E0E6'>input port</span></b>.

>[!info] Input ports
>
>These can be like sensors, some TCP connection, file stream or message queue.

This **steam is possibly infinite**. This means that the data <b><span style='color: var(--mk-color-red)'>cannot store the entire stream accessibly</span></b> (*we don't have infinite space*). Thus the system will need to be able to process the data while receiving data.

>[!question] When to process the data?
>The <b><span style='color: #F0E68C'>interval to process the data matters</span></b>. **Too short**, then we might have <b><span style='color: var(--mk-color-red)'>a lot of overhead</span></b>
>
>**Too long**, then we might have a <b><span style='color: var(--mk-color-red)'>delay in getting processed data</span></b>.
## Stateful Stream Processing

We cannot just perform trivial record at a time transformations (*data comes in then just process*), we need the <b><span style='color: #F0E68C'>store and access intermediate data</span></b> to <b><span style='color: #98FB98'>ensure stability</span></b>.

This is because what if there are **issues** that occur which results in missed data or duplicated data being processed.

![[Stateful Stream Processing Example.png|center|250]]

So we can store a <b><span style='color: #B0E0E6'>local state</span></b> (*store the intermediate data at that time*) which can be <b><span style='color: #F0E68C'>accessed by many different places</span></b> (*databases, local files, variables*).

We can then <b><span style='color: #F0E68C'>push intermediate data into a persistent storage</span></b> to act as a <b><span style='color: #B0E0E6'>checkpoint</span></b>. So if any issues were to happen we can just get resume from the checkpoint.

>[!success] As reliable as a batch processing system

>[!success] Guarantee extract one processing
>It means that the data is <b><span style='color: #98FB98'>extracted and processed only once</span></b>.
# Spark Stream Processing
---
![[Structured Streaming Processing Model.png|center|350]]

Spark is initially designed for batch processing, **to handle streaming**, Spark will do something called a <b><span style='color: #B0E0E6'>micro-batch stream processing</span></b>.

>[!info] Micro batch
> Spark will <b><span style='color: #F0E68C'>accumulate a small sample of the stream input data</span></b> and this is called a micro batch.

Each of these **micro-batches** are then <b><span style='color: #F0E68C'>processed similarly in a distributed manner</span></b> (*and [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Stream Processing.md#Data Transformation|checkpointed]] as well*). 

>[!success] Quickly and efficiently recover from failures
>Each micro batch is a normal spark batch processing. Then **if some issue happens** then we will just carry out the normal [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Apache Spark.md#Lineage|spark error handling]].

>[!success] Deterministic nature ensures end to end exactly once processing guarantee
>Only once one micro batch finishes then it will move on to the next micro batch.
>
>And no double processing.

>[!failure] Latency of a few seconds
> Since we <b><span style='color: var(--mk-color-red)'>wait for the previous batch to finish</span></b> there will be latency.
> 
>It is ok for some application (*maybe some other part also cause delays*) but some others are not.

In Spark, the **data stream** is a <b><span style='color: #B0E0E6'>unbounded table</span></b>. Unlike batch processing where the table is of fixed size, here the <b><span style='color: #F0E68C'>size of the table will varies</span></b>.

To define a streaming query, there are **5 steps**:
1) Define input sources
2) Transform data
3) Define output sink and output mode
	- Output writing details
	- Where and how to write the output
4) Specify processing details
	- **Triggering details**: When to trigger the results
	- **Checkpoint location**: Where to store the streaming query process info for failure recovery
5) Start the query

>[!important] Just like in Spark, the input source must also be from a persistent storage

>[!info] All the optimisations Spark uses can be applied here
>
>We can also do performance tuning besides tuning the Spark SQL engine:
>- Cluster resource provisioning appropriately to run 24/7
>- Number of partitions for shuffles to be set much lower than batch queries
>- Setting source rate limits for stability, don't let the cluster be overwhelmed
>- Multiple streaming queries in the same Spark application
## Data Transformation 

There are 2 types of transformation:
1) **Stateless**

These types of transformations <b><span style='color: #F0E68C'>does not require information from previous rows or data</span></b>.

Basically only <b><span style='color: #F0E68C'>focus on the data that we have</span></b> currently. So functions like `select`, `map`, `filter`, `where` are stateless transformation.

2) **Stateful**

A stateful transformation is different, it <b><span style='color: #F0E68C'>requires data that was processed previously</span></b>.

So functions like `DataFrame.groupBy().count()` is stateful since we are using a pre existing data frame which stores some previous data.

So these <b><span style='color: #F0E68C'>already processed data is the state & is stored in memory</span></b>. It is also <b><span style='color: #98FB98'>checkpointed to tolerate failures</span></b> (*for Spark all machines will wait for checkpointing to finish before continuing the next micro batch*). 

>[!example] Example of a stateful transformation
>In a streaming processing pipeline if we want to count the number of words, we need to tally the sum with the already existing count of the word. This is stateful as we need data that was previously processed
## Stateful Streaming Aggregations

When doing **batch processing**, <b><span style='color: #F0E68C'>aggregations are not based on time</span></b> and can be categorised into 2 types:
1) **Global**

These are aggregations with <b><span style='color: #F0E68C'>no specified key</span></b> for example `data.groupBy().count()`. This <b><span style='color: #F0E68C'>results in all rows are aggregated into one group</span></b> (*basically its like not using any group by and doing count*).

2) **Grouped**

These are our usual <b><span style='color: #F0E68C'>aggregations with some specified key</span></b>.

However for **stream processing**, there is a <b><span style='color: #F0E68C'>extra element to consider and that is time</span></b>.
<div style="page-break-after: always;"></div>

### Time Semantics

Now we need to **define the window where we will process** the data.

![[Time Semantics Example.png|center|500]]

#### Processing Time

This means the <b><span style='color: #F0E68C'>time when the data is received</span></b> by the spark cluster.

If we take a look at the example above. Lets say our processing-time window uses 08:22 to 08:23. So <b><span style='color: #F0E68C'>any data received within this period will be considered as 1 batch</span></b>.

>[!important] The time depends on the Spark cluster server time

>[!success] Easier to process for Spark
>The spark cluster only needs to check when the data arrives, anything beyond the specified time will be in the other cluster.

>[!failure] The end result can be affected by many issues
> For instance **depending on the network**, the <b><span style='color: var(--mk-color-red)'>data might arrive at different timings</span></b> to the spark cluster.
> 
> There are also other factors like Spark's processing speed and network congestion, which <b><span style='color: var(--mk-color-red)'>might affect the final result</span></b> (*not deterministic*).
#### Event Time

This means the <b><span style='color: #F0E68C'>time when the event first happens</span></b>.

So taking the same example above with the same interval, when **data is transmitted** over it will <b><span style='color: #F0E68C'>contain the data and the timestamp</span></b> (*which is the event time*).

So in our event time window, 1 batch will consist of the 3 extra data packets which arrived after 08:23.

>[!important] This time depends on the user
>It is still a unique time stamp But most of the time it uses the standard UTC format.

>[!success] It gives a deterministic result
>Because it <b><span style='color: #F0E68C'>does not matter when the data arrives, it matters when the event happens</span></b> which determines the window it will be in.
>
>It <b><span style='color: #98FB98'>decouples the processing speed from the results</span></b>.

>[!failure] Spark needs to know how long more to keep the window open before processing
>
>One major issue is that even with event time, the <b><span style='color: var(--mk-color-red)'>data might arrive later</span></b> (*5 mins, 1hr*). So Spark needs to know <b><span style='color: #F0E68C'>how long more to wait for these latecomers</span></b>.

>[!failure] Extra overhead
>
>Instead of sending data we need to <b><span style='color: #F0E68C'>send the time the event happens</span></b> also. And during <b><span style='color: #F0E68C'>processing we need to check this time</span></b> also which adds to the computation process
### Window Types

Spark we can indicate the event time window as 2 types:
1) **Tumbling**

It is essentially <b><span style='color: #F0E68C'>partitioning of the time into intervals</span></b>, with no overlaps.

Sample command to have a 5 minute interval: `sensorReadings.groupBy("sensorId", window("enevtTime", "5 Minute")).count()`

2) **Overlapping**: More preferred

Here is the same but now the intervals <b><span style='color: #F0E68C'>can overlap one another</span></b>.

Sample command to have a 10 minute interval with a 5 minute sliding interval: `sensorReadings.groupBy("sensorId", window("enevtTime", "10 Minute", "5 Minute")).count()`

>[!info] This sliding interval is the window where the records get processed
> So every 5 minutes this 10 minute window will get processed.
#### Watermarks

When Spark stores data in windows it stores in memory, however since streaming data in infinite, <b><span style='color: var(--mk-color-red)'>it cannot always store it it memory</span></b> (*run out of space*), it will need to <b>remove drop some records</b>.

So can Spark balance, accuracy and feasibility, and thus they use something called <b><span style='color: #B0E0E6'>watermarks</span></b>. It essentially lets the <b><span style='color: #F0E68C'>user decide when the window can be closed</span></b> (*the missing data is acceptable by the user*).

![[Spark Watermark Example.png|center|600]]

The example above uses this command to have a 10 minute interval with a 5 minute sliding interval and a 10 minute watermark: `sensorReadings.withWatermark("eventTime", "10 minutes").groupBy("sensorId", window("eventTime", "10 Minute", "5 Minute")).count()`.

In general the command will be `<eventSource>.withWatermark("<timestampVarName>", <watermark timing>).groupBy.("<var you want to compute>", window("<timestampVarName>", "<interval>", "<overlap & add new interval>").<action like count, avg> ())`

How does Spark compute the watermark. At the **start of the interval** it will <b><span style='color: #F0E68C'>take the latest event time data received before this interval and minus the watermark interval</span></b>.

**Early records** if its outside of any window, <b><span style='color: #FFD700'>create a new window</span></b>.

>[!important] Any window which includes this watermark time will be kept in memory
>

>[!example] Example of computing the watermark
>
>**At time 12:15**, the latest data received is 12:14 (*event time*), it will then just minus 10 minutes which will give a watermark of 12:04.
>
>So in our example the windows for 12:00 - 12:10 **still reside in memory** to account for any latecomers. <b><span style='color: #F0E68C'>So even if data comes in at 12:01 which is before the watermark it will still be counted</span></b>.
>
>But **at 12:20**, the watermark will be 12:21 (*time in consistency*) minus 10 minutes which is 12:11 so the window for 12:00 - 12:10 will be **closed**
# Flink Stream Processing
---
A [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Stream Processing.md#Spark Stream Processing|downside]] to Spark when doing stream processing is its <b><span style='color: var(--mk-color-red)'>latency</span></b>. So **Flink** is developed to <b><span style='color: #98FB98'>achieve real time stream processing</span></b>.
## Event Driven Streaming Application

![[Event Driven Stream Processing Example.png|center|300]]

**Flink** follows an <b><span style='color: #B0E0E6'>event driven streaming processing</span></b> architecture. Flink <b><span style='color: #F0E68C'>only accepts inputs from event logs</span></b>, which are <b><span style='color: #F0E68C'>read only</span></b> (*persistent, cannot be removed for backup reasons*) using an index which are just pointers.

The output from a processing step can be into another event log as well.

>[!example] Another example of a event driven streaming platform is Kafka
>It provides a <b><span style='color: #F0E68C'>producer-consumer</span></b> concept. The event logs are a <b><span style='color: #F0E68C'>distributed system</span></b> and can be <b><span style='color: #F0E68C'>stored by different topics and data within topics</span></b> as well.
>
>![[Kafka Example.png|center|500]]

>[!success] Using event logs decouples senders & recrivers

>[!success] Provides asynchronous, non-blocking event transfer

>[!success] Exactly once consistency
### Evolution of Analytics Pipelines

**Traditionally** there will be distributed databases which stores data. And to do analytics on the entire database can be costly, so we use a <b><span style='color: #F0E68C'>ETL</span></b> (*extract transpose load*) to <b><span style='color: #F0E68C'>process the data into a data warehouse</span></b>.

Then any reports or dashboards can just fetch this preprocessed data from the data Wearhouse.

>[!fail] There is a single point of failure on the ETL
>
>If we **process** for a **short period** then there will be a <b><span style='color: var(--mk-color-red)'>lot of work</span></b> for the ETL.
>
>If it is **too long** then the data will <b><span style='color: var(--mk-color-red)'>not be in real time</span></b>.

Most people want a <b><span style='color: #98FB98'>real time data update</span></b> thus they move towards a <b><span style='color: #F0E68C'>streaming analytics application</span></b>. Where the <b><span style='color: var(--mk-color-turquoise)'>stream processor</span></b> will handle the data and then directly update the database or to the dashboard.

>[!note] It is not a must to change to a streaming analytics pipeline if the latency between updated data is acceptable
## Flink Dataflow Model

Flink essentially <b><span style='color: #F0E68C'>uses a dataflow graph</span></b> which just signifies a set operations to do and the order in which each operation is done.

In the graph:
- **Nodes** represent <b><span style='color: #F0E68C'>operators</span></b> (*functions or operations to do*) also known as <b><span style='color: #B0E0E6'>tasks</span></b>
- **Edges** denotes <b><span style='color: #F0E68C'>data dependencies</span></b> between 2 operations

**Example of a actual Flink dataflow model**:
![[Flink Dataflow Model Example.png|450]]

This is very similar to our [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/MapReduce.md#Basic MapReduce|MapReduce]]. The left half is our map and the right half is the reduce. So <b><span style='color: #F0E68C'>corresponding keys will be passed to the corresponding next operator</span></b>.

>[!Important] The reduce operators are stateful
>If we look at the example above when the first word (*Flink*) enters it will emit a count of 1 but when another similar word comes in it will emit a count of 2.
<div style="page-break-after: always;"></div>

## Flink System Structure

![[Flink System Structure.png|center|450]]

It is similar to [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Apache Spark.md#Spark Architecture|Spark]]:
1) The user will **submit an application**, known as a <b><span style='color: #B0E0E6'>job</span></b>
2) Then the dispatcher will start and send the application to the job manager
3) The job manager will **requests slots** to the resource manager
4) Resource manager will **register and allocate slots** amongst the task managers (*worker / executer*)
5) The job manager will take the allocated slots and **assign them tasks** (*do the task*)
6) The task manager **might** also need to **exchange data** within one another

>[!info] Slots
>They are a <b><span style='color: #F0E68C'>basic processing unit</span></b> in Flink. Each <b><span style='color: #F0E68C'>worker consist of multiple slots</span></b>, thus a worker can do multiple tasks.
### Task Execution

![[Task Manager & Slots Visualisation.png|center|450]]

So a **job** is like a dataflow model/graph which will then be <b><span style='color: #F0E68C'>distributed to multiple</span></b> <b><span style='color: #B0E0E6'>task managers</span></b> (*some machine to do work*).

Then each of these <b><span style='color: #F0E68C'>task managers has its own set of slots</span></b>, depending on the hardware (*CPU, memory*). So our **job manager** will <b><span style='color: #F0E68C'>assign a tasks to a set of slots</span></b>.

>[!success]  Parallelism
> So with the architecture it allows for:
> - **Data** parallelism: Data can be spilt into chunks to be processed by different slots
> - **Task** parallelism: Tasks (*operators*) can be done on different slots
> - **Job** parallelism: Multiple applications can be running so it can handle multiple execution of jobs (*different slots different jobs*)
<div style="page-break-after: always;"></div>

### Data Transfer in Flink

As mentioned previously sometimes **data will need to be exchanged between task managers**. This process is known as <b><span style='color: #B0E0E6'>network shuffle</span></b>.

![[Network Shuffling in Flink.png|center|500]]

This sending of data is similar to our [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Apache Spark.md#Dependencies|wide dependency transformation in Spark]]

All this is being <b><span style='color: #F0E68C'>handled by the task manager</span></b> where it takes care of sending data from the sending tasks (*the one that outputs the data*) to the receiving tasks (*the one that needs the data*).

However it is <b><span style='color: var(--mk-color-red)'>inefficient to keep sending data</span></b> , so <b><span style='color: #F0E68C'>each sender will maintain its own buffer</span></b> (*user configured*). Which will <b><span style='color: #F0E68C'>only send data once the buffer is full</span></b> (*this is independent*).

>[!success] This buffer reduces the network overhead

>[!question] What if the buffer never becomes full?
>Flink has its own <b><span style='color: #F0E68C'>timer</span></b>, which will force the sending of messages after a certain period of time.
## Event Time Processing in Flink

For Flink to do event time processing, <b><span style='color: #F0E68C'>each record must have an event timestamp</span></b>, like in Spark

>[!important] Flink also uses watermarks but this watermark is different from Sparks watermark
>The watermark in this case is <b><span style='color: #F0E68C'>provided by the application/user</span></b>. It is their <b><span style='color: #F0E68C'>best guess</span></b> on when all the records at a particular time stamp has arrived.
>
>Watermarks in Flink are <b><span style='color: #F0E68C'>special records which holds a timestamp as a long value</span></b>. So they flow in with the stream of data.

The **watermark** in Flink, indicates the <b><span style='color: #F0E68C'>event time in relation to the processing time</span></b> (*servers time*).

>[!example]  Example of a watermark
>Lets say at event time 12:06, a watermark comes in that has a timestamp of 12:02.
>
>This means that at 12:06 the event time is 12:02, meaning all the events before and equal to 12:02 should have arrived.

So how do we handle late event then? Flink has a **user configuration** called the <b><span style='color: #B0E0E6'>lateness horizon</span></b>. It just <b><span style='color: #F0E68C'>states at what event time interval can Flink still process late events</span></b>. Anything outside this range will not be processed at all.

>[!info] Users can also not allow early records to be processed.

**Example of Watermarks in Flink**:
![[Flink Watermark Example.png|center|600]]

Lets go through some examples:
- **On time**, the record at process time 12:05 has a event time of 12:00. This is on time because it is within our watermark of 12:02
- **Early**, the record at processing time 12:06 with event time 12:025 is considered early because the watermark at processing time 12:06 is 12:02 meaning this event came in earlier than expected. <b><span style='color: #F0E68C'>Flink will process & buffer the early data</span></b> if the user does not allow triggering of early data.
- **Late**, the record at processing time 12:065 with event time 12:01 is late because it is beyond the watermark of 12:02 at processing time time 12:06
- **Not processed**, assuming early events are allowed the event at processing time 12:085 with event time of 12:015 is late because it has exceed the lateness horizon of 12:04 to 12:08.
##  Checkpoint & State Management

Similar to Spark, <b><span style='color: #F0E68C'>each task will have its own state</span></b> that is stored in memory. Everything it receives an input it will fetch the existing state and do some computations.

Then the new value will be emitted and also send back to update the state.

And similarly, to **handle failures**, Flink will have <b><span style='color: #F0E68C'>a checkpoint mechanism</span></b> which uses a remote and persistent storage (*distributed or database*).

>[!info] During checkpointing other tasks can still operate
> This <b><span style='color: #98FB98'>reduces the delay</span></b> and also <b><span style='color: #98FB98'>decouples checkpointing from processing</span></b>.
### Flink's Checkpointing

In Flink **checkpoint** are <b><span style='color: #F0E68C'>managed by the job manager</span></b> (*master node*). It starts of by <b><span style='color: #F0E68C'>sending a "initiate checkpoint" to all input sources</span></b> (*basically to all the event logs*).

>[!important] As long as the checkpoint barrier is not in the source or task they can process as normal

![[Flink Source Checkpointing.png|center|450]]

> The **checkpoint messages are denoted as triangles**.

Once the **sources** see the initiate checkpoint message, it will then <b><span style='color: #F0E68C'>send its state to the remote storage</span></b> (*it is the index at where it has finish processing data*).

Afterwards **every single source** will each <b><span style='color: #F0E68C'>send a checkpoint barrier to all tasks</span></b>. And notify the job manager that is has completed checkpointing.

![[Flink Awaiting Barrier.png|center|450]]

Once a **task receives a checkpoint barrier**, it will first <b><span style='color: #F0E68C'>wait for all other barriers</span></b> from all the sources first.

>[!important] The incoming data will be processed still but the state will be captured and stored separately then the checkpointed state

![[Flink Task Checkpointing.png|center|450]]

Once the the task **receives all the checkpoint barriers**, it will then <b><span style='color: #F0E68C'>save their state to the remote storage</span></b>.

Then the tasks will emit a checkpoint barrier. The sink will receive this and sends it to the job manager to acknowledgement

>[!note] A checkpoint is successfully when all the tasks have acknowledge that their checkpoint was successful to the job manager
### Flink's State Recovery

So when a <b><span style='color: var(--mk-color-red)'>failure happens</span></b>, the <b><span style='color: #F0E68C'>whole application will be terminated and restarted</span></b>.

Once the application has been restarted it will then <b><span style='color: #F0E68C'>retrieve the last checkpointed state</span></b> (*the tasks gets the intermediate data while the source gets the index*).

>[!info] This is why the event log must be persistent
> Recall that the source index / pointer / offset is being checkpointed, so we can just go to that event and continue from there.


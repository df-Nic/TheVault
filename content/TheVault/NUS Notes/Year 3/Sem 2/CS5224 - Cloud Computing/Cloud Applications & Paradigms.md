---
Title: Cloud Applications & Paradigms
Date Created: 07-March-2026
Last Updated: 14-April-2026
Tags:
  - CS5224
  - SWE/CloudComputing/Paradigms
  - SWE/CloudComputing/Applications
  - BigData/MapReduce
  - BigData/Hadoop
  - BigData/ApacheSpark
---
# Cloud Applications
---
Recall that [[Year 3/Sem 2/CS5224 - Cloud Computing/Cloud Concepts & Models.md#Cloud Provider|cloud providers]], they provide:
- Basic & higher level services with different levels of abstraction (*IaaS, PaaS, SaaS*)
- Compute & storage resources (*Virtual servers, storage, networking*)
- Management services (*Load balancer, auto-scaling, monitoring, message queue*)

All this can be **accessed through a user interface** (*GUI or CLI*).

So as a developer who wants do **develop something on the cloud** (*enterprise computing*), ideally you want to <b><span style='color: #FFD700'>partition your application into n equal sized tasks that are independent</span></b>.

>[!question] Why partition into equal sized tasks?
>We want to <b><span style='color: #FFD700'>take advantage of parallelism</span></b>. This can <b><span style='color: #98FB98'>reduce execution time</span></b> by $1/n$.
>
>If not running things <b><span style='color: var(--mk-color-red)'>sequentially will be inefficient</span></b>.

Try and **avoid**, <b><span style='color: #FFD700'>complex workflows & multiple dependencies</span></b> (*finish something then do something else*), or applications with <b><span style='color: #FFD700'>intense communication</span></b> (*data communication*) among concurrent instances or if the workload <b><span style='color: #FFD700'>cannot be arbitrarily partitioned</span></b>.

>[!failure] Key challenges for both parties
>As a cloud **provider**, the challenge is to basically <b><span style='color: #FFD700'>maintain & manage</span></b> your application or system in addition to other people's one as well.
>
>As a cloud **consumer**, the challenge is to <b><span style='color: #FFD700'>consider many aspects</span></b> in developing software like:
>- **Performance isolation**, with [[Year 3/Sem 2/CS5224 - Cloud Computing/Virtualisation & Multitenancy.md|virtualisation & multitenancy]] when utilisation is high how do we <b><span style='color: #FFD700'>scale</span></b>
>- **Reliability**, using multiple servers to interact can lead to <b><span style='color: #FFD700'>high server failures</span></b> (*one fail everything goes down*)
>- **Latency / bandwidth fluctuations**, due to sharing of resources and potentially hosting somewhere far
>- **Data logging**, good to have to know what is happening, but this have <b><span style='color: #FFD700'>performance considerations</span></b> (*when & how much which determines how much space is needed*)
## Architecture Styles

In a typically cloud application, the <b><span style='color: #FFD700'>rely heavily on the internet and web technology</span></b>, because:
- Typically using the web is how you **access** the application for <b><span style='color: #98FB98'>high accessibility</span></b>.
- **Web browser universally** (*not everyone follows standards but make sure it works on the common ones*)
- <b><span style='color: #98FB98'>Ease of web-based service development</span></b>, simple way to **develop & manage** because the frontend will call the backend which is on a server ([[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Software Architecture.md#Client Server|client server architecture]])

So we will **focus on a web application architecture**:
![[Basic Web Server Architecture.excalidraw.png|center]]

By level:
- The **presentation** layer is the one where your <b><span style='color: #FFD700'>users will interact with your system</span></b> (*UI or CLI*), it <b><span style='color: #FFD700'>sits between client & server side</span></b>.
- The **application** layer is the <b><span style='color: #FFD700'>implementation logic</span></b> and it <b><span style='color: #FFD700'>receives client requests to execute from the web client</span></b>.
- The **data** layer comprises of <b><span style='color: #FFD700'>persistent data stores</span></b>, to be used by the web server to execute their tasks

So in terms of a **web service for cloud applications**:
- <b><span style='color: #FFD700'>Services are naturally distributed</span></b>, thus we requires message passing between multiple servers
- Services are accessed by different clients using different programming languages & technologies, thus we <b><span style='color: #FFD700'>require a standard interface for communication between clients & server</span></b>
### Communication Between Client & Server Side

To communicate there are **2 common protocols**:
1) **Simple object access protocol** (*SOAP*)
One of the first protocols to connect web services together. Defines a <b><span style='color: #FFD700'>common web service messaging format</span></b> for request & response exchanges based on XML & uses TCP or UDP as the transport protocols.

>[!info] SOAP has a very strict standards when it comes to structure and security features
>In terms of what data can be returned. But this <b><span style='color: #98FB98'>security</span></b> comes at a <b><span style='color: var(--mk-color-red)'>cost of flexibility</span></b>.
>

>[!success] String security

>[!failure] Heavyweight

>[!failure] Structure format to follow thus inflexibility

>[!example] Typically used for large enterprise application like bank applications

2) [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Software Architecture.md#Representational state transfer|Representational state transfer]] (*REST*)
It is **used for distributed hypermedia systems**, providing:
- Support for <b><span style='color: #FFD700'>communication with stateless servers</span></b>
- <b><span style='color: #FFD700'>Platform & language independent</span></b>
- Supports <b><span style='color: #FFD700'>data caching</span></b>

>[!success] Lightweight

>[!success] More flexible
>As you can now move different types of objects instead of following a standard structure (*not just XML can be JSON*).

<b><span style='color: #FFD700'>REST must follow these design principles</span></b>, if not they will just be a HTTP request:
1) **Uniform interface**, a standard way to communicate with the server
2) **Client server decoupling** (*client-server architecture*), client and server are separate from one another
3) **Stateless**, all requests are independent thus it does not need to store information (*like HTTP, but websites do remember through cookies*)
4) **Cacheability**
5) **Layered system architecture**, a layer only communicate with its neighbours and nothing more
6) **Code on demand** (*this is optional because browsers can block JavaScript or applets which disables executing code in the frontend*)
# Cloud Paradigms
---
Previously we did discuss on the following:
- IaaS
- PaaS
- SaaS

There are the **common widely used cloud paradigms** (*are just some pattern or model*). But currently now a new paradigm has gained popularity and that is <b><span style='color: #87CEEB'>function as a service</span></b> (*FaaS*).
## Function As A Service

It comes from the <b><span style='color: #FFD700'>world of functional programming</span></b> (*everything is just a function*).

>[!goal] Build scalable, reactive, event-driven applications
>[[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Event Driven Architecture.md|Event-driven applications]] are mainly application which reacts accordingly when something happens (*this something is called an event*). And typically the app should <b><span style='color: #98FB98'>react fast</span></b>.

The main idea is to <b><span style='color: #FFD700'>build functions as unit of deployment</span></b> (*functions are known as Lambda*). So when an <b><span style='color: #FFD700'>event happens it triggers a lambda function & exits after execution</span></b>.

>[!tldr] Lambda
>It is essentially another word for a particular function. It comes from [[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Static Analysis & Type Systems.md#Lambda Calculus|lambda calculus]].
>
>And 1 property of lambda function is that they are [[Year 3/Sem 2/CS5224 - Cloud Computing/Cloud Applications & Paradigms.md#Communication Between Client & Server Side|stateless]]
****

In FaaS, there are some **best practices**:
1) Functions should only <b><span style='color: #FFD700'>perform 1 action</span></b>
2) It should be <b><span style='color: #FFD700'>self-contained, do not call other functions</span></b> if not it will be not be lightweight
3) Because it must be self-contained, then it must use as <b><span style='color: #FFD700'>few libraries as possible</span></b>

>[!question] Why must it be self contained?
> FaaS is <b><span style='color: #FFD700'>good for real time applications</span></b>, so if it is not lightweight then it will take longer to run which causes delays.

In FaaS is <b><span style='color: #FFD700'>no idle capacity</span></b>, what it means is that when your application is idling, there is no infrastructure or resource to mange or pay, <b><span style='color: #FFD700'>only when a lambda function is activated then the resources will be provisioned</span></b>. So it <b><span style='color: #98FB98'>reduces cost</span></b>!

>[!success] So FaaS applications are lightweight
>Because we divide our application is divided into smaller, single-purpose functions (*small & contained*).

FaaS also has **other advantages**:
- <b><span style='color: #98FB98'>Lower provision time</span></b>
- <b><span style='color: #98FB98'>Low to none ongoing administration</span></b> (*providers provides this abstraction*)
- Allows for <b><span style='color: #98FB98'>elastic scaling</span></b> as each action is inherently scaled
- <b><span style='color: #98FB98'>No capacity planning</span></b> required (*scaling is handled by the provider*)
- <b><span style='color: #98FB98'>Low maintenance</span></b> (*providers does everything like PaaS*)
- <b><span style='color: #98FB98'>High availability</span></b> is inherent in the FaaS model (*managed by the provider*)
- <b><span style='color: #98FB98'>Resource utilisation is excellent</span></b> (*no idle capacity, so cost are less*)
- <b><span style='color: #98FB98'>Debugging is easier</span></b> in theory since functions are small

>[!fail] Limited ability to persist connection & states
>All this is kept in an external service or resource.

>[!fail] FaaS cannot work well if you want to do something complex
>FaaS model has <b><span style='color: var(--mk-color-red)'>resource limits</span></b> because we want to use as little libraries as possible to keep it light weight
### Serverless FaaS

>[!tldr] Serverless
>It is to build (*serverless*) applications <b><span style='color: #FFD700'>without the need to provision or manage servers</span></b>. And everything runs on a <b><span style='color: #FFD700'>per-use basis</span></b> (*only allocate when being used*).
>
>>[!important] This does not mean there is no server, eventually you need to have a server (*hardware*) to run everything

So we only <b><span style='color: #FFD700'>provide the functions</span></b>, there is **no VMs, containers infrastructure, servers** etc are all <b><span style='color: #FFD700'>managed by someone</span></b> else (*so lightweight again*) and it follows the <b><span style='color: #FFD700'>pay as you use</span></b> scheme (*pay when Lambdas execute*).

So our **vendors or providers** will provide the consumers with a <b><span style='color: #FFD700'>provision-free scalability solutions</span></b>.

>[!question] What are the use cases for Serverless FaaS?
>They are good for applications when we <b><span style='color: #FFD700'>need to react to something</span></b> (*typically real time*):
>- Real time data process
>- Virtual assistants
## How Lambda Works

We have a **lambda function** which is just your <b><span style='color: #FFD700'>application logic</span></b> (*some code you want to execute*).

Then we need to define a **configuration**, which is just <b><span style='color: #FFD700'>what event sources will invoke</span></b> these lambda functions. And these <b><span style='color: #FFD700'>events can have their own priority</span></b>.

>[!example] When the API gateway receives a HTTPS request

So now the **provider** will have a system to integrate event source with lambda function, manage infrastructure that detects events and invoke lambda.

So to **set up a lambda**, there are 3 steps:
1) Create the lambda service
	- Provide business logic
	- Configuration, region to run AWS credentials
	- Indicate what events to trigger the lambda function
2) Deploy service created
3) Invoke / test the service
## MapReduce Programming Model

**Supports** arbitrarily <b><span style='color: #FFD700'>divisible workload</span></b> & <b><span style='color: #FFD700'>distributed computing on large data sets on multiple machines</span></b> (*clusters, public or private clouds*).

Inspired by the map and reduce functions in functional programming languages.

>[!question] How large is the data?
>Web-scale data on the order of 100s of GBs to TBs to PBs. But is typically input data set will <b><span style='color: #FFD700'>not likely fit on a single computers hard drive</span></b> (*so we need a distributed file system*).

In general here is the **programme structure** of MapReduce:
1) **Read** (a lot of) data
2) **MAP** (*extract data you need from each record*)
3) **Shuffle** and Sort data
4) **REDUCE** (*aggregate, summarise, filter, transform extracted data, etc.*)
5) **Write** the results

>[!note] This paradigm is called same program multiple data
> Is because the master instance will split the data and the program will do the same thing just on different segments of the data.

### What is Actually Happening in MapReduce

![[Images/CS5224 Images/Hadoop's MapReduce.png|center]]

In [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/MapReduce.md|MapReduce]], an application will start the following components:
- **Master instance** (*handles your workers and mappers*)
- Start up $M$ number of worker instances for the **mapping phase** (*also known as worker nodes*)

So given a large input our master instance will **first** <b><span style='color: #FFD700'>partition the data into M segments</span></b> (*split*), then it will be passed as an <b><span style='color: #FFD700'>input to our mappers as a key value pair</span></b>.

>[!important] The partition or split size matters
>Initially as you increase the job size performance improves because parallelism utilises more machines.
>
>If its too **large** there ill be <b><span style='color:var(--mk-color-red)'>limited parallelism</span></b> (*not all  mappers will be utilised*). And it can be <b><span style='color: var(--mk-color-red)'>limited to the networks bandwidth</span></b>.
>
>If its too **small**, then there will be a <b><span style='color:var(--mk-color-red)'>high overhead of map tasks</span></b> (*overwhelm the master worker*).
>
>So all this boils down to <b><span style='color: #FFD700'>cost & speed</span></b>.

Our <b><span style='color: #87CEEB'>mapper</span></b> will then read the input and <b><span style='color: #FFD700'>process</span></b> it accordingly and <b><span style='color: #FFD700'>output a new list of key value pairs</span></b> which are <b><span style='color: #FFD700'>stored in the mappers local disk</span></b>.

>[!fail] It is slow because we are reading and writing from the local disk
>Spark solves this by storing intermediary results in memory.

Once **all of the map instances are done**, then the <b><span style='color: #87CEEB'>shuffling phase</span></b> begins, where our <b><span style='color: #87CEEB'>reducers</span></b> will <b><span style='color: #FFD700'>read from the local disk and merge values who's keys are assigned</span></b> to that reducer (*sort & merge*).

>[!success] We can reuse machines from the mapping phase in the reduce phase
>Because we are guarantee that all the map phase is finished before the reduce phase starts.
>
>But the number need not be the same.

Once **all the reducers are done**, the <b><span style='color: #FFD700'>final result is written to a shared storage server</span></b> ([[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Hadoop.md#Hadoop Distributed File System|HDFS]]). And the master instance will terminate the application.

>[!note] So all you need to provide what the mapper & reducer does
>The shuffle, merging and sorting is all done by the MapReduce system implementation

>[!success] Both the mappers and the reduces all run in parallel
### Hadoop & Apache Spark

So [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Hadoop.md|Hadoop]] (*or Apache Hadoop*) is an <b><span style='color: #FFD700'>open source version</span></b> for MapReduce, developed by Apache & Yahoo.

And this <b><span style='color: #98FB98'>allows for large scale analytics</span></b> through an analytics engine with a distributed storage layer.

Here is a **high level architecture** of Hadoop:

![[Hadoop Architecture.png|center]]

Then we also have [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Apache Spark.md|Apache Spark]], it is <b><span style='color: #98FB98'>fast</span></b> because it <b><span style='color: #FFD700'>stores intermediary data in memory</span></b> and thus can <b><span style='color: #98FB98'>react to real time data</span></b> or events for real-time & advance analytics.

>[!failure] If there is not enough memory then it will spill into the disk

And Spark can <b><span style='color: #FFD700'>run independently or on top of Hadoop</span></b>.

So in **summary**:

|       Feature        |    Apache Spark    | Hadoop (*MapReduce*) |
| :------------------: | :----------------: | :------------------: |
|   Batch Processing   |        Yes         |         Yes          |
| Real-time Processing |        Yes         |          No          |
|   Machine Learning   | Built-in (*MLlib*) | Need external tools  |

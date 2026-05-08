---
Title: Scalability
Date Created: 28-November-2025
Last Updated: 02-February-2026
Tags:
  - CS3219
  - SWE/Scaling
---
# What is Scalability?
---
So scalability is an [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Specifying Software Requirements.md#Classifying Quality Attributes|internal quality attribute ]]. And depending on your **choice** it has <b><span style='color: var(--mk-color-red)'>both hardware and software consequences</span></b>.

It is the <b><span style='color: #F0E68C'>ability to handle changing capacity</span></b>. Or in other words is the systems capability to handle a growing amount of work by adding recourses to the system. This is known as the <b><span style='color: #B0E0E6'>ability to scale</span></b>.

>[!info] Ability to scale
>It is the <b><span style='color: #F0E68C'>capability to handle growth</span></b> (*or increase its capacity*) in some dimension of operations specific to the application.
>
>For instance, number of requests than can be processed in a given time window, amount of data than can be managed and processed.

But it is not always about scaling up, we need <b><span style='color: #B0E0E6'>scaling down</span></b> as well. This is when there is **very little workload** at the moment, there is <b><span style='color: #F0E68C'>no need to keep having high resource allocation</span></b> (*basically don't waste money*).

>[!example] Example of hardware scaling
>To accommodate increased incoming data would mean adding disk capacity.

>[!example] Example of software scaling
>To accommodate increase number of transaction processed could mean architecting the application to use parallel and distributed computing.

And we also mentioned previously there are 2 types of scaling:
1) [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Specifying Software Requirements.md#Vertical Scaling|Vertical]]: <b><span style='color: #F0E68C'>Adding capability to machines</span></b> the software is deployed on
2) [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Specifying Software Requirements.md#Horizontal Scaling|Horizontal]]: <b><span style='color: #F0E68C'>Adding additional machines</span></b> (*nodes*) to the deployment

>[!question] Why do we need to scale?
>As time passes the applications <b><span style='color: var(--mk-color-red)'>volume might increase</span></b>, this means more customers, data, requests, etc.
>
>We need to manage this increase workload to <b><span style='color: #F0E68C'>keep the response time constant</span></b> (*if responsiveness is important*).
## Strategies To Scale

There are **2 ways** that we can scale:
1) <b><span style='color: #F0E68C'>Replicate</span></b> the resources to handle more capacity
2) <b><span style='color: #F0E68C'>Optimise</span></b> the available resources (*hashing, better algos, faster programming language*)

>[!note] If we were to replicate and add more servers we need a load balancer
>A [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Scalability.md#Load Balancer|load balancer]] is to ensure that the <b><span style='color: #98FB98'>requests is evenly distributed</span></b>. If not all requests will go to 1 server and defeats the purpose.
## Scaling Post-Hoc

It is <b><span style='color: var(--mk-color-red)'>very expensive to think about scalability post-hoc</span></b> (*after deployment*).

**Adding capacity after development** leads to <b><span style='color: var(--mk-color-red)'>downtime</span></b>, <b><span style='color: var(--mk-color-red)'>costs</span></b> to upgrade the database, <b><span style='color: var(--mk-color-red)'>increase effort</span></b> (*if you want to reimplement*).

>[!success] Best to think about it during the designing of the architecture
>This is because scaling is a architecture decision, incorporated from the beginning as an estimation of the evolution of the software.
# System Architecture & Evolution
---
Most systems start small first (*n-tier & hosted on a single server*). This is a [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Software Architecture.md#Monolithic|monolithic]] architecture.

So as the system grows in complexity when it becomes:
- Feature rich
- More requests & performance drops (*latency increase, insufficient resources*)
- Single server is overloaded (*bottleneck*)

>[!note] if the load stays the same or is relatively low there is no need to scale
## Scale-Up

It is essentially <b><span style='color: #F0E68C'>vertical scaling</span></b>, we <b><span style='color: #F0E68C'>upgrade the hardware</span></b>.

>[!example] Example of scaling up
>Upgrade the resource from 4 CPU & 16 GB RAM to 8 CPU & 32 GB RAM.

>[!success] Simple to do

>[!success] Supports larger network seamlessly

>[!failure] There is a limit on the number of CPU & memory one can add

>[!failure] Costly, it does require money

>[!warning] There is a short downtime when we want to upgrade the system
## Scale-Out

It is essentially <b><span style='color: #F0E68C'>horizontal scaling</span></b>, we <b><span style='color: #F0E68C'>replicate the service</span></b> and run multiple copies on multiple nodes.

![[Scale-Out Example.png|center|350]]

So if we have $R$ number of requests and $N$ server then each server will handle $R / N$ requests.
 
If we replicate we need 2 additional element to the design:
1) **Load balancer**
2) **Session store**

>[!success] Can keep adding new service instances

>[!success] Grows request processing capacity

>[!success] Resilient to failures
>If we face an error, not everything is lost, only whatever happen in that session (*replica in the session store*)
>
>Also if a service fails another service can pick it up.

>[!failure] Single database capability limits response time
>Now the <b><span style='color: var(--mk-color-red)'>database becomes the bottle neck</span></b>.
>
>We can solve this using, [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Scalability.md#Caching|caching]] or scaling the [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Scalability.md#Scaling The Database|database]]
### Load Balancer

**All requests** go through this load balancer. Then the load balancer will <b><span style='color: #F0E68C'>choose which service replica will process the requests</span></b>.

Its goal is to ensure that <b><span style='color: #98FB98'>each replica is equally busy</span></b>.

Then lastly, it will <b><span style='color: #F0E68C'>route the response back</span></b> to the correct user.

>[!example] Example of load balancers
>- **Off the shelf**: Nginx
>- **Cloud provider**: AWS elastic load balancing
### Session Store

When a user **interacts** with the **application** a **user session** is created to <b><span style='color: #F0E68C'>keep track of the session state</span></b> and <b><span style='color: #F0E68C'>identify the sequence of user interaction</span></b>.

If the **server stores the state** then we are <b><span style='color: #F0E68C'>like assigning 1 user to 1 service</span></b>. And if its request is sent to another service then things will go wrong. This we <b><span style='color: var(--mk-color-red)'>cannot scale horizontally</span></b>.

If the **user stores the state** then we might be <b><span style='color: var(--mk-color-red)'>leaking sensitive information</span></b>, <b><span style='color: var(--mk-color-red)'>data tampering</span></b> or not enough memory.

>[!info] Essentially we are trying to make our services stateless

So by <b><span style='color: #98FB98'>decoupling the handling of the state</span></b>, our services will just need to <b><span style='color: #F0E68C'>access this state in the session store</span></b>, to handle requests (*does not matter which service handle the request*).
### Caching

To solve the limitation with scaling-out, we can employ caching, if we <b><span style='color: #F0E68C'>do not change the data frequently</span></b>. 

We can <b><span style='color: #F0E68C'>store frequently retrieved and commonly accessed</span></b> database results in memory.

Caching can be done on the backend, frontend & even the middleware.

This allows for <b><span style='color: #98FB98'>quick retrieval without burdening the database</span></b>.

Here is the processing logic:
- If the data is in the distributed cache, retrieve and return
- If not then query the database and load the results into cache

>[!important] Depending on the data we need to decide when to remove data from the cache to prevent state results

# Scaling The Database 
---
One issue with horizontal scaling is that the <b><span style='color: var(--mk-color-red)'>database becomes the bottleneck</span></b>. So now we want to scale our database.
## Scaling Up & Out The Database

So **scaling up** essentially is to use a <b><span style='color: #F0E68C'>bigger and more power datastore</span></b>. However this is not a good solution.

>[!failure] Single point of failure

>[!failure] The growth of the database exceeds the processing capability of a single node

>[!failure] High latency
>We need low latency database access. If we only have 1 centralised database then different clients around the world will <b><span style='color: var(--mk-color-red)'>face network issues</span></b> (*latency*).

So instead use [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Distributed Databases.md|distributed database]](*scaling out*). One solution is to use <b><span style='color: #B0E0E6'>read replicas</span></b>. Essentially we have <b><span style='color: #F0E68C'>one or more database which acts as a read only</span></b> database, these are called <b><span style='color: #B0E0E6'>secondary databases</span></b>.

Then we will have <b><span style='color: #F0E68C'>1</span></b> <b><span style='color: #B0E0E6'>primary database</span></b> which all the writes goes into.

So then the <b><span style='color: #F0E68C'>changes are asynchronously replicated</span></b> into the secondaries and these <b><span style='color: #98FB98'>secondaries can be deployed in different regions</span></b>.

>[!note] This follows the [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Microservices.md#Command Query Responsibility Segregation (CQRS)|CQRS pattern]]
>And obviously the tradeoff is that <b><span style='color: var(--mk-color-red)'>sometimes the data is not sync</span></b> yet but <b><span style='color: #F0E68C'>eventually it will be synced</span></b>.

>[!success] If the primary goes down people can still read the data
>No data is lost since there are backups.
>
>And in this scenario there will be a mechanism like a queue to store all the write requests.
## Partitioning The Data

We can <b><span style='color: #F0E68C'>distribute the database over multiple independent disk</span></b> partitions and database engines.

We can do <b><span style='color: #B0E0E6'>horizontal partitioning</span></b> where it <b><span style='color: #F0E68C'>splits the logical table</span></b> (*by row*) into multiple physical partitions such as:
- Value based (*by location / region of the data bring created*)
- Hash function
- Primary key

There is also <b><span style='color: #B0E0E6'>vertical partitioning</span></b> where we <b><span style='color: #F0E68C'>partition by columns</span></b>, so for instance:
- All the static data columns in 1 partition
- Read only data is in 1 partition
- Columns that are dynamic data in another partition

>[!important] The database engine takes care of all these partitioning and putting all the data together.

>[!note] All these partitions should be stored in different databases
## Scaling Using Distributed Databases

Here we <b><span style='color: #F0E68C'>increase the number of storage nodes</span></b>, which <b><span style='color: #F0E68C'>stores copies of the data</span></b>.

So as mention in the [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Scalability.md#Scaling Up & Out The Database|scaling-out of databases]]there is a mechanism to ensure that the data is consistent since there is 1 database to write and the rest to read

>[!success] Improves availability

>[!failure] We need to maintain consistency
## Scaling Processing With Multiple Tiers

![[Scaling Processing With Multiple Tiers Example.png|center]]

Essentially we have a <b><span style='color: #F0E68C'>multi tiered application</span></b>, where an application <b><span style='color: #F0E68C'>calls another dependent services that has its own load balancer</span></b>.

Essentially all services use some <b><span style='color: #F0E68C'>core service that provides the database access</span></b> (*backend for frontend (BFF) pattern*).

This extends, statelessness, load-balanced, cached architecture (*basically just adding another tier that is stateless, load-balanced and cached*). 

We can extend this by <b><span style='color: #F0E68C'>assigning different tiers to different load balanced services</span></b>.

>[!success] Provide high performance and availability
> Since each service is cached and load-balanced. And all this can be scaled depending on the load.

>[!failure] Account for code complexity
# Why Do We Scale
---
## Increase Responsiveness

The reason we scale is to ensure responsiveness of the application is satisfied. We use things like caching or message brokers to achieve this.

But we can also improve responsiveness by **doing persistence to the database later**. This means we can <b><span style='color: #F0E68C'>process the request than any changes to the data which needs to be updated can be done later</span></b>.

>[!example] Example of not fully persisting in the database
>Lets say you place an order but you changed your address. The software can just accept the new address and update the address after the request is processed.

So events are sent to the backend and the data can be <b><span style='color: #F0E68C'>stored in a remote queue to be written to the database</span></b> since <b><span style='color: #98FB98'>writing to queue is faster than to the database</span></b>.
## Fault Isolation

We <b><span style='color: #98FB98'>replicate to ensure there is no single point of failure</span></b>. There might be degraded performance when some services goes down but the whole app still runs!

![[Swim Lane Architecture Example.png|center|400]]

Usually <b><span style='color: #B0E0E6'>swim lanes or Pod architecture</span></b> for fault isolation. It essentially <b><span style='color: #F0E68C'>categorised groups of users to a set of services, servers and databases</span></b>. So if it <b><span style='color: #98FB98'>does go down, it will not affect ALL users</span></b>.

>[!important] Failure should be contained & not go beyond the boundary

>[!success] Easy fault detection within the swim lane

>[!success] Fault isolation

>[!success] Meet expectation of region-specific requirements

>[!success] Faster response time from a customer-specific perspective
>Since they are allocated to this set of databases and servers which can be also near where the user is (*low latency*).
# Scale Cube
---
![[Scale Cube.png|center]]

**X-axis**: <b><span style='color: #F0E68C'>Scale horizontally</span></b> by running multiple copies of the application with a load balancer.

**Y-axis**: Split the application into multiple different functions / services (*like microservices, AKA functional decomposition*).  So if we <b><span style='color: #F0E68C'>scale we can just scale the specific service</span></b>.

**Z-axis**: It runs the same code, but it runs on the different parts of the data. So it <b><span style='color: #F0E68C'>uses distributed data storage</span></b> (*can be location base, customer base etc*).

>[!note] If you do y-axis you might want to incorporate x and z axis scaling as well
>As there is <b><span style='color: var(--mk-color-red)'>no point to put all the services into 1 server</span></b> is the same as not scaling.
>
>But it is <b><span style='color: #98FB98'>easy to do z-axis with y-axis</span></b>. Because we can do database per service and each service is independent thus it is the same as z-axis.


---
title: Microservices
Date Created: 2025-10-07
Last Updated: 2025-10-13
tags:
  - CS3219
  - SWE/Architecture/MicroServices
---
# Microservices Architectural Style
---
A microservice application is a <b><span style='color: #F0E68C'>collection of smaller services</span></b> (*offers a well-defined business capability/user needs*) and when combined solves a big problem.

>[!important] Business capabilities are one of the ways to identify microservices

Each of them offers a <b><span style='color: #F0E68C'>well-defined business capability</span></b> (*aligned with the business needs or user requirements*), with a <b><span style='color: #F0E68C'>limited scope</span></b>.

**Each microservice** are developed and deployed <b><span style='color: #F0E68C'>independently</span></b> (*not in silos since they need to communicate with one another*). Other services won't be influenced by how other services are developed, allowing <b><span style='color: #98FB98'>development to be done in parallel</span></b>.

>[!note] Software principals which Microservices follows
>- [[Year 2/Sem 1/CS2103 - Software Engineering/Design Principles.md#Separation of Concerns|Separation of concerns]]
>- [[Year 2/Sem 1/CS2103 - Software Engineering/Designing A Software.md#Coupling|Loose coupling]]
>- [[Year 2/Sem 1/CS2103 - Software Engineering/Designing A Software.md#Cohesion|Strong cohesiveness]]

These microservices **communicate** with each other through <b><span style='color: #F0E68C'>well defined mechanisms</span></b> (*API calls*).

>[!note] When we say well defined, it means we specify what it should do
>
>For example, our question service should have the capability to fetch a question and bring it to the collaboration service.
## Microservices Characteristics

A microservice is a **architectural style** that structures an application as a **collection of services** that are:
- Organised around business capabilities
- Loosely coupled (*there is still some coupling due to the communication*)
- Owned by a small team (*due to limited scope of the service*)
- Independently deployable
### Organised Around Business Capabilities

Microservice offers a <b><span style='color: #F0E68C'>well-defined business capability</span></b> (*all the features / requirements*) and their **boundaries** (*what they can and cannot do*) are closely <b><span style='color: #F0E68C'>aligned with business capabilities</span></b>.

This is something like divide and conquer, where the big application is spilt into smaller segments.

>[!example] Example using a online retail solution
>**Domain**: Online retail domain
>
>So it consist of solutions like warehouse, finance, customers, delivery
>
>2 of these boundaries can be:
>1) **Warehouse**: Which handles the orders, the stock, the preparation of delivery
>2) **Finance**: Handles financial reports, payroll, company accounts

>[!success] High cohesiveness
>When we design a service, its **features** should be <b><span style='color: #F0E68C'>highly related</span></b> and they have their own defined <b><span style='color: #F0E68C'>responsibility allocated</span></b> (*a functional requirement*). And this follows the [[Year 2/Sem 1/CS2103 - Software Engineering/Design Principles.md#Single Responsibility Principle|single responsibility principle]]
### Developed & Deployed Independently

#### Development

Once we segregate the responsibilities to the various services, development can be done **independently**. This means that between each service, it <b><span style='color: #F0E68C'>does not share any code</span></b> or requires <b><span style='color: #F0E68C'>implementation from other services</span></b>.

Decisions & development are handled by <b><span style='color: #F0E68C'>small teams</span></b>, which are <b><span style='color: #F0E68C'>cross-functional</span></b> (*different specialisations like UI, DB, backend*). Being cross-functional allows the <b><span style='color: #98FB98'>service to be owned by the team</span></b>.

>[!warning] What if the team is not cross-functional?
>
>Then we will end up with a [[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Modeling and Software Architecture.md#Layered Architecture|layered architecture]]. This is because a team will be in charge of one component of the whole service, for instance UI, DB and backend. 

>[!abstract] 2-pizza teams
>Small teams can be formed based on this idea, where only 2 pizza's are required to feed the whole team.

So because they are independent, **each microservice can have its own**:
- Deployment
- Resources (*CPU, memory, I/O, manpower, etc*)
- Scaling
- Monitoring requirements
#### Deployment

Similar to a monolithic deployment, we can deploy it as such:
- Deploy multiple services on the host (*physical or virtual machine*)
- Deploy each services instance as a Java virtual machine process (*JVM*)
- Deploy multiple service instances in the same JVM

There are also certain **patterns** for deployment of microservices:
1) **Service instance per host**
This means that we will run each service instance in <b><span style='color: #F0E68C'>isolation</span></b> on its own host. Thus they will <b><span style='color: #98FB98'>have all the resources</span></b> on that machine.

2) **Service instance per container**
Each service instance runs on its <b><span style='color: #F0E68C'>own container</span></b>. The container image <b><span style='color: #F0E68C'>consist of applications and libraries</span></b> required to run the service.

This is <b><span style='color: #98FB98'>scalable</span></b> as we can just create another container to handle more traffic.

3) **Service instance per VM**
Package each service in a <b><span style='color: #F0E68C'>virtual machine</span></b> (*EC2, AMI*). Each service instance is a VM that is launched using that VM image.

>[!info] An VM image is just a configuration of the resources you need to launch the service
### Well-Defined Communication Mechanisms

When all the services are deployed it needs to be able to **communicate with one another**, and these communications can be either <b><span style='color: #F0E68C'>synchronous</span></b> (*Blocking / waiting*) or <b><span style='color: #F0E68C'>asynchronous</span></b> (*Not blocking*).

**Examples of async and sync communication**
![[Sync & Async Communication Examples.png|center]]

>[!note] For asynchronous communication there is a intermediary where it holds data that another service will receive
>This intermediary is known as a event bus or event queue.
# Discovering Microservices
---
Before developing a microservice architecture we **need to know what microservices are needed**.
## Domain Driver Design (DDD)

It is a <b><span style='color: #F0E68C'>domain centric approach</span></b> to software design. DDD is not a process but more of a philosophy where it **gives** us a collection of:
- **Patterns**
- **Principles**
- **Practices**

This allows us to determine software designs.

>[!success] Good for complex problem domains

>[!success] Can manage complexity

>[!success] Create software that closely reflects business needs
### Domain Model

Each business has a <b><span style='color: #B0E0E6'>business space</span></b> which is the critical and fundamental or foundational <b><span style='color: #F0E68C'>concept behind the business</span></b> (*for LeetCode, is to help people prepare for technical interviews*)

<b><span style='color: #B0E0E6'>Domains</span></b> on the other hand is a specific area of <b><span style='color: #F0E68C'>functionality or business capability</span></b> (*example, e-commerce*). 

In the context of the business is the <b><span style='color: #B0E0E6'>problem space</span></b> which is essentially the <b><span style='color: #F0E68C'>problem that we intend to solve</span></b>.

How do we <b><span style='color: #F0E68C'>represent this domain</span></b> such that we can find solutions is through a <b><span style='color: #B0E0E6'>domain model</span></b>. It is an <b><span style='color: #F0E68C'>abstraction of the necessary information to solve the problem</span></b> (*some diagram*).

>[!important] In DDD we do not think about the solution but the problem space

Now when looking into problem domain model, <b><span style='color: #FFA07A'>avoid seeing it as a single unified system</span></b>. Instead look at it as a <b><span style='color: #F0E68C'>collection as multiple smaller domain models</span></b> (*smaller problems*) known as <b><span style='color: #B0E0E6'>sub-domains</span></b>.

>[!info] This sub-domain reflects some of the business organisation's structure

Sub-domains can be categorised into 3 types:
1) **Core**: It is <b><span style='color: #F0E68C'>key to the business</span></b> without it there is no business, this is usually <b><span style='color: #F0E68C'>developed in-house</span></b> since it is <b><span style='color: #F0E68C'>something that differentiates</span></b> you from others thus this component should not be leaked to others
2) **Supporting**: It is something needed for the application to run but it is <b><span style='color: #F0E68C'>not a differentiator</span></b>. It can be <b><span style='color: #F0E68C'>outsourced</span></b>
3) **Generic**: Not specific to the business (*Usually use off-the-shelf software*)

>[!important] The domain model should be kept isolated from technical complexities

**Example of a domain model**:

![[Domain Model Example.excalidraw.png|center|500]]
### Bounded Context

Now we want to develop a software to solve the problem so the <b><span style='color: #F0E68C'>solution space of the domain model</span></b> is known as the <b><span style='color: #B0E0E6'>bounded context</span></b>.

It essentially the <b><span style='color: #F0E68C'>objects, functionality & events</span></b> that is required within a sub-domain. And within each bounded context it <b><span style='color: #F0E68C'>can have relationships</span></b> (*collaborations*) between other bounded context.
#### Collaboration Between Bounded Contexts

These collaborations can happen in various ways:
1) **Shared kernel**
It is where 2 contexts are developed independently but <b><span style='color: #F0E68C'>overlap in some subset of each other's domain</span></b>.

>[!example] Example of a shared kernel collaboration
>So given 2 contexts, they might rely on the same set of data and both of them are connected to use the same database.

>[!failure] Makes both services highly coupled

2) **Upstream-downstream**

![[Upstream-Downstream Example.png|center|500]]

The 2 contexts are in a <b><span style='color: #F0E68C'>provider-consumer relationship</span></b>.

Here <b><span style='color: #B0E0E6'>upstream</span></b> is the <b><span style='color: #F0E68C'>provider</span></b> and the <b><span style='color: #B0E0E6'>downstream</span></b> is the <b><span style='color: #F0E68C'>consumer</span></b>. This is done using a API endpoint.

>[!success] Less couped than shared kernel

But we can do better by using a <b><span style='color: #F0E68C'>conformist relationship</span></b>. So lets use the example above, instead of the recommendation context contacting the order context, the order context can <b><span style='color: #F0E68C'>publish data into a centralised database</span></b>, which the recommendation context will access.

>[!success] This is the least coupled
> Since the recommendation context has <b><span style='color: #98FB98'>no control in the order service</span></b>, it is conforming to what the order service is giving and can only act on what is provided.
#### Interactions Between Contexts

Interactions should <b><span style='color: #F0E68C'>model the interactions in the real domain</span></b>.

However we need to consider a few things:
- Do we need to send all the information? Can we omit some?
- Can we minimise the number of interactions between contexts?
- Should the context be interacting with this other context or should it be done by another context? (*decoupling a context from one context*)
- Use asynchronous communication? (*like a pub sub system or event bus*)
## Event Storming

It is <b><span style='color: #F0E68C'>lightweight process</span></b>, where you can **directly think of the solutions** (*in the domain space*) to the problem.

<span style='color: #B0E0E6'>Domain events</span> are some <b><span style='color: #F0E68C'>event that occurs in the domain</span></b> & is relevant. And these events record some sort of <b><span style='color: #F0E68C'>state change</span></b>.

>[!note] These events are immutable, it cannot be changed
>You <b><span style='color: var(--mk-color-red)'>do not update or change the previous event</span></b> you just continue and update the state accordingly.

>[!example] Examples of events
>- Product added to cart: Here the state of the cart is updated
>- Payment card submitted: The state of the system will be changed to know that the payment details are entered

By **identifying events** that can happen, it will allow you to <b><span style='color: #98FB98'>solve the problem</span></b>.

To **trigger an event** we need a <b><span style='color: #B0E0E6'>command</span></b>. These commands can come from the user or from the system.

Now when a command is trigger and some event happens we need to know what <b><span style='color: #F0E68C'>data or objects we will be working on</span></b> this is known as an <b><span style='color: #B0E0E6'>aggregate</span></b> (*can have more than 1 per bounded context*).

>[!info] Policies
>Sometimes after an event happens it triggers another command, this is known as a policy.
>
>It is like if something happens do something. And it also can connect between bounded contexts.

**Example of event storming**:
![[Event Storming Example.excalidraw.png|center]]

So this <b><span style='color: #98FB98'>helps with separating the boundaries</span></b> with the different concepts, thus we can draw the boundary context (*thus identifying the services and their boundaries*). 

So here are some key pointers for even storming for microservices:
- Requirement analysis helps in the discovery of domain events.
- Be sure that your <b><span style='color: #F0E68C'>command/event are coming from a business need</span></b>.
- Don’t be too much influenced by the CRUD approach while extracting your domain events.
- <b><span style='color: #FFA07A'>Do not assume</span></b> that **microservices boundaries are synonymous** with the aggregates or bounded context from DDD or Event Storming.
- Microservices <b><span style='color: #F0E68C'>boundaries evolve over time</span></b>
# Data Patterns
---
Microservices are developed and deployed **independently**. This sounds like there is no coupling but however there is. Services might have <b><span style='color: var(--mk-color-red)'>interdependence due to co-ownership of data</span></b> (*relies on data from another service*).

>[!question] So why not just let each microservice have their own database?
>The <b><span style='color: #F0E68C'>general guideline is that each microservice owns their data</span></b>.
>
>However this still has some issues for instance <b><span style='color: var(--mk-color-red)'>data consistency</span></b> (*update, delete*) and <b><span style='color: var(--mk-color-red)'>data duplication</span></b> (*storing overlapping data*).

Thus in terms of microservices when we talk about <b><span style='color: #B0E0E6'>data independence</span></b>, it does not mean each microservice owns a database but rather, microservices <b><span style='color: #F0E68C'>should not modify the same data</span></b> as much as possible (*reading is fine*).

We can exploit the database to try and achieve this:
- **Private-tables-per-service**: Each services <b><span style='color: #F0E68C'>owns a set of tables</span></b> which only they have access to
- **Schema-per-service**: Each service <b><span style='color: #F0E68C'>has a database schema</span></b> that is private to that service

However **enforcing restrictions at a database level** comes with a downside which is that the choice of database <b><span style='color: var(--mk-color-red)'>might not be suited for some services</span></b>.

## Database-Server-Per-Service Pattern

It is very simple where <b><span style='color: #F0E68C'>each service has its own database server</span></b>.

>[!success] Enforces loose coupling
>Excludes the REST API which is required for communication.

>[!success] Allows scaling at the database level

>[!success] Easy to replace the underlying database technology for each service

>[!failure] Bad for large applications
>Large applications might have <b><span style='color: #F0E68C'>a lot of services</span></b> and thus an <b><span style='color: var(--mk-color-red)'>explosion in the number of databases</span></b>.

>[!failure] Deal with different kinds of databases
>Each service can use the database that they need (*relational, graph, vector, etc*)

>[!failure] Expensive & unmanageable
## Shared Database

>[!warning] This is an antipattern

Here all the <b><span style='color: #F0E68C'>data is stored into 1 database</span></b> and when data is required a join is done on multiple tables.

So all the updates and queries will all go into this one database. We can also <b><span style='color: #F0E68C'>restrict users from doing certain queries</span></b>.

The [[Year 2/Sem 2/CS2102 - Database Systems/Creating and Populating Tables with Constraints.md#Constraints|ACID]] properties should be enforced if this were to be used.

>[!failure] Development-time coupling
>If there is a <b><span style='color: #F0E68C'>change in the schema</span></b>, then it will affect other services.

>[!failure] Interfere with one another during runtime when updating the data
>When multiple clients updates the same data at the same time then it may cause an issue.

>[!failure] Chosen database may not satisfy the needs of all services
## Data Lake Pattern

![[Data Lake Pattern Example.png|center|550]]

Each microservice will have their own database, however there is now a <b><span style='color: #F0E68C'>read only data sink</span></b> (*or data lake*).

This data sink will <b><span style='color: #F0E68C'>contain data from all the relevant microservices</span></b> through a **messaging infrastructure**.
- Only the relevant data is steamed to the data lake
- Any changes to the data, this change can then e streamed to the data lake

The **data aggregated** in the data lake is <b><span style='color: #98FB98'>optimised for query-ability</span></b>.

>[!success] Keeps the advantages of database-server-per-service pattern

>[!success] Reduces coupling from services which it has data dependency with
>Each service can have their own data base and the reading of data from these services are done separately in the data sink.
## Saga Pattern

>[!info] This is more of handling data transactions rather than the data itself

In a **distributed system** it can be <b><span style='color: var(--mk-color-red)'>difficult to maintain the ACID properties</span></b> of the databases.

How can we ensure consistency when modifying data across services? In terms of the ACID properties, we can ensure that as long as <b><span style='color: #F0E68C'>one part of the transaction fails to execute, the entire transaction gets cancelled</span></b>.

However in an actual application when something happens we cannot just simply invalidate what was done we need some sort of <b><span style='color: #B0E0E6'>compensating action</span></b>.

This is what the **saga pattern** does, for every transaction there is a defined compensating action.

>[!important] This rollback however is not immediate

>[!info] Compensating action
>It is essentially what are the <b><span style='color: #F0E68C'>actions to be taken if some transaction fails</span></b>.

These **compensating actions are registered** on something called a <b><span style='color: #B0E0E6'>routing slip</span></b>, which is passed along to the next step and will be used to execute the actions when a failure occurs.

>[!important] Saga is not an ACID transaction
>Saga does not promise that when a roll back happens the system will return to the initial state, but it is <b><span style='color: #F0E68C'>brought back to a reasonably compensated state</span></b> instead.

**Example of the saga pattern**:
![[Saga Pattern Example.png|center|400]]

>[!question] Why only it is reverted back to a reasonably compensated state?
>When we look at [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Microservices.md#Event Sourcing|events]] in a system is facts that happen (*immutable*), we can't say that this event happen and then later say this event did not happen.

So who will handle these compensation actions:
- <b><span style='color: #F0E68C'>Create a service</span></b> just to handle these compensation actions
- Have each <b><span style='color: #F0E68C'>service handle their own</span></b> compensation actions

Here the <b><span style='color: #F0E68C'>sequence of the compensation action matters</span></b>, is like saying notifying the client that a refund is made but the refund is not done.

But a **guideline when ordering** these compensation actions is that harder to compensate actions if possible (*if the business allows it*) move it to the end of the transaction. 

>[!example] Example of a hard to compensate action
>For instance, if we were to send an email to the user for every compensation action that was done, why not just do it at the end and send 1 email.
# Event Sourcing & CQRS
---
These 2 patterns are usually used together, however if you are using CQRS you are definitely using event sourcing (*but not the other way round*).

These 2 are not completely related to data and they are 2 different patterns.
## Event Sourcing

>[!question] What are events?
>It <b><span style='color: #F0E68C'>represents a state change</span></b> in the application. It indicates that something has happen and thus is <b><span style='color: #F0E68C'>immutable</span></b>.
>
>Events are also a <b><span style='color: #F0E68C'>source of truth</span></b>.

Given a **current system state**, it is the result of <b><span style='color: #F0E68C'>a series of consecutive events</span></b>. If we were to **save all these events** in some <b><span style='color: #F0E68C'>append only event log</span></b> or store then we will have a comprehensive audit of exactly what the system did.

But more importantly we will <b><span style='color: #F0E68C'>have a mechanism to undo</span></b>. We can either go back to a previous state or rederive the current state through the logs alone.

>[!info] Event sourcing is a data storage pattern

Event sourcing is not about persisting the state of the application but <b><span style='color: #F0E68C'>focusing on persisting the state of events</span></b> (*events in the solution space*).

>[!tldr] Event sourcing vs relational modeling
>In **relational or NoSQL**, it <b><span style='color: #F0E68C'>stores a state</span></b> of something at that given time, where as **event sourcing** <b><span style='color: #F0E68C'>stores the events</span></b> which allows the system to easily derive the current state from the initial state.
## Command Query Responsibility Segregation (CQRS)

There are 2 things that can happen:
1) The user does some action which <b><span style='color: #F0E68C'>writes</span></b> to the event log (*command*), it <b><span style='color: #F0E68C'>changes the application state but returns no data</span></b>
2) The other is to request for the current state, this is a <b><span style='color: #F0E68C'>read</span></b> (*query*), it <b><span style='color: #F0E68C'>returns data but does not change the application state</span></b>

So in **CQRS**, it <b><span style='color: #F0E68C'>separates the write and reads</span></b>.

![[Overview of CQRS.png|center|400]]

How it works is that all the **writes** will <b><span style='color: #F0E68C'>go into a event log</span></b> (*example, Kafka*). Then when a **query** comes we can generate a [[Year 2/Sem 2/CS2102 - Database Systems/Nested Queries.md#Copying a Table|materialised view]] by using <b><span style='color: #DDA0DD'>KSQL</span></b> and the given <b><span style='color: #F0E68C'>event stream</span></b>.

![[Command & Query Model Example.png|center]]

There is a **command model** to <b><span style='color: #F0E68C'>processes these events and update the database</span></b> and a **query model** to <b><span style='color: #F0E68C'>handle the queries</span></b>.

<b><span style='color: #98FB98'>Multiple views can be precomputed</span></b> to match the various queries that can happen.

**Kafka, is a pub sub system** where there are **listeners** which will <b><span style='color: #F0E68C'>take the interested parts of the events and update the view accordingly</span></b>.

>[!success] If something goes wrong, the internal state of the database can be recovered from the log

>[!success] Read and writes can be optimised independently
>Since reads and writes are decoupled they can be <b><span style='color: #F0E68C'>scaled independently</span></b>.

>[!success] A single write model can push data into many read models or materialised views

>[!success] The read model can be in any database or a range of different databases

We can <b><span style='color: #F0E68C'>split the state database into write and read databases</span></b> and use a synchronising mechanism to ensure everything is in sync.

>[!success] Database can be optimised for read or writes

>[!failure] If you try to read right after a write the state might not be there
>The view might not have been generated but <b><span style='color: #F0E68C'>eventually it will be generated</span></b>.
# Other Patterns
---
>[!info] These patterns are more about communication & routing
## Service Communication

When we create multiple services we want some mechanism for them to **interact with one another**. As mentioned before it can be [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Microservices.md#Well-Defined Communication Mechanisms|either synchronous or asynchronous]].

In the <b>typical request response</b> type of communication is <b><span style='color: #F0E68C'>synchronous</span></b>. Because when the client sends a request it <b><span style='color: var(--mk-color-red)'>waits for a response</span></b>.

Another mechanism is a **notification** (*one way request*). It sends a request to a service and <b><span style='color: #F0E68C'>no reply is expected or sent back</span></b>.

Then there is also a **asynchronous request response** type of communication. As the name suggest it is <b><span style='color: #F0E68C'>asynchronous</span></b>. The client still expects a response but the <b><span style='color: #98FB98'>client don't need to wait</span></b> and can do other things.
## API Gateways

This is another pattern where it <b><span style='color: #F0E68C'>gets these requests to the correct services</span></b>. It encapsulates the internal system architecture and <b><span style='color: #F0E68C'>provides an API that is tailored to each client</span></b>.

>[!info] You can think of it as a gateway or entry point to your various services
>Then the API gate way will route the request to the corresponding services.

This is not only for <b><span style='color: #F0E68C'>client service communication</span></b> (*external to internal*) but it can also be used for <b><span style='color: #F0E68C'>service to service communication</span></b> (*external to external*). And it need not be only 1 gateway **you can use 2 gateways**.

There can be **other functionalities** built into the gateway as well such as:
- **Authentication**
- **Monitoring**
- **Load balancing**
- **Caching**
## Service Collaboration

When we want **2 services to collaborate** with each other there are 2 mechanisms to do this:
1) **Orchestration**
2) **Choreography**

>[!info] Orchestration
>It <b><span style='color: #F0E68C'>relies on a central component</span></b> (*the brain*) to guide and drive the process.

>[!info] Choreography
>We **need some mechanism to initiate the request**. But the services <b><span style='color: #F0E68C'>once they get the information they will work out the details by themselves</span></b>.
>
>For instance the controller can publish and event and the services and subscribe to this event and then do the necessary actions when they see an event.
>
>It can be <b><span style='color: var(--mk-color-red)'>hard to enforce ordering</span></b>.

For **orchestration** if you want to have some **ordering** in the tasks that are done then the <b><span style='color: #F0E68C'>"brain" will handle it</span></b>. But for **choreography** it is a bit different we will <b><span style='color: #F0E68C'>need multiple events to signal the service</span></b> to either wait or they can continue.
## Service Discovery

Now our Gateway needs to know how does it communicate with the different services. It <b><span style='color: #F0E68C'>needs to know the location</span></b> which is some IP address and port (*assigned to service once its set up*).

Once a new service is discovered, there should be a <b><span style='color: #B0E0E6'>service registry</span></b> which <b><span style='color: #F0E68C'>keeps track of the known service instances</span></b> it encounters (*on startup or developer manually fill this up*).

There are some patterns for service discovery:
1) **Client-side discovery**
The <b><span style='color: #F0E68C'>client will determine</span></b> the network location of the available service instance. It will <b><span style='color: #F0E68C'>query the service registry and does it own load-balancing</span></b> algorithm to select a service.

>[!success] No middleman thus faster

>[!success] Good for internal microservice within the same cluster

>[!failure] Coupling between registry

>[!failure] Each client has its own logic to query and load balancing

2) **Server-side discovery**
The request will go to the <b><span style='color: #B0E0E6'>load balancer</span></b> (*NGINX plus or AWS elastic load balancer*) will query the service registry and then <b><span style='color: #F0E68C'>choose the correct service instance</span></b> to send the request to.

>[!note] So similar to client side discovery where the service registry is used to register and deregister service instances

>[!success] Simpler client

>[!success] Less coupled
>Since there is a centralised load balancer to do the rerouting

>[!failure] Load balancer is now the bottleneck
### Service-registry

For both of these to work we need a service registry.

So when a service gets deployed, **someone must take the address of this and register it**.

This can be done in 2 ways:
1) **Self-registration pattern**: Which is done by the service itself
2) **3rd party registration pattern**: A 3rd party registers the service instances

Then the client or <b><span style='color: #F0E68C'>router will just query this service registry</span></b> (*needed for both user and server side discovery*) to find the available instances of the service.

This **service registry** will <b><span style='color: #F0E68C'>check the status</span></b> of the service and if it is <b><span style='color: var(--mk-color-red)'>down it will deregister the service</span></b>.

>[!info] Registrar
>For **3rd party registration patterns**, there is a registrar which <b><span style='color: #F0E68C'>checks the status</span></b> of the service with the given address (*constant pinging*).
>
>Then they will update the status accordingly.
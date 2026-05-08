---
title: Modeling and Software Architecture
Date Created: 2025-02-10
Last Updated: 2025-09-28
tags:
  - CS3213
  - SWE/Architecture
  - SWE/SoftwareDesign
---
# System Modeling
---
The goal is to <span style='color:var(--mk-color-yellow)'>develop abstract models</span> of a system. In requirement elicitation, modeling is not important but is useful in developing software.

In **plan-driven development** it is <span style='color:var(--mk-color-yellow)'>emphasized heavily</span>, while in **agile development** it is more <span style='color:var(--mk-color-yellow)'>lightweight</span> (*model just enough*).

They are developed as part of:
- **Requirement engineering**: Help derive detailed requirements of the system
- **System design**: Describe the system to engineers implementing the system
- **Documentation**: Document system structure & operation

> [!note] Modeling is about abstractions
> When modeling we <span style='color:var(--mk-color-yellow)'>leave out details</span> to make the system <span style='color:var(--mk-color-green)'>easier to understand</span>. It is not a **representation** which <span style='color:var(--mk-color-yellow)'>describes how to implement</span> it.

To **create abstractions** we can take <span style='color:var(--mk-color-orange)'>different perspectives</span>:
- **External perspective**: Context or environment of the system
- **Interaction perspective**: Interactions between system & environment or system & components
- **Structural perspective**: Model the organization of a system or the data structure processed by it
- **Behavioral perspective**: Model the dynamic behavior of the system & how it responds to events
## Modeling Languages
### UML Diagrams

Also known as <span style='color:var(--mk-color-turquoise)'>unified modeling language</span>, a widely known modeling language proposed in the context of plan driven development.

> [!question] Why UML?
> - **Provides various levels of abstraction**
> - Widely-known modeling language
> - No need to reinvent & explain notations
> - A lot of tool support
> - Absorb previous standards

Some <span style='color:var(--mk-color-orange)'>common & popular diagrams</span> are:
- [[Models#Class Diagram|Class diagrams]]: Shows the show the object classes in the system and the associations between these classes
- [[Models#Sequence Diagrams|Sequence diagrams]]: Shows the interaction between different options and the data passed between them 
- [[Models#Activity Diagrams|Activity diagrams]]: Shows the activities involved during system execution 
- [[Models#Use Case Diagram|Use case diagrams]]: Diagrams shows the interactions between system & its environment a more visual representation of [[Project Requirements#Use Case|use cases]]
#### State Diagrams

It is a <span style='color:var(--mk-color-yellow)'>behavioral model</span>, which focuses on <span style='color:var(--mk-color-yellow)'>system states</span> and the <span style='color:var(--mk-color-yellow)'>events that causes transitions</span> in the states.

![[State Diagram Example.svg|center]]
### C4

It is developed for <span style='color:var(--mk-color-yellow)'>software architectures</span>, it consists of <span style='color:var(--mk-color-orange)'>hierarchical diagrams & abstractions</span>:
- **System context**: Its a starting point to show how the <span style='color:var(--mk-color-yellow)'>system fits into the world</span> around it (*user interaction*)
- **Containers**: <span style='color:var(--mk-color-yellow)'>Zooms into the software</span> and show high level technical building blocks (*database, web app*)
- **Components**: <span style='color:var(--mk-color-yellow)'>Zooms into a container</span> and shows the components inside (*building blocks of containers*)
- **Code**: *Optional* but it zooms into a components and show the code to implement it

This diagram should be <span style='color:var(--mk-color-yellow)'>self-describing</span> (*use appropriate images like the standard database symbol*).
# Software Architecture
---
> [!info] Architecture
> It is how the <span style='color:var(--mk-color-yellow)'>whole system is designed</span>, in terms of the **components** and the **decisions made**.

> [!info] Conway's law
> Architecture not only prescribes the structure of the systems being developed but also <span style='color:var(--mk-color-yellow)'>influences the structure of the team/organization</span>.
> 
> If there are 3 teams, it is most likely there will be 3 components.


> [!failure] Software design is not software architecture
>  **Software architecture** is <span style='color:var(--mk-color-yellow)'>part of software design</span>, while **software design** also <span style='color:var(--mk-color-yellow)'>includes other parts</span> (*detailed class design*).

In a **waterfall model**, system architecture and design are <span style='color:var(--mk-color-yellow)'>all emphasize</span> in the early stages.

In a **agile model**, architecture should only <span style='color:var(--mk-color-yellow)'>focus on the high level to mitigate risk</span> as **changing architecture later** will be <span style='color:var(--mk-color-red)'>expensive</span>.

> [!quote] Big design up front is dumb, no design up front is even dumer

There are <span style='color:var(--mk-color-turquoise)'>architecturally significant requirements</span> (*ASRs*), which have a <span style='color:var(--mk-color-yellow)'>measureable impact on the architecture</span>. These requirements are **mainly non-functional**.

> [!note] Representing architecture
> We can use <span style='color:var(--mk-color-turquoise)'>block diagrams</span> to informally model a system architecture.
>
> > [!example] Architecture block diagram example
> > ![[Architecture Block Diagram Example.png|center|400]] 
> > Here a **block** represents a <span style='color:var(--mk-color-yellow)'>component</span> while an **arrow** represents <span style='color:var(--mk-color-yellow)'>data or control flow</span>.
> 
> **Other models** which can be used are <span style='color:var(--mk-color-blue)'>UML</span> or <span style='color:var(--mk-color-blue)'>C4</span> diagrams

> [!note] 20 minute rule
> **Designing an architecture** requires a lot of <span style='color:var(--mk-color-red)'>domain knowledge and experience</span>.
> 
> You can learn from others or other projects for a very long time or can follow this 20 minute rule which just states to <span style='color:var(--mk-color-yellow)'>learn something new about the field for 20 minutes</span> (*videos, papers, projects, colleagues*).
## Reasons to Carry Out Architecture Modeling

### Quality Attributes

For a system to meet its  [[Requirements Gathering#Quality Attributes|quality attributes]] <b><mark style='background:var(--mk-color-yellow)'>depends on the architecture</mark></b>.

> [!example] Some results of having a good architecture
> 1) **High performance** requires managing time based behavior of components and their access to shared resources
> 2) **Modifiability** requires assigning responsibilities to components and limit their interaction, so that a change ideally affects only a single component
> 3) **Safe and secure** systems require safeguards and recovery mechanisms
### Modifiability

We need to ensure **modifiability** for future developers to <span style='color:var(--mk-color-yellow)'>maintain or improve</span> on an existing software. Having a <span style='color:var(--mk-color-green)'>good architecture will improve on its modifiability</span> (*only local or non-local at least*).

There are <span style='color:var(--mk-color-orange)'>3 categories of changes</span>:
1) **Local change**: Only a single component is affected (*add a function, or a new rule*)
2) **Non-local change**: Multiple elements are affected
3) **Architectural change**:  Affects the whole system as it affects how elements interact
### Communication

As mentioned architecture is modeling is an abstraction of the system, thus it is a basis for <span style='color:var(--mk-color-yellow)'>mutual understanding, negotiating, forming consensus</span>, and communicating with each other.

Non-technical people are also more likely to understand the architecture to the extent they need to.
### Other Reasons

- An architecture is the key artifact that allows the architect and the project manager to <span style='color:var(--mk-color-yellow)'>reason about cost and schedule</span>
- An architecture can be created as a <span style='color:var(--mk-color-yellow)'>transferable, reusable model</span> that forms the heart of a product line
- Architecture based development focuses <span style='color:var(--mk-color-yellow)'>attention on the assembly of components</span>, rather than simply on their creation
- By restricting design alternatives, architecture channels the creativity of developers, <span style='color:var(--mk-color-yellow)'>reducing design and system complexity</span>
- An architecture can be the foundation for training of a new team member
- The analysis of an architecture enables <span style='color:var(--mk-color-yellow)'>early prediction of a system’s qualities</span>
- The architecture is a carrier of the earliest, and hence<span style='color:var(--mk-color-yellow)'> most fundamental, hardest to change design decisions</span>
- An architecture <span style='color:var(--mk-color-yellow)'>defines a set of constraints</span> on subsequent implementation
- The architecture <span style='color:var(--mk-color-yellow)'>dictates the structure of an organization</span>, or vice versa
- An architecture can provide the <span style='color:var(--mk-color-yellow)'>basis for incremental development</span>
## Approaching Architecture

It can be a <span style='color:var(--mk-color-red)'>complex activity</span> to design an architecture (*many aspects*). It also **involves tradeoffs**, where some quality attributes might conflict one another.

![[Approaching Architecture Example.svg|center]]

> [!info] Architectural tactics
> Assign <span style='color:var(--mk-color-yellow)'>decision that influences</span> a [[Requirements Gathering#Quality Attributes|quality attribute]].

> [!info] Architectural patterns
> A <span style='color:var(--mk-color-yellow)'>establish architectural solution</span>, which typically comprise <span style='color:var(--mk-color-yellow)'>multiple architectural tactics</span>.
### Attribute-Driven Design (ADD)

ADD is a <span style='color:var(--mk-color-yellow)'>systematic</span> way of software architecture, **each iteration** you <span style='color:var(--mk-color-yellow)'>address</span> an <span style='color:var(--mk-color-yellow)'>architecturally-significant requirement</span>.

![[Attribute Driven Design Example.png|center|450]]

There are <span style='color:var(--mk-color-orange)'>7 steps</span>:
1) Get all the ASRs
2) Establish a iteration goal (*what ASRs do you want to accomplish*)
3) Choose an existing structure within the architecture to refine / improve
4) Select multiple possible designs that satisfy the ASRs, the <span style='color:var(--mk-color-red)'>hardest part in ADD</span> (*use design concepts*)
5) Give the structure (*should be high level*) some context (*components, layers*)
6) Record the design decisions (*what was said or written to come to this conclusion*)
7) Check if it addresses the goal in part 2 (*can involve other people to validate*)

We will **repeat** this process <span style='color:var(--mk-color-yellow)'>until the design is good enough</span>

> [!success] Advantage of ADD
> It is <span style='color:var(--mk-color-green)'>applicable to both agile and plan driven</span> settings.
# Architecture Patterns
---
### Big Ball of Mud

It is not really a pattern but an <span style='color:var(--mk-color-red)'>antipattern</span> (*avoid as there is a lack of architecture*). Doing this will result in <span style='color:var(--mk-color-red)'>poor maintainability & extensibility</span>.

However this is <span style='color:var(--mk-color-orange)'>quite common</span> because:
- Lack of architectural design
- Business pressure to come up with a product quickly
- Erosion of architecture over time
### Layered Architecture

It is similar to the [[Designing A Software#N-Tier Style|n-tier architecture]] where different <span style='color:var(--mk-color-yellow)'>components are grouped into a cohesive set of services</span> called <span style='color:var(--mk-color-turquoise)'>layers</span>.

The **placement of the layer is important** as only a <span style='color:var(--mk-color-yellow)'>layer can use layers</span> **directly beneath** it, which means a <span style='color:var(--mk-color-yellow)'>layer provides an interface</span> for the **layers above**.

> [!info] Layer bridging:
> Sometimes a <span style='color:var(--mk-color-yellow)'>layer might use another layer not directly beneath</span> it this is known as layer bridging.
> 
> This might violate the constraint which may be due to performance issues.

> [!summary] Advantages & disadvantages of layered architecture
> > [!success] Benefits
> > - **Portability**: Layers can be general or specific to an OS or environment (*file management, 1 layer implementation for Linux 1 for Windows*)
> > - **Reusability**: Reuse lower layers in other applications
> > - **Modifiability**: If the interface does not change, the layers can be modified without affecting upper layers
>
> > [!failure] Tradeoffs
> > - **Performance**: Needs to traverse down many layers (*call overhead*)
> > - **Progress blocking**: Higher levels need lower level abstractions which is not provided
> > - **Portability & modifiability**: A result from **layer bridging** which can prevent this
### Pipe-and-Filter Architecture

> [!info] Filter
> They are **processing components** that takes an <span style='color:var(--mk-color-yellow)'>input and produce an output</span> (*transform, filter or enriched data*).
> 
> They should be <span style='color:var(--mk-color-yellow)'>stateless</span> and make <span style='color:var(--mk-color-yellow)'>no assumptions based on other filters</span> (*independent*).

> [!info] Pipes
> They <span style='color:var(--mk-color-yellow)'>connect multiple filters together</span> signifying **data flow** from 1 filter to another.

> [!summary] Advantages & disadvantages of layered architecture
> > [!success] Benefits
> > - **Modifiability**: Filters are independent and can be modified freely
> > - **Reconfigurability**: Filters can be combined in different ways
> > - **Evolution**: Adding additional filters for future implementation is easy
>
> > [!failure] Tradeoffs
> > - **Data formatting**: A standard format of data transfers must be agreed on since we are passing data from 1 filter to another, we cannot have random data formats
> > - **Performance**: Every transformation (*filter*) will need to parse inputs and format to the agreed upon output which can be time consuming
### Model-Centered Architecture

Instead of components interacting with one another, there will be a <span style='color:var(--mk-color-yellow)'>central mode which all components talk</span> to (*repository*). This is also known as a <span style='color:var(--mk-color-turquoise)'>repository style</span>.

> [!summary] Advantages & disadvantages of model-centered architecture
> > [!success] Benefits
> > - **Modifiability**: All components are independent and do not need to know about others
> > - **Consistent data**: All data is managed in 1 place thus it will be consistent
>
> > [!failure] Tradeoffs
> > - **Single point of failure**: If the central node fails then the whole software fails
> > - **Performance**: Distributing the repository can be difficult
### Model View Controller

MVC can be seen as an **instantiation of a model-centered architecture**.

There are <span style='color:var(--mk-color-orange)'>3 main components</span>:
1) **Model**: Like your classes or components & updates the view
2) **Controller**: For user interaction and updates the model accordingly
3) **View**: Renders the presentation of the model (*UI)

> [!attention] View & controller depends on the model and not each other

> [!summary] Advantages & disadvantages of MVC
> > [!success] Benefits
> > - **Modifiability**: View & controllers are independent, also they can be added any time
> > - **Centralized state management**: The states can be managed and persisted 
> > - **Concurrency**: Views & controllers can run on their own threads or processes
>
> > [!failure] Tradeoffs
> > - **Not good for simple UIs**: MVC is not good as it significant add up-front complexity
> > - **Not good for complex UIs**: A change in the model will require change in views using the same model
### Microkernel Architecture

Also known as a <span style='color:var(--mk-color-turquoise)'>plug-in architecture</span>, there is a **base system** (*microkernel*) with some <span style='color:var(--mk-color-yellow)'>main functionality</span> and then we can add in **plug-in components** to <span style='color:var(--mk-color-yellow)'>add on more functionality</span>.

The components can be <span style='color:var(--mk-color-green)'>added at any time</span> and this architecture is <span style='color:var(--mk-color-green)'>good for products installed as a single monolithic deployment</span>.

> [!summary] Advantages & disadvantages of microkernel architecture
> > [!success] Benefits
> > - **Modifiability**: Plug-ins can be be evolved independently from the microkernel as long as the interface do not change
> > - **Extensibility**: Plug-ins provide a controlled mechanism to extend a core product
> > - **Testability**: Plug-ins can be tested by different groups of people, not necessary the developers of the microkernel
>
> > [!failure] Tradeoffs
> > - **Vulnerability & security**: Since plug-ins can be developed by different organisation it can introduce vulnerabilities & privacy threats
### Monoliths

They are typically a <span style='color:var(--mk-color-yellow)'>single deployable unit</span>.

They can distinguish architecture from a distributed architecture (*microservices or SOA*).
### Client-Server Architecture

There will be a **main server** which <span style='color:var(--mk-color-yellow)'>provides services simultaneously</span> to multiple distributed clients (*like a database you request data from it*).

The <span style='color:var(--mk-color-yellow)'>client will request services</span> from the server and the server will response accordingly (*server never initiate communication*).

This architecture consist of <span style='color:var(--mk-color-orange)'>2 types of functionality</span>:
1) **Discovery functionality**: There needs to be a protocol to allow the client to find the server and communicate with it
2) **Interaction functionality**: How to interact with the server and what the server will return

> [!success] Benefits of client-server architecture
> - **Low coupling**: Between server and clients as the connection is established dynamically, which the server has no prior knowledge of its clients
> - **Scalability**: Both server functionality and number of clients can be easily scaled (*all depends on the server*)
> - **Independent**: Both client & server can evolve independently
### Service-Oriented Architecture

Focuses on <span style='color:var(--mk-color-yellow)'>services which are separately deployed</span>, these services can belong to different systems & organisations (*Amazon interact with bank system when paying*).

This **interaction** is done through <span style='color:var(--mk-color-yellow)'>interfaces and the network</span>. They can also <span style='color:var(--mk-color-yellow)'>provide dynamic service discovery</span>.

> [!success] Benefits of server-oriented architecture
> - **Deployability**: Services can be individually managed
> - **Testability**: Services can be individually tested
> - **Reliability**: If one service goes down, others might still be up & running
### Microservice Architecture

Unlike service-oriented, these are services which <span style='color:var(--mk-color-yellow)'>communicate through service interfaces</span> (*organization based*).

Typically they are <span style='color:var(--mk-color-yellow)'>stateless</span> & developed by small teams and code bases.

**Service dependencies** are typically <span style='color:var(--mk-color-yellow)'>acyclic</span>.

> [!summary] Advantages & disadvantages of microservice architecture
> > [!success] Benefits
> > - **Deployability**: Quick time to market deployability
> > - **Independent**: Each team is in charge of 1 service and they decide their own technology choices
> > - **Scalability**: More services can be dynamically added
>
> > [!failure] Tradeoffs
> > - **Network communication overhead**
> > - **Complex transactions**
> > - **Different technologies**: It has varying maintenance cost
> > - **Design & maintainence**: Designing & maintaining can be challenging
# Architectural Tactics
---
As mentioned tactics are decision which influences a quality attribute.

We **cannot solely rely on patterns**:
- The pattern might not solve the problem
- Might need to modify & adapt existing systems
- It often emerges as a series of smaller decisions
- Tactics make them more systematic
## Availability Tactics

![[Availability Tactics.png|center|450]]

> [!abstract] Some tactics to detect faults
> - **Monitor**: Monitor various components of the system (*example using a system monitor*)
> - **Heartbeat**: Periodic message exchange between a system monitor and a process being monitored
> - **Sanity checking**: Checks the validity of specific operations or their output based on

> [!abstract] Some tactics for preparation & repair
> Preparation and repair tactics are based on a variety of combinations of <span style='color:var(--mk-color-yellow)'>retrying a computation or introducing redundancy</span>.
> - **Redundant spare**: One or more duplicate components can step in if a component fails
> - **Rollback**: Revert to a previous, known good state
> - **Software upgrade**: In service upgrade in a non service affecting manner

> [!abstract] Some tactics for reintroduction
> Reintroduction occurs after a <span style='color:var(--mk-color-yellow)'>repaired component is re introduced</span>.
>
> - **Shadow**: Operate a component in a “shadow mode” while being monitored d before reverting it back to an active mode
> - **Escalating restart**: Automatic restart at different granularities (*example lowest level might clear caches, while highest one restarts the whole system*)

> [!abstract] Some tactics for preventing faults
> - **Removal from service**: Temporarily placing a system component in an out of service state to mitigate potential faults (*example suspected memory leak*)
> - **Transactions**: Provide ACID properties (*atomic, consistent, isolated, and durable*)
> - **Increase competence set**: set of states in which the program can “competently” operate
## Performance Tactics

![[Performance Tactics.png|center|450]]

> [!info] Manage work requests
> In cases where the system <span style='color:var(--mk-color-red)'>cannot maintain adequate response levels</span> (*frame or bit rate*), <span style='color:var(--mk-color-yellow)'>sampling frequency can be reduced</span> (*reduce work load*).

> [!info] Limit event response
> If **events arrive too quickly**, the system might <span style='color:var(--mk-color-red)'>not be able to respond</span>, we can simply <span style='color:var(--mk-color-yellow)'>queue</span> them, <span style='color:var(--mk-color-yellow)'>set a delay </span>or just <span style='color:var(--mk-color-yellow)'>discard them</span>.
> > [!question] When to discard and why?
> > One advantage of discarding is that <span style='color:var(--mk-color-green)'>performance and adherence will be predictable</span> for those being processes.
> >
> > To drop a process it <span style='color:var(--mk-color-yellow)'>requires a policy</span> and will require notifications.

> [!info] Maintain multiple copies of data
> The idea of **data replication**, involves <span style='color:var(--mk-color-yellow)'>keeping separate copies</span> of the data to <span style='color:var(--mk-color-green)'>reduce the contention from multiple simultaneous accesses</span>.
> 
> For example redundant array of independent disks (*RAID*), where RAID 1 mirrors a disk (*creates an exact copy*).

> [!info] Schedule Resources
> The [[Process Scheduling|OS has various scheduling]] tasks.
> - **First in, first out (FIFO)**: Simplest policy where tasks are served in order, however long task might block all other tasks
> - **Fixed priority scheduling**: Assigns different kind of requests a particular priority and assigns requests in priority order
> - **Round robin scheduling**: Orders the task by priority and assigns a fixed time unit to it before continuing with the next

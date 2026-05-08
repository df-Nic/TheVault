---
title: Designing A Software
Date Created: 2024-09-23
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE
  - SoftwareDesign
---
# What Does it Mean to Design
---
To design is the process of **transforming a problem into a solution**, this <span style='color:var(--mk-color-orange)'>solution is called design</span>.

There are <span style='color:var(--mk-color-orange)'>2 main aspects</span> to **software design**:
1) **Product/external design** - <span style='color:var(--mk-color-yellow)'>Design external behavior</span> to meet user requirements
2) **Implementation/internal design** - Design how to **implement the product** to <span style='color:var(--mk-color-yellow)'>meet external behavior requirements</span>

When designing essentially there are **2 parts to consider**, <span style='color:var(--mk-color-yellow)'>high-level and low level design</span>.
- **High level** would be the different components needed like `logic`, `ui`, `storage`
- **Low level** would be the classes and functions inside of the components.

There are <span style='color:var(--mk-color-orange)'>2 design approaches</span>:
1) **Top Down** - **High level first** then flesh out lower levels. <span style='color:var(--mk-color-green)'>Good for big systems</span> as the high level design needs to be stable.
2) **Bottom Up** - **Low level first** then put them together to create high level systems. Good when <span style='color:var(--mk-color-green)'>designing for an existing system</span> or <span style='color:var(--mk-color-green)'>re-purposing exiting components</span>.
3) **Mix** - Top down approach first but **when designing low levels switch to bottom up**.

There is also another approach called <span style='color:var(--mk-color-turquoise)'>agile design</span>. The full design is not done up front but rather <span style='color:var(--mk-color-yellow)'>sequentially</span>. Essentially the design should just be enough for the team to continue with the project and it can <span style='color:var(--mk-color-yellow)'>change over time</span>.

# Design Fundamentals
---
## Abstraction

The idea of abstraction is to only <span style='color:var(--mk-color-yellow)'>handle details that are relevant to the current perspective</span> or task at hand. Meaning we only focus on the things that are important currently.

There are <span style='color:var(--mk-color-orange)'>2 types of abstraction</span>:
1) **Data abstraction** - Instead on focusing on the lower level data items, just <span style='color:var(--mk-color-yellow)'>focus on the bigger entities</span>
2) **Control abstraction** - Abstract away control flow and <span style='color:var(--mk-color-yellow)'>focus tasks at a higher level</span>.

This is **not limited** to just data & control, it <span style='color:var(--mk-color-orange)'>can be used</span> for:
- Classes
- Architecture
- Models

If we **repeatedly apply abstraction** we will progressively <span style='color:var(--mk-color-yellow)'>achieve higher levels of abstraction</span>.
## Coupling

It is the <span style='color:var(--mk-color-yellow)'>measure of the degree of dependence</span> between components, classes, methods etc.

In general we want to have <span style='color:var(--mk-color-green)'>low coupling</span>, which signals that the component is <span style='color:var(--mk-color-yellow)'>less dependent</span> on other components.

> [!faq] Why Low Coupling?
> **High coupling** (*Tight/strong coupling*) is <span style='color:var(--mk-color-red)'>discouraged</span> as in come with its disadvantages:
> - **Harder to maintain** - A change in one module can change other modules as well
> - **Harder to integrate** - Compoents coupled has to be integrated at the same time
> - **Testing and reuse is harder** - Need to reuse all the coupled components inetad of just 1.

Lets have 2 components `X` and `Y`, if `X` contains `Y`. Meaning **a change** in `Y` <span style='color:var(--mk-color-yellow)'>may require a change</span> in `X`.

This can be in the <span style='color:var(--mk-color-orange)'>form</span> of:
- Function calls
- Variable calls
- Inheritance
- Variable of the other object
- Access to the internal structure (<span style='color:var(--mk-color-red)'>High level of coupling</span>)
- Have the same data format or communication protocol

> [!abstract] Types of Coupling
> - **Content coupling**: one module modifies or <span style='color:var(--mk-color-yellow)'>relies on the internal</span> workings of another module e.g., accessing local data of another module
> 
> - **Common/Global coupling**: two modules <span style='color:var(--mk-color-yellow)'>share the same global data</span>
> 
> - **Control coupling**: one module <span style='color:var(--mk-color-yellow)'>controlling the flow of another</span>, by passing it information on what to do e.g., passing a flag
> 
> - **Data coupling**: one module <span style='color:var(--mk-color-yellow)'>sharing data</span> with another module e.g. via passing parameters
> 
> - **External coupling**: two modules share an externally imposed convention e.g., data formats, communication protocols, device interfaces.
> 
> - **Subclass coupling**: a class <span style='color:var(--mk-color-yellow)'>inherits</span> from another class. Note that a child class is coupled to the parent class but not the other way around.
> 
> - **Temporal coupling**: <span style='color:var(--mk-color-yellow)'>two actions are bundled together</span> just because they happen to occur at the same time e.g. extracting a contiguous block of code as a method although the code block contains statements unrelated to each other
## Cohesion

It is a measure of how <span style='color:var(--mk-color-yellow)'>strongly-related </span>and <span style='color:var(--mk-color-yellow)'>focused</span> the various responsibilities of a component are.

We want a <span style='color:var(--mk-color-green)'>high cohesion component</span> as it keeps related functionalities while <span style='color:var(--mk-color-yellow)'>keeping out unrelated things</span>.

> [!question] Why High Cohesion?
> **Low cohesion** (*Weak cohesion*) is <span style='color:var(--mk-color-red)'>discouraged</span> as in come with its disadvantages:
> - **Makes the module less understandable**, as it can be difficult to expreess module functiinality high a higher level.
> - **Lowers maintainability** as it can be modified because of unrelated causes or it requires changes in many other mdules to achieve a small change
> - **Lowers reuseability**, since they do not represent logical units of fuctionality

To **ensure cohesion** we can follow these <span style='color:var(--mk-color-orange)'>guidelines</span>:
- **Code related to a single concept** should be kept together
- Code that is **invoked** close together **in terms so time** should be together
- Code that **manipulates the same data structure** should be kept together (*Does not refer to int, string float etc*)
# Integration
---
This process happens **after designing a software**. Since it is **worked on by multiple users** it has to be "pieced" togethers in the end.

There are <span style='color:var(--mk-color-orange)'>2 approaches to integration</span> for **timing and frequency**:
1) **Late & 1 time** - Wait for everything to be finished and then <span style='color:var(--mk-color-yellow)'>integrate all of them at the end</span>
2) **Early & Frequent** - Also known as <span style='color:var(--mk-color-turquoise)'>continuous integration</span>, <span style='color:var(--mk-color-yellow)'>integrate frequently</span> in parallel and in small steps

> [!question] Which One is Recommended?
> The **late & 1 time** approach is <span style='color:var(--mk-color-red)'>not recommended</span>.
> 
> This is because it often <span style='color:var(--mk-color-yellow)'>causes component incompatibilities</span> leading to <span style='color:var(--mk-color-red)'>delays</span>, since it needs to be reworked.
> 
> Unlike the other approach where integration is frequent and the <span style='color:var(--mk-color-green)'>compatibilitiy issues are small</span> and can be fixed easily.

There are <span style='color:var(--mk-color-orange)'>2 ways</span> of **integrating components**:
1) **Big-bang integration** - Integrate all the components at the<span style='color:var(--mk-color-yellow)'> same time</span>
2) **Incremental integration** - Integrate component a <span style='color:var(--mk-color-yellow)'>few at a time</span>

> [!question] Which One is Better?
> **Incremential integration** is <span style='color:var(--mk-color-green)'>prefered</span>.
> 
> This is because when lumping everything together can <span style='color:var(--mk-color-red)'>uncover too many problems</span> at the same time <span style='color:var(--mk-color-red)'>making debugging complex</span>.
## Incremental Integration

The **order in which components are integrated**, incremental integration can be <span style='color:var(--mk-color-orange)'>done in 3 ways</span>:
1) **Top-Down** - High level components are integrated before lower-level components, this allows <span style='color:var(--mk-color-green)'>discovery of higher-level problems</span>
2) **Bottom-up** - Low level components are first instead
3) **Sandwich** - Mix of the 2, the idea is to use both at the same time and meet in the middle

**High level components**
>Are components that are user facing such as `UI`

**Low level components**
>Are mainly backend components like `Storage` or `Cache` something the user will not know of

> [!info] Placeholders
> There are <b><span style='color:var(--mk-color-red)'>some issues</span></b> with the top-down and bottom-up approaches.
> 
> When integrating there can be dependencies within components like `UI` needing `Logic` to process user inputs and so on. But due to the integration process it <span style='color:var(--mk-color-yellow)'>might not be available yet</span>. 
> 
> Thus for **top down integration**, it will require the use of <span style='color:var(--mk-color-yellow)'>stubs</span> in place of lower level components.
> 
> And for **bottom up integration** it will need <span style='color:var(--mk-color-yellow)'>drivers</span> which are just some interface to test components since `UI` is not integrated yet.
# Design Patterns
---
<span style='color:var(--mk-color-turquoise)'>Design patterns</span> are <span style='color:var(--mk-color-yellow)'>elegant</span>, <span style='color:var(--mk-color-yellow)'>reusable solutions</span> to a commonly <span style='color:var(--mk-color-yellow)'>recurring problem</span> with in software design.

In the book "**Gang of Four**" (*GOF*), used this term as solutions that are <span style='color:var(--mk-color-yellow)'>discovered and refined over time</span> through repeated attempts at solving such problems.

> [!example] Examples of Recurring Design Problems
> **Initite UI update without coupling with backend** since maybe UI needs to be updated when someting changes backend.
> 
> **Finiding the best architecture**, since assembling a system will use existing implemented systems using different technologies.

The <span style='color:var(--mk-color-orange)'>format</span> for a design pattern:
- **Context** - What is the <span style='color:var(--mk-color-yellow)'>scenario</span> where the design problem is encounter
- **Problem** - <span style='color:var(--mk-color-yellow)'>Main difficulty</span> to be resolved
- **Solution** - The core of the solution, includes the <span style='color:var(--mk-color-yellow)'>most general details</span>, which may need **further refinement for a specific context**
- **Anti-patterns** (*Optional*) - **Commonly used solutions** which are usually <span style='color:var(--mk-color-red)'>incorrect or inferior</span>
- **Consequences** (*Optional*) - <span style='color:var(--mk-color-yellow)'>Identifying the pros and cons</span> of applying the pattern
- **Other useful info** (*Optional*) - Code examples, known uses, other related patterns, etc.
## Types of Design Patterns
### Singleton Pattern

**Context**
>**Some classes** should <span style='color:var(--mk-color-yellow)'>not have more than 1 instance</span> (*Main controller class*), these are known as <span style='color:var(--mk-color-turquoise)'>singletons</span>.

**Problem**
>Normal **class** can be <span style='color:var(--mk-color-yellow)'>instantiated multiple times</span> by invoking the constructor.

**Solution**
> Just **make the constructor** `private` and have a function to retrieve that 1 instance of the object

**Example of a Singleton implementation**
```Java
class Logic {
	private static Logic theOne = null;
	// Cannot get called outside the class
    private Logic() {
        ...
    }
    // The class will store the only instance of the Logic object
    public static Logic getInstance() {
        if (theOne == null) {
            theOne = new Logic();
        }
        return theOne;
    }
}
```

> [!abstract] Pros & Cons for Singleton
> <b><mark style='background:var(--mk-color-green)'>Pros</mark></b>:
> - Easy to apply
> - Effective in achieving its goal with minimum extra work
> - A easy way to access the singleton object from anywhere in the code base
> 
> <b><mark style='background:var(--mk-color-red)'>Cons</mark></b>:
> - Acts like a global variable, increases [[#Coupling|coupling]]
> - Difficult to replace with stubs (*Static method cannot be overridden*)
> - Data carryies over from test to test
### Facade Pattern

**Context**
>Components need to **access functionality** <span style='color:var(--mk-color-yellow)'>deep inside other components</span>.

**Problem**
>**Going deep** will <span style='color:var(--mk-color-red)'>expose internal details</span> it should not have knowledge of.

**Solution**
> Include a <span style='color:var(--mk-color-turquoise)'>facade class</span>, which <span style='color:var(--mk-color-yellow)'>acts as a middle man</span> between front facing components and the backend components.

**Example:**
![[Facade Example.png|center]]
### Command Pattern

**Context**
>A system might need to <span style='color:var(--mk-color-yellow)'>execute a number of different commands</span> each doing their own task.

**Problem**
>Somewhere the code **executes the commands** <span style='color:var(--mk-color-yellow)'>without having to know the command type</span>.

**Solution**
>Have a general `Command` class like a <span style='color:var(--mk-color-yellow)'>interface</span> that can be passed around.

**Example:**
![[Command Pattern Example.png|center|400]]

The `CommandQueue` class will store a list of command and will call the `execute()` function. If it is undoable then save the previous state somewhere.
### Abstraction Occurrence Pattern

**Context**
>It is possible for many objects to to have **many copies of the same information** but with <span style='color:var(--mk-color-yellow)'>1 small difference</span> (*Serial number of a book*).

**Problem**
>Having many of these objects results in data duplication which leads to <span style='color:var(--mk-color-red)'>inconsistencies if duplicates are not updated properly</span> (*One change everything needs to change*).

**Anti-pattern**
> Have a another class to specifically store the information that differs from one object to another.

**Example:**
![[Abstraction Occurrence Pattern Anti-pattern.png|center|400]]

**Solution**
>Use composition and have 2 classes to make 1 class instead (*Separate the common and unique info*).

**Example:**
![[Abstraction Occurrence Pattern Example.png|center|400]]
### Model View Controller Pattern

**Context**
>Applications are mostly, storage/retrieval of information, displaying information (*UI*) and changing stored information.

**Problem**
><span style='color:var(--mk-color-red)'>High coupling</span> can result **from the interlinked nature of the features** described in the context.

**Solution**
>**Segregate them into 3 different components**, <span style='color:var(--mk-color-turquoise)'>model</span>, <span style='color:var(--mk-color-turquoise)'>view</span>, <span style='color:var(--mk-color-turquoise)'>controller</span>.

> [!abstract] MVC
> **MVC**, stands for model, view & controller
> 
> **View** - It <span style='color:var(--mk-color-yellow)'>displays data, interacts</span> with user and pulls data from the model if necessary
> **Controller** - <span style='color:var(--mk-color-yellow)'>Detects UI events</span> (*clicking, text box*) and acts accordingly (*Update model or view if necessary*)
> **Model** - <span style='color:var(--mk-color-yellow)'>Stores and maintains data</span>, updates the view if necessary

**Example:**
![[Images/CS2103 Images/MVC Example.png|center|400]]

Note that **different components** of the application can be <span style='color:var(--mk-color-yellow)'>handled by different MVC</span>.
### Observer Pattern

**Context**
>Some objects want to **observe another**, meaning that it is interested to be <span style='color:var(--mk-color-yellow)'>notified when a change happens to it</span> (*like our UI*).

**Problem**
>We <span style='color:var(--mk-color-red)'>should not couple</span> the **observed objects to the ones that are observing it**.

**Solution**
>Have an <span style='color:var(--mk-color-yellow)'>interface to act as a middle man</span> to **communicate** between 2 parties.

![[Observer Pattern Example.png|center|400]]

Essentially, all the UI will have inherited the `Observer` class which has a `Update` function for all `UI` elements to implement.

The `model` <span style='color:var(--mk-color-yellow)'>will contain a list of observers</span>, which when the model gets updated it will call the `nofifyUIs` function which will call the `update` function for all the observers.
## Applying Design Patterns

In the GoF book it <span style='color:var(--mk-color-orange)'>divides design patterns into 3 categories</span>:
1) **Creational** - based on how objects are created (*Singleton, abstract, factory, factory method*)
2) **Structural** - based on the composition of objects into large structures while catering for extension (*Façade, adapter*)
3) **Behavioural** - based on how objects interact and responsibility distribution (*observer, state, mediator*)

These patterns <span style='color:var(--mk-color-yellow)'>can be applied in combination</span> and they are usually embedded in a larger design.

> [!question] Using Design Patterns
> Design patterns provide a <span style='color:var(--mk-color-yellow)'>high-level vocabulary</span> to talk about design.
> 
> These patterns can be:
> - **Domain specific** - Patterns for distributed applications
> - **Created in-house** - Patterns just for the company
> - **Self created**
> 
> **Knowing more patterns** can get you to be <span style='color:var(--mk-color-green)'>more experience</span>.
> 
> But **do not overuse patterns**, they <span style='color:var(--mk-color-red)'>add overhead</span> and <span style='color:var(--mk-color-red)'>increase the levels of astraction</span>, thus make sure that:
> - It is <span style='color:var(--mk-color-yellow)'>benefits is substantial</span>
> - <span style='color:var(--mk-color-yellow)'>Tradoffs are carefully considered</span> (*is it not appropriate or overkill*)

The difference between design patterns and principles is that, **patterns** are <span style='color:var(--mk-color-green)'>more general</span> and have <span style='color:var(--mk-color-green)'>wider applicability</span> and <span style='color:var(--mk-color-green)'>greater overlap</span>.

While the design <span style='color:var(--mk-color-red)'>principles are more set in stone</span> with their own rules, axioms, observations etc.
# Architecture
---
Software architectures <span style='color:var(--mk-color-yellow)'>follow various high-level styles </span>(*aka architectural patterns*).

The following are some styles which <span style='color:var(--mk-color-yellow)'>usually will be mixed around in most applications</span>.

Other <span style='color:var(--mk-color-orange)'>well-known architectural styles</span> which will not be covered include:
- Pipes-and-filters architecture
- Broker architecture
- Peer-to-peer architecture
- Message-oriented architecture.
## N-Tier Style

This style models the the <span style='color:var(--mk-color-yellow)'>high layers are more dependent</span> layers compared to lower ones (*they use services provided by lower layers*).

It is also known as <span style='color:var(--mk-color-turquoise)'>multi-layered</span> or <span style='color:var(--mk-color-turquoise)'>layered</span>.

**Example:**
![[N-Tier Style Architecture.png|center]]
## Client Server Style

In this architecture, there is <span style='color:var(--mk-color-yellow)'>1 component</span> playing the role of a <span style='color:var(--mk-color-yellow)'>server</span> and at least <span style='color:var(--mk-color-yellow)'>1 client accessing the services of the server</span>.

This is many **used in distributed applications** like games.

**Example:**
![[Client Server Architecture Example.png|center|450]]
## Event Driven Style

It models the <span style='color:var(--mk-color-yellow)'>control of the flow of the application</span> by **detecting events** from <span style='color:var(--mk-color-turquoise)'>emitters</span> and **communicating those events to the respective components**.

This is mainly **used in GUIs**.

**Example:**
![[Event Driven Architecture.png|center|400]]
## Transaction Processing Style

The transaction processing style <span style='color:var(--mk-color-yellow)'>divides the workload</span> of the system down to a **number of transactions** which are then given to a <span style='color:var(--mk-color-turquoise)'>dispatcher</span> that <span style='color:var(--mk-color-yellow)'>controls the execution</span> of each transaction.

Work like, task queueing, ordering are all handled by the dispatcher.

Essentially, a **task will be sent to the dispatcher** which will then <span style='color:var(--mk-color-yellow)'>send the work needed to be done to the respective systems</span>.

**Example:**
![[Transaction Processing Architecture.png|center]]

## Service Oriented Style

SOA build applications by <span style='color:var(--mk-color-yellow)'>combining functionalities</span> packed as <span style='color:var(--mk-color-turquoise)'>programmatically accessible services</span>. It aims to achieve interoperability between services which may **not be implemented in the same language or the same company**.

Essentially the application uses services or applications made by other companies. Like making transactions through the internet you will go through the bank's service.

A common way to **implement** this is through <span style='color:var(--mk-color-yellow)'>XML web services</span>, which is a **mode of communication** between service providers and users.

![[Service Oriented Style Example.png|center]]
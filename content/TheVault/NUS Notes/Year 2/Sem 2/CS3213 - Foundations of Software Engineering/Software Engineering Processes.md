---
Title: Software Engineering Processes
Date Created: 28-November-2025
Last Updated: 20-April-2026
Tags: 
title: Software Engineering Processes
tags:
  - CS3213
  - SWE
  - SoftwareProcesses
---

# Software Process Models
---
When **developing software**, there are a few <span style='color:var(--mk-color-orange)'>general activities that will take place</span>:
1) **Software specification**
2) **Software development**
3) **Software validation**
4) **Software evolution**

These **set of activities** (*Not limited to the list*) is known as a <span style='color:var(--mk-color-turquoise)'>software process</span>. And a **simplified representation of this process** is known as a <span style='color:var(--mk-color-turquoise)'>software process model</span>.

> [!info] Which process is the best
> There is <span style='color:var(--mk-color-yellow)'>no silver bullet</span>, it is possible that a team might **combine 2 or more models**.
## Waterfall Model

It is a simple <span style='color:var(--mk-color-yellow)'>linear plan-driven</span> software process model, where the <span style='color:var(--mk-color-yellow)'>output of one phase will be used in the next phases</span>.

> [!info] Plan-driven models
> A [[Project Management#Sequential Models|waterfall model]] is an example of a plan-driven model, where <span style='color:var(--mk-color-yellow)'>development starts only after requirement engineering and design</span> (*start only after everything is planned out*).

> [!failure] Cons of waterfall model
> Generally waterfall models are <span style='color:var(--mk-color-red)'>not popular</span> to use because:
> - **Inflexible to change**
> - **Errors in previous stages require workarounds in the next**
> - **Issues might be discovered late causing delays**

> [!important] Requirements Management Planning
> This is to **account for changing or evolving requirements** in waterfall models. To do this we will require the following:
> - **Requirements identification**: Have a way to uniquely identify each requirements
> - **Change management process**: A way to <span style='color:var(--mk-color-red)'>access the impact & loss of changes</span>
> - **Traceability policies**: A <span style='color:var(--mk-color-yellow)'>type of version control</span> to keep track of evolving requirements & system design
> - **Tool support**: Use management tools to assist in the documenting of changing requirements

<span style='color:var(--mk-color-orange)'>When</span> do we use the waterfall model:
- **Critical systems** (*Safety and security is important*)
- **Embedded systems** (*Has to interface with hardware*)
- **Large software systems** (*Part of a larger system developed by several partner companies*)
## Incremental Development

<span style='color:var(--mk-color-yellow)'>Interleaves</span> the activities of **specification**, **development** and **validation**. The system is developed as a series of versions (*increments*), <span style='color:var(--mk-color-yellow)'>adding functionality throughout increments</span>.

> [!summary] Advantages & disadvantages of incremental development
>  > [!success] Advantages
> > - Can <span style='color:var(--mk-color-green)'>accommodate</span> for **changing user requirements**
> > - More <span style='color:var(--mk-color-green)'>rapid delivery of software</span>
> > - **Cost of changing requirements** is <span style='color:var(--mk-color-green)'>low</span>
>
> > [!fail] Disadvantages
> > - Process is <span style='color:var(--mk-color-red)'>less measurable</span> (*For managers due to changing requirements*)
> > - <span style='color:var(--mk-color-red)'>Degrading</span> system structure, as additions might require updating the old implementation (*Refactoring required*)
## Integration & Configuration

A process model that follows this is a <span style='color:var(--mk-color-turquoise)'>reuse based development process</span>. The idea is that there are <span style='color:var(--mk-color-yellow)'>many existing systems, frameworks, libraries</span> etc. And we want to <span style='color:var(--mk-color-yellow)'>reuse them rather</span> than developing from scratch.

**Example flow of integration & configuration**
![[Example flow of integration & configuration.png|center]]

> [!summary] Advantages & disadvantages of Integration & Configuration
>  > [!success] Advantages
> > - Reduces software to be developed, <span style='color:var(--mk-color-green)'>reducing cost and managing risk</span>
> > - <span style='color:var(--mk-color-green)'>Faster delivery</span> of software
>
> > [!fail] Disadvantages
> > - Control over <span style='color:var(--mk-color-red)'>system evolution is difficult or lost</span>
> > - Reused components might <span style='color:var(--mk-color-red)'>compromise requirements</span> as it might not meet all of the requirements requiring a workaround.
# Agile Software Engineering
---
**Agile software development frameworks** typically are <span style='color:var(--mk-color-red)'>not complete software process models</span> (e.g., Scrum is not specific

Unlike plan-driven, **agile is designed** for <span style='color:var(--mk-color-yellow)'>changing</span> and <span style='color:var(--mk-color-yellow)'>unclear requirements</span> and developing software in <span style='color:var(--mk-color-yellow)'>increments</span>, <span style='color:var(--mk-color-yellow)'>delivering value quickly</span>.

> [!info] Software Requirements Document
> Or <span style='color:var(--mk-color-turquoise)'>software requirements specification</span> (*SRS*) is an official statement on what should be implemented. It can <span style='color:var(--mk-color-yellow)'>contain both system and user requirements</span>

<span style='color:var(--mk-color-orange)'>Agile development is</span>:
- Both a <span style='color:var(--mk-color-yellow)'>mindset</span> and <span style='color:var(--mk-color-yellow)'>concrete management and engineering framework</span>
- Focuses on <span style='color:var(--mk-color-yellow)'>delivering value</span> in increments & avoiding waste
- <span style='color:var(--mk-color-yellow)'>Feedback loops</span> and customer involvement
- <span style='color:var(--mk-color-yellow)'>Adaptative</span> to changing requirements
- Lightweight process
- Empowering teams and people (*People are part of the process*)
- Inspired by lean manufacturing principles
- Lots of buzzwords and certifications

> [!success] Advantages of agile
> - Better customer satisfaction
> - Faster time to delivery
> - Increased collaboration
> - Better work environment and software quality
> - Better alignment with business needs
## Agile Manifesto

**Written in 2001**, it emphasises the following:
- <span style='color:var(--mk-color-yellow)'>Individuals and interactions</span> over processes and tools
- <span style='color:var(--mk-color-yellow)'>Working software</span> over comprehensive documentation (*Does not mean no documentation*)
- <span style='color:var(--mk-color-yellow)'>Customer collaboration</span> over contract negotiation
- <span style='color:var(--mk-color-yellow)'>Responding to change</span> over following a plan

> [!abstract] Agile principles in the agile manifesto
> - <span style='color:var(--mk-color-yellow)'>Prioritise customer satisfaction</span> though **early and continuous delivery** of valuable software
> - <span style='color:var(--mk-color-yellow)'>Allow changing requirements</span> even in the later stages of development
> - <span style='color:var(--mk-color-yellow)'>Delivery working software frequently</span> (*Shoter timescales are preferred*)
> - **Business people and developers** must <span style='color:var(--mk-color-yellow)'>work together</span> daily throughout the project
> - <span style='color:var(--mk-color-yellow)'>Build projects around motivated individuals</span>, provide the resources needed and trust in them
> - <span style='color:var(--mk-color-yellow)'>Face to face conversion</span> to convey information <span style='color:var(--mk-color-green)'>efficiently and effectively</span>
> - **Working software** is the <span style='color:var(--mk-color-yellow)'>primary measure of progress</span>
> - Promote **sustainable development**, development should be able to <span style='color:var(--mk-color-yellow)'>maintain at a constant pace</span> indefinitely.
> - Attention to <span style='color:var(--mk-color-yellow)'>technical excellence and good design</span> enhances agility
> - <span style='color:var(--mk-color-yellow)'>Simplicity</span>, maximising amount of work done is important
> - <span style='color:var(--mk-color-yellow)'>Promote self-organizing teams</span> for better result
> - **Reflect** on <span style='color:var(--mk-color-yellow)'>how to become more effective</span> and improve.
## Waste

<span style='color:var(--mk-color-turquoise)'>Waste</span> does not only occur in agile but in <span style='color:var(--mk-color-orange)'>software engineering</span> in general which includes:
- <span style='color:var(--mk-color-yellow)'>Partially done work</span>
- <span style='color:var(--mk-color-yellow)'>Extra processes</span>, does not add value to the customer
- <span style='color:var(--mk-color-yellow)'>Extra features</span>, not needed by the organisation or customer
- <span style='color:var(--mk-color-yellow)'>Task switching</span>, when people are working on multiple projects
- <span style='color:var(--mk-color-yellow)'>Waiting</span> for inputs that are required to finish the current work
- <span style='color:var(--mk-color-yellow)'>Motion</span>, handoffs that require communication
- <span style='color:var(--mk-color-yellow)'>Defects</span>, any software defects or unclear information
- Or in a modem interpretation, hardship in daily work
## Scrum

It is a **lightweight framework for project management**. It does not specify how to carry out activates but <b><mark style='background:var(--mk-color-yellow)'>proposes certain rules to be followed</mark></b>.

> [!note] Characteristics of scrum
> It <span style='color:var(--mk-color-yellow)'>focuses on delivering value</span> via increments in sprints.
> 
> It is also founded on <span style='color:var(--mk-color-orange)'>empiricism</span> and <span style='color:var(--mk-color-orange)'>lean thinking</span>:
> - **Empiricism** - Knowledge comes from experience and decision making based on observations
> - **Lean thinking** - Reduce waste and focus on the essentials

> [!note] Scrum pillars
> There are <span style='color:var(--mk-color-orange)'>3 main pillars</span> in scrum:
> 1) **Transparency** - <span style='color:var(--mk-color-yellow)'>Process is visible</span> for developers and customers
> 2) **Inspection** - Artifacts and process are <span style='color:var(--mk-color-yellow)'>inspected frequently to detect problems</span>
> 3) **Adaption** - <span style='color:var(--mk-color-yellow)'>Adjustments</span> are made if the product is unacceptable

**Overview of the entire scrum process**
![[Scrum Process Overview.png|center]]
### Scrum Team

A scrum team is <span style='color:var(--mk-color-yellow)'>typically small</span> (*Around 10 or fewer people*), this team is also <span style='color:var(--mk-color-yellow)'>self-managing</span> and there are <span style='color:var(--mk-color-yellow)'>no hierarchies</span> inside.

> [!info] Roles in a scrum team
> It mainly consist of <span style='color:var(--mk-color-orange)'>3 roles</span>:
> 1) **Scrum master** - Accountable for <span style='color:var(--mk-color-yellow)'>establishing & facilitating the scrum process</span>. They also are responsible for <span style='color:var(--mk-color-yellow)'>coaching & removal of impediments</span>
> 2) **Product owner** - Accountable for <span style='color:var(--mk-color-yellow)'>maximising value</span> of the product. They **manage the product backlog** and <span style='color:var(--mk-color-yellow)'>communicate the goal of the product</span> (*Customers or stakeholders*)
> 3) **Developers** - : Focused on <span style='color:var(--mk-color-yellow)'>creating an increment</span> each sprint. They are **accountable for the sprint backlog**
### Scrum Events

A **milestone in scrum** is known as a <span style='color:var(--mk-color-turquoise)'>sprint</span>. The **aim of the sprint** is to <span style='color:var(--mk-color-green)'>create a useful increment</span>. Each sprint will <span style='color:var(--mk-color-yellow)'>start immediately after the previous sprint</span>. 

If a<span style='color:var(--mk-color-red)'> sprint becomes obsolete</span>, the **product owner can cancel the sprint**.

And a sprint consists of a <span style='color:var(--mk-color-orange)'>few activities</span>.
#### Sprint Planning

In sprint planning the <span style='color:var(--mk-color-yellow)'>important items in the product backlog will be addressed by the product owner</span>, involving the team and sometimes stakeholders.

The goal is to lay out the<span style='color:var(--mk-color-yellow)'> work that needs to be done for the sprint</span>, this is known as a <span style='color:var(--mk-color-turquoise)'>sprint goal</span>.

> [!tldr] Topics to discuss during sprint planning
> - Why is the sprint valuable?
> - What can be done in this sprint?
> - How will the chosen work be done? (*Spilt work into tasks and how to delegate*)
#### Daily Scrum

It is a **short standup meeting** at the <span style='color:var(--mk-color-yellow)'>same time everyday</span>. During this time, the team will <span style='color:var(--mk-color-yellow)'>focus on the sprint goal and an actionable plan</span> for the next day of work.

They can also share, what was done, what will be done tomorrow and any issues faced.

The <span style='color:var(--mk-color-yellow)'>sprint backlog is adaptable</span>, and new tasks can be added and the <span style='color:var(--mk-color-green)'>plan can also be adjusted</span> if necessary.
#### Sprint review

During this phase, the team will <span style='color:var(--mk-color-yellow)'>present their results</span> to key **stakeholders** and <span style='color:var(--mk-color-yellow)'>progress towards the product goal is discussed</span>.

The team will also <span style='color:var(--mk-color-yellow)'>collaborate on what to do next</span> and adjust the product backlog if necessary.

> [!important] It is not just a presentation on what is done but rather a working session with stakeholders
#### Sprint Retrospective

It is **done within the team** in which they discuss on what went well and <span style='color:var(--mk-color-yellow)'>what needs to be improved on</span> (*increase quality & effectiveness*).

This can <span style='color:var(--mk-color-yellow)'>result in adding improvement items to the next sprint backlog</span>.
### Scrum Artifacts

#### Product Backlog

It is a <span style='color:var(--mk-color-yellow)'>list of things to do for the project</span>. It an consist of items which are **concrete or abstract** but they all work towards the <span style='color:var(--mk-color-turquoise)'>product goal</span>.

> [!info] Product goal
> it is a <span style='color:var(--mk-color-yellow)'>long term objective</span> for the scrum team for the particular project.

In [[Software Engineering Processes#Sprint Planning|sprint planning]], **items from the product backlog can be selected** if they are to be <span style='color:var(--mk-color-yellow)'>done within 1 sprint</span>.
#### Sprint Backlog

Unlike product backlog, sprint backlog consists of <span style='color:var(--mk-color-yellow)'>tasks to be done within the sprint</span> to achieve the sprint goal.

> [!abstract] Components in a sprint backlog
> There are <span style='color:var(--mk-color-orange)'>3 components</span>:
> 1) **Sprint goal**
> 2) **Product backlog items** selected for the sprint
> 3) **Actionable plan** for delivering the increment

During the sprint, the <span style='color:var(--mk-color-yellow)'>sprint backlog can be updated as more is learned</span> (*Discussed with the product owner*).
#### Increment

This is the <span style='color:var(--mk-color-yellow)'>end product of a sprint</span>. It must have concrete stepping point towards the product goal. The definition of "Done" (*end product for sprint*) is defined by the organisation or the scrum team.

It is <span style='color:var(--mk-color-yellow)'>alright to have more than 1 increment per sprint</span>. However, it must be <b><mark style='background:var(--mk-color-yellow)'>usable and verifiable</mark></b>.
### Timeboxing

This is usually a <span style='color:var(--mk-color-yellow)'>cutoff timing</span> for the respective activates in scrum. This is to <span style='color:var(--mk-color-green)'>keep it short</span> and prevent the team from asking too many questions which can cause delays in each activity.

|        Phase         |    Duration     |
|:--------------------:|:---------------:|
|        Sprint        | 1 month or less |
|   Sprint planning    |  Up to 8 hours  |
|     Daily scrum      |   15 minutes    |
|    Sprint review     |  Up to 4 hours  |
| Sprint retrospective |  Up to 3 hours  |
> The above is **just a guideline** and it varies between organisations.
## Kanban

It is a **visual system** based on Kanban Boards. It visualises the flow of work items (*Units of value*).

> [!note] Elements in Kanban
> It consists of <span style='color:var(--mk-color-orange)'>2 elements</span>:
> 1) **Cards** - Represent work items
> 2) **Columns** - Represent the each stage of the process (*Current stage of a work item*)

The team will need to <span style='color:var(--mk-color-turquoise)'>define the workflow</span> (*Definition of workflow or DoW*), which will <span style='color:var(--mk-color-yellow)'>state the flow of these items</span> and how these items move from one state to another.

The team will also need to enforce a <span style='color:var(--mk-color-turquoise)'>work in progress</span> (*WIP*) limit. This limits the total number of tasks that can be done.

> [!abstract] Scrumban
> **Scrum** is more <span style='color:var(--mk-color-yellow)'>prescriptive</span> and activities are <span style='color:var(--mk-color-yellow)'>time-boxed</span>. Thus **Kanban can be used in scrum** (*Scrumban*) by taking a<span style='color:var(--mk-color-yellow)'> flow oriented perspective</span>, limiting the WIP, and measuring and improving flow.

## Extreme Programming (XP)

It is a influential agile method that <span style='color:var(--mk-color-yellow)'>focuses on software-development</span>. It takes an “extreme” approach to iterative development and best practices.

Unlike **scrum** which <span style='color:var(--mk-color-yellow)'>focuses on agile management mechanisms</span>.

**Planning & feedback loop in XP**
![[Planning & Feedback Loops in Extreme Programming.png|center|350]]
### Pair Programming

It is where <span style='color:var(--mk-color-yellow)'>2 developers work together</span> take collective ownership on their work.

> [!note] Roles in pair programming
> One person will be the <span style='color:var(--mk-color-turquoise)'>driver</span> which will <span style='color:var(--mk-color-yellow)'>do the actual coding</span>. The other will be the <span style='color:var(--mk-color-turquoise)'>navigator</span> which will <span style='color:var(--mk-color-yellow)'>review the code</span> and <span style='color:var(--mk-color-yellow)'>focus on the bigger picture</span>.
> 
> The <span style='color:var(--mk-color-yellow)'>roles will switch</span> after a certain time period, and the <span style='color:var(--mk-color-yellow)'>partners are switched</span> frequently.

Due to the **frequent switching**, everyone can change any code and this <span style='color:var(--mk-color-yellow)'>everyone is responsible</span>. This can only work if everyone has a <span style='color:var(--mk-color-yellow)'>good understanding of the larger system</span>.

> [!summary] Advantages & disadvantages of pair programming
>  > [!success] Advantages
> > - <span style='color:var(--mk-color-green)'>Fewer bugs</span> in the code
> > - Spreads <span style='color:var(--mk-color-green)'>code understanding</span>
> > - <span style='color:var(--mk-color-green)'>Higher quality code</span>
> > - <span style='color:var(--mk-color-green)'>Learn</span> from each other
>
> > [!fail] Disadvantages
> > - <span style='color:var(--mk-color-red)'>Not cost efficient</span>
> > - <span style='color:var(--mk-color-red)'>Difficult to schedule</span>
> > - Possible <span style='color:var(--mk-color-red)'>conflicts</span> and <span style='color:var(--mk-color-red)'>personality clashes</span>
### Tests

XP follows a [[Developer Testing#Test Driven Development|test driven development]], thus [[Developer Testing#Unit Testing|unit tests]] are written before the code. It aims to <span style='color:var(--mk-color-yellow)'>test for all potential cases where the code could fail</span>.

> [!success] Advantages of test driven development
> - It can <span style='color:var(--mk-color-green)'>help in development</span>, by addressing a test case at a time
> - It <span style='color:var(--mk-color-green)'>facilitates other practices</span> as well like continuous integration, collective code ownership, refactoring etc.

It also has [[Developer Testing#Acceptance Testing|acceptance tests]], which <span style='color:var(--mk-color-yellow)'>derived from user requirements</span> and are written with the customer as user stories.
### Continuous Integration

With continuous integration, changes in the **code** can be <span style='color:var(--mk-color-yellow)'>frequently updated to the main branch</span>. This is <span style='color:var(--mk-color-yellow)'>facilitated by units tests</span> (*GitHub actions can automatically run tests*).

This allows the development team to <span style='color:var(--mk-color-yellow)'>work on the latest version of the software</span>.
### Simple Design & Refactoring

XP mandates that <span style='color:var(--mk-color-yellow)'>simple is best mentality</span>. Design and code written must be kept as simple as possible.

The team will only **refactor** as part of the lifecycle of the project to <span style='color:var(--mk-color-green)'>ensure maintainability and extendibility</span>.
### Other XP Practices

<span style='color:var(--mk-color-turquoise)'>On-site customer</span>, is a **representative of the end-user** which should be <span style='color:var(--mk-color-yellow)'>available full time</span>. They are <span style='color:var(--mk-color-yellow)'>part of the development team</span> and is responsible for <span style='color:var(--mk-color-yellow)'>brining system requirements</span>.

<span style='color:var(--mk-color-turquoise)'>Sustainable pace</span>, try and <span style='color:var(--mk-color-yellow)'>not have large amount of overtime</span> as this will result in <span style='color:var(--mk-color-red)'>lower code quality and productivity</span>.
# DevOps
---
In software development, **one challenge** faced is the <span style='color:var(--mk-color-red)'>deployment of software quickly and reliably</span>.

> [!abstract] Silos
> Developers and operations were <span style='color:var(--mk-color-yellow)'>traditionally separated</span>.
> 
> > [!info] Developers
> > They are responsible for <span style='color:var(--mk-color-yellow)'>creating increments / value</span> and they want to <span style='color:var(--mk-color-yellow)'>deploy software quickly</span>.
>
> > [!info] Operations
> > <span style='color:var(--mk-color-yellow)'>Manage</span> and <span style='color:var(--mk-color-yellow)'>maintain</span> IT infrastructure. They <span style='color:var(--mk-color-yellow)'>operate software security and monitoring</span> and want to <span style='color:var(--mk-color-yellow)'>avoid downtimes and issues</span>. 
> 
> The **interests** between the 2 parties are <span style='color:var(--mk-color-red)'>conflicting</span>.

In <span style='color:var(--mk-color-turquoise)'>DevOps</span>, both developers and operations (*or whole organisation*) <span style='color:var(--mk-color-yellow)'>work together</span> to deliver value. This makes <span style='color:var(--mk-color-green)'>deployments routine and predictable</span> (*automate shipping increments*).

It has many <span style='color:var(--mk-color-yellow)'>similarities to agile and lean software engineering</span>, sharing the same aspects and goals.

> [!tldr] DevOps process
> ![[DevOps Process.png|center|300]]
> 
> It is usually an<span style='color:var(--mk-color-yellow)'> infinite loop</span> that <span style='color:var(--mk-color-yellow)'>intertwines phases</span> associated with development and operations (*the concret phases might differ*).
> 
> This <span style='color:var(--mk-color-yellow)'>loop emphasizes feedback</span> between development & operations.
## Flow in DevOps

In DevOps, it has its own <span style='color:var(--mk-color-orange)'>concept of flow</span>:
- **Reduce batch sizes** - For <span style='color:var(--mk-color-green)'>quicker delivery times</span>
- **Reduce handoffs** - Minimise passing of work between departments / teams, <span style='color:var(--mk-color-green)'>reducing time for development</span>
- **Continually identify and evaluate flow constraints**
## Feedback in DevOps

In DevOps, **failures and issues cannot be prevented** for complex systems. Thus it is important for <span style='color:var(--mk-color-yellow)'>fast and constant feedback</span> from all stages of the value stream.

> [!question] Why constant feedback is important?
> It is better to remediate problems early on as they are <span style='color:var(--mk-color-green)'>small</span>, <span style='color:var(--mk-color-green)'>cheaper</span> and <span style='color:var(--mk-color-green)'>easier to fix</span>.

With **automatic builds, integration and tests processes**, we can <span style='color:var(--mk-color-green)'>get immediate feedback</span> for faster propagation of issues.

> [!info] Blameless postmortems
> **Issues or incidents occurred should be discussed** on how similar issues can be prevented. This is to <span style='color:var(--mk-color-green)'>prevent any blaming or judging</span> which can <span style='color:var(--mk-color-red)'>result is less willingness to share</span>.
## Continuous Learning & Experimentation

DevOps <span style='color:var(--mk-color-yellow)'>promotes & requires active learning</span>. Instead of working rigidly defined, the system of <span style='color:var(--mk-color-yellow)'>work is dynamic</span>.

> [!note] Experimentation
> Try new phases to **generate new improvements** <span style='color:var(--mk-color-yellow)'>enabled by standardization of work procedures and
> documentation of the results</span>. 
> 
> What was learnt will be propagated to the rest of the organisation.

## DORA

It is a matrix to <span style='color:var(--mk-color-yellow)'>measure the DevOps performance</span>, which can be used for continuous improvement.

> [!important] Key metrics in DORA
> - **Change lead time** - Time it takes for code commit or change to be successfully deployed to production
> - **Deployment frequency** - How often application changes are deployed to production
> - **Change fail rate** - Percentage of deployments that causes failures in production resulting in hotfixes or rollbacks
> - **Failed deployment recovery time** - Time it takes to recover from a failed deployment

This requires **monitoring of code and infrastructure**, where the **metrics and insights** can be used to <span style='color:var(--mk-color-green)'>improve the value stream</span>.

> [!abstract] Value stream mapping
> **Value Stream Management** - <span style='color:var(--mk-color-yellow)'>Makes the sequence of activities</span> to deliver value
> **Value Stream Mapping** - Identify and analyze value streams aiming to <span style='color:var(--mk-color-yellow)'>reduce or eliminate inefficiencies</span>
> 
> **Example:**
> ![[Value stream mapping.png|center]]
## Continuous Integration & Deployment

CI/CD frequently <span style='color:var(--mk-color-yellow)'>integrate changes, test them, and automatically deploy</span> them, through scripts.

> [!info] Infrastructure as Code
> **Configuration of the server infrastructure** should be <span style='color:var(--mk-color-yellow)'>treated similar</span> to code, such as configuration of files or scripts.
> 
> In addition apply best practices such as version control and CI/CD

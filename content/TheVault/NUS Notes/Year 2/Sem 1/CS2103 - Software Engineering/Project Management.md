---
title: Project Management
Date Created: 2024-09-24
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE
---
# Software Development Life Cycle
---
## Process Models

During development, developers go through a **timeline with different stages** (*Design, implementation, testing*) which is known as <span style='color:var(--mk-color-turquoise)'>SDLC</span>.
### Sequential Models

Also known as <span style='color:var(--mk-color-turquoise)'>waterfall model</span>, is a **linear development process** going through different development stages.

**Waterfall model example:**
![[Sequential SDLC Model.png|center|400]]

At each stage, certain "**outputs**" will be produced and it <span style='color:var(--mk-color-yellow)'>will be used in the next stages</span>. And in a strict environment, it <span style='color:var(--mk-color-red)'>will never go back to a previous stage</span> once the requirements are met.

> [!tldr]+ Pros & Cons for Sequential Models
> <b><mark style='background:var(--mk-color-green)'>Pros</mark></b>
> - Less wastage (*Only need to deliver 1 version of the product*)
> - Requirements are fixed, <span style='color:var(--mk-color-yellow)'>well understood</span> and work needed to complete is predictable
>   
> <b><mark style='background:var(--mk-color-red)'>Cons</mark></b>
> - Overestimate or underestimate effort and timer needed for each phase
> - High risk of overrunning deadlines (Non-delivery)
> - Cut corners to meet deadlines
 
### Iterative Models

In this model, the development process goes through multiple phases or iterations, with <span style='color:var(--mk-color-yellow)'>each phase producing a version of the product</span>.

**Iterative model example:**
![[Iterative SDLC Model.png|center|400]]

At each iteration, a newer version of the final product is produced and sent for testing and feedback which is used to improve on the next version.

There are **2 types** of iterative models, <span style='color:var(--mk-color-orange)'>breath-first</span> (*Build a finished product and improve at each iteration*) and <span style='color:var(--mk-color-orange)'>depth-first</span> (*Each iteration build finish some features of the final product*). Both can be used as a mixture as well.

> [!tldr]+ Pros & Cons for Iterative Models
> <b><mark style='background:var(--mk-color-green)'>Pros</mark></b>
> - **There is a viable version** of the product even if the deadline is delayed (*From previous iterations*)
> - Flexible environment, as requirements can change or reallocation of resources can be done mid way
>   
> <b><mark style='background:var(--mk-color-red)'>Cons</mark></b>
> - High wastage as there are many versions of the final product (*Inefficient usage of recourses*)
### Agile Models

The <span style='color:var(--mk-color-orange)'>key features</span> of agile are:
- **Requirements are prioritised** based on the <span style='color:var(--mk-color-yellow)'>user needs</span>. These needs are clarified regularity and will be factored into the development schedule.
- The team will do a rough design of the whole project and evolve it as it progresses.
- Emphasis on <span style='color:var(--mk-color-yellow)'>transparency</span> and <span style='color:var(--mk-color-yellow)'>responsibility</span>, sharing their progress on a daily basis.

2 well known agile models are <span style='color:var(--mk-color-turquoise)'>eXtreme programming</span> (*XP*) and <span style='color:var(--mk-color-turquoise)'>Scrum</span>.
#### Scrum

There are <span style='color:var(--mk-color-orange)'>3 main rolls</span> in scrum:
1) **Scrum master** - Project manager
2) **Product owner** - Stakeholders of the business
3) **Team** - People who will do the actual design, analysis, implementation and testing

A scrum project is divided in <span style='color:var(--mk-color-turquoise)'>sprints</span> (*Milestones*), which are on a **weekly or monthly basis**. And before a start of a sprint a <span style='color:var(--mk-color-turquoise)'>planning meeting</span> is held to reflect and report on the progress done. 

This <span style='color:var(--mk-color-yellow)'>meeting can be done daily</span> (*thus known as daily scrum*). This 15 minute meeting is to:
1) Answer what was done
2) Answer what is going to be done today
3) Disclose any impediments

The **issues raised** will be <span style='color:var(--mk-color-yellow)'>taken offline</span> right after the meeting and <span style='color:var(--mk-color-red)'>not during the meeting</span>.

**After each sprint**, the team will <span style='color:var(--mk-color-yellow)'>create a deliverable product increment</span>. The **features** (*in the product backlog*) to be **added** are decided at the <span style='color:var(--mk-color-yellow)'>start of the previous sprint meeting</span> and how much commitment is needed. The <span style='color:var(--mk-color-red)'>features added cannot be changed</span>. 

The team can be <span style='color:var(--mk-color-yellow)'>broken down into smaller sub-teams</span>. 

The <span style='color:var(--mk-color-yellow)'>requirements can change throughout the project</span>. This is known as <span style='color:var(--mk-color-turquoise)'>requirement churn</span>, thus the <span style='color:var(--mk-color-yellow)'>requirements can never be fully understand</span> and thus agile goal is to maximise user requirements. 

#### Extreme Programming

Instead of delivering everything at some future date, this <span style='color:var(--mk-color-yellow)'>process delivers the software to users when they need it</span> (*stress customer satisfaction*).

This empowers developers to have the confidence to respond to changing customer requirements at any time.

XP, **highly emphasizes teamwork**. All members are equal partners and they <span style='color:var(--mk-color-yellow)'>want to solve the problem efficiently</span>.

> [!note] Success Factors of XP
> XP aims to <span style='color:var(--mk-color-orange)'>improve the product</span> in these ways:
> 1) **Communication**
> 2) **Simplicity**
> 3) **Feedback**
> 4) **Respect**
> 5) **Courage**
> 
> Developers communicate with their team and customers, and constantly get feedback.

**XP rules**
![[Rules of XP.png|center|450]]

Other things that are <span style='color:var(--mk-color-orange)'>related to XP</span>:
- Pair programming
- CRC cards
- Project velocity
- Standup meetings
### Unified Process

This process is a <span style='color:var(--mk-color-green)'>more flexible</span> and <span style='color:var(--mk-color-green)'>customizable</span> process, rather than a single fixed process.

**Unified process general timeline**
![[Unified Process General Timeline.png|center|350]]


It consists of <span style='color:var(--mk-color-orange)'>4 phases</span> each with their own objective

1) **Inception**

At this stage, developers understand the problem, communicate with customers, understand the problem and plan the development effort.

Developers will also come up with a basic use case model, rough project plan, vision and scope.

2) **Elaboration**

At this stage, developers refine and expand requirements and determine high-level design.

Developers will also come up with a system architecture, design models and a prototype.

3) **Construction**

At this stage, developers will be focusing on development, design models refined and testing and multiple releases of the system

Developers will come up with test cases of all levels as well as a system release.

4) **Transition**

At this stage the system is ready to be release, and developers familiarize end users with the system.

Developers will come up with a final system release and a instruction manual.
### CMMI

Or <span style='color:var(--mk-color-turquoise)'>Capability Maturity Model Integration</span>. It defines <span style='color:var(--mk-color-orange)'>5 maturity levels</span> for a process and it serves as a criteria to <span style='color:var(--mk-color-yellow)'>determine which stage of development</span> the team is at.

**Overview of the 5 Levels**
![[CMMI 5 Levels.png|center|350]]


# Project Planning
----
## Milestones

A milestone **indicates a end of a stage** where <span style='color:var(--mk-color-yellow)'>significant progress is made</span>. It should <span style='color:var(--mk-color-orange)'>take into account</span>:
- **Dependencies**
- **Priorities** on features

For milestones, they **do no need a concrete plan** on what has to be done, sometimes it is **ok to use a high-level plan** for the whole project and a detailed one for the subsequent milestones.
## Buffers

They are essentially **additional time** given to <span style='color:var(--mk-color-yellow)'>absorb any unforeseen delays</span>. This is because getting the correct estimate can be hard.

However do not <span style='color:var(--mk-color-red)'>inflate task estimates to create hidden buffers</span>. Meaning we extend the task deadline based on the buffer, but rather we should <span style='color:var(--mk-color-yellow)'>allocate explicit buffers</span> while keeping the task deadline the same.

![[Buffer Example.png|center]]
## Issue Trackers

Also known as <span style='color:var(--mk-color-turquoise)'>bug trackers</span> are essentially tools to keep track of <span style='color:var(--mk-color-yellow)'>task assignments and progress</span> (*GitHub*). For **small projects**, general purpose tools like spreadsheets can be used.

It is an **essential part of project management** to monitor progress.

**Some tools:**
- GitHub
- Trello
- Jira

### Work Breakdown Structure

Or WBS, it depicts<span style='color:var(--mk-color-yellow)'> information</span> about <span style='color:var(--mk-color-yellow)'>tasks</span> and their details in terms of <span style='color:var(--mk-color-yellow)'>subtasks</span>.

We want to <span style='color:var(--mk-color-yellow)'>divide tasks into smaller well defined units</span>. As for large tasks we can break it down into sub tasks.

We can also indicate **prerequisite** tasks and **estimated effort**.

**WBS example:**
![[Work Breakdown Structure Example.png|center|500]]

Effort is usually <span style='color:var(--mk-color-yellow)'>measured in man hour/day/month</span>. So it is calculated by number of people it needs to complete the task in a specified time period.

**Example:** 2 man day means this task can be done in 1 day by 2 people.
### Grant Chart

A Gantt chart is a **2-D bar-chart**, drawn as <span style='color:var(--mk-color-yellow)'>time vs tasks</span> (*Tasks are represented by bars*).

**Example:**
![[Grant Chart Example.png|center|400]]
**Where:**
- A **solid bar** represents the <span style='color:var(--mk-color-yellow)'>main task</span>
- A main tasks is composed of <span style='color:var(--mk-color-yellow)'>subtasks</span> which are the **grey bars**
- The **diamond** represents an <span style='color:var(--mk-color-yellow)'>important deadline/deliverable/milestone</span>

### PERT Chart

It stands for <span style='color:var(--mk-color-turquoise)'>program evaluation review technique</span>. It is to show the <span style='color:var(--mk-color-yellow)'>order/sequence of tasks</span>. It is essentially a graph where the nodes are tasks and the **edges are he precedence between tasks**.

**Example:**
![[PERT Chart Example.png|center|500]]

> [!question] How can PERT Chart Help?
> It can help determine the <span style='color:var(--mk-color-orange)'>following inportant information</span>:
> - The order in which the tasks has to be completed first
> - Tasks which can be done concurrently (*Branced out tasks*)
> - The shortest possible completion time
> - Identify the <span style='color:var(--mk-color-turquoise)'>critical path</span>
> 
> **Critical path**
> > It is a path where any **delay** can <span style='color:var(--mk-color-red)'>affect the project duration</span>. Thus tasks on the critical path must be <b><span style='color:var(--mk-color-yellow)'>completed on time</span></b>.

## Team Structures

**Each member** in the team should be <span style='color:var(--mk-color-yellow)'>responsible in some aspect</span> of the project. **If not** then it will cause <span style='color:var(--mk-color-red)'>chaos</span> since the <span style='color:var(--mk-color-yellow)'>responsibilities are not assigned</span>.

**Types of structures:**
![[Types of Team Structures.png|center]]

**Echoless team**
> Every member is <span style='color:var(--mk-color-yellow)'>equal</span> in terms of responsibility and accountability

Also known as a <span style='color:var(--mk-color-turquoise)'>democratic team structure</span>, where a <span style='color:var(--mk-color-yellow)'>consensus must be reach</span> when a **decision** is required.

This team structure is <span style='color:var(--mk-color-green)'>good in finding solutions to hard problems</span> since **everyone contributes ideas**. But it has a <span style='color:var(--mk-color-red)'>high risk of falling apart</span> because of a **lack of an authority figure** to manage and resolve conflicts.

**Chief programmer team**
>There is <span style='color:var(--mk-color-yellow)'>1 authoritative figure</span> (*Chief programmer*). Major decisions are done by him and the rest has to obey him

Essentially this **leader** will make the <span style='color:var(--mk-color-yellow)'>decisions and delegate</span> work to the team members. They also work closely with other domain specialists.

This allows **individual members** to <span style='color:var(--mk-color-green)'>concentrate on areas which they have expertise</span> on. But the <span style='color:var(--mk-color-red)'>leader is heavily relied upon</span> where they have to be good in managing and technical skills.

**Strict hierarchy team**
> Essentially is a **hierarchy** with a <span style='color:var(--mk-color-yellow)'>strictly defined organisation</span> among team members.

Where each **member will work on their own tasks and reports to a boss**. This is good for large scale projects as with a good team structure it can <span style='color:var(--mk-color-green)'>reduce communication overhead</span>.
## Revision Control

A <span style='color:var(--mk-color-turquoise)'>revision control system</span> can be done in <span style='color:var(--mk-color-orange)'>2 ways</span>:
1) **Centralized** (*CRCS*) - Uses a <span style='color:var(--mk-color-yellow)'>central repository</span> that is shared by the team
2) **Distributed** (*DRCS*) - <span style='color:var(--mk-color-yellow)'>Each member has their own repository</span>, thus allowing multiple repositories working together

**Example of DRCS**
![[DRCS Example.png|center|300]]
### Forking Flow

![[Forking Flow Revision Control Example.png|center|400]]

The `main` repository is <span style='color:var(--mk-color-yellow)'>kept in isolation</span> while all the developers work on a "copy".

**How this works**:
1) Set up an **organisation** on GitHub and set up a **team** and **add its members**
2) Each **member will fork** the repository
3) The members will just update their own fork respectively
4) To add the changes made, **create a pull request to the upstream repository**
5) Other **members will review the PR** and the author will make the necessary changes or resolve conflicts
6) Another member (*Not the author*) will approve and merge the PR
7) All other members will have to **sync with the upstream repo**

**How to pull from the upstream repo**:
```Shell
git getch upstream

git merge upstream/master
```
### Feature Branch Flow

![[Feature Branch Flow Example.png|center|400]]

For this flow there is **no forks**. But rather everyone will <span style='color:var(--mk-color-yellow)'>branch out based on the different features</span>. Then to **merge** with the main repo a <span style='color:var(--mk-color-yellow)'>PR can be created as usual</span>.

For this flow, it is better to have some <span style='color:var(--mk-color-yellow)'>branch protection</span> to <span style='color:var(--mk-color-green)'>reduce accidental commits</span> or changes in code. But it is **not suitable** when the <span style='color:var(--mk-color-red)'>contributors cannot be trusted </span>.
### Centralized Flow

Is is even simpler there is no branching, everything is done on the `master` branch. Meaning <span style='color:var(--mk-color-yellow)'>everyone will pull and commit to the same branch</span>.
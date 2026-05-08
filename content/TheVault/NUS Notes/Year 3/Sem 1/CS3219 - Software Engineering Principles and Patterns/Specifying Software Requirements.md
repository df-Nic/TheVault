---
title: Specifying Software Requirements
Date Created: 2025-08-31
Last Updated: 2025-09-28
tags:
  - CS3219
  - SWE
  - SWE/Requirement-Elicitation
---
# Functional & Non-Functional Requirements
---
>[!info] Requirements
>They are specifications of **what should be implemented**.

**Functional requirements** (*FR*) specifies what the <b><span style='color:var(--mk-color-yellow)'>system should do</span></b>. Typically some behavior or function

**Non-functional requirements** (*NFR*) on the other hand describes does not concern with functionality but rather <b><span style='color:var(--mk-color-yellow)'>how the system should operate</span></b>.

NFR's usually refer to as [[Requirements Gathering#Non-Functional|quality attributes]] of a system. And there is <b><span style='color:var(--mk-color-red)'>no quantifiable score</span></b>, there needs to be <b><span style='color:var(--mk-color-yellow)'>tradeoffs & thus finding the right balance</span></b> (*it affects one another*).

A **combination of these NFRs** <b><span style='color: var(--mk-color-yellow)'>defines the software quality</span></b>.

>[!abstract] Requirements development / elicitation phases
>1) [[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Requirements Gathering.md#Elicitation Techniques|Elicitation]] (*discover requirements*)
>2) Analysis (*understand requirements*)
>3) Specification (*essentially log down all requirements*)
> 	  - **User** centric requirements (*why the user wants this feature*)
> 	  - **Product** centric (*what the product does for the user*) <- <b><span style='color: var(--mk-color-green)'>Easier to create tests and acceptance criteria</span></b> since it it states what the product will do
>4) Validation (*are the requirements correct and feasible*)

**Quality attributes tradeoff**:
![[Quality Attribute Tradeoff Table.png|center]]

> To read this table, the rows are what was improved, the columns are how it was affected due to that quality attribute being improved.

**Quality attribute prioritisation**:
![[Quality Attribute Prioritisation Table Example.png|center]]

>"<" this means the row quality is preferred, while the "^" means the column quality is preferred (*the scores are hypothetical, it depends on the team*). 
## Classifying Quality Attributes

>[!info] Internal Quality Attributes
>Things that are <b><span style='color:var(--mk-color-yellow)'>not directly observable</span></b> when the software executes. 

>[!info] External Quality Attributes
>
>Things that are <b><span style='color:var(--mk-color-yellow)'>observable</span></b> when the software executes.

**External** quality attributes <b><span style='color:var(--mk-color-yellow)'>contributes to the user experiences</span></b>, while **internal** quality attributes are mostly <b><span style='color:var(--mk-color-yellow)'>perceived by developers/maintainers</span></b> and it encompasses aspects of **design** that may <b><span style='color: var(--mk-color-yellow)'>impact external attributes</span></b>.

**Examples of external** (*left*) **& internal** (*right*) **quality attributes**:
![[Examples of External & Internal Quality Attributes.png|center]]

>[!note] Design decisions are based what they software wants
>For example lets take an **embedded software** which operates on low/small resources should be:
>- Efficient
>- Reliable
>- Robust (*How the system fails gracefully*)
>- Safe
>- Secure
## Quality Attributes

### Performance

When users talk about performance they primarily talk about <b><span style='color:var(--mk-color-yellow)'>responsiveness</span></b>, however this is just 1 aspect of performance.

>[!info] Performance is an external quality attribute
>Uses can experience it and with a **low performance** will result in an <b><span style='color:var(--mk-color-red)'>unhappy user</span></b>.

Some **dimensions** for performance:
- Response time
- Throughput (*actual amount of data being transferred affected by bandwidth, packet loss, processing power*)
- Data capacity
- Dynamic capacity (*max number of concurrent users*)
- Predictability in real-time systems (*need to meet response time threshold*)
- Latency (*time delays affected by distance, network traffic, transport protocol*)
- Behavior in degraded models or overloaded conditions

>[!question] How does performance affect other quality attributes? 
>For example real-time systems, **performance impacts safety**. If overloaded or cannot keep up it will <b><span style='color: var(--mk-color-red)'>not response to critical events on time</span></b>.

Performance requirements can **affect design choices**
- Strict response times can require replicated databases (*locality for fast queries but hard to ensure consistency of data*)
- Latency can lead to deploying caches (*no need to keep sending data*)
- Monolithic vs Microservices
- Choice of hardware
- Type of network

>[!tldr] Caching
>
>[[Caching#Caching|Caching]] can be used to <b><span style='color:var(--mk-color-yellow)'>store frequently accessed data</span></b>.
>
>It is <b><span style='color:var(--mk-color-green)'>fast</span></b>, typically <b><span style='color:var(--mk-color-yellow)'>transient</span></b> (*store temporarily*) & stores a subset of data, not everything.
>
>Examples: Amazon ElasticCache, Redis Cache
### Scalability

It represents the software to <b><span style='color:var(--mk-color-yellow)'>accommodate growth</span></b>. However it is <b><span style='color:var(--mk-color-red)'>not always future proof</span></b>, thus a estimate growth usage is good to have.

>[!info] [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Scalability.md|Scalability]] is an internal quality attribute

[[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Scalability.md|Scaling]] a software <b><span style='color:var(--mk-color-red)'>has software & hardware consequences</span></b>. We either need to expand hardware capabilities or to enhance software performance (*parallel & distributed computing*).
#### Vertical Scaling

**Vertical** scaling refers to increasing the capacity of the system by <b><span style='color:var(--mk-color-yellow)'>adding more capability to the machines</span></b>. This can be upgrading & swapping to a better config / hardware.

>[!success] Easier to maintain as there will only be a few hardware to manage

>[!failure] Single point of failure all the software capabilities lies with the upgraded system
>If this system fails then everything fails.
#### Horizontal Scaling

**Horizontal** scaling refers to increasing the capacity of the system by <b><span style='color:var(--mk-color-yellow)'>adding more machines</span></b>.

>[!success] Increase resilient / fault tolerance
>Safe from single point of failure

>[!failure] Adds cost & complexity due to having more machines to manage

>[!example]  A good example is Kubernetes
>
>It can do <b><span style='color:var(--mk-color-yellow)'>auto scaling or dynamic scaling</span></b>, which essentially adds more containers or removes them if and when.

In terms of microservices which are small, focused & independently deployable, it is suited for horizontal scaling.
### Usability

Many aspects fall under usability, like ease of use (*meaningful messages, prompts, tool tips*), user-friendliness, learnability (*auto complete, customisations*), etc.

>[!info] Usability is an internal-external attribute
>Because the design choices that influences usability can be perceived by the users.

In a formal sense, it is the <b><span style='color:var(--mk-color-yellow)'>effort required to prepare inputs, operate and decipher output</span></b> (*essentially how much effort the user needs to put in*).

Ways to **calculate usability**:
- Average time needed to specify inputs
- Average time to complete a task
- Number of errors the user makes when doing a task
- Waiting time
- etc
# Requirement Specification
---
Typical **requirements management process** will include the following activities:
- Collect initial requirements from stakeholders
- Analyze requirements
- Define and record requirements
- Prioritize requirements
- Agree on and approve requirements
- Trace requirements to work items
- Query stakeholders after implementation on needed changes to requirements
- Utilize test management to verify and validate system requirements
- Assess the impact of changes
- Revise requirements
- Document changes
## Requirement Documentation

For <b><span style='color: #B0E0E6'>traceability</span></b>, when **recording down requirements** and <b><span style='color: #F0E68C'>what is it satisfied by</span></b>, it must contain the following:
- **Type**
- **Unique identifier**
- **High-level description**
- **Priority**
- **Other information** (*sprint, link to higher level objective*)

They can also be linked to:
- Use cases
- Design documents
- Code module
- Test cases
- etc

>[!example] Documents to store these requirements
>**Textual**:
>- Vision & scope document
>- Use case document
>- Software requirement specification (*SRS*)
>- Product backlog
>  
> **Visual**:
> - Structured analysis models (*data flow diagram, er diagram, state transition diagram*)
>   
>**Recollect**:
>- Feature list
>- User story
>  
> **Online tools**:
> - GitHub
> - JIRA
> - Word/Spreadsheet
## Requirement Validation

After listing down the requirements we need to do a [[Requirements Gathering#Validation|requirement validation]], to <b><span style='color:var(--mk-color-yellow)'>ensure what we collected is correct</span></b>.

When checking for validity we will concern ourselves with <b><span style='color:var(--mk-color-turquoise)'>validation</span></b> & <b><span style='color:var(--mk-color-turquoise)'>verification</span></b>.

>[!info] Validation
>
>Did we get the <b><span style='color:var(--mk-color-yellow)'>right requirements</span></b>. Does it trace back to the business objectives.

>[!info] Verification
>
>Did we get the <b><span style='color:var(--mk-color-yellow)'>requirements right</span></b>. Does it follow what the user wants?
>
>Usually requirements will <b><span style='color:var(--mk-color-yellow)'>have desirable properties</span></b> (*completeness, correctness, feasibiility, prioritization, unambiguity*).

This validation process can be done [[Requirements Gathering#Formal Reviews|formally]] or [[Requirements Gathering#Informal Reviews|informally]].
## AI in Requirements Engineering

Using LLMs, you can carry out a [[Requirements Gathering#Personas|persona specification]]by prompting the LLM that you are this use for what project tell me the requirements.

You can also <b><span style='color:var(--mk-color-yellow)'>specify the format you want the requirements to be recorded in</span></b>, thus making it a template for your requirements.

You can also ask LLMs to help <b><span style='color:var(--mk-color-yellow)'>tag or find sub-tasks</span></b> for your requirements for <b><span style='color:var(--mk-color-green)'>better traceability</span></b>.

It can also help <b><span style='color:var(--mk-color-yellow)'>correct requirements</span></b> (*ambiguity, confecting, missing requirements,*).

Lastly it can also <b><span style='color:var(--mk-color-green)'>help in prioritisation</span></b> by doing a feasibility prediction to see which requirements can be implemented successfully.

>[!warning] Just be careful of non-deterministic outputs & non-explainable chain of thoughts
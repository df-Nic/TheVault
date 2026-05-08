---
title: Requirements Gathering
Date Created: 2025-02-06
Last Updated: 2025-09-28
tags:
  - CS3213
  - SWE
  - RequirementElicitation
---
# Requirements Engineering
---
Or <span style='color:var(--mk-color-turquoise)'>RE</span> is the <span style='color:var(--mk-color-orange)'>process</span> of:
- **Finding out**
- **Analysing**
- **Documenting**
- **Checking**

> [!note] Requirements
> Descriptions of the <span style='color:var(--mk-color-yellow)'>services</span> that a system should provide and the <span style='color:var(--mk-color-yellow)'>constraints</span> on which it is operated on.

**RE is important** because it <span style='color:var(--mk-color-yellow)'>reflects the needs of the customers</span> for a system. The **cost of finding errors in the earlier stages** is <span style='color:var(--mk-color-green)'>lest costly</span>.

> [!important] RE is about the problem space, NOT the solution

RE is also **important for certain activities** in development such as:
- Customer relation & communication
- Software design
- Quality assurance & acceptance
- Maintenance & evolution

> [!abstract] Wicked Problem
> RE is also known as a <span style='color:var(--mk-color-turquoise)'>wicked problem</span>.
> 
> **Some characteristics**:
> - **No stopping rule** - There is no stopping of RE as its <span style='color:var(--mk-color-red)'>difficult to determine if we collected all requirements</span> (*relevant*)
> - **One-shot operation** - it is <span style='color:var(--mk-color-red)'>resource-intensive</span> & we <span style='color:var(--mk-color-red)'>cannot reset</span> after developing the software
> - **Unique** - <span style='color:var(--mk-color-yellow)'>Requirements are always different</span> for each project

> [!failure] Problems of RE
> - Users' incomplete understanding of needs
> - Conflicting views of different users
> - Users’ poor understanding of computer capabilities and limitations
> - Analysts’ poor knowledge of problem domain
> - It is easy to omit "obvious" information
> - Requirements evolve over time
> - The boundary of the system is ill defined
> - Unnecessary design information may be given (psychological trait)
> - Requirements often vague and untestable, e.g. "user friendly",
## Types Of Requirements

### Functional

These requirements describe what the <span style='color:var(--mk-color-yellow)'>system should do</span>. Most of the time stakeholders will focus on this.

> [!important] Functionality does not determine architecture
> A functionality can be developed in a variety of designs / methods

The **measurability** for function requirements is relatively simple, it weather the <span style='color:var(--mk-color-yellow)'>functionality works as intended</span>.
### Non-Functional

These requirements do not directly concern with the functionality of the system but <span style='color:var(--mk-color-yellow)'>how the system should be developed</span>.

These <span style='color:var(--mk-color-orange)'>arise through user needs</span> which can be due to:
- Budget constraints
- Organisation policies
- Security & safety regulations
- Interoperability with other systems

> [!danger] Tradeoffs between quality attributes
> Non-functional requirements can <span style='color:var(--mk-color-red)'>conflict with one another</span>, thus we need to choose which one to prioritise (*Security over usability*).

**Measurability** for non-functional requirements can be tricky, but we should write it in a <span style='color:var(--mk-color-yellow)'>quantifiable way so it can be objectively tested</span>.

> [!abstract] Quality attribute scenarios
> it can be used to <span style='color:var(--mk-color-yellow)'>clarify & document</span> non-functional requirements, <span style='color:var(--mk-color-green)'>making them measurable & testable</span>.
> 
> ![[Quality Attribute Scenarios.svg]]
> 
> > [!example] Quality Attribute Scenarios: Availability
> > 1. Source: server
> > 2. Stimulus: crashes
> > 3. Artifact: the server software
> > 4. Environment: any operational state
> > 5. Response: detects the abnormal state and re routes the traffic to another server
> > 6. Response measure: within 5 seconds of the server becoming unresponsive (*Better than 99.99% uptime since how can we measure 99.99%*)
#### Quality Attributes

##### Usability

It is a measure of how <span style='color:var(--mk-color-yellow)'>easy it is for the user to use</span> the product and the <span style='color:var(--mk-color-yellow)'>support the system provides</span>.

> [!example] Aspects of usability
> - Learning system features (*Functionality or design aspects*)
> - Using a system efficiently (*Short cuts or some functionality*)
> - Minimising user errors (*Undo*)
> - Adapting the system to user needs (*Auto complete*)

Some <span style='color:var(--mk-color-orange)'>metrics</span> to compute usability:
- Number of errors
- Learning time
- Number of tasks accomplished & how fast to complete the task
- User satisfaction
##### Availability

It is the notion of the <span style='color:var(--mk-color-yellow)'>system is there and ready to perform its task</span>. This also brings about <span style='color:var(--mk-color-turquoise)'>reliability</span> where if the system breaks it can <span style='color:var(--mk-color-yellow)'>recover by itself</span>.

> [!info] Linking availability to security & performance
>  1) **Security** 
>  There are certain cyber attacks which aims to make a <span style='color:var(--mk-color-yellow)'>service unavailable</span> (*DDOS*)
>  
>  2) **Performance**
>  It can be <span style='color:var(--mk-color-red)'>difficult to tell apart</span> if a system is very slow to respond or it has failed

Some <span style='color:var(--mk-color-orange)'>metrics</span> to compute availability:
- Availability percentage
- Time interval on when the system must be available
- Time to detect the fault
- Time to repair the fault

> [!quote] Service level agreements (SLAs)
> It shows the **common quantifiables** for the different availability percentages.
> 
> ![[Service Level Agreements (SLAs).png|center]]
##### Performance

It is more on the <span style='color:var(--mk-color-yellow)'>effectiveness of the software</span> in performing a task.

Some <span style='color:var(--mk-color-orange)'>metrics</span> to compute performance:
- Fast response time (*Latency*)
- Events completed within a timeframe (*Or non-completed as well*)
- Variance in response time (*Jitter*)
- Usage of computing resources
##### Modifiability

Its about the <span style='color:var(--mk-color-yellow)'>cost of performing changes</span> (*bug fixes, updates, performance improvements*). Most of the **cost occurs** <span style='color:var(--mk-color-red)'>after it has been released</span>.

Some <span style='color:var(--mk-color-orange)'>metrics</span> to compute cost of modification:
- Number of affected artifacts
- Effort & time needed
- Money
- Bugs introduced after modifying
##### Deployability 

It is the **ease and efficiency** with which a software application can be installed, configured, and made <span style='color:var(--mk-color-yellow)'>operational in a target environment</span>.

We **can use some aspects** of [[Software Engineering Processes#DORA|DORA]] for deployability.

Some <span style='color:var(--mk-color-orange)'>metrics</span> to compute deployability:
- Cost
- % of failed deployments
- Repeatability of the process
- Traceability of the process
- Cycle time of the process
##### Energy Efficiency

With global warming, there are <span style='color:var(--mk-color-yellow)'>policies & requirements are to save energy</span>. Being energy efficient is a increasingly popular non-functional requirement.

Some <span style='color:var(--mk-color-orange)'>metrics</span> to compute energy efficiency of a software:
- Kilowatt load on the system
- Amount of energy saved
- Time period in which the system must stay on
##### Security

The system’s ability to <span style='color:var(--mk-color-yellow)'>protect data and information</span> from unauthorized attack.

> [!info] CIA principles
> - **C**onfidentiality - Data or services are protected from people with unauthorised access
> - **I**ntegrity - Data & services are not subjected to unauthorised manipulation
> - **A**vailability - The system must be up and available for legitimate use

Unlike the others, security is <span style='color:var(--mk-color-red)'>hard to measure</span>. Some <span style='color:var(--mk-color-orange)'>metrics</span> to quantify security are:
- Resources compromised or ensured after an attack
- Accuracy of attack detection
- How much data is vulnerable to a particular attack

> [!abstract] Data security & privacy
> The government has some policies (*PDPA, GDPR, CPPA*), which are classified as non-functional requirements.
##### Safety

It is the system’s ability to <span style='color:var(--mk-color-yellow)'>avoid straying into states</span> that cause or lead to damage, injury, or loss of life.

It is also concerned with <span style='color:var(--mk-color-yellow)'>detecting and recovering from these unsafe</span> states to prevent or minimize resulting harm.

Unlike the others. Some <span style='color:var(--mk-color-orange)'>metrics</span> to quantify safety are:
- Amount or percentage of entries into unsafe states that are avoided
- Amount or percentage of unsafe states from which the system can (automatically) recover
- Amount or percentage of time the system is shut down
# RE Activities
---
And **before getting requirements** we <span style='color:var(--mk-color-yellow)'>must know who are the</span> <span style='color:var(--mk-color-turquoise)'>stakeholders</span> needs in the system.

> [!info] Stakeholders
> A person or organisation who has an <span style='color:var(--mk-color-yellow)'>influence over the system requirements</span> or is <span style='color:var(--mk-color-yellow)'>impacted by the system</span>.

Once we define the stakeholders we can start with RE and there are <span style='color:var(--mk-color-orange)'>3 key activities</span>:
1) **Elicitation** & **analysis**
2) **Specification**
3) **Validation**
## Elicitation & Analysis

This is the first step, where <span style='color:var(--mk-color-yellow)'>requirements are discovered</span> by interreacting with stakeholders (*can be functional or non-functional*).

This is the aim of the <span style='color:var(--mk-color-turquoise)'>elicitation process</span> to <span style='color:var(--mk-color-yellow)'>understand how the system can support their needs</span>.

After getting the requirements we can do a <span style='color:var(--mk-color-turquoise)'>feasibility study</span>, which is a <span style='color:var(--mk-color-yellow)'>short focus study</span>, answering <span style='color:var(--mk-color-orange)'>3 key questions</span>:
1) Does the system being developed contribute to the <span style='color:var(--mk-color-yellow)'>overall objectives</span> of the organisation?
2) Can the system be implemented <span style='color:var(--mk-color-yellow)'>within schedule & budget</span>, with current technologies?
3) Can the system be <span style='color:var(--mk-color-yellow)'>integrated with other systems</span> used.
### Elicitation Techniques

There are <span style='color:var(--mk-color-orange)'>many ways</span> to **gather user requirements** and **user stories** can be <span style='color:var(--mk-color-yellow)'>written or supported</span> based on any of these techniques.
#### Interview

it can be a <span style='color:var(--mk-color-yellow)'>one to one</span> setting or <span style='color:var(--mk-color-yellow)'>in small groups</span>, where the interviewer will ask questions pertaining to the system in development.

> [!abstract] Ways to conduct an interview
> 1) **Closed interview**: Stakeholders are asked a <span style='color:var(--mk-color-yellow)'>predefined set of questions</span>
> 2) **Open interview**: There is no predefined agenda, the engineering team <span style='color:var(--mk-color-yellow)'>explores a range of issues</span> with stakeholders, which develops a <span style='color:var(--mk-color-green)'>better understanding of their needs</span>.

> [!caution] Things to keep in mind when doing interviews
> **Don't make it fully open-ended**, try and ask some questions to get started & stay focus on the system.
> 
> **Do not expect specific and detailed requirements** as its <span style='color:var(--mk-color-red)'>difficult to visualise</span> what the system will be (*prototyping might help here*).
> 
> The **way in which questions are asked** has a <span style='color:var(--mk-color-yellow)'>significance on the response</span>.
#### Document Analysis

It is essentially <span style='color:var(--mk-color-yellow)'>reading existing documentation</span> (*Can be on other software*). From this you can <span style='color:var(--mk-color-green)'>gain domain knowledge</span> and <span style='color:var(--mk-color-green)'>reduce the time needed to interact with stakeholders</span>.

Not only that but we can also <span style='color:var(--mk-color-yellow)'>get existing requirement specifications</span> or <span style='color:var(--mk-color-yellow)'>corporate or industry standards</span>.

> [!warning] Risk of reading documents is that they can be out of date and not maintained anymore
#### Questionnaires

They are **useful** for a <span style='color:var(--mk-color-yellow)'>large population of stakeholders</span> as well as to get <span style='color:var(--mk-color-yellow)'>prioritization</span> of predefined requirements.

> [!failure] Drawbacks of Questionnaires
> **Questions are typically closed-ended** as its <span style='color:var(--mk-color-red)'>costly for stakeholders to fill</span> up & they do <span style='color:var(--mk-color-red)'>not allow follow-up questions</span>.
#### Workshops

They are facilitated sessions with **multiple stakeholders**, in workshops there <span style='color:var(--mk-color-yellow)'>will be formal roles</span> like, facilitator and scribe.

From observation, it is better if **workshops are conducted** in <span style='color:var(--mk-color-yellow)'>small groups rather than big ones</span> (*around 6*), which reduces communication overhead.

> [!abstract] Advantages & Disadvantages of Workshops
> 
> > [!success] Advantages
> > - More effective in <span style='color:var(--mk-color-yellow)'>resolving disagreements</span> compared to talking to individuals
> >  Useful when <span style='color:var(--mk-color-yellow)'>quick elicitation turnaround</span> is needed due to scheduling constraints
> 
> 
> > [!failure] Disadvantages
> > It can be <span style='color:var(--mk-color-yellow)'>resource intensive</span> & sometimes it <span style='color:var(--mk-color-yellow)'>requires a lot of time and participants</span>

> [!example] User Story Workshops
> Everyone <span style='color:var(--mk-color-yellow)'>contributes to user stories</span> & prioritisation can happen later by customers.
> 
> It can also **combine elements of brainstorming & low-fidelity prototyping** (*paper prototype*).
#### Focus Groups

Unlike workshops, focus groups are **facilitated sessions with users** who <span style='color:var(--mk-color-yellow)'>does not have decision-making power</span> (*users*).

This allows them to **explore** different <span style='color:var(--mk-color-yellow)'>needs</span>, <span style='color:var(--mk-color-yellow)'>impressions</span> & <span style='color:var(--mk-color-yellow)'>preferences</span> from end users.

> [!example] Is like developing a game and letting gamers play test it
#### Prototyping

It is to <span style='color:var(--mk-color-yellow)'>develop a simplified model </span>of the system (*using Figma for example*):
- **Low-fidelity**: Paper model
- **High-fidelity**: An executable model with simple implementation of the system

**Useful** for parts of the system that are <span style='color:var(--mk-color-yellow)'>not well understood as well as user interfaces</span> and <span style='color:var(--mk-color-yellow)'>explore design alternatives</span>.

It can also be used to:
- **Clarify**
- **Validate**
- **Complete** requirements (*or refine them*)
#### Observation / Ethnography

It is essentially <span style='color:var(--mk-color-yellow)'>seeing how users operate</span> on their daily activities, this can be in <span style='color:var(--mk-color-orange)'>2 ways</span>:
1) **Active**: The person will actually <span style='color:var(--mk-color-yellow)'>participate in the activities</span>
2) **Passive**: They just observe others

This helps <span style='color:var(--mk-color-green)'>uncover implicit system requirements</span> based on how people work and not the formal process. 

However it <span style='color:var(--mk-color-red)'>cannot uncover new features</span> because you are observing them using an existing system (*can use prototyping to address this issue*).
#### Personas

It is an <span style='color:var(--mk-color-yellow)'>archetype of a user group</span>, it can be given a hypothetical name, goals, frustrations etc. This can be based on research or assumptions.

Personas can be <span style='color:var(--mk-color-yellow)'>used in meetings</span> as a way to think about requirements.
## Specification

Requirements gathered are **converted** into a <span style='color:var(--mk-color-yellow)'>standard format</span> (*documentation*).
### User Stories

[[Project Requirements#User Stories|User stories]] (*agile*) <span style='color:var(--mk-color-yellow)'>describes some functionality</span> that is valuable to users/stakeholders. However it **serves as a placeholder**, as it represents customer requirements <span style='color:var(--mk-color-red)'>not documentation</span>.

It contains <span style='color:var(--mk-color-orange)'>3 aspects</span> (three Cs)
1) **Card**: A written description of the story (*specification*)
2) **Conversation**: Verbal exchange with the customer to flesh out the details (*elicitation & analysis*)
3) **Confirmation**: Acceptance tests specified by the customer (*validation*)

> [!note] Writing acceptance tests
> It is recommended to be <span style='color:var(--mk-color-yellow)'>short & incomplete</span> as it should only **convey information to let developers know when the task is done**.

User stories <b><mark style='background:var(--mk-color-yellow)'>should not contain a lot of details</mark></b>, but **short annotations or notes can be included**.

> [!info] Epics
> It is a type of <span style='color:var(--mk-color-yellow)'>user stories that are large</span> in terms of development and will be <span style='color:var(--mk-color-yellow)'>spilt into multiple smaller stories</span> later on.
### Use Case

[[Project Requirements#Use Case|Use cases]] (*plan-driven*) describes the <span style='color:var(--mk-color-yellow)'>interaction between an actor and the system </span>. It is usually coupled with a diagram called [[Models#Use Case Diagram|use case diagram]].

> [!info] Use case diagram
> A **high level description** of all the actors and the interactions they have with the system, documented with a textual description.

A use case might encompass **multiple** <span style='color:var(--mk-color-turquoise)'>scenarios</span>.

> [!info] Scenarios
> It is like a flow of a <span style='color:var(--mk-color-yellow)'>single instance of usage of the system</span> (*How will the user use the system to do something*).
> 
> It can include:
> - What can go wrong
> - Normal flow of events
> - Pre-requisites
> - What the system does before and after a scenario
>   
>  These use cases <span style='color:var(--mk-color-green)'>captures more of the user requirements</span> as compared to user stories. 

Here are some <span style='color:var(--mk-color-orange)'>guidelines when writing use cases</span> with natural language:
- **Standard formatting**
- **Language consistency** to distinguish between **mandatory** & **desirable** requirements
- Use text highlighting
- **Avoid the use of jargon** (*Slang or not commonly known prefixes like LGTM*)
- Associate **a rational** with each user requirement, documenting why and who proposed the requirement for consultation.

You can also **add graphs table images** and many more if it is <span style='color:var(--mk-color-red)'>difficult to write it clearly</span>.
## Validation

Lastly, we need to **check** that the **requirements** defined is <span style='color:var(--mk-color-yellow)'>what the customer wants</span>.

> [!info] V-model & testing for plan driven development
> ![[V-Model & Testing (Plan-Driven).png|center]]

For **agile**, requirements are validated through <span style='color:var(--mk-color-yellow)'>frequent communication</span> with stakeholders. While for **plan-driven**, it focuses on defects and unclarities in the <span style='color:var(--mk-color-yellow)'>requirements document</span>.

> [!summary] What to check on the requirements document
> 1) **Validity checks**: Check if the<span style='color:var(--mk-color-yellow)'> requirements reflect the real needs</span> of the system users.
> 2) **Consistency checks**: Ensure that the requirements <span style='color:var(--mk-color-yellow)'>do no conflict</span>
> 3) **Completeness checks**: All functions and constraints intended by the system user is inside
> 4) **Realism checks**: Requirements can be <span style='color:var(--mk-color-yellow)'>implemented within the proposed budget</span>
> 5) **Verifiability**: System requirements should be <span style='color:var(--mk-color-yellow)'>written so that they are verifiable</span>
### Informal Reviews

They are done by other **people** who are <span style='color:var(--mk-color-yellow)'>not tasked to conduct proper reviews</span>.

<span style='color:var(--mk-color-orange)'>Types</span> of informal reviews:
- **Peer review**: Someone other than the author, reviews the requirements
- **Informal reviews**: Collect unstructured feedback from others (*1 person, a group or a walkthrough*)
### Formal Reviews

Also known as <span style='color:var(--mk-color-turquoise)'>inspections</span> are usually carried out by a <span style='color:var(--mk-color-yellow)'>team of reviewers</span>.

<span style='color:var(--mk-color-orange)'>Types</span> of formal reviews:
- **Formal requirements reviews**: Done by reviewers who check for errors & inconsistencies
- **Inspection**: Tedious and time consuming, but one of the highest leverage software quality techniques available

> [!note] More on inspections
> Though <span style='color:var(--mk-color-red)'>time consuming and requires multiple stakeholders & formal roles</span>, it <span style='color:var(--mk-color-green)'>works for every software product</span>, not just requirement documents.
> 
> Any **defects** will be placed in a <span style='color:var(--mk-color-turquoise)'>defect checklist</span> and the <span style='color:var(--mk-color-yellow)'>team will need to rework & follow-up</span>.
# RE Process Models
---
## Agile Methods & RE

Typically agile methods do not provide a complete PR process model because <span style='color:var(--mk-color-yellow)'>changes in requirements are rapid</span>.

The <span style='color:var(--mk-color-red)'>requirements document will be out of date</span> as soon as it is written. Thus **typically**, <span style='color:var(--mk-color-yellow)'>user stories are written</span>.

> [!note] High level requirements document
> It is ok to **have a high level requirements document** which documents business and dependability requirements.
## Plan-Driven & RE

Here there is a process model which describes how to combine the individual activities. <span style='color:var(--mk-color-yellow)'>RE is done before implementation</span> of the system.

This **results in a requirements document** (*or software requirements document*), which may be part of the system development contract and it <span style='color:var(--mk-color-yellow)'>states what the developers should implement</span>.

This document can contain both <span style='color:var(--mk-color-turquoise)'>user requirements</span> & <span style='color:var(--mk-color-turquoise)'>system requirements</span>.

> [!note] Plan-Driven specific requirements
> These types of requirements are <b><mark style='background:var(--mk-color-orange)'>only specific to plan-driven models</mark></b>. Can be written in text, graphs, mathematical system models.
>
> > [!info] User requirements
> > Essentially they are **services & constraints the system** is <span style='color:var(--mk-color-yellow)'>expected to provide to system users</span> at a **high-level** (*external behavior only*).
> 
> > [!info] System requirements
> > It is a <span style='color:var(--mk-color-yellow)'>more detailed description</span> on what is to be implemented. Providing a detailed specification of the whole system.

> [!important] Requirements management planning
> To account for changing requirements.

## Spiral Model

![[Spiral Model.png|center|500]]

We **start in the middle**, where we are mostly <span style='color:var(--mk-color-yellow)'>interested high-level requirements</span>.

As we go **further into the outer rings**, the <span style='color:var(--mk-color-yellow)'>requirements are more detailed</span>. Which we will eventually end up at the **red box** which is the <span style='color:var(--mk-color-yellow)'>output of the model</span>.

if you are using <span style='color:var(--mk-color-blue)'>agile development</span>, then there is no need to prototyping as the <span style='color:var(--mk-color-yellow)'>system can be implemented concurrently</span>.

> [!warning] Varying iterations
> There is **no need to go the full spiral** as the number of iteration varies. Once the requirement are elicited, you can exit the spiral
## Elicitation & Analysis Model

![[Elicitation & Analysis Model.png|center]]

The **first step** is to discover user requirements & domain requirements. Afterward we can <span style='color:var(--mk-color-yellow)'>classify and organise them</span> which can be done through <span style='color:var(--mk-color-turquoise)'>viewpoints</span>.

> [!info] Viewpoints
> **Stakeholders are divided into groups** called <span style='color:var(--mk-color-turquoise)'>viewpoints</span>, then the <span style='color:var(--mk-color-yellow)'>requirements from that viewpoint are in 1 group</span>.

Afterwards, <span style='color:var(--mk-color-yellow)'>requirements will be prioritized</span> & any <span style='color:var(--mk-color-yellow)'>conflicts will be resolved</span> (*have to meet with stakeholders*).

Lastly, the <span style='color:var(--mk-color-yellow)'>requirements will be documented and output</span> into the next round. 
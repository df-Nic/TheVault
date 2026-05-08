---
title: Project Requirements
Date Created: 2024-09-07
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE
  - RequirementElicitation
---
# Requirements
---
A requirement is just something that needs to **fulfilled by the project**. In a project it can be <span style='color:var(--mk-color-orange)'>classified into 2 types of projects</span>:
1) **Brownfield project** - Develop an <span style='color:var(--mk-color-yellow)'>existing</span> project
2) **Greenfield project** - Develop a project <span style='color:var(--mk-color-yellow)'>from scratch</span>

These **requirements** are usually **from stakeholders** (*People that are involved or affected by the project*).

**Identifying requirements** can be <span style='color:var(--mk-color-red)'>difficult</span>, as stakeholder might <span style='color:var(--mk-color-yellow)'>not know their precise needs</span> or they are <span style='color:var(--mk-color-yellow)'>not sure on how to communicate their requirement correctly</span>.
## Non-Functional & Functional

**Functional requirements**
>They specify what the <span style='color:var(--mk-color-yellow)'>system should do</span>.

Some <span style='color:var(--mk-color-orange)'>samples</span> are:
- Login feature
- Register feature
- Add to cart feature

**Non-functional requirements**
>They <span style='color:var(--mk-color-yellow)'>specify the constrains</span> the system is developed or operated.

It can be **in terms of**, privacy, response time, data requirements, environment requirements etc.

Some <span style='color:var(--mk-color-orange)'>samples</span> are:
- Product should follow security policies
- Product should respond within 1 second
- Product should work on both mobile and PC

As compared to functional requirements, they are <span style='color:var(--mk-color-red)'>harder to spot</span> and can be <span style='color:var(--mk-color-yellow)'>critical to the success of the software</span>.

```ad-summary
title: Quality of Requirements
collapse: open
Here are some characteristics of well-defined requirements :
- Unambiguous
- Testable (verifiable)
- Clear (concise, terse, simple, precise)
- Correct
- Understandable
- Feasible (realistic, possible)
- Independent
- Atomic
- Necessary
- Implementation-free (i.e. abstract)

Besides these criteria for individual requirements, the set of requirements as a whole should be:
- Consistent
- Non-redundant
- Complete
```
## Prioritising Requirements

Some requirements are **more important than others** (*More urgent*) and thus they should be <span style='color:var(--mk-color-yellow)'>more focused on</span>.

The **level of importance is subjective** and should be <span style='color:var(--mk-color-yellow)'>defined by stakeholders</span>.

**For example:** `Essential`, `Typical`, `Nodel`

it is also possible for a requirement to be `out of scope`. They are <span style='color:var(--mk-color-yellow)'>requirements that are good to have</span> but is not required for the product.
## Gathering Requirements

```ad-tldr
title: Ways of Gathering Requirements
collapse: open

There are <span style='color:var(--mk-color-orange)'>2 types</span> of requirement gathering techniques:
1) **Ask**
	- Surveys
	- Interviews
	- Focus groups
2) **Ownself invention**
	- Study other products
	- Observe users
	- Brainstorm
```

**Brainstorming**
>Is a group activity to <span style='color:var(--mk-color-yellow)'>generate diverse and creative ideas</span>. There is <span style='color:var(--mk-color-green)'>no such thing as bad ideas</span> as the goal is to come up with whacky ideas.

**Product studying**
>Study other existing products can <span style='color:var(--mk-color-yellow)'>identify shortcomings</span> that can be addressed in the new product.

**Observing users**
>Observe user patterns in their environment and <span style='color:var(--mk-color-yellow)'>uncover patterns</span> or ways to <span style='color:var(--mk-color-yellow)'>make their life easier</span> of a particular subject.

**Focus groups**
>Unlike surveys or interview, it is a informal interview in a group setting to <span style='color:var(--mk-color-yellow)'>get to know certain issues or requirements</span> from stakeholders.
### Prototyping

It is the process of <span style='color:var(--mk-color-yellow)'>building a mock up</span> to:
- **Get feedback**
- **Validate technical concepts**
- **Give a preview to stakeholders**
- **Can act as field testing**

In prototyping, the interview <span style='color:var(--mk-color-yellow)'>knows how the users interact</span> with the product from which they can understand what <span style='color:var(--mk-color-yellow)'>features are needed</span> as well as the <span style='color:var(--mk-color-yellow)'>priority of said features</span>.

## Specifying Requirements

Here are some **important things** to have when <span style='color:var(--mk-color-orange)'>specifying requirements</span>:
- **Prose**
- **Feature list**
- **User stories**
- **Use case**
- **Prototypes** (*Mainly for GUI*)
- **Supplementary requirements** (*Non-functional requirements*)
- **Glossary** (*Specify terms related to the project and its definition*)
### Prose

It is essentially a **text description** for requirements. It is <span style='color:var(--mk-color-green)'>useful for describing abstract ideas</span> like the vision of a product.

One thing to take note is that try and <span style='color:var(--mk-color-red)'>not give lengthily prose</span>. As it can be hard to follow.
> [!example] Example of a Prose
> TEAMMATES aims to become the **biggest student project in the world** (biggest here refers to 'many contributors, many users, large codebase, evolving over a long period'). Furthermore, it aims to serve as a training tool for Software Engineering students who want to learn SE skills in the context of **a non-trivial real software product**.
### Feature List

Basically a **list of features** of a product <span style='color:var(--mk-color-yellow)'>grouped according to some criteria</span> such as aspect, priority, order of delivery, etc.

> [!example] Example of a Feature List
> A sample <span style='color:var(--mk-color-turquoise)'>feature list</span> from a simple **Minesweeper game**:
> 
> 1) Basic play – Single player play.
> 2) Difficulty levels
> 	- Medium levels
> 	- Advanced levels
> 3) Versus play – Two players can play against each other.
> 4) Timer – Additional fixed time restriction on the player.
> 5) ...
### User Stories

A <span style='color:var(--mk-color-turquoise)'>user story</span> is a **description of a feature** told from the <span style='color:var(--mk-color-yellow)'>perspective from the user</span>, <span style='color:var(--mk-color-red)'>not developer</span> who desires this new capability but they are <span style='color:var(--mk-color-red)'>not detailed enough</span> to **tell us exact details** of the product.

It captures requirements that are convenient for **scoping**, **estimation** and **scheduling**. Also the <span style='color:var(--mk-color-yellow)'>specifications should be low level</span>.

> [!example] Writting a User Story
> There are <span style='color:var(--mk-color-orange)'>3 things to take note</span> when writting user stories:
> 1) The user/role
> 2) The function
> 3) The benefit (*Optional if its too obvious*)
> 
> Thus it should be in this format: As a `{User/Role}` I can `{function}` so that `{benefit}`

These <span style='color:var(--mk-color-turquoise)'>user stories</span> can be written physically or using a digital tool (*GitHub Project Boards*). And they can be either <span style='color:var(--mk-color-yellow)'>functional or non function requirements</span>.

For **broader functionality features**, a **higher level** user story, <span style='color:var(--mk-color-turquoise)'>epics</span> (*themes*) is preferable <span style='color:var(--mk-color-yellow)'>to breakdown the functionality</span> into smaller user stories.

Certain **conditions of satisfaction can be specified** in the user story, to say what needs to be true to be accepted as done.

Other useful information that can be added to the user story are:
- **Priority** - How important is the user story
- **Size** - Amount of effort needed to implement the user story
- **Urgency** - How soon must the feature be added

> [!info] Recording Requirements with User Stories
> In the early stages of development, user stories is a <span style='color:var(--mk-color-green)'>good way of recording requirements</span>.
> 
> 1) **Clear the mind** of preconceived product ideas
> 2) Define the target user as a **persona**
> 3) Define the **problem scope**
> 4) **List the scenarios** to form a narrative
> 5) **List user stories** to support scenarios
> 
> And <b><span style='color:var(--mk-color-red)'>do not</span></b>
> - Evaluate the value of the user stories while brainstorming
> - Be hasty in discarding unusual user strories
> - Go into too much detail
> - Be biased by preconceieved product ideas
> - Discuss implimentation or weather it will be actually implimented
### Glossary

It is essentially a **project dictionary**, which serves to ensure that all <span style='color:var(--mk-color-yellow)'>stakeholders have a common understanding</span> of the noteworthy terms, abbreviations, acronyms etc.
### Supplementary Requirements

A <span style='color:var(--mk-color-turquoise)'>supplementary requirements</span> section can be used to <span style='color:var(--mk-color-yellow)'>capture requirements that do not fit elsewhere</span>. Typically, this is where most **non-functional requirements** will be listed.
# Use Case
---
This describes an <span style='color:var(--mk-color-yellow)'>interaction between the user and the system</span> for a **specific functionality** of the system. This <span style='color:var(--mk-color-yellow)'>captures functional requirements</span> of a system.

UML has a diagram called [[Models#Use Case Diagram|use case diagram]] that <span style='color:var(--mk-color-yellow)'>illustrates the use cases of a system</span> (*Table of content like*).

Use cases can be <span style='color:var(--mk-color-yellow)'>specified in various levels of detail</span>. It can be **high level** (*Broad scope*) or **low level** (*Something specific*).

> [!important] Things to Note when Modeling Use Case
> It is good to <span style='color:var(--mk-color-yellow)'>start with high level</span> use cases and <span style='color:var(--mk-color-yellow)'>progressively work toward lower level</span> use cases.
> 
> But be mindful of which level of detail you are working at and <span style='color:var(--mk-color-red)'>not to mix use cases of different levels</span>.

We can also use use cases as **documenting system requirements**

> [!info] Pros & Cons of Documentation Using Use Cases
> <b><mark style='background:var(--mk-color-green)'>Advantages</mark></b>:
> - They use a simple notation and are <span style='color:var(--mk-color-green)'>easy for users to understand</span> and give feedback.
> - They decouple user intention from mechanism, allowing the <span style='color:var(--mk-color-green)'>system designers more freedom</span> to optimize how a functionality is provided to a user.
> - Identifying all possible extensions encourages us to <span style='color:var(--mk-color-green)'>consider all situations</span> that a software product might face during its operation.
> - Separating typical scenarios from special cases encourages us to <span style='color:var(--mk-color-green)'>optimize</span> the typical scenarios.
> 
> <b><mark style='background:var(--mk-color-red)'>Disadvantages</mark></b>:
> - They <span style='color:var(--mk-color-red)'>cannot capture</span> requirements that does **not involve user interaction** with the system.
## Writing Use Cases

### Identify

First we need to **identify** the <span style='color:var(--mk-color-turquoise)'>actors</span> (*Users*) and the <span style='color:var(--mk-color-turquoise)'>system</span>.

The **system** is essentially the <span style='color:var(--mk-color-yellow)'>product you are developing</span>. While the **user** is anyone <span style='color:var(--mk-color-yellow)'>outside of the system</span>.

> [!note] Actor's In Use Cases
> A actor can be a person ao another person, but they <b><span style='color:var(--mk-color-yellow)'>cannot be part of the system</span></b>.
> 
> In a use case:
> - There can be multiple actors
> - An actor can be in many use cases
> - A person or system an play many roles (*Actors*)
> - Many persons can play a single role
### Details

Now we need to write the main body which consist of a **sequence of steps** that describes the <span style='color:var(--mk-color-yellow)'>interaction between system, and actors</span>. It can also <span style='color:var(--mk-color-yellow)'>include loops</span> as well by **indicating what steps gets repeated**.

Each step just needs to be a **simple description** of who does what and this description <b><mark style='background:var(--mk-color-yellow)'>only tells the external visible behavior</mark></b> and <span style='color:var(--mk-color-red)'>not the internal details of the system</span>.

In addition the step also <span style='color:var(--mk-color-yellow)'>give the intention</span> of the actor (*Be as general as possible*).

The **body** can be <span style='color:var(--mk-color-orange)'>spilt into a few sections</span>:
- **Main Success Scenario** (*MSS*)
	>Describes the interaction <span style='color:var(--mk-color-yellow)'>assuming nothing goes wrong</span>. MSS should be <b><mark style='background:var(--mk-color-yellow)'>self-contained</mark></b> meaning it should give a complete usage scenario. Can have loops as well.

- **Extensions** (*Add-ons*)
	>They are <span style='color:var(--mk-color-yellow)'>exceptional/alternative flow of events</span>, something that is **not expected in the MSS**.

Extensions are labeled as `3a.` or `3b.` indicating it can **happen after step 3** while `*a.` means it can **happen at any step**.

<span style='color:var(--mk-color-red)'>Catastrophic failures should not be included</span> since it is beyond the systems control.

- **Include** (*Using other use cases*)
	>To denote another use case, **in the MSS** just <span style='color:var(--mk-color-yellow)'>underline the next</span>. Use it when it is **repeated** or to **prevent cluttering**.

- **Preconditions**
	>States the <span style='color:var(--mk-color-yellow)'>required state the system must be</span> in before the use case starts (*E.g. Logged in*).

- **Guarantees**
	>Specify what the <span style='color:var(--mk-color-yellow)'>guaranteed outcome</span> is at the end of the operation.

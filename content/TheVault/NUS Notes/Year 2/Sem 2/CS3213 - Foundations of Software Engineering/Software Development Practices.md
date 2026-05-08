---
title: Software Development Practices
Date Created: 2025-03-17
Last Updated: 2025-09-28
tags:
  - CS3213
  - SWE
  - SWEPractices
---
# Development Practices
---
In **architecture** it describes more of the <b><span style='color:var(--mk-color-yellow)'>"What" are we building</span></b> aspect, while **development practices** are more on the <b><span style='color:var(--mk-color-yellow)'>"How" are you building</span></b> a software.

Development practices are **linked** to the <b><span style='color:var(--mk-color-yellow)'>people and the organisation</span></b>.

> [!question] Is there a universal set of practices?
> There are <b><span style='color:var(--mk-color-red)'>no universal practices</span></b>, however <b><span style='color:var(--mk-color-yellow)'>there are good practices that we can apply</span></b>.

**Similarities between code & practices**:
- Need for agreement
- No silver bullets (*Some practices can work in a broad sense but its not absolute*)
- Change over time (*Organisation changes thus the practices will change*)

In the end, learn the best practices, know that its important to have teamwork, collaboration and consistency as well as thinking about your organisation's needs.
## Source Control

**Primary output** of SWE is <b><span style='color:var(--mk-color-yellow)'>code</span></b>, and we need some way of <b><span style='color:var(--mk-color-yellow)'>managing our code</span></b> and that's where source comes in.

> [!failure] Source control IS NOT git
> Git is a **tool** for source control.

When<span style='color:var(--mk-color-orange)'> thinking about source control management</span> (*SCM*):
- Who is allowed to view / change code
- How are changed managed
- How are dependencies managed
- How does source control integrate with your tools
- Branches, tags, merges, etc

SCM <span style='color:var(--mk-color-orange)'>tool considerations</span>
- Centralised vs Decentralised
- Dependency management
- Scalability (*Example, git has a issue with large groups consisting tens of thousands*)
- Development tool support
- Expertise/opinions in your team

> [!note] GitHub repository type
> GitHub is not solely decentralized, it <b><span style='color:var(--mk-color-yellow)'>can be both depending on how you set it up</span></b>. 

<span style='color:var(--mk-color-orange)'>Good SCM practices</span>:
- **Single source of truth** (*defined definitions, unambiguous*)
- Security
- Consistency
- Small focused changes - ideally idempotent / orth to others
- Clarity of what is being changed and why
- Use branches and tags appropriately
	- Make it easy for everyone to find the right code and not trample
	- Avoid long lived branches
- Use toolset for managing dependencies
### Centralised & Decentralised

When something is **centralised**, it means that there is <b><span style='color:var(--mk-color-yellow)'>only 1 main place</span></b> which determines the state of code.

While for **decentralised** it has <b><span style='color:var(--mk-color-yellow)'>more than 1 place</span></b> where each place has some version as part of the bigger product.

> [!fail] Issues with centralised setups
> The disadvantage is that there is a <b><span style='color:var(--mk-color-red)'>single point of failure</span></b>.

> [!fail] Issues with decentralised setups
> The disadvantage is that its <b><span style='color:var(--mk-color-red)'>difficult to get the latest versions for each of the repositories</span></b>.

Naturally it is a **tradeoff** between what you want to use.
## Coding Styles

We want **code** to be <b><span style='color:var(--mk-color-yellow)'>consistent</span></b> for everyone and making it <b><span style='color:var(--mk-color-yellow)'>understandable</span></b>.

Why is <span style='color:var(--mk-color-orange)'>coding style important</span>:
- Unnecessary changes in the SCM (*reformatting*)
- Inconsistency make code harder to read
- Always differences in style

<b><span style='color:var(--mk-color-yellow)'>Consistency is key</span></b> and we should <b><span style='color:var(--mk-color-yellow)'>agree as a team</span></b>.

<span style='color:var(--mk-color-orange)'>Key elements of style guide</span>:
- **Consistency** is better than optimality
- Focus on **making code clearer** and unsurprising
- **Practicality is better** than clever and pretty
- Not just formatting - idioms and how things get done
- Use an auto formatter
## Software Versioning

> [!info] Versioning
> Is <b><span style='color:var(--mk-color-yellow)'>assigning identifiers</span></b> to bundles of software (*code base version used*).
> 
> > [!example] Example of GitHub release
> > In github when doing a release it will **create a tag for it**.

How to **handle versioning depends** on <b><span style='color:var(--mk-color-yellow)'>how we deploy an application</span></b>:
- Web services with rolling releases (*v1, v1.1*)
- App stores
- Sending binaries to customers on a floppy disk
- Embedded inside an airplane or medical device

> [!question] Why do we need have versioning?
> As developers we need to **know what version the users are using**. But also we need to **know what version you are using** as we <b><span style='color:var(--mk-color-yellow)'>have dependencies which needs to be managed</span></b>.
### Semantic Versioning

Its a propose a <b><span style='color:var(--mk-color-yellow)'>simple set of rules and requirements</span></b> that dictate **how version numbers are assigned and incremented**.

Its usually used when there is a public API.

The numbering does as such **MAJOR.MINOR.PATCH**
- **Major** version when you make <b><span style='color:var(--mk-color-yellow)'>incompatible API changes</span></b>
- **Minor** version when you <b><span style='color:var(--mk-color-yellow)'>add functionality</span></b> in a <b><span style='color:var(--mk-color-yellow)'>backward compatible</span></b> manner
- **Patch** version when you make <b><span style='color:var(--mk-color-yellow)'>backward compatible bug fixes</span></b>

> [!warning] This is not the only way
> This is not the only way you can also <b><span style='color:var(--mk-color-yellow)'>use words or names</span></b>. But ensure it is <b><mark style='background:var(--mk-color-yellow)'>identifiable</mark></b>.
> 

How do we know, weather this version will break the system, well we don't. As a developer we will not know how others use the API.

> [!abstract] Hyrum's law
> With a sufficient number of users of an API, it does not matter what you promise in the contract: all observable behaviors of your system will be depended on by somebody.

> [!important] Semantic versioning is a label to heuristic
> It does <b><span style='color:var(--mk-color-red)'>not guarantee that it will not break anything</span></b>. It can <b><span style='color:var(--mk-color-green)'>guarantee that regression tests works</span></b>.
#### Commits

We can also just use **commits as our versioning** since <b><span style='color:var(--mk-color-yellow)'>every commit will have a unique hash</span></b> based on the source code.

> [!success] Advantages
> - **Automatic**, there is <b><span style='color:var(--mk-color-green)'>no additional setup</span></b> or effort required
> - Useful to **internally track builds**

> [!fail] Disadvantages
> - **Not all commits are release versions**
> - The has value **gives no information** and is **difficult to remember**
#### Assigned Identifiers

As mentioned previously it is just using common schemes like <b><span style='color:var(--mk-color-yellow)'>rolling numbers or words, date</span></b>.

> [!success] Advantages
> - **Easy to remember**
> - Help in **branding** (*like macOS uses big cats in the past*)
> - Can be used to **infer ordering between versions**

> [!fail] Failure
> If our product has **very frequent changes**, then it is **not practical** (*preferably 6 to 12 months*).

> [!question] So which scheme to use?
> There is <b><mark style='background:var(--mk-color-yellow)'>no one best scheme</mark></b>, it depends on:
>  - Organisational needs
>  - Deployment strategy
>  - Frequency of releases
>  - Need of the users or maybe the marketing aspect 
## Branching Strategies

There are many <span style='color:var(--mk-color-orange)'>types of branching strategies</span>:
1) **Categorical branches**: One branch can be for all features, one for bug fixes and so on
   ![[Categorical branches.png|center]]
2) **Trunk branches**

![[Trunk branches.png|center]]

However when we **branch** out we <b><span style='color:var(--mk-color-yellow)'>want some isolation</span></b>.

> [!important] Keep your branches short or short lived
> Leaving it too long will have issues in a company setting as other people will make changes which results in you needing to update your branch.

> [!question] What is the best branching strategy
> It mainly **depends** on the <b><span style='color:var(--mk-color-yellow)'>organisation, deployment strategy and other aspects</span></b>.
> 
> But we need to ensure 2 things:
> 1) **Single source of truth**
> 2) Consistency

## Dependencies

Dependencies are **anything** that is needed for your <b><span style='color:var(--mk-color-yellow)'>software to work correctly that is not in your control</span></b>.

Some of these includes:
- Libraries
- Build tools
- External services
- Build tools
- Compile time vs run time dependencies, big difference

Dependencies can **help but they can also be a** <b><mark style='background:var(--mk-color-red)'>liability</mark></b>:
- It can <b><span style='color:var(--mk-color-green)'>make coding easier</span></b>
- But if something does not work then <b><span style='color:var(--mk-color-red)'>debugging can be complicated</span></b> (*multiple points of failure*)

<b><span style='color:var(--mk-color-red)'>Dependency HELL</span></b>, also known as diamond dependencies:
![[Dependency Hell.png|center]]

**Packet manages does help** with this but if not we <b><span style='color:var(--mk-color-yellow)'>need to fix either one</span></b>.

> [!question] What to do when a dependency introduces a change that breaks your code?
>  - **Package manager** configuration files to denote the version to use
>  - You can **fork the repository** and modify this (*can also be done if they can't or don't fix a bug, or they deprecate a feature or out of date*)
>  - You can just **add it into your code**

The **bottom line** is that we <b><span style='color:var(--mk-color-yellow)'>need to manage dependencies</span></b> and if there is something wrong we have to develop it ourselves.

<span style='color:var(--mk-color-orange)'>How can we managing dependencies</span>
- Small/ critical library: keep in same library
- Medium library: Keep your own repository
- Large well established library (*especially one that gets updated frequently*): submodule by GitHub
- Runtime: Lockfiles, containers
- Packages managers (*Both compile time and run time dependencies*)
- There is no silver bullets...
## Depreciation

Systems or API can become obsolete, so **how can remove this code that we do not need**? Remember that <b><span style='color:var(--mk-color-red)'>code is more of a liability</span></b> since it has <b><span style='color:var(--mk-color-yellow)'>operational cost and requires effort to update the code base</span></b>.

However we **cannot just remove it** since existing systems and developers are likely to rely on code (*can affect functions to entire software stacks*). It is possible that software will eventually be decommissioned.

> [!info] Deprecation
> It is the process of orderly <b><span style='color:var(--mk-color-yellow)'>migrate away from</span></b> and <b><span style='color:var(--mk-color-yellow)'>eventual removal</span></b> of obsolete systems.
> 
> We want to be able to plan for and execute an <b><span style='color:var(--mk-color-yellow)'>orderly</span></b> migration.

Deprecation is <b><mark style='background:var(--mk-color-yellow)'>not related to how old the code</mark></b> is.

> [!fail] Bad practices
> Having **multiple systems performing the same function** <b><span style='color:var(--mk-color-red)'>impedes the evolution</span></b> of newer systems.
> 
> This is because the new systems will need to maintain compatibility with the older systems.

Once s <span style='color:var(--mk-color-orange)'>software system exists</span>, either:
- Support it
- Carefully deprecate it
- Stop functioning when some external event causes it to break

> [!question] Why is deprecation difficult?
> - The new system might be better but also **different**
> - **Emotional attachment** to old systems
> - Funding and executing deprecation efforts can be **difficult politically**
> - Migrating to entirely new system can be **extremely expensive**

> [!example] Java's advisory deprecation
> In <b><span style='color:var(--mk-color-purple)'>java</span></b> we can denote that a function is deprecated by using the tag `@Deprecated`. This does not break the code but just <b><span style='color:var(--mk-color-yellow)'>gives a warning to the user</span></b>.
> 
> This is <b><span style='color:var(--mk-color-red)'>not present in all programming languages</span></b>.
### Deprecation Warnings

It can help prevent new uses but it <b><span style='color:var(--mk-color-red)'>rarely leads to migration of existing systems</span></b>.

What happens is that these warnings can overwhelm users to the point they <b><span style='color:var(--mk-color-yellow)'>ignore them</span></b> (*transitive dependencies*).

These warnings warnings should be **actionable** and **relevant**.

> [!info] Actionable
> Being actionable means that it should <b><span style='color:var(--mk-color-yellow)'>mention the newer counter part</span></b>.

> [!info] Relevant
> It should <b><span style='color:var(--mk-color-yellow)'>show at a time when new lines are touched</span></b>.
### Compulsory Deprecation

Unlike just warnings, this <b><span style='color:var(--mk-color-yellow)'>comes with a deadline for removal</span></b>. Without it it becomes easier to ignore deprecations

Usually a <b><span style='color:var(--mk-color-yellow)'>team of experts</span></b> will be **responsible for migration**.
## Code review

There will always be **pressure to push code out quickly** which can be <b><span style='color:var(--mk-color-red)'>buggy and affects code quality</span></b>.

A very simple approach is to <b><span style='color:var(--mk-color-yellow)'>just show someone your your code</span></b>.

> [!cite] Research on code reviews
> Formal reviews catches **60%** of the defects while informal reviews catch **50%**.
> 
> Up to **75%** of code review comments affect software evolvability and maintainability rather than functionality.

Code review also talks about **maintainability**, where we need to <b><span style='color:var(--mk-color-yellow)'>think about the future, how will it be used or evolved</span></b>.

> [!success] Benefits of code review
> - Soliciting feedback on **improving code design / practice**
> - **Teaching / demonstrating** your coding methods & design
> - **Awareness of state of the product**
> - **Improving maintainability** by highlighting problems
### Size & Speed

Both aspects of **time** and **speed** are <b><span style='color:var(--mk-color-yellow)'>important for productivity and effectiveness</span></b>.

The **time taken to review** <b><span style='color:var(--mk-color-red)'>grows exponentially with the size of the review</span></b>. In addition it also provides <b><span style='color:var(--mk-color-red)'>diminishing returns on thoroughness</span></b>.

If you have no time to review it is good to just tell them to not block their progress.
### Review Practices

#### For Authors

- Keep reviews **small**
- Write a **good description and annotations** (*Guide the reviewers*)
- Choose the **right reviewers**
- **Beware of your own inertia** (*If a reviewer suggests something, do it unless there is a strong reason*), you want to move forward fast
- Think carefully about the feedback you receive and try to **learn from it**
#### For Reviewers

- **Push back** on changes that are overly broad (*YAGNI, you ain't gonna need it*), or poorly describe / commented
- **Attack the code not the person**
	- Ask questions
	- Point out the problems you see
	- Suggest solutions
- **Consider not just the normal cases** but when happens when:
	- Things fail / exception circumstances
	- Things needs to be changed in the future / maintainability
- Be **responsive** but **balanced with severity** / importance of change
## Quality Assurance

Never ship a product without verifying quality, <b><span style='color:var(--mk-color-turquoise)'>software quality assurance</span></b> (*SQA*) is not just testing but <b><span style='color:var(--mk-color-yellow)'>ensuring product quality</span></b>.

SQA is everything that you need to do before the product gets to the customer.

> [!question] How will you do SQA?
> Well it <b><span style='color:var(--mk-color-yellow)'>depends on the product or organisation</span></b>.
> 
> We also need to know who does the QA and what are the expectations.

SQA <span style='color:var(--mk-color-orange)'>best practices</span>:
- **Simulate the customer** as much as possible and find where the product fails to live up to expectations (*we will not know what the customer will do*)
- Must be **done by someone other than the developer**
- Not just finding crashes, it is **anything that is different from the ideal customer experience**

**Common release processes**:
![[Common Release Processes.png|center]]

It **does not matter if its agile or waterfall**, the good project managers will do <b><span style='color:var(--mk-color-yellow)'>frequent feedback from customers</span></b>.
- Agile will do this once a month
- Waterfall will do this between 3 to 6 months
## Deployment

Now after everything is done, now **how do we give the product to the users**?

Some <span style='color:var(--mk-color-orange)'>deployment methods</span>:
- Zip files on a server
- Web apps / DevOps
- App stores
- Physical media
- Pre-installed on devices

The deployment strategies <b><span style='color:var(--mk-color-yellow)'>affects SWE and how the code is being developed</span></b>. It <b><span style='color:var(--mk-color-yellow)'>affects dependences, reviews, testing, QA and releases</span></b>.

There are also some <span style='color:var(--mk-color-orange)'>deployment considerations</span>:
- Speed / **friction** for releases / updates
- Scalabilities
- Risk
- Cost

> [!info] Friction
> Friction is the <b><span style='color:var(--mk-color-yellow)'>time and effort to take a product and get it to be used by the customer</span></b>. We will **want a balance**, do not want to have too little or too much.
> 
> A **minimal friction** is when there is **very little effort**, making the <b><span style='color:var(--mk-color-red)'>product change too fast and you wont be able to catch any bugs</span></b> (*Like press 1 button to deploy*).
> 
> **High friction the opposite** where there needs a lot of time and effort (*Deploying on the app store*).
> 
> You can **bypass friction** but <b><span style='color:var(--mk-color-yellow)'>only for important updates</span></b>.
# Junior vs Senior Developers
---
There are some behaviors and actions that are done differently for junior and senior developers.

**Junior** engineers:
- Hide their code until they are ready
- Estimates and completion largely uncorrelated (*bad estimation*)
- Long-lived branches with big merges
- Larger, unstructured commits with fuzzy messages
- Takes CR feedback as criticism as opposed to change

**Senior** engineers:
- Share code and ideas they are being developed
- Provide accurate estimates and delivers on time
- Soft-lived branches with smaller merges
- Small, focussed commits with clear reasoning
- Takes CR as feedback and opportunity to improve
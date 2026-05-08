---
title: Software Engineering Principles & Patterns
Date Created: 2025-08-14
Last Updated: 2025-09-28
tags:
  - CS3219
  - SWE
  - SWE/Deployment
  - SWE/Delivery
---
# Software Crisis
---
This issue or what people know it as **software crisis 2.0**, refers to the challenge of effectively handling and utilizing data and computational power available. This coupled with the rise in demand of digital consumption.

![[Software Crisis 2.0.png|center]]

# Types of Applications
---
We can categorise software applications into a few categories:
- Computation & response
- Nature of code & data
- Deployment mode
- etc...
>[!important] There is no 1 best application type
## Edge Systems

>[!info] An edge refers to the devices that are near the source of the data

Edge systems essentially makes <b><span style='color:var(--mk-color-yellow)'>heavy computation done on the cloud</span></b> (*a centralised processing*) while <b><span style='color:var(--mk-color-yellow)'>less taxing or low-latency tasks are done on the user-end</span></b> (*edge device*).

>[!success] Low latency, thus faster response times
>Critical safety systems cannot afford latency. Thus it is faster if the processing is done on the edge.

>[!success] Balances the work load between the centralised computing & local decision making

>[!failure] Limited computation power on the edge side

>[!failure] Most edge devices have no power sources, thus suffer from limited battery life & heat dissipation

Computation on the **cloud is considered centralised** where its <b><span style='color:var(--mk-color-yellow)'>computing resources are all in 1 place</span></b>. A **de-centralised** computing is where its <b><span style='color:var(--mk-color-yellow)'>resources are distributed out</span></b> into multiple locations.
## Cloud Computing Applications

When we talk about **cloud computing**, it means that the <b><span style='color:var(--mk-color-yellow)'>software is hosted on an external server</span></b>. And these services can be accessed through the internet (*example, AWS*).

>[!abstract] Cloud enabled vs Cloud native
>
>A **cloud enabled** application, is usually for legacy systems where it originally was <b><span style='color:var(--mk-color-yellow)'>not meant to run on the cloud but was redesigned to do so</span></b>.
>
>While **cloud native** applications are applications which are <b><span style='color:var(--mk-color-yellow)'>initially developed to run on the cloud</span></b>.

>[!success] Cloud computing helps in reducing hardware issues
>The <b><span style='color: var(--mk-color-red)'>setting up, maintenance and cost of hardware can be pricy</span></b>.
>
>So this is where cloud computing started, where companies handle the hardware for the users but the software is handled provided by the user.
### Cloud Enabled Applications

There are a few models:
- IAAS - Infrastructure as a service (*AWS, Google Cloud*)
- PAAS - Platform as a service (*AWS elastic beanstalk, Heroku*)
- SAAS - Software as a service (*Google Apps, Salesforce, SAP*)
- FAAS - Function as a service (*Run when needed/Event driven execution model*)

**Difference between the different models**
![[Cloud Computing Model Differences.png|center|550]]

**IAAS, is the most used model** due to its <b><span style='color:var(--mk-color-green)'>degree of freedom</span></b> for users to manage.
### Cloud Native Applications

It is to build, deploy, manage application <b><span style='color: var(--mk-color-yellow)'>in a cloud computing environments</span></b>.

Characteristics of a cloud-native application:
- Immutable infrastructure
- Microservice based applications (*Multiple smaller applications*)
- API driven (*Application programming interface*)
- Service mesh
- Containers (*Docker*)
- Dynamically managed

>[!abstract] Difference between API and service mesh
>
>Both are related to communications but they <b><span style='color:var(--mk-color-yellow)'>operate at different layers & scopes</span></b>.
>
>An **API** is more user facing where it allows <b><span style='color:var(--mk-color-yellow)'>1 software to communicate with another different software</span></b>.
>
>A **service mesh** on the other hand is more backwards facing where it <b><span style='color:var(--mk-color-yellow)'>communicates between microservices</span></b> distributed in the same system.

# Software Delivery & Deployment
---
>[!info] Delivery is how are you going to distribute your software

>[!info] Deployment is the time between acquisition to execution of the software

When we talk about **delivery & development**, it is <b><span style='color:var(--mk-color-yellow)'>all activities to make it available for use</span></b> after deployment.

Some of these activities include:
- User acceptance testing
- Performance test
- Manual testing

>[!caution] Deployment decisions can affect the [[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Requirements Gathering.md#Quality Attributes|quality attributes]] of the software
>It is a **2 way thing**, what quality attributes you want will affect the deployment process and vice versa.

During deployment there are some <b><span style='color:var(--mk-color-red)'>issues</span></b> which is faced due to the software crisis:
- Device proliferation (*More devices*)
- Hardware advances, reduction in hardware cost, increasing processing power
- Infinite amount of data available & its demand
<div style="page-break-after: always;"></div>

Thus we need to re-think software development in terms of:
- Exploit hardware advances (*Efficiently utilise the computing process*)
- Cater to all devices (*Both windows and mac OS*)
- Managed data
- Network devices, users, applications
## Deployment Considerations

When deploying there are come aspects to consider:
1) **Integration of the internet & related advances**
	- Harness new technologies such as cloud computing
	- Allowing global access
	- Enhances <b><span style='color:var(--mk-color-green)'>portability</span></b>

2) **Large scale content delivery**
	- Increase the location & number of end-points
	- This improves the quality of service by enhancing data transfers
	- Enhances <b><span style='color:var(--mk-color-green)'>availability</span></b> & <b><span style='color:var(--mk-color-green)'>performance</span></b>

3) **Heterogenous platforms**
	- Coexist between different platforms (*OS, Browser, PC & Console*)
	- Enhances <b><span style='color:var(--mk-color-green)'>interoperability</span></b>

4) **Dependency & change management**
	- Handle version updates & dependencies between internal & external (*third party*) components (*example use a container*)
	- Enhances <b><span style='color:var(--mk-color-green)'>maintainability</span></b>

5) **Coordination & communication among components**
	- Using API or synchronous/asynchronous communication
	- Enhances <b><span style='color:var(--mk-color-green)'>performance</span></b>

6) **Security**
	- Ensure encryption, authentication & authorisation, management & attribution
	- Enhances <b><span style='color:var(--mk-color-green)'>secutity</span></b> & <b><span style='color:var(--mk-color-green)'>usability</span></b>
<div style="page-break-after: always;"></div>

## Deployment Mechanisms

### Bare Metal

This means that the application <b><span style='color:var(--mk-color-yellow)'>runs directly on the person's OS & hardware</span></b> (*code to executable*).

The programmer have to cater to the platform, customise build & linking which can affect availability of libraries & dependencies.

You would want to **consider this** if you are targeting specific platforms or just building customised <b><span style='color: var(--mk-color-yellow)'>applications for a specific hardware</span></b>. Or there is <b><span style='color: var(--mk-color-yellow)'>library availability & dependencies</span></b>.

>[!success] Full access over computing resources

>[!success] Isolated, meaning it does not share hardware resources

>[!failure] Potentially wasted hardware resources, since it can claim all of it but might not utilise it fully

>[!failure] Cost & productivity since developers need to handle compatibility across platforms

>[!failure] Scalability issues, not easily plug and play into another OS or platform
### Virtual Machines

Using [[Operating System Overview#Virtual Machines|virtual machines]] can <b><span style='color:var(--mk-color-yellow)'>allow apps to be run on different platforms</span></b> assuming they have a hypervisor and allows for that specific OS.

>[!example] A simple example of deploying using a VM
>
>If the application is developed in Windows, package it in a Windows VM
>
>For other OSs, if their hypervisor is compatible with a Windows VM they can use the application. 

>[!success] Reduced Cost since VM improve resource utilisation through sharing
>This is done by the hypervisor.

>[!success] Flexible since it can now be used across compatible platforms
>The hypervisor will handle the abstraction from multiple guest OSes.

>[!success] It is scalable since it is easy to add more VMs to balance the work load (Horizontal scaling)

>[!failure] Still requires a full OS inside each VM

>[!failure] Side channel attacks, where a VM extracts information from shared hardware resources

>[!failure] "Noisy neighbour", where 1 VM takes up all the resources, while others have less
>If there is a <b><span style='color: var(--mk-color-red)'>memory leak</span></b> (*fail to release memory*) in one VM, then the hypervisor will allocate more resources, starving the rest.
### Containers

Containers are <b><span style='color: var(--mk-color-green)'>lighter than VMs</span></b> since it <b><span style='color:var(--mk-color-yellow)'>does not requires an OS inside the container unlike VMs</span></b>.

Usually one container will do its own specific tasks/service. To **run the container** you will need a <b><span style='color: var(--mk-color-yellow)'>container engine</span></b> to run the application in it.

>[!success] Allows for rapid deployment
>Fast to deploy and remove containers.

>[!success] Write once & run anywhere
>
>Ideal for CI/CD, agile, DevOps practices. All you need to do is deploy the container.
>
>Caters for heterogeneous platforms for interoperability & portability.

>[!success] Granular & Controllable
>
>Deployments can be of the whole system or certain elements
>
>Can also monitor deployment, rollback, patch and redeploy easily.

>[!success] Other benefits
>
>- Easy integration with internet & related advances (*for cloud native applications*)
>- Supports dependency & change management for maintainability
>- Environment management (*For both development & deployment*)
>- Reproducible (*Will be the same application*)
>- Isolation & Security
>	- Avoid conflicting dependencies
>	- Provide some sand-boxing for code execution
>- Quick to launch (*In milliseconds*)
>- Can be used with orchestrators (*Kubernetes*)

>[!failure] Not suitable for all application
>
>**Performance critical applications** (*GPU intensive*) are not suitable.
<div style="page-break-after: always;"></div>
#### Orchestrator

An orchestrator is a software which <b><span style='color:var(--mk-color-yellow)'>manages containers</span></b>.

Some of the tasks it does are:
- Integrate & coordinate many parts (*Modules hosted on containers*)
- Scale up/down based on demand (*Duplicating containers when there is a lot of traffic*)
- Provide fault tolerance to the application (*It knows when a container is down*)
- Provide communication among containers (*using a mesh*)
### Serverless Deployment

Serverless is a <b><span style='color:var(--mk-color-yellow)'>cloud-native deployment model</span></b>. There are still servers... but are maintained by a third party. Which they <b><span style='color: var(--mk-color-yellow)'>manage the servers and resource allocation</span></b>

Developers will deploy functions or apps to servers (*or in containers to servers*). Only when <b><span style='color:var(--mk-color-yellow)'>it is called it will trigger that function</span></b> and will go back to sleep once idle (*FAAS*).

>[!important] These applications must be stateless
>Stateless meaning it <b><span style='color: var(--mk-color-yellow)'>does not keep the current state</span></b> and each request is independent of all other requests.

>[!success] Metered on demand, only charged when running

### Scrum

**Software development life cycle** (*SDLC*)

![[Software Development Life Cycle.png|center|350]]

>[!note] Factors affecting software development
>
>- Requirements
>- Process (Resource, time)
>- Criticality
>- Consequences
>- People (*Competence*)
>- Technology
<div style="page-break-after: always;"></div>

We will mainly focus on [[Software Engineering Processes#Scrum|Scrum]] which is an [[Software Engineering Processes#Agile Software Engineering|agile]] process, it has a:
- Iterative development with feedback loops
- Quick response to change

>[!info] Agile is a software process model with a set of principles and values

>[!info] Scrum is a framework, with a proposed set of rules to follow

## Continuous Integration & Deployment

![[CI & CD Pipeline.png|center|600]]

With CI/CD, developers can **make changes** of all types <b><span style='color:var(--mk-color-yellow)'>safely and quickly in a sustainable way</span></b>.

>[!info] Each stage is trigged by some event from the previous phase

The difference between continuous delivery and deployment is that, for **delivery** the <b><span style='color:var(--mk-color-yellow)'>software can be released to production at any time</span></b>. While deployment is released automatically (*immediately*).

>[!success] Low risk releases
>Cause you are always testing and getting feedback from CI/CD so the risk to meet users needs is low

>[!success] Faster time to market & early feedback

>[!success] Higher quality due to regression testing
>You are always testing when you make a commit to trigger this CI/CD

>[!success] Lower cost due to shorter lifecycle to deploy
<div style="page-break-after: always;"></div>

### Continuous Deployment Strategies

1) **In-place deployment**
Essentially, the <b><span style='color:var(--mk-color-yellow)'>application will be stopped</span></b> (*no one can access it*), the latest version will be installed, started & validated.

It can be thought of as a maintenance, then the team will do the updates.

>[!success] Minimum disturbance to infrastructure
>
>There is no need for new VMs, servers, containers etc.

>[!success] Reduced infrastructure cost
>
>Everything is reused, there is no new infrastructure needed.

>[!failure] Affects availability

2) **Rolling deployment**
The infrastructure of the application will be <b><span style='color:var(--mk-color-yellow)'>replaced one by one with newer versions while running</span></b>.

>[!failure] No isolation between old & new versions
>
>Old and new versions will all be in the same environment during replacement, which can cause new bugs to affect old modules causing issues like data corruption.

>[!failure] Complicates rollback
>
>There is no 2 seperate versions, thus developers need to one by one roll each component back.

>[!failure] There will be downtime
>
>But not as bad as in-place.

3) **Blue/Green deployment**
There are **2 environments**:
- One in production (*blue*)
- One for development (*green*)

Once the update is ready the <b><span style='color:var(--mk-color-yellow)'>traffic can be switch</span></b> to the green environment. The the blue environment will become used for development.

It <b><span style='color: var(--mk-color-green)'>solve the issue of rolling deployment</span></b>, where now old and new modules can never be in the same environment.

>[!success] Near-zero downtime

>[!success] Allows rollback
>
>Just switch back to the blue environment.

>[!success] Simplified CI/CD workflow by limiting the complexity

>[!failure] Run 2 different versions of the application

4) **Canary Deployment**

Also known as <b><span style='color:var(--mk-color-turquoise)'>incremental rollout</span></b>, which is a variant of blue-green deployment.

Essentially it <b><span style='color:var(--mk-color-yellow)'>deploy newer versions to a small subset of users</span></b>, then if it is working it will release to another subset of users.

>[!success] Reduce risk of deployment
>Unlike blue green where if there is something wrong with the update it will affect a lot of users.

>[!success] Can be used for A/B testing
>
>A/B testing is just comparing 2 versions of the application to see which one performs better.
## DevOps

![[DevOps Process.png|center|300]]

[[Software Engineering Processes#DevOps|DevOps]]is a <b><span style='color:var(--mk-color-yellow)'>practice</span></b> that combines development and operations.

>[!success] These practices, reduces time between committing changes & deployment while maintaining quality

So **after code is committed**, there is a pipeline to build, test and release (*from here it goes to the customer*). Now we need a feedback loop where there is come monitoring mechanisms (*using tools*). Then plan on what to do with the feedback.

Some practices in DevOps:
- Continuous integration
- Continuous delivery
- Continuous monitoring & logging
- Communication & Collaboration between developers & operations
- Infrastructure as Code

>[!warning] DevOps is not fully agile
>
>Yes DevOps does focus on the product and improving it for better customer satisfaction,

>[!info] Site Reliability Engineer (SRE)
>
>**Not focused on building new features** but rather improving reliability, fixing issues, responding to incidents & taking on-call responsibilities.
>
>All to have an impact on customer service.

# Generative AI in Software Development
---
We should use AI to <b><span style='color:var(--mk-color-yellow)'>improve on software engineers' efficiency</span></b>.

This can be done through:
- Automation (*CI/CD*)
- Pattern detection (*Query patterns*)
- Collaboration (*Copilot, ChatGPT*)

>[!example] Vulnerability Detection using AI
>
>![[Vulnerability Detection Using AI.png|center|400]]
>
>Vulnerabilities have a repeating pattern, we can thus use ML to identify such patterns in our code.

Some ways to boost productivity are:
- Efficient coding (*Generate boiler code, summarise & understand*)
- Tackle new problems creatively (*Generate and document*)
- Code translation (*From legacy code to python*)
- Writing maintainable code (*Static analysers*)
- Better testing (*Generate tests through automated testing*)

We can also use AI in the SDLC:
![[Using AI in SDLC.png|center]]

>[!warning] Potential risks of using AI
>
>- Garbage in garbage out 
>- Traceability of source (*How reliable is the solution*)
>- Data safety
>- Susceptible to vulnerabilities (*Generate malicious code*)
>- Increasing technical debt (*Maintaining generated code is hard*)

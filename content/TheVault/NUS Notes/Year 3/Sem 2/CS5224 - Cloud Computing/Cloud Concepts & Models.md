---
Title: Cloud Concepts & Models
Date Created: 24-January-2026
Last Updated: 13-April-2026
Tags:
  - CS5224
  - SWE/CloudComputing
---
# Cloud Essential Characteristics
---
There are **5 essential characteristics of a cloud computing environment**:
1) On-demand self service  (*some service portal to do what you want*)
2) Broad network access (*ubiquitous access, continuous network access to access the cloud*)
3) Resource pooling (*Share resources with all users, location dependent*)
4) Rapid elasticity (*time to market / fast deployment*)
5) Measured service (*pay per use*)
## Brief Introduction to Resource Pooling

Generally it is <b><span style='color: #FFD700'>either single tenant or multi tenancy</span></b>.

![[Single vs Multi-Tenancy.png|center]]
# Service Models
---
There are **3 common service models** (*there other service models*):
1) Software as a service (*SaaS*)
2) Platform as a service (*PaaS*)
3) Infrastructure as a service (*IaaS*)

**Service models comparison**:
![[Cloud Service Model Comparison.png|center]]

>[!note] As the list goes down, decreasing levels of abstraction but increasing control
> This is in terms of ease of use, management effort & fast deployment.

>[!question] Why the different models?
>Each <b><span style='color: #FFD700'>provides different levels of abstraction & management</span></b>. So it all depends on the need of the developer.
## Infrastructure As a Service

<b><span style='color: #FFD700'>Provides computing resources</span></b> (*CPU, memory, disk*) through <b><span style='color: #FFD700'>virtual</span></b> machine instances.

![[Infrastructure As a Service.png|cemter]]

>[!info] Here we are building infrastructure using the cloud
>Through renting processing, storage, network capacity, OS etc. <b><span style='color: #FFD700'>Anything on a hardware level</span></b>.
>
>Then we install the things we need (*libraries & frameworks*) then develop the application.

When using IaaS it is the <b><span style='color: var(--mk-color-red)'>lowest level of abstraction</span></b> but <b><span style='color: #98FB98'>highest level of control</span></b> (*you can configure more*).

So typically **IaaS providers**:
- Some <b><span style='color: #FFD700'>web UI to access these resources</span></b>
- Provide a <b><span style='color: #FFD700'>centralised physical resource management</span></b>
- <b><span style='color: #FFD700'>Elastic services & dynamic scaling</span></b>
- Uses a <b><span style='color: #FFD700'>shared infrastructure</span></b> across multiple users
- <b><span style='color: #FFD700'>Preconfigured VM</span></b>
- Metered services (*pay per use*)

So all this is provided by the IaaS providers, the rest is controlled by you.

>[!example] Amazon EC2, DigitalOcean, Linode, Alibaba ECS

>[!success] Scalability & no hardware procurement

>[!fail] Privacy concerns because data is stored on their database
>Or data locality is violated.
## Platform As a Service

A software <b><span style='color: #FFD700'>platform where developers build cloud applications</span></b> & deploy them.

>[!example] Google's app engine, Amazon AWS, Microsoft Azure

There are **2 parts** to this:
1) Platform software (*platform used to develop*)
2) Computing resources (*needed to run the platform software*)

![[Platform As a Service.png|center]]

>[!info] PaaS provider
>They develop the <b><span style='color: #87CEEB'>platform software</span></b> & decides where to host / run. They also manages the <b><span style='color: #FFD700'>libraries or anything that needs coding</span></b> (*exposes API, infrastructure, versioning*).
>
>>[!question] What is a platform software?
>>It is a <b><span style='color: #FFD700'>ready made environment</span></b> with their own database, servers, OS, compute etc.

>[!info] PaaS consumer
>Uses the PaaS (*the libraries, functions etc, and not care about the infrastructure*) in the application they are developing.

Here we have <b><span style='color: var(--mk-color-red)'>less control on where the software is deployed</span></b>. The resources & deployment is all handled by a cloud provider.

So typically **PaaS providers**:
- Some <b><span style='color: #FFD700'>web UI to access development platforms</span></b>
- All in 1 solution (*same IDE to test, deploy, host & maintain*)
- <b><span style='color: #FFD700'>Offline</span></b> access for developers (*won't need to bare network cost*) . Thus <b><span style='color: #98FB98'>development is done offline to reduce cost</span></b>
- <b><span style='color: #FFD700'>Build in scalability, maintenance & versioning</span></b>
- <b><span style='color: #FFD700'>Collaborative platform</span></b> for developers
- <b><span style='color: #FFD700'>Diverse client tools</span></b> to access the platform (*GUI or UI*)

>[!tldr] Typically PaaS runs on the providers IaaS
>**Not always** but since the provider needs to have the infrastructure to host these software in their own environment.
>
>But we can <b><span style='color: #FFD700'>decouple them</span></b>. For instance the PaaS provider can be somewhere in the world but uses another IaaS provider that is physically located in the same region as the cloud consumer.

>[!success] Database, frameworks, middleware are ready to use

>[!fail] Vendor lock-in
## Software As a Service

Essentially they are <b><span style='color: #FFD700'>applications that are running on browsers</span></b>.

>[!info] SaaS provider
>They manage everything from the installation, to the software & hardware

>[!info] SaaS consumer
>They just install the application or remotely runs it on the cloud. Just <b><span style='color: #FFD700'>providing information</span></b> to do the things they want.

So typically **SaaS providers**:
- Provides <b><span style='color: #FFD700'>multi-tenanted application</span></b> (*isolation of personal data from others*)
- Web access
- <b><span style='color: #FFD700'>Centralised management</span></b> of SaaS services
- <b><span style='color: #FFD700'>Multi-device support</span></b>
- <b><span style='color: #FFD700'>Scalability</span></b> under varying loads
- <b><span style='color: #FFD700'>High availability</span></b>
- <b><span style='color: #FFD700'>API integration</span></b> with other software

>[!note] SaaS requires a human element and is not suitable for real time processing

>[!example] Salesforce.com, Google apps

>[!success] Reduce time to market
>Because everything is available, you just need to <b><span style='color: #FFD700'>customise or build something on top</span></b> it for your own purposes.

>[!fail] Lowest flexibility
# Cloud Computing Reference Architecture
---
Here we are focusing on what <b><span style='color: #FFD700'>cloud services provide</span></b> & how they <b><span style='color: #FFD700'>interact with one another</span></b>.

There are **5 actors**:
1) Cloud **consumer**
2) Cloud **provider**
3) Cloud **auditor**
4) Cloud **broker**
5) Cloud **carrier**

>[!info] Actors
>They are entities (*person / organisation*) that participates in a transaction or process and performs tasks in cloud computing.
## Cloud Consumer

These are the people who maintains a business relationship with & <b><span style='color: #FFD700'>uses services from cloud providers</span></b> based on their needs.
## Cloud Provider

They are the ones who <b><span style='color: #FFD700'>offers a cloud service</span></b> to the cloud consumers.

They have to manage:
- [[Year 3/Sem 2/CS5224 - Cloud Computing/Cloud Concepts & Models.md#Deployment Models|Service deployment]]
- Service orchestration
- Cloud Services Management
- Security
- Privacy
### Service Orchestration

>[!abstract] Service orchestration
>Compose system components to support the cloud providers activities in arrangement, coordination and management of computing resources to provide cloud services to cloud consumers.

There are **3 layers**:
1) **Service layer**, an <b><span style='color: #FFD700'>interface between provider & consumer</span></b> to allow the consumer to use the services on the cloud
2) **Resource abstraction & control layer**, <b><span style='color: #FFD700'>abstract what the user wants to do & translate it to instructions</span></b> for the hardware to execute.
3) **Physical resource layer**, which is the hardware
### Cloud Service Management

These are <b><span style='color: #FFD700'>service-related functions for the management & operation</span></b> of services provided to the cloud consumers.

Some of these services include:
- **Business support**

A set of business related services to <b><span style='color: #FFD700'>deal with clients & supporting processes</span></b> (*like billing, customer support, etc.*).

- **Provisioning / Configuration**

For provisioning it can be in terms of automatically deploying cloud systems based on the requested services / resources / capabilities.

For configuration, it can be in terms of resource changing where we adjust for repairs, upgrades & joining new nodes into the cloud.

- **Portability / Interoperability**

Provides mechanisms to support data portability, service interoperability & system portability.
### Security & Privacy

>[!important] The provider is not the sole responsible person for security & privacy
>All the actors plays appart.

For **security** it spans across all layers of the reference model and concerns all relevant actors. The goal is to <b><span style='color: #FFD700'>make things secure</span></b>.

For **privacy**, it more on the <b><span style='color: #FFD700'>accessibility to sensitive data</span></b> (*personal information or personally identifiable information*).

>[!note] Personal information is not personally identifiable information
>Personal information (*PI*) can be your name, email, phone number.
>
>But **personally identifiable information** (*PII*) on the other hand is <b><span style='color: #FFD700'>information that can uniquely identify a person</span></b>, like a NRIC or email address.

With cloud computing there is an increase elasticity (*wider*) [[Year 3/Sem 2/CS5224 - Cloud Computing/Introduction to Cloud Computing.md#Increased Security Vulnerabilities|trust boundary]]. It is a logic perimeter that <b><span style='color: #FFD700'>represents which IT resources are trusted by an organisation</span></b>.

Consumers giving up certain aspects of control results in them placing trust on the providers.

>[!danger] Implications on the cloud
>- Increased security vulnerabilities
>- Reduces operational governance control
>- Multi-tenancy: Overlapping trust boundaries
## Cloud Auditor

<b><span style='color: #FFD700'>Conducts independent assessment</span></b> of cloud services, system operations, performances & security of cloud implementation.

But most importantly it is to <b><span style='color: #FFD700'>verify compliance with regulatory & security policy & conformance to standards</span></b> through review of objective evidence.
## Cloud Broker

<b><span style='color: #FFD700'>Manages the use, performance & delivery of cloud services</span></b> & negotiates the relationship between cloud providers & cloud consumers (*helps consumers integrate cloud services*).

There are **3 main services**:
1) **Service intermediation**, provides value-added services to cloud consumers (*enhancing an existing cloud service*)
2) **Service aggregation**, it does the following:
	- Combines & integrates multiple services into 1 or more new services (*consumer has no choice*)
	- Provides data integration
	- Ensures secure data movement between cloud consumers & multiple cloud providers
3) **Service arbitrage**, same as aggregation but with the flexibility to choose services from multiple agencies
## Cloud Carrier

<b><span style='color: #FFD700'>Provides connectivity & transport of cloud services</span></b> (*essentially the internet*) from cloud providers to cloud consumers.

Cloud providers <b><span style='color: #FFD700'>set up SLAs</span></b> with a cloud carrier to provide consistent services to their consumers.

**May be** required to provide dedicated & <b><span style='color: #FFD700'>secured connections</span></b> between cloud providers & consumers.
# Deployment Models
---
The are **4 deployment models**:
1) Public cloud
2) Private cloud
3) Community cloud
4) Hybrid cloud
## Public Cloud

It is available to the <b><span style='color: #FFD700'>general public</span></b> (*shared by all consumers*). It is the most commonly used cloud infrastructure.

>[!info] So anyone can sign up for an account and pay for their services can use it.

In an organisation stand point they are the consumers & they want to access IT resources & services provided by cloud providers.

>[!question] What are the organisation needs?
>- <b><span style='color: #98FB98'>Low upfront cost</span></b> (*potentially pay as you go model*)
>- <b><span style='color: #98FB98'>Available</span></b> anytime, anywhere
>- <b><span style='color: #98FB98'>Maintenance is handled by the provider</span></b>

>[!fail] Trust boundaries are an issue
>Data and storage is shared with others.

>[!example] Some public cloud providers Amazon, Microsoft, Google, Salesforce
## Private Cloud

Solely used by an <b><span style='color: #FFD700'>organisation</span></b> (*exclusive access*), suitable for enterprises with large scale IT.

>[!question] What are the organisation needs?
>- <b><span style='color: #98FB98'>High level of control</span></b> (*especially for sensitive data*)
>- <b><span style='color: #98FB98'>Restricted</span></b> access (*limited to within the organisation*)
>- <b><span style='color: #98FB98'>Maintenance is handled predominantly in-house</span></b>

>[!info] Out-sourced private cloud
>These third party private cloud providers.
>
>So <b><span style='color: #FFD700'>dedicated IT recourses are</span></b> hosted by a third party provider. 
>
>Also the organisation has it own <b><span style='color: #87CEEB'>virtual private cloud</span></b> an <b><span style='color: #FFD700'>isolated environment</span></b> within the public cloud that is <b><span style='color: #FFD700'>only customisable by the organisation</span></b>.

>[!fail] Out-sourcing a private cloud is more expensive in general as it provide its own isolated IT resources & security

>[!important] But whether it is on-site or a third party it all depends on security.
## Community Cloud

Shared by <b><span style='color: #FFD700'>multiple organisations</span></b> based on <b><span style='color: #FFD700'>common operational & regulatory requirements</span></b>.

>[!question] What are the organisation needs?
>- Cannot afford a private cloud, but wants some security
>- Shared needs & regulatory compliance with other organisations
>- <b><span style='color: #98FB98'>Still have restricted access</span></b> but often limited to participating organisations

>[!important] Need a clear governance structure for management
> This governance structure just tells which organisations have what access to what resources.

>[!example] Government departments, educational institutions, health care industry
## Hybrid Cloud

Also known as <b><span style='color: #87CEEB'>federated cloud</span></b> which consist of <b><span style='color: #FFD700'>2 or more public & private clouds that interoperate</span></b> (*basically any 2 or more different types of cloud deployments*).

Even with 2 different clouds they <b><span style='color: #FFD700'>remain as distinct entities</span></b>.

>[!question] What are the organisation needs?
>- <b><span style='color: #98FB98'>Balance control & cost</span></b>
>- <b><span style='color: #98FB98'>Flexible approach depending on data & applications</span></b> (*sensitive data on private, application on public*)

Because it is flexible, it allows for data & application interoperability.

>[!fail] You are forced to use 2 different types of cloud
## Sovereign Cloud

>[!question] Why do we need sovereign cloud?
>The main idea of a sovereign cloud is mainly for <b><span style='color: #FFD700'>data regulation</span></b>.
>
>So it stores data (*& metadata*) within national borders to meet regulatory & compliance needs of a country or jurisdiction

>[!question] What are the organisation needs?
>- <b><span style='color: #98FB98'>Adhere to local data protection regulations</span></b>
>- <b><span style='color: #98FB98'>Prevents foreign access to data under all circumstances</span></b>

>[!example] MS sovereign cloud, sovereign cloud oracle, SAP sovereign cloud
>Even with all these providers you <b><span style='color: var(--mk-color-red)'>cannot fully trust them</span></b>.


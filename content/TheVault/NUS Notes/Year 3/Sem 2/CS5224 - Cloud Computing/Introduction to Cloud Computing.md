---
Title: Introduction to Cloud Computing
Date Created: 19-January-2026
Last Updated: 11-April-2026
Tags:
  - CS5224
  - SWE/CloudComputing
---
# Overview of Cloud Computing
---
There are many definitions but fundamentally they all boils down to <b><span style='color: #FFD700'>on-demand service</span></b> (*pay per use*) + <b><span style='color: #FFD700'>elastic resource</span></b> (*changes based on demand*).

Generally we are <b><span style='color: #FFD700'>running code somewhere on someone's platform</span></b>.

**Why cloud computing?** If we **choose to deploy it ourselves** we require a local server which we need to host and setup.

>[!failure] Time to market will be slow

Where in cloud computing **someone provides hardware** all a developer needs is to provide the application.

>[!success] Speed up the time to market

>[!success] Reduce cost
> There is still some cost (*pay on demand*) but is cheaper if the hardware & software is provided and maintained by a third party.

>[!success] Improves availability

>[!success] Rapid Elasticity
>Also most cloud providers <b><span style='color: #FFD700'>scale up & down computing resources based on demand</span></b>, thus ensuring <b><span style='color: #98FB98'>elastic resource demand & elastic computing resource</span></b>.

>[!failure] Reliance on the cloud providers
>Now we rely on them to ensure our application is running. So if <b><span style='color: var(--mk-color-red)'>something happens in the cloud the application will be affected</span></b> (*Like the Cloudflare outage*). So we are giving up control.
## Cloud Services

>[!info] Cloud service 
>Any IT resource that is <b><span style='color: #FFD700'>remotely accessible</span></b> via a cloud.

At a high level there are 3 different [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Software Engineering Principles & Patterns.md#Cloud Enabled Applications|types of services]]:
- **IAAS** (*Infrastructure as a service*)
- **PAAS** (*Platform*)
- **SAAS** (*Software*)

# Business Drivers
---
When building application on the cloud for a business they **key drivers** are:
- **Capacity planning** (*elasticity in load*)
- **Cost reduction**
- **Organisation agility**
## Capacity Planning

We need to <b><span style='color: #FFD700'>determine & fulfill future demands</span></b> on IT resources, produces & services.

>[!danger] Challenges in capacity planning
>- Usage / demand fluctuations
>- Peak usages (*holidays*)
>- Cost of resource provisioning

There are **strategies** to plan for capacity:
1) **Lead** strategy: Add capacity in <b><span style='color: #FFD700'>anticipation</span></b> of demand
>[!fail] If we underestimate, this will be an issue

2) **Lag** strategy: Add capacity when resources <b><span style='color: #FFD700'>reach full capacity</span></b>
>[!fail] It will take some time to add additional capacity

3) **Match** strategy: Add capacity in <b><span style='color: #FFD700'>small increments</span></b> as demand increases

>[!important] Ideally avoid under-provisioning & over-provisioning
>Because <b><span style='color: var(--mk-color-red)'>poor planning will lead to cost consequences</span></b>.
## Cost Reduction

<b><span style='color: var(--mk-color-red)'>On premise systems requires a big cost</span></b>. You will need up front <b><span style='color: #FFD700'>investment cost</span></b> (*hardware cooling, space etc*) & also <b><span style='color: #FFD700'>operational costs</span></b> (*manpower, electricity, software licences*).

So here are things to consider:
- Cloud vs on-premise
- Different cloud providers (*inter-cloud*)
- Different solutions/products offered by the same provider (*intra-cloud*)

>[!success] Cloud computing offers cost efficiency at scale
> If on-premise you need to invest even more to scale up.

>[!success] Removes fixes cost associated with capital equipment
> By changing from a on-premise traditional IT to cloud computing, <b><span style='color: #FFD700'>cost is just the variable operational cost</span></b>.
## Organisational Agility

It is a organisation's responsiveness to change. With <b><span style='color: var(--mk-color-red)'>on-premise infrastructure, up-front investment & infrastructure ownership costs may prohibit change</span></b>.

>[!success] Elastic IT resources to respond to business cycles beyond what was previously predicted or planned

>[!success] Software fixes/updates: Update datacenters vs millions of clients
>The cloud provider handles updates to quickly get around updating all users.

>[!success] Datacenter allows faster introduction of new hardware innovations
# Technical Concepts
---
## Scaling

To achieve elasticity we need [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Scalability.md|scaling]] which is the ability of the IT resource to handle increase or decrease usage demands.

Typically there are 2 types of scaling, <b><span style='color: #87CEEB'>horizontal</span></b> & <b><span style='color: #87CEEB'>vertical</span></b> scaling.

>[!info] Horizontal scaling
>Also known as scaling **out or in**, is just <b><span style='color: #FFD700'>adding more instances of the same resource</span></b>. This enables <b><span style='color: #98FB98'>fault tolerance & redundancy</span></b>.

>[!info] Vertical scaling
>Also known as scaling **up or down** is to <b><span style='color: #FFD700'>replace resource with higher or lower capacity or add resources to a single node</span></b>.

>[!note] There is also elastic scaling which is specifically for resources
>These are your CPU, RAM, storage and so on.

**Scaling comparison**:

|                   |                         Horizontal                         |                           Vertical                            |
| :---------------: | :--------------------------------------------------------: | :-----------------------------------------------------------: |
|       Cost        |          Less expensive using commodity hardware           |           More expensive using specialized hardware           |
|   Availability    |               Resources instantly available                |            Resources normally instantly available             |
|   Ease of setup   |          Resource replication & automated scaling          |                   May need additional setup                   |
| Hardware Capacity |              Not limited by hardware capacity              |             Limited by maximum hardware capacity              |
|  Implementation   | Need a redesign of the architecture or is more complicated | No need to design as everything still run on the same machine |
# Challenges in Cloud Computing
---
## Technical Challenges

Here are some of the technical challenges:
- Software development (*different cloud platforms & services across cloud providers*)
- Tools are continuously evolving
- Moving large data is expensive
- Security
- Internet dependence
- Quality of service
- Energy cost
## Non-Technical Challenges

### Increased Security Vulnerabilities

This is mainly because we are giving up control, more specifically we are allowing the <b><span style='color: #FFD700'>cloud providers to have access to our data</span></b>. So <b><span style='color: #87CEEB'>shared responsibility</span></b> is important.

This is known as the <b><span style='color: #87CEEB'>expansion of trust boundary</span></b> which <b><span style='color: var(--mk-color-red)'>introduces new vulnerabilities</span></b>.

>[!fail] Overlapping trust boundaries allows consumers to steal or damage data
>So one consumer can steal or damage other people's data.
>
### Reduced Operational Governance Control

Similarly by giving up control, we also lose some levels con governance control. There are different levels of IT resource governance between on-premise & cloud.

>[!fail] Cloud providers may not maintain or meet some SLA guarantees

>[!fail] Introduced latency & bandwidth constraints
>There is a physical distance between the consumer and provider.
### Privacy / Legal Issues

>[!example] Data localisation / residency on data privacy & storage
>It says that data belonging to lets say a Singapore citizen must be kept within Singapore. 
>
>Basically data must be within national borders.

So we cannot just deploy it anywhere on the cloud. But the **available locations are up to the providers** as they want to <b><span style='color: #FFD700'>store data in affordable / convenient locations</span></b>.

There is also legal issues on accessibility & disclosure of data (*some laws require data to be disclosed appropriately*).

Tensions between personal rights (*privacy*) & society.


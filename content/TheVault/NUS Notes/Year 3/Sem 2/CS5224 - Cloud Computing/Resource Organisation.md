---
Title: Resource Organisation
Date Created: 31-January-2026
Last Updated: 02-April-2026
Tags:
  - CS5224
  - SWE/CloudComputing/ResourceOrganisation
  - SWE/Scaling
---
# Resource Organisation
---
The main **goal of resource organisation** is to <b><span style='color: #98FB98'>achieve elasticity</span></b> (*scaling*) & a <b><span style='color: #98FB98'>balanced utilisation of cloud resources</span></b>.

>[!note] Rapid elasticity
>Elasticity is the <b><span style='color: #FFD700'>response to the fluctuation of customer demands</span></b> (*scale up & down as well*).
>
>A cloud provider manages many customers so it need to handle the demand as well as the allocation of recourses (*cannot just give everything to 1 person because they need it*).

>[!question] Why should we balance resource utilisation?
>Like all hardware it has its own time to live. If we keep on using that machine eventually it will not function. So by balancing we can <b><span style='color: #98FB98'>potentially keep these resource running longer</span></b> & also <b><span style='color: #98FB98'>over time the amortized cost will decrease</span></b>.

Here are some architectures for resource organisation:
- Workload distribution
- Service load balancing
- Resource pooling
- Dynamic scalability
- Elastic resource capacity

>[!abstract] Time to market
>Typically when **replacing machines**, providers will want to get some profit out of it by <b><span style='color: #FFD700'>selling it</span></b>.  If not then when the machine spoils they do not benefit as much as if they were to sell it.
>
>Thus there is this time to market indicator to <b><span style='color: #FFD700'>gauge when to sell old machines for newer ones</span></b>.
# Workload Distribution Architecture
---
The main idea is to <b><span style='color: #FFD700'>distribute consumer's workload over available cloud resources</span></b>, on the <b><span style='color: #FFD700'>application layer</span></b>.

>[!note] It mainly uses the idea of [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Scalability.md#What is Scalability?|horizontal scaling]]

The **key component** to achieve this is called the <b><span style='color: #87CEEB'>load balancer</span></b>.

>[!important] Workload distribution is more on the application level not at the machine level

>[!success] Achieve greater levels of fault tolerance for applications
>Because of horizontal scaling, if one cloud service goes down there are still replicas which the load balancer can direct the traffic to.

>[!success] Seamlessly provides the required amount of load balancing capacity needed
>But you still need to setup the tools then everything for you seamlessly.
## Load Balancer

It essentially <b><span style='color: #FFD700'>automatically distributes workload</span></b> (*incoming app traffic*) to <b><span style='color: #98FB98'>reduce over-utilisation or under-utilisation</span></b> of resources (*elastic load balancing*).

However it <b><span style='color: #FFD700'>only routes traffic to healthy targets</span></b>.

>[!info] Healthy targets
>They are essentially service which are online & running essentially.

>[!example] An example from AWS is its elastic load balancing service (ELB)

There are different **types of load balancers** for <b><span style='color: #FFD700'>different levels</span></b>:
- **Application** load balancer
- **Network** load balancer (*monitors network conditions*)
- **Gateway** load balancer (*Backend level, looks at intrusion detections & packets*)
- **Classic** load balancer (*It is the previous version of the load balancer for backward compatibility*)
### Application Load Balancer

The application load balancer acts as a <b><span style='color: #FFD700'>single point of contact for clients</span></b>. This load balancer <b><span style='color: #FFD700'>contains 1 or more listeners</span></b>.

![[Application Load Balancer.png|center|550]]

>[!info] Listener
><b><span style='color: #FFD700'>Checks requests</span></b> from clients using the protocol (*http*) & port configured.
>
>For 1 listener there are <b><span style='color: #87CEEB'>user-defined rules</span></b> <b><span style='color: #FFD700'>routes requests to its registered targets</span></b> (*target groups*).

>[!info] User-defined rules
>These rules consist of <b><span style='color: #FFD700'>priority</span></b>, one or more <b><span style='color: #FFD700'>actions</span></b> & one or more <b><span style='color: #FFD700'>conditions</span></b>.
>
> >[!important] A default rule is necessary
> >This is to route all unknown requests that does not fit into any of the rules.

Essentially this is how it all comes together:
1) There are a bunch of <b><span style='color: #FFD700'>listeners which listens request from a specific configured protocol & port</span></b>
2) Afterwards it will check the request & <b><span style='color: #FFD700'>based on the rules & priority will route it to the correct target group</span></b> only if that <b><span style='color: #FFD700'>target group is healthy</span></b> (*based on the health check*).
## Service Load Balancing Architecture

A **specific application** & **specialised variation** of the workload distributed architecture. 

The key idea here is to do <b><span style='color: #FFD700'>redundant deployment of cloud services</span></b> (*onto*) & <b><span style='color: #FFD700'>work with a load balancer</span></b> to dynamically distribute workloads.

>[!question] So why is this a specialised variation?
> It is because we use a load balancer & in addition we are horizontally scaling our cloud services.

Now our <b><span style='color: #FFD700'>resource pool is a duplication of various cloud services</span></b>.

>[!fail] It is not the most cost efficient
>It may <b><span style='color: var(--mk-color-red)'>not need be that the whole cloud service needs to be replicated</span></b>, maybe only part of it.
### Independent & Built-In Load Balancer

In the service load balancing architecture there can be **2 types of load balancers** used.
1) **Independent**
2) **Built-in**

For **independent** load balancers they are a <b><span style='color: #FFD700'>separate entity</span></b> from cloud services & the host servers. So it <b><span style='color: #FFD700'>intercepts the request & then routes it</span></b>.

![[Independent Load Balancer.png|center|350]]

>[!success] Workload processing is horizontally scaled
>We can just add more load balancers to handle more request to be redirected.

For **built-in** the <b><span style='color: #FFD700'>cloud service itself has a load balancer</span></b> as part of the application. So all requests goes to 1 virtual machine then it will redistribute.

![[Built-In Load Balander.png|center|450]]

>[!success] Since the load balancer is moved in-house we can monitor and know the traffic

>[!fail] The load balancer itself can be overloaded
>Besides routing requests it still process requests. So in the event the virtual server is overloaded the load balancer might not be able to do its task.
# Resource Pooling Architecture
---
Here we are <b><span style='color: #FFD700'>balancing at a resource level</span></b> (*CPU, memory, GPU, storage, servers, network*) to serve diverse needs of cloud consumers.

So lets **split each of the different resource into its own pool**. However a cloud consumer will not just want 1 specific resource, they would want a collection of different resources. Thus this <b><span style='color: var(--mk-color-red)'>makes management complex due to multiple pools for specific consumer or application</span></b>.

To better manage this we <b><span style='color: #FFD700'>create a hierarchical structure</span></b>:
- **Parent** (*basically all the resources that the provider has*)
- Split into **sibling** or **nested**

>[!info] Sibling pool
>All the resources are drawn physically from the same group, essentially its <b><span style='color: #FFD700'>all from the same location</span></b> (*data center*).
>
>This will <b><span style='color: #98FB98'>improve latency</span></b> because everything is not spread out. It is also <b><span style='color: #FFD700'>isolated</span></b> from one another so <b><span style='color: #FFD700'>each cloud consumer is given access to its respective pool</span></b>.
>
>>[!example] In location A, there are servers, CPU & memory and in location B there are CPU, memory & network so these are our 2 sibling pools

>[!info] Nested pool
>Divide the larger pool into <b><span style='color: #FFD700'>smaller ones with the same type of resources</span></b>. The only <b><span style='color: #FFD700'>difference will be the quantity of these resources</span></b>.
>
>This is <b><span style='color: #98FB98'>useful for assigning to different departments or groups</span></b> within an organisation.
>
>>[!example] In the AI department they might need more memory so their pool will have more memory allocated as compare to maybe the sales department
## Dynamic Scalability Architecture

Similar to [[Year 3/Sem 2/CS5224 - Cloud Computing/Resource Organisation.md#Resource Pooling Architecture|resource pooling]] but now we make <b><span style='color: #FFD700'>resource utilisation variable to meet usage demand fluctuations</span></b>.

A consumer can dynamically allocate resources from resource pools based on a **predefined scaling conditions**:
1) Dynamic **horizontal** scaling, <b><span style='color: #FFD700'>same resource scaled dynamically</span></b> (*replication*)
2) Dynamic **vertical** scaling, <b><span style='color: #FFD700'>scale processing capacity of a single resource</span></b>
3) Dynamic **relocation**, <b><span style='color: #FFD700'>resource relocated to a host with a larger capacity</span></b>

>[!important] We always scale before hitting the limit if not then issues will arise

>[!question] Why relocation?
>Sometimes vertical scaling might not work, for instance an IO machine & we <b><span style='color: var(--mk-color-red)'>need to bring it down in order to upgrade it</span></b>.
>
>So if availability is important, relocation can be better which is to move to a better machine.

<b><span style='color: #FFD700'>To know when to scale there is a monitor</span></b>.

>[!question] How do we know when to scale?
>There is a machine called the <b><span style='color: #87CEEB'>automated scaling listener</span></b>, which monitors capacity.
>
>It <b><span style='color: #FFD700'>takes a decision based on pre-defined scaling policy</span></b> & then it will replicate the resource.
### Elastic Resource Capacity Architecture

>[!example] An example of a dynamic scaling architecture using vertical scaling

This architecture is to <b><span style='color: #FFD700'>dynamically provision</span></b> of virtual servers. It job is to <b><span style='color: #FFD700'>upscale or down</span></b> your machine by allocating & reclaiming CPU, RAM, etc, before capacity threshold is reached.

It uses a **intelligence automation engine** to <b><span style='color: #FFD700'>monitor & to allocate resources accordingly</span></b>.

**Elastic resource capacity example flow**:
![[Elastic Resource Capacity Flow.png|center]]
# Cloud Bursting Architecture
---
The idea is that you <b><span style='color: #FFD700'>want to deploy in-house</span></b> (*security reasons*). However you still want the flexibility to <b><span style='color: #FFD700'>use the cloud when you need to</span></b> (*increased traffic*).

>[!tldr] Essentially we scale on-premise IT resources into the cloud whenever the threshold is met

We <b><span style='color: #FFD700'>pre-deploy</span></b> onto the cloud which remains <b><span style='color: #FFD700'>inactive & redundant</span></b> until <b><span style='color: #87CEEB'>cloud bursting</span></b>.

>[!info] Burst-out
>To meet higher usage demand, dynamic <b><span style='color: #FFD700'>scaling of on-premise resources to cloud-based resources</span></b>.

>[!info] Burst-in
>On lower demand, <b><span style='color: #FFD700'>revert back to on-premise</span></b> & release cloud resources.

For this architecture we need to use a:
- Automated scaling listener (*when threshold exceeds, redirect to the cloud*)
- <b><span style='color: #FFD700'>Resource replication</span></b> (*resources on the cloud & on-premise are synchronised*)

>[!fail] Need to maintain the same version on-premise & on the cloud
>This <b><span style='color: var(--mk-color-red)'>replication to the cloud has some cost</span></b>. Also the <b><span style='color: var(--mk-color-red)'>cost of keeping it dormant</span></b> when not in use.

>[!fail] We need to ensure data is synchronise between on-premise & on the cloud
> Cloud providers might not charge data going in but <b><span style='color: var(--mk-color-red)'>might charge for data going out of the cloud</span></b> (*when we burst in*).
> 
> We need to <b><span style='color: #FFD700'>have some resource replication system</span></b> to ensure that the state management databased are synchronised.


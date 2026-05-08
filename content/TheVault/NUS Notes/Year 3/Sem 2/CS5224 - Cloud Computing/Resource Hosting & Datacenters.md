---
Title: Resource Hosting & Datacenters
Date Created: 05-February-2026
Last Updated: 05-February-2026
Tags:
  - CS5224
  - SWE/CloudComputing/ResourceHosting
  - Database/Datacenter
---
# Resource Hosting
---
So there are **2 ways** to host resources:
1) **On-premise**, responsible for deploying, operating & maintaining internet connectivity (*between local machines*), etc..

>[!success] Complete control over quality of service (QoS)

>[!success] Ensures security

>[!fail] Upfront costs & a lot of responsibility is on you

2) **Cloud-based**, use multiple cloud carriers, the <b><span style='color: #FFD700'>QoS dependent on carriers</span></b>

>[!success] Easier to adopt for applications with relaxed bandwidth & latency
>Because the responsibility is on the providers.

>[!fail] Security concerns
>Security might be more lax due to [[Year 3/Sem 2/CS5224 - Cloud Computing/Introduction to Cloud Computing.md#Increased Security Vulnerabilities|trust boundaries]].
# Datacenters
---
Typically when moving from on-premise to datacenters there are **2 key performance metrics to take note of**, [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Infrastructure.md#Bandwidth & Latency|bandwidth & latency]].

Typically in datacenters you are now <b><span style='color: #FFD700'>operating on somewhere distant not locally</span></b>.

>[!abstract] Bandwidth
>It is the number of <b><span style='color: #FFD700'>bits transferred per unit time</span></b>.
>
>**Important** when a <b><span style='color: #FFD700'>substantial amount of data transfer is required</span></b> by the application.
>
>>[!success] Improving bandwidth is simpler than latency
>>For bandwidth we can <b><span style='color: #FFD700'>just make the "pipe" bigger</span></b> to allow more data to flow through.

>[!abstract] Latency
>It is the <b><span style='color: #FFD700'>time taken for a packet to travel from one data node to another</span></b>.
>
>**Important** when <b><span style='color: #FFD700'>response time is key</span></b> for application.
>
>>[!warning] Latency comes with physical characteristics
>> Latency is actually <b><span style='color: var(--mk-color-red)'>limited by the speed of light</span></b> (*at best we can have a optic fiber cable*).

>[!important] If can keep things local
>Like connectivity, your compute. If you can do it locally (*in house or within the same location or within the same server*) then it will be good.

There is also a **ranking for the type of datacenters** (*think of it as tiers*):

| Tier |                                                                Description                                                                |                Expected Uptime                 |
| :--: | :---------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------: |
|  1   |                          Single path for power distribution, USP & cooling distribution, no redundant components                          | 99.671% is approx. 28 hrs of downtime annually |
|  2   |                                                  Partial redundancy for power & cooling                                                   |                    99.741%                     |
|  3   | Multiple paths for power & cooling, and each path with redundant components, concurrently maintainable (*almost everything is redundant*) |    99.982% is approx. for 1.5 hrs annually     |
|  4   |                                        Redundancy for every component (*everything is redundant*)                                         |                    99.995%                     |
So you can see as **tiers increase**, what the <b><span style='color: #98FB98'>datacenters offer gets better, availability is better</span></b> but also the <b><span style='color: var(--mk-color-red)'>cost increases</span></b>.

>[!info] Tier 3 is the most common industry standard datacenter
>Why not got for tier 4? The cost for the improvement in uptime is not worth while.

>[!abstract] Tier 5 datacenters
>There is also a tier 5, which is still in the works with a lot of redundant systems, fueled by renewable energy & it has a uptime of 99.999%, but it all cost with large cost.
## Components Of Datacenters

Here is an overview on how a general datacenter is built:
![[Components of a Datacenter.png|center|450]]

Generally there is:
- Main server hall
- Mechanical yard (*host cooling systems*)
- Electrical yard (*generators & power distribution centers*)
### Main Server Hall

#### The Architecture

Here is where the compute, storage & networking equipment are located. It is <b><span style='color: #FFD700'>designed in terms of hierarchy</span></b>.

**Example of a  hierarchy in the main server hall**:
![[Hierarchy of Main Server Hall.png|center|450]]

>[!question] Why do it in a hierarchical style?
>If we treat it individually then we essentially have 1 route for each set of machines then we <b><span style='color: var(--mk-color-red)'>need additional connections to link everything together</span></b> (*cost*).
##### Datacenter Servers

At the **lowest level** where all the servers are located it uses a <b><span style='color: #87CEEB'>modular architecture</span></b> along <b><span style='color: #FFD700'>with commodity hardware</span></b> (*inexpensive hardware*), which are the [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Infrastructure.md#The Server|servers]].

>[!abstract] Modular architecture
>Essentially it uses the idea to combine smaller modules to make larger ones.

**Block diagram of a server**:
![[Hardware Inside a Datacenter Server.png|center|500]]

So there are:
- CPU's
- Memory
- Additional slots (*for customisation & extension*)
- Networking & internet

>[!note] There is only no input / output
##### Machine Racks

These <b><span style='color: #FFD700'>servers will then be modularized & packed</span></b> together to form [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Infrastructure.md#The Rack|server racks]]

These racks, supports servers, storage & networking equipment. It **consist of**:
- Power
- Battery backup
- Network switches
- Rack level switch (*Top of Rack or TOR*)
- Payload bay to slot in servers (*a typical commodity rack can house 42 1 unit servers each of 1.75in height*)

>[!info] This rack level switch connects IT resources (*servers*) within the rack & also connects the rack to the datacenter network

Then we can <b><span style='color: #FFD700'>modularise these racks again as scaled up computational resources</span></b> to form a [[Year 3/Sem 1/CS4225 - Big Data Systems for Data Science/Infrastructure.md#The Datacenter|datacenter]].

>[!note] You can see the hierarchy here start from 1 server and piece everything together to form a datacenter
#### The Storage

In datacenters there are **2 categories to storage**:
1) **Private** to individual running tasks (*local DRAM or disk*)
2) **Shared** state for a distributed workload (*distributed storage network*)

Similarly, we want <b><span style='color: #FFD700'>data to be local</span></b> (*between servers*) so that computation will be fast, only when <b><span style='color: #FFD700'>data is required elsewhere then we can share the data</span></b>.

>[!success] By keeping data local for computation we essentially reduce communication time

>[!warning] When sharing data it raises the issue of synchronisation of data
>When data is edited on one end it must be reflected with the other machines.

So the same hierarchical structure comes into play again, where:
- The **server** contains our <b><span style='color: #FFD700'>caches, DRAM, disks & flash drives</span></b>
- The **rack** will house all these servers & can store local & distributed memory
- The **datacenter** is the same where it can store local & distributed memory
#### The Network

There are various protocols which <b><span style='color: #FFD700'>allows different machines within the hierarchy to interact with one another</span></b>.

Between datacenters or more specifically **between racks** it uses a <b><span style='color: #87CEEB'>local area network</span></b> (*LAN*) with <b><span style='color: #FFD700'>redundant connectivity</span></b> & if **cloud consumers** were to communicate **with the datacentre** it uses the <b><span style='color: #87CEEB'>wide area network</span></b> (*WAN*).

Between **servers & storage systems** it communicates through the <b><span style='color: #87CEEB'>storage area network</span></b> (*SAN*).
#### The Cooling

Datacenters <b><span style='color: var(--mk-color-red)'>consumes a lot of energy & all of this is converted into heat</span></b>. So cooling is an important aspect when making datacenters.

>[!example] Example of a raised-floor cooling system
>![[Raised-Floor Cooling System.png|center|500]]

<b><span style='color: var(--mk-color-red)'>Air cooling is very expensive</span></b> a <b><span style='color: #98FB98'>more efficient way</span></b> is using **liquid** (*water*) cooling. That is why some datacenters are near the ocean or in fact in the ocean.

>[!warning] Of course the water usage will be very high

>[!info] And recently there are plans to have datacenters to be in space
## Power Usage Of Datacenters

<b><span style='color: var(--mk-color-red)'>Datacenters do use a lot of electricity</span></b> just to be operational.

A good **measure of how efficient a datacenter is** (*in term of power consumption*) by using the <b><span style='color: #DDA0DD'>power usage efficiency formula</span></b>:
![[Power Usage Efficiency Formula.png|center|450]]

>[!success] The ideal case will be if PUE = 1
### Energy Proportional Systems

<b><span style='color: var(--mk-color-red)'>Energy efficiency is not a linear function of load</span></b>. So this is where energy proportional systems comes in.

>[!danger] Idle systems uses 50% power

An energy proportional system <b><span style='color: #98FB98'>consumes almost no power when idle</span></b>. Then when load increases then it will also <b><span style='color: #98FB98'>gradually consume more power</span></b>.

>[!success] The power is proportional to the load for energy proportional systems


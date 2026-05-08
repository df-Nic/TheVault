---
title: Infrastructure
Date Created: 2025-08-15
Last Updated: 2025-09-28
tags:
  - CS4225
  - BigData
  - DataCenters
  - DataCenters/Architecture
---
# Cloud Computing
---
**Cloud computing**, is when <b><span style='color:var(--mk-color-yellow)'>software is hosted on an external server</span></b>. And these services can be accessed through the internet (*for example AWS*).

Cloud computing can also be known as as <b><span style='color:var(--mk-color-turquoise)'>utility computing</span></b>, since computing resources follows a <b><span style='color:var(--mk-color-yellow)'>pay as you go</span></b> scheme (*metered service*)

>[!success] It is very scalable, has infinite capacity to improve

>[!success] It is elastic, can scale up or down on demand
## Virtualisation & Containers

1) **Traditional Stack**
Here all <b><span style='color:var(--mk-color-yellow)'>application runs on 1 OS</span></b>, just like running an application on your normal laptop.

>[!failure] Cannot share computing resources since only 1 application will control 100% of the hardware.

2) **Virtual Machines**
Each application will be in <b><span style='color:var(--mk-color-yellow)'>their own environment called a virtual machine</span></b>. Thus they are <b><span style='color:var(--mk-color-yellow)'>isolated</span></b> from other VMs.

Through the **hypervisor**, it will <b><span style='color:var(--mk-color-yellow)'>allocate hardware resources</span></b> to the respective virtual machines.

>[!failure] High overhead since each VM needs to have its own OS

3) **Containers**
It is essentially a <b><span style='color:var(--mk-color-yellow)'>VM but without the need for the OS</span></b>. It will use the host's OS instead.

Only the application plus its dependencies are in the container.

>[!success] Lightweight since there is no need to have an OS in the container
## Types of Services

There are a few types of services, some of them are:
- **Infrastructure as a Service** (*IaaS*), known as utility computing
	- User rents a virtual machine and makes all the decisions on what to run on it
	- Example: Utility Computing, Amazon’s EC2, Rackspace, Google Compute Engine
- **Platform as a Service** (*PaaS*)
	- Provides hosting for web applications and takes care of the hardware maintenance, upgrades etc.
	- Example: Google App Engine. User provides their web application (e.g. in Python / Java) and the system takes care of all the details for hosting it.
- **Software as a Service** (*SaaS*)
	- User typically doesn’t write code, and is just using an existing app
	- Example: Gmail, Dropbox, Zoom

# Data Centers
---
You can think of a data center as one big computer instead of multiple servers.

What makes up a data center:
- At the lowest layer is just a **single server** (*Commodity hardware*)
- With multiple servers it forms a **rack** which is connected to a **rack switch** (*or top-of-rack switch, ToR*)
- With multiple racks it forms a **data center** connected to a **datacenter switch** (*or core switch*)

>[!info] Commodity Hardware
>
>Essentially they are <b><span style='color:var(--mk-color-yellow)'>cheap hardware for the general users</span></b>.
>
>Using a large number of these cheap machines to <b><span style='color: var(--mk-color-green)'>work in parallel to enhance efficiency and cost</span></b>.

>[!question] What is a Rack Switch or Datacenter switch?
>
>Both are essentially a networking device which is used to interact with servers or racks respectively.
>
><b><span style='color:var(--mk-color-yellow)'>Any interaction must go through these switches</span></b>.

When dealing with **data centers, it is better to**:
- **Scale "out"** and not scale "up"
	- Also known as horizontal vs vertical scaling
	- It is <b><span style='color:var(--mk-color-green)'>cheaper and efficient</span></b> to get more machines than to increase the power of each individual machine
- **Move processing to data**
	- Due to bandwidth and latency, it is <b><span style='color:var(--mk-color-green)'>better to do computations on servers</span></b> rather than collating it first in a centralised location.
- **Process data sequentially**
	- It is more <b><span style='color:var(--mk-color-green)'>efficient to retrieve sequentially</span></b> especially in disks when it involves disk seeks (*spinning the disk*)
	- It also makes throughput reasonable
- **Seamless scalability**
	- We should be able to scale out without disrupting the existing the system
	- And we <b><span style='color: var(--mk-color-yellow)'>want linear scalability</span></b>, if I double the number of processers it will double the performance (*Not always doable*)
## Bandwidth & Latency

**Bandwidth** refers to <b><span style='color:var(--mk-color-yellow)'>how much information can be sent per second</span></b> (*32GB/s*).

>[!info] Bandwidth along the whole path is the minimum bandwidth along the path
>
>If the bandwidth from A to B is 1 GB/s while from B to C is 10 MB/s, then the **total bandwidth is 10 MB/s**.

**Latency** refers to <b><span style='color:var(--mk-color-yellow)'>how long it takes to transfer information from one end to another</span></b> (*1ms*).

There are 2 ways to calculate latency:
1) One way (*From one end to another*)
2) Round trip (*From one end to another and the back to the source*)

>[!info] Latency combines approximately additively
>
>If the latency from A to B is 1ms while B to C is 100ms, the total latency is 1 + 100 = **101ms**.

**Throughput** refers to the <b><span style='color:var(--mk-color-yellow)'>actual amount of data bring transferred</span></b>.

Even if the cable can transmit 32GB/s it does not necessary mean that 32GB of data will be sent per second, it can be less.

>[!question] Which is more important?
>
>For **large** amount of data, <b><span style='color:var(--mk-color-green)'>bandwidth is more important</span></b> as it tell us how long the transmission will take
>
>For **small** amount of data, <b><span style='color:var(--mk-color-green)'>latency is better</span></b> since it tells us how much delay there will be
## Storage Hierarchy

>[!info] As we go up the storage hierarchy, we increase in capacity but latency & bandwidth is slower
>From server -> rack -> data center
>
>Latency and bandwidth is lower due to the switches.
### The Server

![[Typical Data Center Server Layout.png|center|500]]

Inside a server it will typically contain the following hardware:
- **DRAM** (*Dynamic random access memory*): They have a <b><span style='color:var(--mk-color-red)'>limited capacity</span></b>, however <b><span style='color:var(--mk-color-green)'>operating on it is fast</span></b>.
- **Disk**: They have a <b><span style='color:var(--mk-color-green)'>large capacity</span></b>, however <b><span style='color:var(--mk-color-red)'>operating on it is slow</span></b>
- **Flash**: In between DRAM & disk (*like an SSD*) 
- **L1 Cache**: This cache is specifically for 1 processor
- **L2 Cache**: This cache is shared between multiple processors

>[!info] For DRAM once the system shuts off, the data inside DRAM will be lost

>[!caution] Disk reads are much more expensive than DRAM resulting in higher latency & lower bandwidth
>
>However in terms of pricing, <b><span style='color:var(--mk-color-green)'>disks are the cheapest</span></b>, followed by flash then DRAM.
<div style="page-break-after: always;"></div>

### The Rack

![[Typical Data Center Rack Layout.png|center|350]]

Here a rack will contain multiple servers and in order for a server to communicate with another server it has to go through the rack switch.

>[!important] Switches are connected to the servers local DRAM
>So all data from disk must enter the DRAM first before moving to the switch.

>[!failure] Communication is slow between servers
>
>Since it has to go through the rack switch.
### The Datacenter

![[Typical Data Center Layout.png|center|350]]

Now a datacenter will contain multiple racks and similarly to communicate between racks it has to go through the datacenter switch.

>[!failure] Communication is even slower
>
>Now for the server to communicate to another server it has to potentially go through the rack switch and then the datacenter switch then to another rack switch.
<div style="page-break-after: always;"></div>

### Hierarchy Performance

![[Data Center Hierarchy Performance.png|center|500]]

>[!info] To read this graph, treat each item in the x-axis as its own column and we are transferring data from a local DRAM to the specified location 

Some key observations is that:
- <b><span style='color:var(--mk-color-red)'>Latency increases</span></b> as we **go up** the hierarchy (*Local to Rack to Datacenter*)
- <b><span style='color:var(--mk-color-red)'>Bandwidth decreases</span></b> as we **go up** the hierarchy
- <b><span style='color:var(--mk-color-red)'>Bandwidth bottlenecked</span></b> by **switches**

>[!note] Latency is dominated by disk speed
>Disk transfers have high latency so it takes about the same amount of time regardless of the hierarchy.

>[!note] Lower bandwidth is not always due to switches it can also be due to the disk, thus it depends which is the smaller of the 2


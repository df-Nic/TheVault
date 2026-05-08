---
Title: Virtualisation & Multitenancy
Date Created: 12-February-2026
Last Updated: 12-April-2026
Tags:
  - CS5224
---
# Virtualisation
---
Virtualisation is to enables a <b><span style='color: #FFD700'>single physical infrastructure to function as multiple logical infrastructure or resource</span></b>.

>[!important] This follows the IaaS model

Essentially it is <b><span style='color: #FFD700'>1-to-many utilisation</span></b> where multiple systems (*OSs*) can share resources on a single hardware.

>[!question] Why would we want to virtualise instead of giving everything to 1 system?
>It is to <b><span style='color: #98FB98'>improve utilisation</span></b> through sharing, which <b><span style='color: #98FB98'>leads to lower cost</span></b> & <b><span style='color: #98FB98'>improve scalability</span></b>.

![[Virtualisation Visualisation.png|center]]

>[!success] Hardware independence
>In a non virtualised environments, software is dependent on the hardware.

>[!success] Resource consolidation
>Increase hardware utilisation as we can pool everything into 1 & then use load balancing to utilise all our resources, this <b><span style='color: #98FB98'>reduces overall cost & increase revenue for the provider</span></b>.

>[!success] Resource replication
>We can scale rapidly as resources are virtual (*created as a virtual disk images*).
>
>In virtualisation we can <b><span style='color: #98FB98'>allocate more resources then we have to consumers</span></b> (*hedging that you will not use everything*) but we do still need to manage what if we over estimate.

>[!fail] Performance overhead

>[!fail] Single point of failure
>If our <b><span style='color: var(--mk-color-red)'>virtualisation infrastructure layer / software fails</span></b> then everyone will not be able to access the resources as in the end everything still runs on a physical infrastructure.

There are various types of virtualisation:
- **Processor** virtualisation
- **Memory** virtualisation
- **Storage** virtualisation
- **Network** virtualisation

All of these work in the same way, in the <b><span style='color: #FFD700'>virtual infrastructure we abstract out the physical resource to a pool of virtual resources</span></b>.

>[!note] Virtual memory is not the same as the one in [[Year 2/Sem 2/CS2106 - Introduction to Operating Systems/Virtual Memory Management.md|OS]]
## Virtualisation Approaches

To allow virtualisation to work we need a <b><span style='color: #87CEEB'>virtualisation software</span></b> (*virtual infrastructure*), which usually <b><span style='color: #FFD700'>sits between the virtual machine & the physical infrastructure</span></b>.

>[!abstract] Virtualisation Software
>They are your [[Year 2/Sem 2/CS2106 - Introduction to Operating Systems/Operating System Overview.md#What is an Operating System?|hypervisor]] or <b><span style='color: #FFD700'>virtual machine manager</span></b> (*VMM*).
>
>This <b><span style='color: #FFD700'>allows the providers to manage VMs & execute what the customer wants</span></b>. But underneath everyone is using the same physical infrastructure resource. 

There are a **few approaches** & this <b><span style='color: #FFD700'>determines the privilege levels the guest OS will run</span></b> in:
- **Full** virtualisation (*software-assisted virtualisation*)
Our virtualisation software makes the <b><span style='color: #FFD700'>OS thinks that they have full, direct access</span></b> to the hardware.

Here the virtualisation layer, needs to <b><span style='color: #FFD700'>map instructions to instructions for the physical hardware</span></b> (*binary translation*).

>[!info] The VMM is at ring 0
>It provides all the virtual infrastructures needed for VMs (*since it communicates to the hardware through the VMM*).
>
>**Ring 0** just means it has <b><span style='color: #FFD700'>full kernel access</span></b> (*to the hardware & the privileges decreases as it goes up*).

>[!success] Easy to install & use
>No need to modify the guest OS.

>[!success] Virtual guest OS can be easily migrated to native hardware

>[!success] Can run different OSs simultaneously
>Means it can handle multiple OSs.

>[!success] Best isolation & security for VMs

>[!fail] Binary translation overhead which reduces system performance
>It needs time to do this translation.

>[!fail] Need the correct combination of hardware & software
>Hardware might not have the **drivers** needed for the virtualisation software.

- **Para** virtualisation
Here we <b><span style='color: #FFD700'>modify the guest OS</span></b> (*now at ring 0*), so that it knows it is running on a virtualised environment. So it instead of doing OS request to hardware, it will do a <b><span style='color: #87CEEB'>hypercall</span></b> (*OS-assisted virtualisation*).

>[!abstract] Hypercalls
>They are essentially system calls which privilege to <b><span style='color: #FFD700'>communicate directly between OS & the hypervisor without any translation</span></b>.

>[!success] Better performance because there is no need for binary translation

>[!success] No need for special hardware

>[!fail] Overhead of guest OS kernel modifications
>This modified OS <b><span style='color: var(--mk-color-red)'>cannot migrate to run on physical hardware</span></b>, because it is configured to run on a VM.

>[!fail] VM's lack of backward compatibility
>If the VM infrastructure changes (*hypervisor changes*) existing modified OS's might not be able to run on it. Or it cannot migrate to other hosts.

- **Hardware-assisted** virtualisation (*native virtualisation*)
Here <b><span style='color: #FFD700'>hardware extends its functionality to support virtualisation</span></b>. Guest states are stored in virtual machine control structures.

Now the OS can **directly trap the hypervisor** <b><span style='color: #98FB98'>without any binary translation & OS modification</span></b>. 

So our VMM can have the highest root privilege while the guest OS & user applications have the same non-root privilege.

>[!success] The benefits of both para & full virtualisation
>The hardware handles everything.

**Summary** of all the approaches:

|            Description             |                 Full                  |    Para    |                               Hardware-Assisted                               |
| :--------------------------------: | :-----------------------------------: | :--------: | :---------------------------------------------------------------------------: |
|             Technique              | Binary translation & direct execution | Hypercalls | OS requests trap to VMM without any binary translation or para virtualisation |
|       Guest OS modification?       |                  No                   |    Yes     |                                      No                                       |
|           Compatibility            |               Excellent               |    Poor    |                                   Excellent                                   |
| Is guest OS hypervisor independent |                  Yes                  |     No     |                                      Yes                                      |
|         Popular vendor(s)          |              VMware ESX               |    Xen     |                      Microsoft, Virtual Iron, XenSource                       |
# Hypervisors
---
There are **2 types** of hypervisors:
1) **Type 1** (*bare metal or native*), which <b><span style='color: #FFD700'>runs on physical infrastructure without any help from the host OS</span></b>

>[!note] This runs directly on hardware

>[!danger] Security: Host OS gets compromised
>It is <b><span style='color: var(--mk-color-red)'>worse case scenario</span></b> because viruses can bleed into other applications.

2) **Type 2** (*hosted or embedded*), which requires the <b><span style='color: #FFD700'>help of host OS to communicate with underlying infrastructure</span></b>

>[!note] This is like a program that runs on an existing OS

>[!danger] Security: Guest OS gets compromised
>**Not as bad** if the host OS gets compromised due to it <b><span style='color: #98FB98'>running in an isolated environment</span></b>.
# Containers
---
It allows for the existence of **multiple isolated user space instances** (*apps + libraries*), <b><span style='color: #98FB98'>without the need to have a guest OS</span></b> (*lightweight*).

>[!success] Lightweight

>[!success] Portability
>Just needs what you require to run the application, no need for the OS.

So [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Software Engineering Principles & Patterns.md#Containers|containers]] can <b><span style='color: #FFD700'>allow applications which requires different OSs to run & share the host system's kernel</span></b> (*OS*).

>[!important] This follows the PaaS model

>[!example] A popular platform to deploy containers is docker
## Docker

It is an open platform for <b><span style='color: #FFD700'>developing, shipping and running applications</span></b>. It enables you to <b><span style='color: #FFD700'>separate your applications from your infrastructure</span></b> so that you can <b><span style='color: #98FB98'>deliver software quickly</span></b>.

Docker package & run an application in a loosely isolated environment (*container*).

Uses the idea of <b><span style='color: #87CEEB'>namespaces</span></b> to provide the isolated workspace. Written in the Go programming language and takes advantage of several features of the Linux kernel.

>[!abstract] Namespaces
>Basically process isolation, where it takes advantage of the Linux process information like the process ID and the type of file system.
>
### Docker Architecture

Here is an **overview** of the architecture:
![[Docker Architecture.png|center]]

>[!info] It uses a [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Software Architecture.md#Client Server|client-server architecture]].
### Docker Components

- **Docker desktop**
This is just the <b><span style='color: #FFD700'>entry point to docker</span></b>, it includes your docker daemon, client, compose etc. So this just enables you to build & share containerised applications & microservices.

- **Docker client**
The primary way users interact with docker & <b><span style='color: #FFD700'>communicate with multiple daemons</span></b>.

- **Docker daemon**
It listens to what the user wants to do and executes it (*just a background process*). It is <b><span style='color: #FFD700'>in charge of building, running & distribution</span></b> the docker containers.

It <b><span style='color: #FFD700'>listens for docker API requests & manages docker objects</span></b> (*images, containers, networks, etc*).

It can <b><span style='color: #FFD700'>communicate with other daemons</span></b> to manage docker services.

Docker client and daemon **communicate** using [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Software Architecture.md#Representational state transfer|REST]] API, over UNIX sockets or a network interface.

- **Docker registries**
Its main task is to <b><span style='color: #FFD700'>store images</span></b>.

There is a thing called a <b><span style='color: #87CEEB'>docker hub</span></b>, which is a <b><span style='color: #FFD700'>public registry</span></b> that anyone can use & docker looks for images on it by default.

- **Images**
<b><span style='color: #FFD700'>Read only template with instructions on creating a docker container</span></b>. Often based on another image but you can also create your own using a `dockerfile`.

- **Containers**
<b><span style='color: #FFD700'>Runnable instances of an image</span></b> (*when it starts executing*), where you can create, start, stop, move or delete a container using the **docker API**.

It also <b><span style='color: #FFD700'>controls how isolated a container's elements are</span></b> from other containers or the host machine.

>[!success] There is a lot of control that the user can have when using docker containers
# Multitenancy
---
>[!info] This follows the SaaS model

Essentially a cloud provider will have a <b><span style='color: #FFD700'>single instance of a software</span></b> on a server where each <b><span style='color: #FFD700'>consumer thinks it has a copy</span></b> of this software (*office365, MS Teams, etc*).

So essentially it enables multiple consumers (*tenants*) to <b><span style='color: #FFD700'>share the same application</span></b>.

It has a **dedicated instance** with a <b><span style='color: #FFD700'>customised view</span></b>, but they are <b><span style='color: #98FB98'>isolated</span></b> from others in terms of data where they can <b><span style='color: #FFD700'>only access & configure information that is own by them</span></b>.

>[!abstract] Multitenancy vs Virtualisation
>Multitenancy is the result of virtualisation. <b><span style='color: #FFD700'>Without virtualisation, multitenancy cannot happen</span></b>.
>
>**Multitenancy** deals with dedicated software instances for each consumer. **Virtualisation** deals with the abstraction of physical resources.

Here are some **characteristics** of multitenancy:
- **Usage / Tenant isolation**, a consumer does not affect another
- **Data security**, separate procedures for each tenant
- **Recovery**, backup & restore for 1 user
- **Scalability**, can scale based on usage
- **Metered usage**, charged for what is being used
- **Data tier isolation**, databases, tables can be isolated or be a shared resource

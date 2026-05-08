---
title: Operating System Overview
Date Created: 2025-01-15
Last Updated: 2025-09-28
tags:
  - CS2106
  - Hardware
---
# What is an Operating System?
---
A simple definition is that an **OS**, is just a <span style='color:var(--mk-color-yellow)'>intermediary program between the user and computer hardware</span>.

> [!question] Why is the OS Important?
> This is useful, because an **OS** helps to <span style='color:var(--mk-color-yellow)'>encode programs into machine code</span> for the hardware.
> 
> Without it, the <span style='color:var(--mk-color-red)'>user will have to manually encode</span> it every time the program executes.

Over the years there are <span style='color:var(--mk-color-orange)'>significant improvements</span> in OS such as:
- **Multiprogramming** - Allowing multiple programs to be executed at the same time
- **Time-Sharing** - Allowing multiple users to run programs on the same OS through virtualization (*Illusion of concurrency*)
# Why do We Need an OS?
---
## Abstraction

The OS <span style='color:var(--mk-color-yellow)'>serves as a layer of abstraction</span> from the low level details. By <span style='color:var(--mk-color-yellow)'>providing a common interface</span> (*Known as a Shell*) of high level functionality.

Thus it is <span style='color:var(--mk-color-green)'>efficient</span> and <span style='color:var(--mk-color-green)'>portable</span> since the **user can perform tasks through the OS**.

> [!question] Why does it Work?
> Essentially, hardware of the same category is <b><mark style='background:var(--mk-color-yellow)'>well defined</mark></b> and has <b><mark style='background:var(--mk-color-yellow)'>common functionality</mark></b>.
> 
> *For example, a disk drive you can most likey only read and write data, thus the common functionality is what the OS provides and will issue specfic instructions for the specfic type of hardware.*
> 
> The **device that does this** is called a <span style='color:var(--mk-color-turquoise)'>device driver</span>.
## Resource Allocation

As mention before, it <span style='color:var(--mk-color-green)'>allows for multiprogramming</span> by managing resources from your hardware.

> [!abstract] How does it allocate resources
> Typically when a program is executed, certain memory, CPU, etc are provided. And there are <span style='color:var(--mk-color-yellow)'>multiple programs running</span> at once.
> 
> In addition, when a **program is idling**, instead of wasting resources, it can <span style='color:var(--mk-color-yellow)'>reallocate</span> to execute some other programs.
## Control Program

The OS can control the execution of programs, to <span style='color:var(--mk-color-green)'>prevent errors and improper use</span> and <span style='color:var(--mk-color-green)'>provides security and protection</span>.

This **allows for sharing of a computer** by multiple people, as the <span style='color:var(--mk-color-yellow)'>OS ensures a seperate space</span> for each user so that <span style='color:var(--mk-color-green)'>program cannot read data from another user's program</span>.
# OS Structures
---
Some <span style='color:var(--mk-color-orange)'>important factors</span> to ensure when designing the structure of an OS:
- **Flexibility**
- **Robustness**
- **Maintainability**

**Simple design of a computer**
![[High Level Design of a Computer.png|center|500]]

It is **important for a CPU to operate** in at least <span style='color:var(--mk-color-turquoise)'>user</span> & <span style='color:var(--mk-color-turquoise)'>kernel</span> modes. It is possible to **switch from user to kernel mode** but it is <span style='color:var(--mk-color-red)'>very expensive</span> (*It takes a lot of cycles*).

> [!important] User vs Kernel Mode
> A **kernel mode** has <b><mark style='background:var(--mk-color-yellow)'>100% access</mark></b> to the whole computer, while **user mode** has <b><mark style='background:var(--mk-color-yellow)'>some restrictions</mark></b> to memory and cannot access hardware by itself.
> 
> Therefore it is **important that applications should be in user mode**, to <span style='color:var(--mk-color-green)'>prevent theft or deletion of data</span> by mallicious software.
> 
> At any point if a program in user mode **access memory that is restricted**, it will cause a <span style='color:var(--mk-color-red)'>segmentation fault</span>.
# OS as a Program
---
**Interactions between components in a computer**
![[Interactions between components in a computer.png|center|500]]

An OS as a program is also known as a <b><mark style='background:var(--mk-color-turquoise)'>kernel</mark></b>. With some special features such as:
- **Dealing with hardware issues**
- Provides **system call interface**
- Code to interrupt handlers, device drivers

**Libraries** provide a level of abstraction and allow one to communicate with the OS even on different versions.

> [!info] Dae-mons
> Programs that <span style='color:var(--mk-color-yellow)'>run in the background of an OS</span>.
> 
> Depending on the task, **different deamons will operate its own specfic tasks** until the system stops.

> [!abstract] Kernal Code
> To **code an OS**, it is <span style='color:var(--mk-color-orange)'>different from normal coding of programs</span>:
> - <span style='color:var(--mk-color-red)'>No</span> **use of system call** in kernel code (*Because the system calls call the kernel, thus a recursive loop*)
> - <span style='color:var(--mk-color-red)'>Cannot</span> **use normal libraries** (*Libaries uses the kernel*)
> - <span style='color:var(--mk-color-red)'>No</span> **normal I/O** (*The I/O uses the kernel*)
# Implementing an Operating System
---
Historically, it is coded in <span style='color:var(--mk-color-purple)'>assembly</span> (*machine code*). But **now it is in high level languages** (*HLL*) like <span style='color:var(--mk-color-purple)'>C or C++</span>.

A **downside** is that it can be <span style='color:var(--mk-color-red)'>heavily hardware architecture dependent</span>.

The <span style='color:var(--mk-color-orange)'>common code organisation</span> for an OS:
- **Machine independent HLL** usage of queues independent of hardware
- **Machine dependent HLL** to set up hardware for the OS
- **Machine dependent assembly code** to access [[MIPS#Registers|registers]] in the CPU and thus has to be written in <span style='color:var(--mk-color-purple)'>assembly</span>

> [!danger] Challenges of Creating an OS
> Here are some <span style='color:var(--mk-color-orange)'>challenges when designing an OS</span>:
> - **Debugging is hard**
> - **Complex**
> - **Enormous Codebase**
> - “No one else” to rely on for nice services
# OS Structures
---
There are <span style='color:var(--mk-color-orange)'>2 popular ways of structuring</span> an OS:
- **Monolithic**
- **Microkernel**
## Monolithic

It is like **one big program**, but is **not necessary compiled as a whole** as <span style='color:var(--mk-color-yellow)'>components can be added or removed</span>.

In addition, **majority of the core components** in the kernel <span style='color:var(--mk-color-yellow)'>runs in kernel mode</span>. But user programs still run in user mode.

> [!abstract] Advantages & Disadvantages of Monolithic Kernels
> > [!success] Efficient
> > It is <span style='color:var(--mk-color-green)'>efficient</span>, as it <span style='color:var(--mk-color-yellow)'>swaps between user and kernel mode less</span>.
> 
> > [!fail] Potential data loss
> >There can be <span style='color:var(--mk-color-yellow)'>buggy code</span> in the device driver, causing the <span style='color:var(--mk-color-yellow)'>system to crash</span> and in the worst case, <span style='color:var(--mk-color-red)'>cause a loss of data</span>, since alot of it is in kernel mode.
## Microkernel

It is a <span style='color:var(--mk-color-yellow)'>small and clean architecture</span> (*essential components only*) which only <span style='color:var(--mk-color-yellow)'>provides basic and essential facilities</span>. Essentially, if the functions can be done in user mode it will be done in user mode.

It uses a <span style='color:var(--mk-color-turquoise)'>inter-process communication</span> (*IPC*) to provide access to these basic and essential services.

> [!abstract] Advantages & Disadvantages of Microkernels
> > [!success] More secure
> > As only <span style='color:var(--mk-color-yellow)'>essential functions are done in kernel mode</span>, the rest are done in user mode.
> 
> > [!fail] Less efficient
> >Since only a **small portion is in kernel mode**, the <span style='color:var(--mk-color-yellow)'>frequency of swapping between user and kernel mode increases</span>.
## Other Operating System Structures

> [!note] Layered Systems
> <span style='color:var(--mk-color-yellow)'>Generalisation</span> of a **monolithic system**, where components are organised into <span style='color:var(--mk-color-yellow)'>hierarchy of layers</span>. Upper layers will make use of lower layers (*Highest is user interface, lowest is hardware*).

> [!note] Client-Server Model
> A variation of a microkernel, which <span style='color:var(--mk-color-orange)'>consist of 2 processes</span>, <span style='color:var(--mk-color-turquoise)'>client and server process</span>, where the client process request services from the server process.
> 
> **Server processes are built on top of a microkernel**. And these 2 processes can be on seperate machines.
# Virtual Machines
----
An OS will **assume total control** of the hardware, but what if you:
- Want to **run several OSes on the same hardware**
- **Test and debug** a beta version of an OS

This is where a <span style='color:var(--mk-color-turquoise)'>virtual machine</span> come in handy, it allows concurrent usage of OSes. It also provides a save environment and tools to test performances of an OS.

> [!question] How does it work?
> It provides a <span style='color:var(--mk-color-yellow)'>virtualisation of the underlying hardware</span>, giving the OSes the illusion of control over the hardware. Thus a normal operating system can run on top of the virtual machine.
## Hypervisor

It is a layer which enables <span style='color:var(--mk-color-yellow)'>resource allocation of hardware</span> to the various virtual machines.

> [!info] Intel Chips
> It allows **nested virtualisation**, which means it can run a VM inside another VM.
### Type 1 Hypervisor

Here the <span style='color:var(--mk-color-yellow)'>CPU provides support for virtualisation</span>, it has functions to allow it to support different OSes.

**Structure of a Type 1 Hypervisor**
![[Structure of a VM using Type 1 Hypervisor.png|center|500]]

The type 1 hypervisor has <span style='color:var(--mk-color-yellow)'>direct access to hardware</span>, which can support multiple OSes.
## Type 2 Hypervisor

Here the hypervisor <span style='color:var(--mk-color-yellow)'>runs on top of a host OS</span>. It has <span style='color:var(--mk-color-yellow)'>drivers which remaps instructions</span> from the guest OS.

![[Structure of a VM using Type 2 Hypervisor.png|center|500]]

> [!fail] Type 2 Hypervisor is Slower
> Unlike a type 1 hypervisor, a type 2 however <span style='color:var(--mk-color-yellow)'>runs on top of another operating system</span>, and thus it will be <span style='color:var(--mk-color-red)'>inherently less efficient and slow</span>. 

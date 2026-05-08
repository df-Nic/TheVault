---
title: Reuse
Date Created: 2024-10-26
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE
  - SoftwareDesign
---
# Why Reuse Just Code More
---
The purpose of **reusing tried and tested components**, is that it can <span style='color:var(--mk-color-green)'>enhance the robustness</span> of the software while <span style='color:var(--mk-color-green)'>reducing manpower and time requirement</span>.

So reusing is a good thing well no there are <span style='color:var(--mk-color-orange)'>some cost associated with it</span>:
- Reuse code can be an <span style='color:var(--mk-color-red)'>overkill</span> (*Increases size but degrades performance*)
- May not be <span style='color:var(--mk-color-red)'>mature or stable enough</span> as it is possible it can change how the software works
- There is a <span style='color:var(--mk-color-red)'>risk of dying off</span>, when using other libraries if they do not update them then there can be **dependency issues**
- The license can <span style='color:var(--mk-color-red)'>restrict how you can develop</span> the software
- The reused software might <span style='color:var(--mk-color-red)'>have bugs, missing features, or security vulnerabilities</span>. And fixes to them might not be fast
- <span style='color:var(--mk-color-red)'>Malicious code</span> can sneak into your product via compromised dependencies
# API
---
Also known as <span style='color:var(--mk-color-turquoise)'>application programming interface</span>. It <span style='color:var(--mk-color-yellow)'>specifies the interface</span> through which **other programs interact with** the component.

When developing large systems, if you **define the API of each component early**, the development team can <span style='color:var(--mk-color-green)'>develop the components in parallel</span> because the future behavior of the other components are now more predictable.

Is like the `String` class in <span style='color:var(--mk-color-purple)'>Java</span>, **all functions** <span style='color:var(--mk-color-yellow)'>except private</span> functions are part of the API.

> [!abstract] Designing APIs
> An API should be <span style='color:var(--mk-color-yellow)'>well-designed</span> (i.e. should cater for the needs of its users) and <span style='color:var(--mk-color-yellow)'>well-documented</span>.
> 
> When you write software consisting of multiple components, you need to define the API of each component.
> 
> One approach is to let the API emerge and evolve over time as you write code.
> 
> You can use <span style='color:var(--mk-color-yellow)'>UML sequence diagrams to analyze the required interactions</span> between components in order to discover the required API and their functionality. Given below is an example.
# Libraries
---
A library is a <span style='color:var(--mk-color-yellow)'>collection of modular code</span> that is <span style='color:var(--mk-color-yellow)'>general</span> and can be used by other programs.

These are some <span style='color:var(--mk-color-orange)'>steps to follow when using a library</span>:
1) <span style='color:var(--mk-color-yellow)'>Read the documentation</span> to confirm that its functionality fits your needs.
2) <span style='color:var(--mk-color-yellow)'>Check the license</span> to confirm that it allows reuse in the way you plan to reuse it. For example, some libraries might allow non-commercial use only.
3) Download the library and <span style='color:var(--mk-color-yellow)'>make it accessible to your project.</span> Alternatively, you can **configure your dependency management tool** to do it for you.
4) Call the library API from your code where you need to use the library's functionality.
# Frameworks
---
If the overall **structure and execution flow** of a specific category of software systems can be **very similar**. The similarity is an <span style='color:var(--mk-color-yellow)'>opportunity to reuse at a high scale</span>.

A **software framework** is a reusable implementation of a software (or part thereof) <span style='color:var(--mk-color-yellow)'>providing generic functionality</span> that can be <span style='color:var(--mk-color-yellow)'>selectively customized to produce a specific application</span>.

Some frameworks **provide a complete implementation** of a default behavior which makes them <span style='color:var(--mk-color-yellow)'>immediately usable</span>.

A framework <span style='color:var(--mk-color-yellow)'>facilitates the adaptation and customization</span> of some desired functionality.

Some frameworks cover <span style='color:var(--mk-color-yellow)'>only a specific component or an aspect</span>.

Unlike libraries, frameworks are <span style='color:var(--mk-color-yellow)'>meant to be customized or extended</span> while **libraries are meant to be used as it is**.

Also **you call the library code**, but the<span style='color:var(--mk-color-yellow)'> framework calls your code</span> (*this is known as inversion control or "Hollywood principle"*).
# Platforms
---
A <span style='color:var(--mk-color-turquoise)'>platform</span> is a **combination** of frameworks, tools, libraries and technologies. In other words it <span style='color:var(--mk-color-yellow)'>provides a run time environment </span>for the application.

Technically a IOS is a platform. For example, Windows PC is a platform for desktop applications while iOS is a platform for mobile applications..

**2 well known platforms** are <span style='color:var(--mk-color-purple)'>JavaEE</span> and <span style='color:var(--mk-color-purple)'>.NET</span>. They both **sit above the operating systems layer** and are used to develop enterprise applications and infrastructure services (*remote code execution,  authentication, security, etc*).

They provide these services to applications in a <span style='color:var(--mk-color-yellow)'>customizable way</span> <span style='color:var(--mk-color-green)'>without</span> developers having to <span style='color:var(--mk-color-green)'>implement them from scratch every time</span>.

**JavaEE (Java Enterprise Edition)**
>Is both a framework and a platform for writing enterprise applications. The runtime used by JavaEE applications is the JVM (Java Virtual Machine) that can run on different Operating Systems.

**.NET** 
>is a similar platform and framework. Its runtime is called CLR (Common Language Runtime) and it is usually used on Windows machines.
# Cloud Computing
---
<span style='color:var(--mk-color-turquoise)'>Cloud computing</span> is the **delivery of computing as a service** <span style='color:var(--mk-color-yellow)'>over the network</span>.

Instead of running it locally, the <span style='color:var(--mk-color-yellow)'>software resides somewhere remote</span> (*larger server farm*), where users access them over the network.

This software are usually <span style='color:var(--mk-color-yellow)'>managed by the cloud providers</span> and users pay for the services they use.

it can <span style='color:var(--mk-color-green)'>optimize hardware and software utilization</span> and <span style='color:var(--mk-color-green)'>reduces the cost to consumers</span>. Furthermore, users can <span style='color:var(--mk-color-green)'>scale up/down their utilization</span> at will **without having to upgrade their hardware and software**.

Cloud computing can <span style='color:var(--mk-color-orange)'>provide services at 3 levels</span>:
1) **Infrastructure as a service (IaaS)**
It <span style='color:var(--mk-color-yellow)'>delivers computer infrastructure as a service</span>. For example instead of physical hardware, user can deploy virtual serves on the cloud.

2) **Platform as a service (PaaS)**
it provides a platform on which <span style='color:var(--mk-color-yellow)'>developers can build applications</span>. Developers do **not need to worry about infrastructures issues like deploying to servers or load balancing**. The only down side is that there is <span style='color:var(--mk-color-red)'>reduced flexibility and limited facilities</span> (*google app engine)*.

3) **Software as a service (SaaS)**
It allows **applications** to be <span style='color:var(--mk-color-yellow)'>accessed over the network</span> instead of installing them on a local machine (*Google drive*).
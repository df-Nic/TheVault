---
title: Design Principles
Date Created: 2024-10-20
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE
  - SoftwareDesign
---
# Separation of Concerns
---
Also known as **SOC**, is to <span style='color:var(--mk-color-yellow)'>separate code</span> (*Functionality*) into <span style='color:var(--mk-color-yellow)'>distinct sections</span> so that each addresses a separate concern.

> [!note] Ways of Seperation
> We can <span style='color:var(--mk-color-orange)'>segregate</span> based on:
> 1) **Feature** - `Add employee` or `Save data`
> 2) **Aspect** - `Database` or `GUI` related
> 3) **Entity** - `Person` or `Bank`
> 
> In summary, it can be applied at the <span style='color:var(--mk-color-yellow)'>class level or higher</span>.

By doing this it <span style='color:var(--mk-color-green)'>reduces functional overlaps</span> and <span style='color:var(--mk-color-green)'>limits</span> the <span style='color:var(--mk-color-red)'>ripple effect</span> when changes happen.

The benefit of doing this is that it <span style='color:var(--mk-color-green)'>achieves better modularity</span>, <span style='color:var(--mk-color-green)'>higher</span> [[Designing A Software#Cohesion|cohesion]] and <span style='color:var(--mk-color-green)'>lower</span> [[Designing A Software#Coupling|coupling]].
# Single Responsibility Principle
---
It states that a <span style='color:var(--mk-color-yellow)'>class should only have 1 reason to change</span>

> [!example] SRP Example
> Lets look at `Person` class, it is responsible for handling what a person does.
> 
> It will only change if the <span style='color:var(--mk-color-yellow)'>definition of a person changes</span> or the person can <span style='color:var(--mk-color-yellow)'>do something new</span>.
# Liskov Substitution Principle
---
It [[Polymorphism#Liskov Substitution Principle|states]] that any derived class must be **substitutable for their base classes**. Essentially a <span style='color:var(--mk-color-yellow)'>subclass should not be more restrictive that the behavior of the superclass</span>.

> [!example] Liskov Example
> Lets say our superclass is `Staff` and the subclass is `Academic` and `Admin`.
> 
> There is a function called `adjustSalary(int)` which has the following functionality
> - `Admin` it works for any value
> - `Academic` it work for values 1 to 100
> 
> Then `Academic` class violates the principle since its <span style='color:var(--mk-color-red)'>more restrictive</span>.
`
# Open-Closed Principle
---
For a module, it should be <span style='color:var(--mk-color-red)'>closed for modification</span> but <span style='color:var(--mk-color-green)'>open for extension</span>. This can be done through an <span style='color:var(--mk-color-purple)'>interface</span>.

Essentially, if something new were to be **added**, the <span style='color:var(--mk-color-yellow)'>existing code does not need to be modified</span>.

> [!example] OCP Example
> Look at the `Parser` function which passes a command to the `Command` class and get the correct command.
> 
> If we were to add a `Delete` command, then we just need to extend it from the `Command` class. And this the `Parser` class <span style='color:var(--mk-color-green)'>does not need to be modified</span>.
# Law of Demeter
---
*"Don't talk to strangers, talk to friends"*, this is know as the <span style='color:var(--mk-color-turquoise)'>principle of least knowledge</span>.

It states that an object should only interact with <span style='color:var(--mk-color-orange)'>objectes closely related</span> to it:
- The object `O` itself
- The objects passed as parameters (`x`)
- The objects created/instantiated in the function call (*directly or indirectly*)
- The objects direct association of `O` (*1 function call from its variables*)

It is to **prevent** the objects from **navigating** the<span style='color:var(--mk-color-yellow)'> internal structures of the other objects.</span>.


> [!example] LoD Example
> > ```Java
> > public void f(Obj x) {
> > 	this.foo(); // This is alright
> > 	this.bank.getAccount().getBalance(); // This violates LoD
> > 	new Bank().getBalance(); // This is alright
> > 	x.addOne(); // This is alright
> > }
> > ```

>Before we continue, the 5 principles mentioned are called <span style='color:var(--mk-color-turquoise)'>SOLID</span> principles.
# Interface Segregation Principle
---
It states that no function should be forced to <span style='color:var(--mk-color-yellow)'>depend on methods it does not use</span>.

**Example of ISP**
![[ISP Example.png|center|400]]

Any function in `Payroll` should not take in an object of `AdminStaff`, but rather `SalariedStaff`.
# Dependency Inversion Principle
---
It states that:
1. **High-level** modules <span style='color:var(--mk-color-red)'>should not depend</span> on **low-level modules**. Both should <span style='color:var(--mk-color-yellow)'>depend on abstractions</span>.
2. <span style='color:var(--mk-color-red)'>Abstractions should not depend on details</span>. Details should depend on abstractions.

**DIP example:**
![[Dependency Inversion Principle.png|center|400]]

Design $a$ is incorrect since a higher class `Payroll` relies on the lower class `Employee`. Where as for design $b$ it is **preferred** since it is <span style='color:var(--mk-color-green)'>flexible and less coupled</span>.
# Additional Principles
---
**YAGNI principle**
> *You Aren't Gonna Need It!*, means do **not add code because you might need it in the future**. <span style='color:var(--mk-color-yellow)'>Code what you need</span>.

**DRY principle**
>*Don't Repeat Yourself*, means that functionality should <span style='color:var(--mk-color-red)'>not be implemented twice</span> even if the implementations are different (*No duplication of information*).

**Brooks' Law**
>**Adding people later into the project** is <span style='color:var(--mk-color-red)'>not beneficial</span>, as there will be additional communication overhead.



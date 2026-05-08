---
title: Models
Date Created: 2024-09-01
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE
  - UML
---

# Introduction to Models
---
**Models** are <span style='color:var(--mk-color-yellow)'>representations</span> of abstractions of a product or something.

With models it <span style='color:var(--mk-color-green)'>provides a simpler view</span> of a complex entity because the model <span style='color:var(--mk-color-yellow)'>captures only selected aspects</span> of it.

Therefore because of this, <span style='color:var(--mk-color-yellow)'>multiple models are needed to fully capture</span> the characteristics of the software (*Can be the same type or different types*).

> [!note] Uses of Models
> Here are some functionality of models:
> 1) **Analyse complex entity related to software development**
> > Models can <span style='color:var(--mk-color-green)'>help understand the problem</span> to be solved. It can also <span style='color:var(--mk-color-green)'>help in building a solution</span> (*Architecture diagram*).
> 
> 2) **Communicate information among stakeholders**
> > Models are essentialy <span style='color:var(--mk-color-yellow)'>visual aids</span> for discussions and documentation (*E.g. Use case diagram can help sell product functionality to customers*).
> 
> 3) **Blueprint for creating software**
> > Models essentially <span style='color:var(--mk-color-yellow)'>tells how the software should function</span> with different components (*E.g. Software can use UML models to generate code based of it*).

Models are a <span style='color:var(--mk-color-green)'>good way of analysing the design</span> of the software before coding.

>*Side node: There is a type of development that uses models to build the product and it is called <span style='color:var(--mk-color-turquoise)'>model-driven development</span> (**MDD**)*.
# UML Models
---
Known as <span style='color:var(--mk-color-turquoise)'>unified modeling language</span>, is a **graphical notation** to <span style='color:var(--mk-color-yellow)'>describe various aspects</span> of a software system.

**Types of UML Diagrams**
![[Types of UML Diagrams.png|center]]

<span style='color:var(--mk-color-turquoise)'>OO structures</span>: They are a **network of objects** that shows how they **interact with one another**.

This is useful in <span style='color:var(--mk-color-yellow)'>networking relevance of different objects in terms of functionality</span>. However this diagram is <span style='color:var(--mk-color-red)'>not set in stone</span>. **Depending on the rules** (*Must follow strictly*) illustrated by the <span style='color:var(--mk-color-turquoise)'>class structure</span>, the OO Solution can change.
## Class Diagram

The class diagram <b><mark style='background:var(--mk-color-yellow)'>describes the structure</mark></b> (*Not behavior*) of an OOP solution.

It essentially **shows** the, **variables**, **functions** and **relationships** between different classes.

**Example of a class Diagram**
![[Class Diagram Example.png|center|450]]
### Representing a Class

**Class diagram example**
![[Class Diagram - Class Representation.png|center]]

The class diagram is spilt into <span style='color:var(--mk-color-orange)'>3 parts</span>:
1) **Class name**
2) **Class attributes**
3) **Class functions**

These compartments <span style='color:var(--mk-color-red)'>excluding the name</span> can be **omitted** if it is <span style='color:var(--mk-color-yellow)'>irrelevant</span> or there are <span style='color:var(--mk-color-yellow)'>no functions/variables</span>.

The attributes & functions shown in the image are **non-static**, for **static** ensure that the attribute name or function name <span style='color:var(--mk-color-yellow)'>is underlined</span> ( _ ).

For **abstract** classes, use `{abstract} className` (*Or Italic it but is not recommended*), for **interfaces** use `<<interface>> className` and a <span style='color:var(--mk-color-yellow)'>dotted line with a triangle head</span>.

A **default value** can be added as well by adding a, `= defaultValue` <span style='color:var(--mk-color-yellow)'>to the right</span>.

> [!abstract] Access Modifiers Notation
> As you can see at the **left of every entry** there is a symbol and these corrospond to the following access modifiers:
> - `+` : Public
> - `-` : Private
> - `#` : Protected
> - `~` : Package Private
> 
> Unlike <span style='color:var(--mk-color-purple)'>Java</span>, in a class diagram there is **no default access modifier**. If it is not stated it means <span style='color:var(--mk-color-yellow)'>visiability is not shown</span> or is <span style='color:var(--mk-color-yellow)'>not important for the purpose</span> of the diagram.

<span style='color:var(--mk-color-turquoise)'>Enumeration</span>, is when a <span style='color:var(--mk-color-yellow)'>fixed set of values</span> can be considered as a data type (*Enums*). It <span style='color:var(--mk-color-yellow)'>limits the values than can be assigned</span> to a value. It is also useful as <span style='color:var(--mk-color-purple)'>Java</span> compiler can **detect invalid assigning of values**. To initialise a <span style='color:var(--mk-color-turquoise)'>enumeration</span> (*Enum*), `<<enumeration>> className`, then the <span style='color:var(--mk-color-yellow)'>next component is all valid values</span>.

**Generic classes** like `class<T>`, can also be expressed in a class diagram as such:

![[Generic Classes in a Class Diagram.png|center]]
### Class Associations

<span style='color:var(--mk-color-turquoise)'>Associations</span> are the connections between different objects, basically the <span style='color:var(--mk-color-yellow)'>interactions between objects</span>, which <span style='color:var(--mk-color-yellow)'>can change over time</span>.

Associations between objects can be **generalised between the corresponding classes**. Thus when implementing associations to classes use <span style='color:var(--mk-color-yellow)'>instance level variables</span>.

**Indicating associations** in a class diagram by simply <span style='color:var(--mk-color-yellow)'>connecting a solid line from 1 class to another</span>.

Another way is to <span style='color:var(--mk-color-yellow)'>show the association as an attribute instead</span>.

**Example:**
![[Class Associations as an Attribute.png|center]]

The example shows that a `board` has 100 `square` association and how it can be shown as an attribute.

> [!example] Writting Attribute Association
> Here is the format for using attributes for associations: 
> > `name: type [multiplicity] = default value`
> 
> Do note that you either choose to represent an association as an **attribute OR a line**, <b><mark style='background:var(--mk-color-red)'>but not both</mark></b>.

In addition to associations, additional decorations can <span style='color:var(--mk-color-yellow)'>add more information to the class diagram</span>, such as:
- **Association labels**
- **Association roles**
- **Multiplicity**
- **Navigability**
#### Association Labels

An <span style='color:var(--mk-color-turquoise)'>association label</span> describes the <span style='color:var(--mk-color-yellow)'>meaning of an association between 2 classes</span>.

There is also a need to <span style='color:var(--mk-color-yellow)'>specify the direction</span> in which to read the label.

**Example:**
![[Association Label Examples.png|center|500]]
#### Association Roles

An <span style='color:var(--mk-color-turquoise)'>association role</span> describes the <span style='color:var(--mk-color-yellow)'>role played by the class</span> in the association.

**Example:**
![[Association Role Example.png|center]]

In this example, an **admin is in change of students**, thus the "charges" role at the student side.

This is optional, however it is <span style='color:var(--mk-color-green)'>good to differentiate multiple associations</span> between the same class (*Many roles to the same class*).

#### Navigability

When there is a line between 2 classes, it is <b><mark style='background:var(--mk-color-yellow)'>not always the case that both classes has a relationship</mark></b> with each other.

<span style='color:var(--mk-color-turquoise)'>Navigability</span> shows <span style='color:var(--mk-color-yellow)'>which object has the association</span>. It can be:
- **Unidirectional** : Class A can navigate (*Has a reference*) to class B, **one sided**
- **Bidirectional** : **Both** classes is associated with each other

If there are **2 unidirectional associations in opposite directions** does <span style='color:var(--mk-color-red)'>not make a bidirectional association</span>. As the association can be <span style='color:var(--mk-color-yellow)'>directed at 2 different objects</span>.

**Example:**
![[Navigability Example.png|center]]

It is the <b><mark style='background:var(--mk-color-yellow)'>arrowhead that denotes navigability not the line</mark></b>.
#### Multiplicity

<span style='color:var(--mk-color-turquoise)'>Multiplicity</span> is the aspect of an OOP solution that <span style='color:var(--mk-color-yellow)'>dictates how many objects take part in each association</span>.

It basically informs how **many objects** of a class is **associated with one object of another class**.

> [!important] Types of Multiplicity
> Here are the different types of multiplicity:
> 1) `0..1` : Also known as **optional Associations**, it indicates that a variable can hold **0 or 1** object of the other class.
> 
> 2) `1` : Also known as **compulsary Associations**, means the variable will **always have**  a instance of an object of the other class.
> 
> 3) `*` : It means the variable can have 0 or more objects of the other class.
> 
> 4) `n..m` : It means the variable can have n to m (*Inclusive*) objects of the other class.

**Example:**
![[Multiplicity Example.png|center]]

- Each student must be supervised by **exactly one professor**.
- A professor **cannot** supervise **more than 5** students but **can have no** students to supervise.
- An admin can handle any number of professors and any number of students, including none.
- A professor/student can be handled by any number of admins, including none.
### Inheritance

To show <span style='color:var(--mk-color-turquoise)'>inheritance</span>, in the class diagram, <span style='color:var(--mk-color-yellow)'>draw a triangle</span> (*Does not matter if filled or not*). The **direction** of the arrow should <span style='color:var(--mk-color-yellow)'>point to the superclass</span>.

Only for **classes that inherits interfaces**, the <span style='color:var(--mk-color-yellow)'>line will be doted</span>.

**Example:**
![[Inheritance in Class Diagram.png|center]]

### Composition

<span style='color:var(--mk-color-turquoise)'>Composition</span> is an association that represents a <span style='color:var(--mk-color-yellow)'>strong whole-part relationship</span>.

There are <span style='color:var(--mk-color-orange)'>2 conditions</span> for 2 classes to be a composition:
- When the <span style='color:var(--mk-color-yellow)'>whole is destroyed, the parts are destroyed</span> as well
- <span style='color:var(--mk-color-red)'>No cyclical links</span>

You can think of it as **2 classes rely on each other** to be of meaning. <span style='color:var(--mk-color-yellow)'>But it all depends on context</span>.

> [!example] Example of Composition
> Take the 2 classes `Book` & `Chapter`
> 
> Firstly, there is no way a `Book` can be an `Chapter`, therefore it is **not cyclical**.
> 
> Secondly, when `Book` is deleted, the `Chapters` are meaningless, and if `Chapters` are deleted, there cannot exist a `Book`. Thus **whole is destroyed, parts are destroyed**.

<span style='color:var(--mk-color-turquoise)'>Composition</span> <span style='color:var(--mk-color-green)'>helps in ensuring data integrity</span> by ensuring when the **whole is deleted, the parts are deleted** as well.

To show <span style='color:var(--mk-color-turquoise)'>composition</span>, in the class diagram, <span style='color:var(--mk-color-yellow)'>draw a solid diamond</span>. The diamond should be at where the "whole" is.

**Example:**
![[Composition Example.png|center]]
### Aggregation

<span style='color:var(--mk-color-turquoise)'>Aggregation</span> represents a <span style='color:var(--mk-color-yellow)'>container-contained relationship</span>. It is a **weaker relationship** that composition. And since it is weaker it is ok to not show in the class diagrams.

To show <span style='color:var(--mk-color-turquoise)'>composition</span>, in the class diagram, <span style='color:var(--mk-color-yellow)'>draw a hollow diamond</span>. The diamond should be at where the container is.

**Example:**
![[Aggregation Example.png|center]]

### Dependencies

A <span style='color:var(--mk-color-turquoise)'>dependency</span> is a need for <span style='color:var(--mk-color-yellow)'>one class to depend on another without having a strict association</span> in the same direction.

In other words, the class does not store an attribute of another class but <span style='color:var(--mk-color-yellow)'>its functions depend on it</span> (*Arguments*).

To show <span style='color:var(--mk-color-turquoise)'>depedencies</span>, in the class diagram, <span style='color:var(--mk-color-yellow)'>the line should be doted instead of solid</span>.

**Example:**
![[Dependency Example.png|center]]

Use a dependency arrow to indicate a dependency only if that <span style='color:var(--mk-color-yellow)'>dependency is not already captured by the diagram in another way</span>.
### Association Classes

This types of classes <span style='color:var(--mk-color-yellow)'>adds additional information about an association</span>. It is another class but it is viewed in a different point of view.

To show <span style='color:var(--mk-color-turquoise)'>association class</span>, in the class diagram, <span style='color:var(--mk-color-yellow)'>extend a dotted line from a association line</span> (*Multiplicity is not required*).

**Example:**
![[Association Class Example.png|center]]
### Notes

We can add additional information to classes in the UML diagrams. In <span style='color:var(--mk-color-yellow)'>additional constraints</span> can be stated as well inside the notes.

For constraints add the `{ }` inside the note.

![[Example of Constraints in a Class Diagram.png|center]]
## Object Diagram

Unlike class diagrams, <span style='color:var(--mk-color-turquoise)'>object diagrams</span> shows the entire **object structure at any point of time**. They are usually <span style='color:var(--mk-color-yellow)'>complemented with class diagrams</span>.

Since an **object diagram is derived from the class diagram**, it can also <span style='color:var(--mk-color-yellow)'>correspond to a class diagram</span> as well.

**Example:**
![[Object Diagram Example.png|center]]

A class object has to be written in the <span style='color:var(--mk-color-orange)'>following format</span>:
- The header, `objectName:className`, the object name <span style='color:var(--mk-color-yellow)'>can be empty</span> indicating an **unnamed object**.
- The header has to be <span style='color:var(--mk-color-yellow)'>underlined</span> as well, with a <span style='color:var(--mk-color-yellow)'>colon at the front</span>.
- Has **no function compartment** but the <span style='color:var(--mk-color-yellow)'>attributes has to be assigned</span> based on the class diagram. It can be omitted if not relevant.

The associations is the **same as a class diagram** with only the <span style='color:var(--mk-color-yellow)'>line</span> and the <span style='color:var(--mk-color-yellow)'>arrowhead</span>. **Multiplicities are omitted** because the <span style='color:var(--mk-color-yellow)'>object's association represents the multiplicity</span>. Labels and roles are **optional**.

With **inheritance**, in the object diagram, <span style='color:var(--mk-color-yellow)'>show either the parent or child class</span> <span style='color:var(--mk-color-red)'>but not both</span>. And <span style='color:var(--mk-color-red)'>do not show dependencies</span>.
# Sequence Diagrams
---
This diagram models the <span style='color:var(--mk-color-yellow)'>interactions between various entities</span> in a system if a <b><span style='color:var(--mk-color-yellow)'>specific scenario</span></b>. It is also known as a <span style='color:var(--mk-color-turquoise)'>UML sequence diagram</span>.
>- It can model how components interaction
>- Models how objects interact with one another

**Basic Notation:**
![[Sequence Diagram Basic Notation Example.png|center|500]]

**Key points to take note of:**
- **Instances** starts with a `:` for example, `:TextUi` or `<Object Name>:TextUi`
- **Function calls** are denoted with <span style='color:var(--mk-color-yellow)'>solid lines</span> and the **function name and arguments above it** <span style='color:var(--mk-color-red)'>don't need to include the object</span>.
- **Returns** are denoted with <span style='color:var(--mk-color-yellow)'>dotted lines</span>.

Optional elements (e.g, activation bars, return arrows) **may be omitted** if the omission does <span style='color:var(--mk-color-yellow)'>not</span> result in ambiguities or <span style='color:var(--mk-color-yellow)'>loss of relevant information</span>.

> [!attention] Activation Bar Common Errors
> Activation bar denotes a function being **executed**
> 
> **Activation bar too long**
> - Ensure that the **arrows are at the tip or at the very end** of the rectangle, and <span style='color:var(--mk-color-red)'>not inbetween</span>.
> 
> **Broken activation bar**
> - As long as the **function has not finished executing**, the <span style='color:var(--mk-color-red)'>rectangle cannot be broken</span>
## Denoting Loops

Loops within the sequence diagram are denoted with a rectangles and a labelled tagged `loop`.

**Example:**
![[Sequence Diagram Loop Example.png|center|250]]
**Key points to take note of:**
- Inside the [ ] is the <span style='color:var(--mk-color-yellow)'>condition</span> for the loop to continue
- The box the `loop` is in <span style='color:var(--mk-color-yellow)'>must be chipped</span> as shown
## Constructors & Object Creation

![[Sequence Diagram Constructors.png|center|300]]

When **creating a new object**, the arrow now **points** to the <span style='color:var(--mk-color-yellow)'>instance of the object</span>. Then to **denote the constructor**, a <span style='color:var(--mk-color-yellow)'>rectangle bar is placed directly below</span> the instance box.
## Deletion

![[Sequence Diagrams Deletion.png|center]]

When **deletion** of an object happens it will be denoted by an `x` in the diagram. 

One side note is that <span style='color:var(--mk-color-purple)'>Java</span> does not have a delete object function, since it uses its own **garbage collection system**. Thus the `x` just refers to when the object has been <span style='color:var(--mk-color-yellow)'>dereferenced</span>.
## Self Invocation

![[Sequence Diagram Self Invocation.png|center]]

When an object **calls a function in the same class, or some other class calls this function** then draw a rectangle box at the side which denotes that the 2 functions are executed simultaneously.

It can also be 
## Alternate Paths

![[Sequence Diagram Alternate Paths.png|center|300]]

Depending on the **condition**, the function will <b><mark style='background:var(--mk-color-yellow)'>call one of the functions but not 2 or more</mark></b>. It is ok for it to not call any function but we need to <b><mark style='background:var(--mk-color-yellow)'>determine the conditions</mark></b>.

Essentially, if it is a `if` `else` statement, use <span style='color:var(--mk-color-turquoise)'>alternate paths</span>.
## Optional Paths

![[Sequence Diagram Optional Paths.png|center ]]

**Similar to alternate paths**, optional paths just indicates if this <span style='color:var(--mk-color-yellow)'>function is called based on some condition</span>.
## Static Functions

![[Sequence Diagram Calling Static Methods.png|center|300]]

Since static methods **exists within the class itself**, we can initialise a class using `<<class>> class Name` and then point to that timeline to call a static method.
## Parallel Paths

![[Sequence Diagram Parallel Paths.png|center|300]]

A normal <span style='color:var(--mk-color-purple)'>java</span> program <span style='color:var(--mk-color-red)'>cannot do multiple things at once</span> thus, this appears if the <span style='color:var(--mk-color-yellow)'>program is multi-threaded</span>. But the diagram states that these <span style='color:var(--mk-color-yellow)'>2 functions are running in parallel</span>.
## Reference Frames

![[Sequence Diagrams Reference Frames.png|center|400]]

The 2 keywords `ref` and `sd` are **used along side** one another. This is used when a <span style='color:var(--mk-color-red)'>sequence can be complicated</span> and should be <span style='color:var(--mk-color-yellow)'>shown as a separate sequence diagram</span>.
# Architecture Diagram
---
It shows the <span style='color:var(--mk-color-yellow)'>overall organisation of the system</span> and can be **viewed as a very high-level design**. It consist of a set of interaction components that are <span style='color:var(--mk-color-yellow)'>required for functionality</span>.

**Characteristics of an architecture diagram:**
- **Simple** to understand
- **Technically Viable**
- **Agreed by everyone**

**Example architecture diagram for minesweeper:**
![[Architecture Diagram Example.png|center|250]]

There is **no universally adopted standard** thus they are <span style='color:var(--mk-color-yellow)'>free-form diagrams</span>.

For **big projects** it can be better to <span style='color:var(--mk-color-yellow)'>go deeper into the lower level designs </span>of some of the components.

**Going deeper into GUI:**
![[Architecture Diagram for GUI.png|center|600]]

This diagram does not show the design of the software but more of the <span style='color:var(--mk-color-yellow)'>architecture of the product</span>.

Try and use <span style='color:var(--mk-color-yellow)'>symbols that are commonly understood</span> (*Dumbs to denote database*), if not explain what the symbol means.

![[Architecture Diagram.png|center|400]]
# Use Case Diagram
---
A use case diagram is a <span style='color:var(--mk-color-yellow)'>visualisation</span> of all the use cases of a system.

**Example:**
![[Use Case Diagram Example.png|center|500]]

**Interpreting the diagram:**
- The bubbles are use cases and they should be <span style='color:var(--mk-color-yellow)'>easy to read</span>
- The stick figures outside of the box is called actors
- The box itself is the system.
- The keyword `<<extends>>` is for **extensions**
- The keyword `<<include>>` is for **inclusions**

The arrows on the left are called <span style='color:var(--mk-color-turquoise)'>actor generalization relationship</span>, which just means whatever the other actor can do they can do it as well.

> [!question] System as an Actor?
> You can **include the system itself** as an actor, to indicate something <span style='color:var(--mk-color-yellow)'>done by itself without external initialisation</span>.
> 
> However it is <span style='color:var(--mk-color-red)'>not recommended</span> as we should make the <span style='color:var(--mk-color-green)'>diagram as simple as possible</span>. Thus we should only involve external actors.
# Conceptual Class Diagrams
---
Also known as <span style='color:var(--mk-color-turquoise)'>OO domain models</span> (*OODM*), they are the lighter versions of a [[#Class Diagram|class diagram]]. It <span style='color:var(--mk-color-yellow)'>captures the class structures in the problem domain</span>.

> [!abstract] Domain Modeling
> The <span style='color:var(--mk-color-turquoise)'>problem domain</span> is the <span style='color:var(--mk-color-yellow)'>context to the problem</span> and <span style='color:var(--mk-color-turquoise)'>domain modeling</span> is to model how things work to understand the problem domain.
> 
> It can be <span style='color:var(--mk-color-orange)'>done</span> through:
> - **Domain specfic modeling notation** - A sector might have its own notation to follow
> - **General purpose modeling notation** - UML diagrams
> - **Other general prupose notation** - Organisation chart

<span style='color:var(--mk-color-orange)'>Unlike class diagrams</span>, CCD's should:
- <span style='color:var(--mk-color-red)'>Not contain solution-specific classes</span>, for instance `DatabaseConnection` though it is in the class diagram it is <span style='color:var(--mk-color-yellow)'>not related to the solution</span> or an <span style='color:var(--mk-color-yellow)'>entity in the problem domain</span>.
- <span style='color:var(--mk-color-green)'>Should represent the class structure</span> of the problem domain
- Be a <span style='color:var(--mk-color-yellow)'>subset of the class diagram</span> (*Omit methods and navigability*)

**Example of a CCD**
![[Conceptual Class Diagram Example.png|center|400]]

![[CCD With Variable Type.png|center|400]]
# Activity Diagrams
---
Or **AD** <span style='color:var(--mk-color-yellow)'>models workflows which represents the process</span> or a set of tasks to be executed based on the scenario (*Flowcharts*).

**AD example:**
![[Activity Diagram Example.png|center|200]]

> Take note that the boxes must have <b><mark style='background:var(--mk-color-yellow)'>curved edges</mark></b>.
## Alternate Paths

Using a **branch node** we can denote the start of an alternate path and a **merge node** to show the end of alternate paths.

Both these nodes are <span style='color:var(--mk-color-yellow)'>diamond shapes</span> and the <span style='color:var(--mk-color-yellow)'>guard conditions must be square brackets</span>. We can omit the `else` condition and **multiple arrows can start from the same corner**.

**Alternate path example:**
![[Activity Diagram Alternate Path.png|center|400]]

>Note that at any alternate path <b><mark style='background:var(--mk-color-yellow)'>only 1 guard condition must be true</mark></b>. But can have multiple arrows going out.
## Parallel Paths

Use a **fork and join nodes** indicate a start and end of a concurrent flow. Which is denoted by a <span style='color:var(--mk-color-yellow)'>shaded rectangle</span>.

In a parallel path, <span style='color:var(--mk-color-yellow)'>all actions are done concurrently</span> and <span style='color:var(--mk-color-yellow)'>all paths should complete</span> before the next action outside the flow.

**Parallel path example:**
![[Activity Diagram Parallel Path.png|center|400]]
## Rakes

It is to indicate that <span style='color:var(--mk-color-yellow)'>part of the activity is in another diagram</span>, it is usually indicated as <span style='color:var(--mk-color-yellow)'>pitch fork icon</span> beside the action.

![[Activity Diagram Rake.png|center|400]]

>In the other diagram make sure you <span style='color:var(--mk-color-yellow)'>label which activity</span> this belongs to
## Swim Lanes

We can also partition the activity diagram to <span style='color:var(--mk-color-yellow)'>denote who is doing what action</span>. These are also called <span style='color:var(--mk-color-turquoise)'>swim lane diagrams</span>.

![[Activity Diagram Swim Lane (Swim Lane Diagram).png|center|400]]
# Other UML Models
---
There are **other** UML models as well:
1) **Communication diagrams**
Like sequence diagrams, this diagram emphasizes the <span style='color:var(--mk-color-yellow)'>data links between various user in the interaction</span>.

2) **State machine diagrams**
it models the<span style='color:var(--mk-color-yellow)'> state-dependent behavior</span>, it models "if the model is in this state what does it do".

3) **Deployment diagrams**
it shows a **system's physical layout**, revealing which pieces of s<span style='color:var(--mk-color-yellow)'>oftware run on which pieces of hardware</span>.

4) **Component diagrams**
It is used to show how a <span style='color:var(--mk-color-yellow)'>system is divided into components</span> and <span style='color:var(--mk-color-yellow)'>how they are connected</span> to each other through interfaces.

5) **Package diagrams**
It shows <span style='color:var(--mk-color-yellow)'>packages and their dependencies</span>. A package is a grouping construct for grouping UML elements.

6) **Composite structure diagrams**
It <span style='color:var(--mk-color-yellow)'>decomposes</span> a class into its internal structure.

7) **Timing diagrams**
A timing diagram <span style='color:var(--mk-color-yellow)'>focuses on timing constraints</span>.

8) **Interaction overview diagrams**
It is a <span style='color:var(--mk-color-yellow)'>combination</span> of **activity diagrams** and **sequence diagrams**.
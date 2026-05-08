---
title: Functional Dependencies
Date Created: 2025-03-25
Last Updated: 2025-09-28
tags:
  - CS2102
  - Database
  - DatabaseDesign
---
# Idea of Functional Dependencies
---
There are many ways to evaluate weather a relational schema is good or not. But there are **things that should not be done** (*minimum requirements*).

A <b><span style='color:var(--mk-color-turquoise)'>normal form</span></b> is a **definition of a minimum requirement** and <b><span style='color:var(--mk-color-yellow)'>functional dependencies is the foundation</span></b> into normal forms.

> [!summary] Some of these minimum requirements are
> - Reduce data redundancy (*We store the same data more than once*) 
> - Improve data integrity
## Anomalies

There are <span style='color:var(--mk-color-orange)'>3 types of anomalies</span>:
1) **Update** anomalies
	>We <b><span style='color:var(--mk-color-yellow)'>update 1 record but we did not update the other rows</span></b>. This is a direct <b><span style='color:var(--mk-color-red)'>result from redundancies</span></b>
2) **Deletion** anomalies
	> We <b><span style='color:var(--mk-color-yellow)'>delete something but it cannot be deleted</span></b>. For instance if we want to delete a value but it is a primary key
3) **Insertion** anomalies
	> We <b><span style='color:var(--mk-color-yellow)'>insert something that is invalid</span></b>. For instance if we insert something but 1 value is null
## Normalization

<b><span style='color:var(--mk-color-turquoise)'>Normalization</span></b> is one way to <b><span style='color:var(--mk-color-yellow)'>prevent anomalies from happening</span></b>.

> [!info] Normalization
> It is the act of changing the table schema or more precisely <b><span style='color:var(--mk-color-yellow)'>decompose it into smaller tables</span></b>.

![[Normalization Example.png|center]]
# Functional Dependencies
---
When **2 values are dependent**, it means that <b><span style='color:var(--mk-color-yellow)'>there is some relationship</span></b> (*NRIC can identify a person*).

This is known as <b><span style='color:var(--mk-color-turquoise)'>functional dependencies</span></b> (*FD*) and we **denote** it as $X \rightarrow Y$ (*read as X determines Y*). This **depends on the requirements off the database**.

**Rule of thumb**, the <b><span style='color:var(--mk-color-yellow)'>LHS is the candidate keys</span></b> then the <b><span style='color:var(--mk-color-yellow)'>RHS is the other attributes</span> in the table</b>.

> [!abstract] Formal definition of functional dependencies
> Lets say we have some set of attributes $A$ and $B$. Both have values $A_{1} \dots A_{n}$ and $B_{1} \dots B_{m}$.
> 
> Then for any <b><span style='color:var(--mk-color-yellow)'>2 objects with the same set of attributes on A, they will have the same values on B</span></b>.
> 
> > [!example] Simple example
> > If $NRIC \rightarrow Name$ then for any 2 objects with the same NRIC, the name will always be the same.

For a functional dependency to be <b><span style='color:var(--mk-color-red)'>false</span></b>, just show that <b><span style='color:var(--mk-color-yellow)'>2 objects on the LHS does not map to the save object on the RHS</span></b>.

> [!important] An FD can hold on one table but does not hold on another

> [!question] How to find functional dependencies?
> 1) Try and <b><span style='color:var(--mk-color-red)'>violate the requirement</span></b> using 2 objects
> 2) The **columns that are the same value** in both objects are a set and is placed on the <b><span style='color:var(--mk-color-yellow)'>left hand side</span></b>
> 3) The **columns that are different in value** are a set and is placed on the <b><span style='color:var(--mk-color-yellow)'>right hand side</span></b>
## Canonical & Minimal Cover

Here we are just <b><span style='color:var(--mk-color-yellow)'>removing redundancies in functional dependencies</span></b>.

Given a set of functional dependencies to find the <b><span style='color:var(--mk-color-turquoise)'>minimal cover</span></b> by doing:
1) Simplify FDs who's RHS has more than 1 attribute
2) Simplify FDs who's LHS has more than 1 attribute
	- Find the attribute(s) which are redundant by using closure.
	- Remove the redundant ones
3) Afterwards remove redundant FDs from the reminding
	- If we remove lets say $\{A\} \rightarrow \{B\}$, the check if the remaining FDs the closure of A contains attribute B

> [!important] Finding redundancies
> Given that $AB \rightarrow C$.
> 
> To know if A or B is redundant find the closure of $\{A\}^{+}$ and $\{B\}^{+}$ if one of the **closure does contain** C, then the removed attribute is <b><span style='color:var(--mk-color-red)'>redundant</span></b>.

For the <b><span style='color:var(--mk-color-turquoise)'>canonical cover</span></b>, it is the **same** however we <b><span style='color:var(--mk-color-yellow)'>remove the restriction that the RHS can only have 1 attribute</span></b>. We find the minimal cover first, then we can combine FDs using the **rule of union or if the LHS is the same**.
## FD Reasoning

We want to **find other functional dependencies that are implied** from a given set of existing functional dependencies.
### Formal Proofs
#### Armstrong's Axioms

> [!summary] Axiom of reflexivity
> It says a <b><span style='color:var(--mk-color-yellow)'>set of attributes implies a subset of attributes</span></b>.
> 
> For instance $\text{StudentID}, \text{Name}, \text{Age} \rightarrow \text{Name}, \text{Age}$

> [!summary] Axiom of augmentation
> If we have $A \rightarrow B$ then we <b><span style='color:var(--mk-color-yellow)'>will always have</span></b> $AC \rightarrow BC$. This is regardless of what C is (*can be the same as A & B, where AA is just A*).
> 
> This is however <b><span style='color: var(--mk-color-red)'>not true for the inverse</span></b>.

> [!summary] Axiom of transitivity
> If $A \rightarrow B$ and $B \rightarrow C$ then **it is implied** that $A \rightarrow C$.
> 
> If $\text{NRIC} \rightarrow \text{Matric Number}$ and $\text{Matric Number} \rightarrow \text{Name}$, then $\text{NRIC} \rightarrow \text{Name}$.
#### Additional rules

##### Rule of Decomposition

Here if $A \rightarrow BC$, then $A \rightarrow B$ and $A \rightarrow C$.

> [!cite] Proof that decomposition is true
> 1) By **reflexivity**, we have $BC \rightarrow B$ and $BC \rightarrow C$
> 2) Then by **transitivity** we will have the following 2
> 	- $A \rightarrow BC$ and $BC \rightarrow B$, thus implies that $A \rightarrow B$
> 	- $A \rightarrow BC$ and $BC \rightarrow C$, thus implies that $A \rightarrow C$
##### Rule of Union

If $A \rightarrow B$ and $A \rightarrow C$ then $A \rightarrow BC$

> [!cite] Proof that union is true
> 1) By **augmentation**, we have $A \rightarrow B$ and $A \rightarrow AB$
> 2) By **augmentation**, we have $A \rightarrow C$ and $AB \rightarrow BC$
> 3) Then by **transitivity** we have $A \rightarrow AB$ and $AB \rightarrow BC$, thus implies that $A \rightarrow BC$
### Closure

It can be **difficult to prove using the axioms and rules**. We can <b><span style='color:var(--mk-color-yellow)'>draw a circuit</span></b> and trace the path of the circuit.

Let $S$ be a set of all attributes $\{A_{1}, \dots A_{n}\}$. <b><span style='color:var(--mk-color-turquoise)'>Closure</span></b>, is a <b><span style='color:var(--mk-color-yellow)'>set of attributes</span></b> (*$\Gamma$*) can can be decided by attributes in $S$ (*directly or indirectly*).

We **denote closure** as $\{A_{1} \dots A_{n}\}^{+}$. Thus to prove that $X \rightarrow Y$ just show that $\{X\}^{+}$ contains $Y$.

> [!note] If an attribute $A$ is in a closure for $\{X\}$, then $\{X\} \rightarrow \{A\}$ is a implicit FD. 
#### Computing Closures

Given $A_{1} \dots A_{n}$, to compute the closure of $\{A_{1} \dots A_{n}\}^{+}$ lets denote this as $\{C\}^{+}$ follow these steps:
1) First <b><span style='color:var(--mk-color-yellow)'>initialise the closure to have all the elements in the closure</span></b>
2) If there is a $A_{i}, A_{j}, \dots, A_{m} \rightarrow B$ such that $A_{i}, A_{j}, \dots, A_{m}$ are in the closure $\{C\}^{+}$ then add $B$ to the set
3) **Repeat step 2** <b><span style='color:var(--mk-color-red)'>until no new attribute can be added</span></b>

> [!example] Example of computing closure
> Assuming, $A \rightarrow B$, $C \rightarrow D$, $BC \rightarrow E$
> 
> The closure of $\{A, C\}^{+}$ will be <span style='color:var(--mk-color-orange)'>computed</span> as follows:
> 1) $\{A, C\}^{+} = \{A, C\}$ (*This is the first step*)
> 2) $\{A, C\}^{+} = \{A, B, C\}$, since $A \rightarrow B$
> 3) $\{A, C\}^{+} = \{A, B, C, D\}$, since $C \rightarrow D$
> 4) $\{A, C\}^{+} = \{A, B, C, D, E\}$, since $BC \rightarrow E$
> 5) No more to add thus we have found the solution
# Superkeys & Keys
---
<b><span style='color:var(--mk-color-turquoise)'>Superkeys</span></b> are a **set of attributes** in a table that <b><span style='color:var(--mk-color-yellow)'>decides all other attributes</span></b> (*Is the same as [[Creating and Populating Tables with Constraints#Primary Key|primary keys]]*).

<b><span style='color:var(--mk-color-turquoise)'>Keys</span></b> (*or candidate keys*) on the other hand **are superkeys** but they are <b>minimal</b> (*How many it does not matter*). Meaning if we **take an attribute out** it will <b><span style='color:var(--mk-color-red)'>not be a superkey</span></b> anymore.

> [!example] Example of keys
> Lets say we have $A \rightarrow BC$ and $BC \rightarrow A$
> 
> Then the **2 keys are A and BC**. BC has more attributes than A, but by definition BC is minimal.

Weather a table has <b><span style='color:var(--mk-color-red)'>redundancy</span></b> and <b><span style='color:var(--mk-color-red)'>anomalies</span></b> <b><span style='color:var(--mk-color-yellow)'>partially depends on the keys</span></b> of a table.

> [!info] If an attribute is in a key it is a prime attribute else it is non-prime
## Finding Keys

To <span style='color:var(--mk-color-orange)'>find the keys and superkeys of a table</span> we can do the following method:
1) For every possible subset (*All combinations of attributes*) derive the [[Functional Dependencies#Closure|closure]]
2) For each <b><span style='color:var(--mk-color-yellow)'>closure containing all attributes</span></b>, they are the **superkeys**
3) The **keys** on the other hand are the <b><span style='color:var(--mk-color-yellow)'>minimal set of the closures</span></b>

> [!important] There can be more that 1 key, thus do not stop at the first key

> [!example] Example of computing closure
> Assuming, $A \rightarrow B$, $B \rightarrow C$ and the table contains only attributes A, B & C.
> 
> Here are the following <span style='color:var(--mk-color-orange)'>closures for each possible subset</span> (*Step 1*):
> - $\{A\}^{+} = \{A, B, C\}$
> - $\{B\}^{+} = \{B, C\}$
> - $\{C\}^{+} = \{C\}$
> - $\{A, B\}^{+} = \{A, B, C\}$
> - $\{A, C\}^{+} = \{A, B, C\}$
> - $\{B, C\}^{+} = \{B, C\}$
> - $\{A, B, C\}^{+} = \{A, B, C\}$
>   
> Here our **superkeys** are $A$, $AB$, $AC$ & $ABC$, the **keys** will only be $A$.

Instead of randomly choosing a closure, just <b><span style='color:var(--mk-color-yellow)'>start with the smallest subset</span></b> and work your way up.

Here is another trick, assuming our table has attributes A, B, C, D. And $A \rightarrow B$, $AD \rightarrow C$ and $B \rightarrow D$. Notice that only **A is not on the right hand side** of any FD.

Thus <b><span style='color:var(--mk-color-yellow)'>A is not affected by any other attribute, thus A must be a attribute in the key</span></b>. Meaning we just need to **focus on the closures that have A**.

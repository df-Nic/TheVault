---
title: ER Diagrams
Date Created: 2025-02-03
Last Updated: 2025-09-28
tags:
  - CS2102
  - Database
  - DatabaseDesign
---
# Entity-Relationship Diagram
---
**Simple ER diagram**
![[ER Diagram.svg|center]]

> [!info] Entity & Entity Sets
> The **box** represents an <span style='color:var(--mk-color-turquoise)'>entity set</span> and a <span style='color:var(--mk-color-turquoise)'>entity</span> is a <span style='color:var(--mk-color-yellow)'>identifiable thing</span> (*Something that can be described with attributes*).

> [!info] Attributes
> The **circle** represents an <span style='color:var(--mk-color-turquoise)'>attribute</span>. **Each entity** should be <span style='color:var(--mk-color-yellow)'>uniquely identifiable by 1 or more attributes</span>. 

> [!note] Dotted line
> It is not an attribute but a **derived attribute** which can be <span style='color:var(--mk-color-yellow)'>obtained by a simple query</span>.
## Relationships

The **diamond** represents a <span style='color:var(--mk-color-turquoise)'>relationship set</span>. Is a <span style='color:var(--mk-color-yellow)'>association between 2 entity sets</span> (*or more which is a n-ary*).

A **relationship is distinguished** by the <span style='color:var(--mk-color-yellow)'>participating entities</span> and <span style='color:var(--mk-color-red)'>not the attributes associated with the relationship</span>.

A relationship can be between the **same entity set**. In this case a <span style='color:var(--mk-color-yellow)'>participation or role</span> is required to give context (*Put beside the line*).

There <span style='color:var(--mk-color-red)'>should not be any black dots</span> (*key attributes*) on the diamond.
## Aggregation

If we want to connect a relationship with another relationship set. We can **draw a box around the diamond**. <span style='color:var(--mk-color-yellow)'>Ensure that there is a gap</span> between the box and the diamond, to <span style='color:var(--mk-color-green)'>prevent ambiguity</span>.

> [!important] Convention
> In our ER diagrams, we will strictly only allow an <b><span style='color: var(--mk-color-yellow)'>entity set to only connect to a relationship set</span></b>, excluding attributes.

> [!warning] Different interpretation compared to n-ary
> Lets have an example where a person has a contract with a company and lawyer.
> 
> For a **n-ary relationship**, a person can have many contracts with a company as long as the lawyer is different.
> 
> As for **aggregation**, if we aggregate company and person, then a person only can have 1 contract with 1 company and with 1 lawyer.
# Identity & Cardinality
---
## Key Attributes

They are <span style='color:var(--mk-color-yellow)'>one or more attributes</span>, which can **identify an entity from the set**. This is something all entity sets have (*Basically a primary or composite primary key*).

They are denoted similarly as an attribute but the **circle is shaded black**. 

> [!note] Types of key attributes
> - **Single attribute** - <span style='color:var(--mk-color-yellow)'>One</span> attribute only
> - **Multiple attributes** - <span style='color:var(--mk-color-yellow)'>2 or more</span> attributes and is <span style='color:var(--mk-color-yellow)'>connected with a line</span> (*[[ER Diagrams#Entity-Relationship Diagram|Shown in the image above]]*)
> - **Several keys** - <span style='color:var(--mk-color-yellow)'>More than 1 way</span> to identify an entity also known as candidate key, if its a <span style='color:var(--mk-color-turquoise)'>candidate keys then it is a set</span> (*2 or more sets of key attribute(s)*)
>  - **Worse case** - <span style='color:var(--mk-color-yellow)'>All attributes</span> are used, this is at least what every entity set has

When choosing which set of attributes are key, try and have a <span style='color:var(--mk-color-green)'>collection of minimal set</span> of attributes.
## Partial Attributes

![[Partial Key Diagram.svg|center]]

Sometimes an entity set will <span style='color:var(--mk-color-yellow)'>require other attributes in another entity set in a relationship</span> to be able to uniquely identify entities. We call this entity a <span style='color:var(--mk-color-turquoise)'>weak</span> entity and the **entity in which it requires the attribute from** is called the <span style='color:var(--mk-color-turquoise)'>dominant</span> entity.
## Cardinality

It denotes **how many times** an entity can <span style='color:var(--mk-color-yellow)'>participate in a relationship</span>. It consists of a minimum and a maximum value (*min <= max*).

The cardinality follows the <span style='color:var(--mk-color-charcoal)'>"look-here convention"</span>, where it is <span style='color:var(--mk-color-yellow)'>associated with the nearest entity set</span> in the diagram.

> [!note] Cardinality Classification
> - **Mandatory** participation - $(1, n)$
> - **Optional** participation - $(0, n)$
> - **One to one** relationship - $(n, 1)$ for **both** entity sets
> - **One to many** relationship - $(n, 1)$ for 1 entity set and $(n, m)$ for the other entity set where $m \gt 1$
> - **Many to many** relationship - $(n, m)$ for **both** entity sets

> [!important] Default cardinality if not stated is $(0, n)$

> [!important] Cardinality for weak entities
> For **weak entities**, their cardinality <b><span style='color: var(--mk-color-yellow)'>must be (1, 1)</span></b>. If it is not then there <span style='color:var(--mk-color-red)'>cannot be a way to identity entities</span>.
> 
> > [!example] Example if it is not (1, 1)
> > Lets take the student and university example if it is (1, n), then a student can study at multiple universities and the set of key attributes will not be able to identify an entity in the relationship.
# ER Diagram Translation
---
We need to translate our **ER diagrams into SQL schemas**, to do this there are <span style='color:var(--mk-color-orange)'>3 rules and 3 exceptions</span>.

> [!note] Rule 1: Map attributes to meaningful domains

> [!note] Rule 2: A entity set is a table & candidate keys are mapped to primary keys or `UNIQUE NOT NULL`

> [!note] Rule 3: A relationship set consists of its own attributes & the key attributes of participating entities
> This just means that the <span style='color:var(--mk-color-yellow)'>key attributes is the primary key for the relationship</span> and at the same time <span style='color:var(--mk-color-yellow)'>it is a foreign key as well</span> (*Which will be a table*).
> 
> As for **aggregation**, the same set of rules apply for both relationship & entity.

> [!error] Exception 1: One to many
> In rule 3, we will set all key attributes as primary keys. Thus this <span style='color:var(--mk-color-yellow)'>will be a one to one relationship</span>. To do this we will <span style='color:var(--mk-color-yellow)'>need to remove attributes as primary key</span> (*depending on cardinality*) and just set them as `NOT NULL`.
> 
> > [!example] Example of exception 1
> > ![[ER Translation Exception 1 Example.png|center]]
> > 
> > ![[ER Translation Exception 1 Fix.png|center]]

> [!error] Exception 2: (1, 1)
> For (1,1) cardinality, it is possible that we **add a record into the entity set but not in the relationship set**. Thus to ensure this cardinality we can <span style='color:var(--mk-color-yellow)'>merge the entity set with the relationship set</span> (*Combine the 2 attributes*).
> 
>  > [!example] Example of exception 2
> > ![[ER Translation Exception 2 Example.png|center]]
> > 
> > ![[ER Translation Exception 2 Fix.png|center]]

> [!error] Exception 3: Weak entity / Partial key
> For any partial key, ensure that the **key attributes from the dominant and the weak entity** are <span style='color:var(--mk-color-yellow)'>primary keys</span>. And <span style='color:var(--mk-color-yellow)'>combine the relationship and the entity</span>.
> 
>  > [!example] Example of exception 3
> > ![[ER Translation Exception 3 Example.png|center]]
> > 
> > ![[ER Translation Exception 3 Fix.png|center]]

**Not all constraints in the ER diagram can be enforced** such as $(1, n)$. However we can try to <span style='color:var(--mk-color-orange)'>enforce it to the best of our abilities</span>:
- Ensure that **identities can uniquely identify** the entity set (*this is the first to enforce*)
- Ensure that **minimum cardinality** is satisfied
- Ensure that **maximum cardinality** is satisfied

> <span style='color:var(--mk-color-red)'>Not everything can be enforced</span> in the list above so enforce as much as possible.


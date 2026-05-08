---
title: Normal Forms
Date Created: 2025-04-07
Last Updated: 2025-09-28
tags:
  - CS2102
  - Database
  - DatabaseDesign
---
# Normal Forms
---
There are 6 levels of normal forms (*1NF - 6NF*), except the **forth one** which is called <b><span style='color:var(--mk-color-turquoise)'>Boyce-Codd NF</span></b> (*BCNF*).

The **lower levels** are <b><span style='color:var(--mk-color-green)'>easier to satisfy</span></b> but may have <b><span style='color:var(--mk-color-red)'>high redundancy</span></b>.

The **higher levels** have <b><span style='color:var(--mk-color-green)'>very little redundancy</span></b> but it might <b><span style='color:var(--mk-color-red)'>not always be possible to satisfy</span></b>.

The **3rd and 4th normal forms is good enough** as it <b><span style='color:var(--mk-color-yellow)'>gets rid of most redundancies and is always possible to satisfy</span></b>.
## Non-Trivial & Decomposed Functional Dependencies

> [!info] Decomposed functional dependencies
> It is when a FD whose <b><span style='color:var(--mk-color-yellow)'>right hand side has only one attribute</span></b>.
> 
>  Every non-decomposed FD can be converted into a decomposed equivalent.
> 
> > [!example] Decomposed functional dependencies examples
> > $A \rightarrow C$, $BC \rightarrow D$, $DEF \rightarrow E$

> [!info] Non-trivial functional dependencies
> It is when a FD whose <b><span style='color:var(--mk-color-yellow)'>right hand side does not appear in the left hand side</span></b>.
> 
> > [!example] Non-trivial functional dependencies examples
> > $A \rightarrow C$, $BC \rightarrow D$

To <span style='color:var(--mk-color-orange)'>summarise trivial FDs</span> given $X \rightarrow Y$:
1) **Trivial** means that $Y \subseteq X$
2) **Non-trivial** means that $Y \subsetneq X$
3) **Completely non-trivial** if $Y \neq \emptyset$ and $X \cap Y = \emptyset$
### Finding Non-Trivial & Decomposed FD

1) **Get all possible subsets** of all the attributes in a table
2) Compute the closure for each subset
3) For each closure **remove the trivial attributes**
4) Then **decompose** for each of the closure

> [!example] Example of finding non-trivial & decomposed FD
> Given $R(A, B, C)$, $A \rightarrow B$, $B \rightarrow A$ and $B \rightarrow C$
> 
> **Final all closures of all subsets**
> - $\{A\}^{+} = \{A, B, C\}$
> - $\{B\}^{+} = \{A, B, C\}$
> - $\{C\}^{+} = \{C\}$
> - $\{AB\}^{+} = \{A, B, C\}$
> - $\{AC\}^{+} = \{A, B, C\}$
> - $\{BC\}^{+} = \{A, B, C\}$
>   
> **Remove all trivial attributes** (*this is why we don't need to bother about $\{A, B, C\}^{+}$*)
> - $\{A\}^{+} = \{B, C\}$
> - $\{B\}^{+} = \{A, C\}$
> - $\{AB\}^{+} = \{C\}$
> - $\{AC\}^{+} = \{B\}$
> - $\{BC\}^{+} = \{A\}$
>   
> **Decompose FD**
> - $\{A\}^{+} = \{B, C\}$ will give us $A \rightarrow B$ & $A \rightarrow C$
> - $\{B\}^{+} = \{A, C\}$ will give us $B \rightarrow A$ & $B \rightarrow C$
> - $\{AB\}^{+} = \{C\}$ will give us $AB \rightarrow C$
> - $\{AC\}^{+} = \{B\}$ will give us $AC \rightarrow B$
> - $\{BC\}^{+} = \{A\}$ will give us $BC \rightarrow A$

# Boyce-Codd Normal Form (BCNF)
----
A table is in BCNF if <b><span style='color:var(--mk-color-yellow)'>every non-trivial and decomposed FD has a superkey on its left hand side</span></b>.

As long as **one of the FD does not hold** then it is <b><span style='color:var(--mk-color-red)'>not in BCNF</span></b>.

> [!question] Why is this the case?
> Assuming that $C_{1} \dots C_{n}$ is not a superkey and its closure contains $B$.
> 
> Then since it is not a superkey it can appear multiple times in the table and thus the same $B$ will appear. <b><span style='color:var(--mk-color-red)'>Leading to redundancies</span></b>, which is what BCNF prevents.

> [!success] Good properties of BCNF
> - **No update or deletion or insertion anomalies**
> - **Small redundancy**
> - **Original table can always be reconstructed** from the decomposed tables

> [!failure] Bad properties of BCNF
> - **Dependencies may not be preserved** after bring decomposed. We might need to join back the tables to check if an update is inappropriate or not.

We say a decomposition <b><span style='color:var(--mk-color-turquoise)'>preserves</span></b> all FDs if the **FDs of both** original table $T$ and the decomposed table $T'$ can be <b><span style='color:var(--mk-color-yellow)'>derived from one another</span></b>.

So all the FDs in table $T$ **can get all FDs** in $T'$ **and** FDs in $T'$ **can also get all FDs** $T$.

> [!example] Example of a preserving FDs 
> Lets say:
> - $T = \{A \rightarrow B, B \rightarrow C, A \rightarrow C\}$
> - $T' = \{A \rightarrow B, B \rightarrow C\}$, after decomposition
>
> Here we can clearly see that every FD in $T'$ is in $T$ and for $T$ using transitivity we can get $A \rightarrow C$ from $T'$.

> [!important] You can use closure to prove a closure for $\{X\}^{+}$ must be the same for both $T$ and $T'$

First **derive the FDs on the decomposed tables** based on the original FDs.
1) So <b><span style='color:var(--mk-color-yellow)'>compute the closure of all the subsets</span></b> in 1 decomposed table **using the original table's FD**
2) **Remove** attributes from the RHS that are <b><span style='color:var(--mk-color-yellow)'>not in the table</span></b> & remove <b><span style='color:var(--mk-color-yellow)'>trivial</span></b> attributes
3) The remaining values will be the FDs for the table (*you can further simplify it like in a [[3NF#Minimal Basis|minimal cover]]*)
4) Repeat the same for the other tables
 
Afterwards **merge the sets** and see if it will get back the same set of FDs as the original table. Might need to derive some of the FDs.
## BCNF Check

A <span style='color:var(--mk-color-orange)'>trivial way</span> is quite simple:
1) Find the **non-trivial and decomposed FD**
2) Check **each of the FDs and see if the left hand side is a superkey** (*which should be known from step 1*)

> [!info] If a table has only 2 attributes it is automatically in BCNF

A **faster way** will be to check if the closure satisfies the <b><span style='color:var(--mk-color-turquoise)'>more but not all</span></b> condition.

> [!info] More but not all
> A closure of a set of attributes can <b><span style='color:var(--mk-color-yellow)'>either only have itself or every single attribute</span></b>.
> > [!example] Example about more but not all
> > Lets say a table $T$ has 4 attributes, $T(A, B, C, D)$
> >
> > - $\{A\}^{+} = \{A, B, C, D\}$ <b><span style='color:var(--mk-color-green)'>satisfies</span></b> the more but not all condition
> > - $\{A\}^{+} = \{A, C, D\}$ <b><span style='color:var(--mk-color-red)'> does not satisfies</span></b> the more but not all condition.
> > - $\{A, B\}^{+} = \{A, B\}$ <b><span style='color:var(--mk-color-green)'>satisfies</span></b> the more but not all condition
> > - $\{A, B\}^{+} = \{A, B, C\}$ <b><span style='color:var(--mk-color-red)'>does not satisfies</span></b> the more but not all condition

As long as **one of the subset does not satisfy the more but not all condition**, then it is <b><span style='color:var(--mk-color-red)'>not in BCNF</span></b>.

> [!question] Why does the more but not all condition work
> Assume we have $\{A\}^{+} = \{A, C, D\}$ and $A$ is not a superkey.
> 
> When we remove trivial attributes and decompose the FD, then we will get $A \rightarrow C$ & $A \rightarrow D$.
> 
> Then it will <b><span style='color:var(--mk-color-red)'>violate that the left hand side must be a superkey</span></b>. Thus there is no need to do these extra steps.
# BCNF Decomposition
---
If a table is not in BCNF, can we **improve it**? A improvement strategy is to <b><span style='color:var(--mk-color-yellow)'>decompose the original table into smaller tables</span></b>, this is also known as <b><span style='color:var(--mk-color-turquoise)'>normalisation</span></b>.

![[Decomposition Algorithm Visualisation.png|center|500]]

**Algorithm to decompose a table**
1) Pick any **closure which violates the more but not all condition**, lets call this $\{X\}^{+}$
2) Then 1 table will contain the closure of $X$ or $\{X\}^{+}$
3) The other table will contain the attributes $X$ and all other attributes not in $\{X\}^{+}$
4) From the existing closures, just remove the attributes that are not present in the 2 fragmented tables
5) Check the 2 tables if they are in BCNF
	- If **the table is in BCNF**, then we can **stop**
	- Else we **repeat step 1 for the tables that are not in BCNF**

> [!important] We only stop when the all the smaller tables are in BCNF

The decomposition final result can be different depending on which closure you picked in step 1. But if they want the **minimal set** it means the <b><span style='color:var(--mk-color-yellow)'>smallest number of fragments needed</span></b>.

> [!warning] We might need to derive the functional dependencies after we spilt the table
> This is where the [[Functional Dependencies#FD Reasoning|functional dependency reasoning]] comes in.

At **each decomposition**, we <b><span style='color:var(--mk-color-yellow)'>remove at least one BCNF violation</span></b>. Because the spilt will cause the violation to be a superkey in the new table.

Thus the **number of recursive decompositions is at most the number of violations**.
## Lossless Join

Essentially when we decompose the table correctly we can <b><span style='color:var(--mk-color-yellow)'>reconstruct the table by joining the smaller tables</span></b> (*fragments*). This is join is known as a <b><span style='color:var(--mk-color-turquoise)'>lossless join</span></b>.

> [!important] Not all lossless joins is a BCNF but all BCNF is a lossless join

> [!question] Why does this hold?
> When we spilt the table, the attribute(s) $X$ will be in both tables.
> 
> And in **one of the tables** $X$ <b><span style='color:var(--mk-color-yellow)'>will be a superkey</span></b>.
### Check If the Decomposition is Lossless

To check if a decomposed table is lossless, <b><span style='color:var(--mk-color-yellow)'>check if the common attributes is a superkey</span></b> in one of the 2 decomposed tables:
1) Do the decomposition by first choosing one of the smaller tables
2) The other table will be the attributes in the remaining fragments/tables
3) Check for common attributes
	- If the common attributes is not a superkey restart and try another combination
	- If it is a common key decompose with another smaller table and repeat step 2
4) At the last 2 smaller tables check between the common attributes in both of them if it is a superkey or not

If the <b><span style='color: var(--mk-color-red)'>common attributes is not a superkey it does not mean it is not lossless</span></b>. You will need to check all possible combinations of decompositions before concluding.

> [!example] An example to check if its losses
> Assuming we have $R = (A, B, C, D, E)$ and we decompose into $R_{1}(A, B, C)$, $R_{2}(A, B, E)$ and $R_{3} (A, C, D)$
> 
> The FDs are $\{A, B\} \rightarrow  \{C\}$, $\{A, C\} \rightarrow  \{D\}$, $\{E\} \rightarrow  \{A, B, C, D\}$
> 
> Lets choose $R_{3}$ first so we decompose $R(A, B, C, D, E)$ into $R_{3}(A, C, D)$ and $R_{t}(A, B, C, E)$
> 
> Next we compute the closure of $\{A, C\}^{+}$ with the original FDs which we will get $\{A, C, D\}$ which is a superkey of $R_{3}$. Then we can move on.
> 
> Then since we have 2 remaining tables we can just take the last 2. Then we find the closure of $\{A, B\}^{+} = \{A, B, C, D\}$ which is a superkey for $R_{1}$ since $D$ is not part of $R_{1}$ we can remove it.
> 
> Thus the decomposition is lossless.
> 
> At any point it is not a superkey then we need to try another combination of decomposition.



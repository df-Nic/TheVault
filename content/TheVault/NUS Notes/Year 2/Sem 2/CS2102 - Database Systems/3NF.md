---
title: 3NF
Date Created: 2025-04-15
Last Updated: 2025-09-28
tags:
  - CS2102
  - Database
  - DatabaseDesign
---
# Third Normal Form (3NF)
---
Unlike [[Normal Forms#Boyce-Codd Normal Form (BCNF)|BCNF]] it is <b><span style='color:var(--mk-color-green)'>not as strict</span></b> however the <b><span style='color:var(--mk-color-red)'>redundancy is not as small as BCNF</span></b>.

It also <b><span style='color:var(--mk-color-green)'>guarantees lossless join property</span></b> but more importantly it <b><span style='color: var(--mk-color-green)'>can preserve all FDs</span></b> which BCNF does not guarantee.

A table <span style='color:var(--mk-color-orange)'>satisfies 3NF</span> **if and only if** every non-trivial and decomposed FD
1) Either the <b><span style='color:var(--mk-color-yellow)'>left hand side is a superkey</span></b>
2) **Or** the <b><span style='color:var(--mk-color-yellow)'>right hand side is a subset of the prime attributes</span></b>

> [!info] A prime attribute is an attribute that appears in any one of the keys

Since it is more lenient then:
- If the table satisfies BCNF it will satisfy 3NF
- If the tables does not satisfies 3NF it will not satisfy BCNF

> [!note] If we can find a BCNF that preserved all FDs when we will go for BCNF
## 3NF Check

To <span style='color:var(--mk-color-orange)'>check if a table is in 3NF</span>:
1) **Drive all the keys** in the table $T$
2) For each of the given FDs, check if
	- The left hand side is a superkey
	- Or, **every** attribute on the right hand side is a prime attribute
3) If all the FDs satisfies the condition then $T$ is in 3NF

> [!example] Example of checking if a table is in 3NF
> Lets say we have $R(A, B, C, D)$ with FDs of $B \rightarrow C$ and $B \rightarrow D$
> 
> **Step 1 derive all the keys**
> Just compute all the closures for all subset of attributes in the table. Simplifying the example they keys are $\{A, B\}$.
> 
> **Step 2 check every FD**
> Firstly $\{B\}^{+} = \{B, C, D\}$ thus the LHS for all FDs are not a superkey.
> 
> And looking at the RHS both of the attributes are not a prime attribute. Thus the table $R$ is not in 3NF
# 3NF Decomposition
---
Unlike [[Normal Forms#BCNF Decomposition|BCNF decomposition]] where we spilt the table recursively in 3NF we only do <b><span style='color:var(--mk-color-yellow)'>1 spilt into many tables</span></b>. 

Steps to <span style='color:var(--mk-color-orange)'>carry out a 3NF decomposition</span>:
1) Drive a <b><span style='color:var(--mk-color-turquoise)'>minimal basis</span></b> (*simplified set of FDs*) of the set of FDs called $S$
2) In the minimal basis **combine the FDs whose left hand sides are the same**
3) **Each of the remaining FDs will be 1 table**
4) If <b><span style='color:var(--mk-color-red)'>none</span></b> of the newly created tables **contains a key of the original table** (*subset*), then create a table that contains a key in the original table (*any key will do*). This is to <b><span style='color:var(--mk-color-yellow)'>ensure lossless join decomposition</span></b>
5) **Remove any subsumed tables** (*tables that are a subset of another table*)
## Minimal Basis

It is also known as a <b><span style='color:var(--mk-color-turquoise)'>minimal cover</span></b>.

 Lets define a set of FDs to be $S$ and the minimal cover to be $S'$ to determine if it is simplified there are <span style='color:var(--mk-color-orange)'>4 conditions</span>:
1) Every FD in $S'$ can be derived from $S$ and vice versa, essentially it should be <b><span style='color:var(--mk-color-yellow)'>preserved</span></b>
2) Every FD in the minimal basis is a [[Normal Forms#Non-Trivial & Decomposed Functional Dependencies|non-trivial and decomposed FD]]
3) No FD in the minimal basis is redundant, <b><span style='color:var(--mk-color-yellow)'>no redundancy for FD</span></b>
4) For each FD in the minimal basis $S'$, <b><span style='color:var(--mk-color-yellow)'>none of the attributes on the left hand side</span></b> is [[Functional Dependencies#Canonical & Minimal Cover|redundant]]

> [!failure] Condition 1 violation
> Given that $S = \{A \rightarrow B, B \rightarrow C, A \rightarrow C\}$ and we have $S' = \{A \rightarrow B, AB \rightarrow C\}$.
> 
> If we look at $S'$ we can see that we <b><span style='color:var(--mk-color-red)'>cannot derive</span></b> $B \rightarrow C$ in $S$.
> 
> $\{B\}^{+}$ in $S$ is $\{B, C\}$ but $\{B\}^{+}$ in $S'$ is $\{B\}$.

> [!failure] Condition 2 violation
> Given that $S = \{A \rightarrow B, B \rightarrow C, A \rightarrow C\}$ and we have $S' = \{A \rightarrow BC, B \rightarrow C\}$.
> 
> If we look at $S'$, $A \rightarrow BC$ is <b><span style='color:var(--mk-color-red)'>not decomposed</span></b>.

> [!failure] Condition 3 violation
> Given that $S = \{A \rightarrow B, B \rightarrow C, A \rightarrow C\}$ and we have $S' = \{A \rightarrow B, B \rightarrow C, A \rightarrow C\}$.
> 
> In $S'$ by <b><span style='color:var(--mk-color-red)'>transitivity we can infer</span></b> $A \rightarrow C$.

> [!failure] Condition 4 violation
> Given that $S = \{A \rightarrow B, A \rightarrow C, C \rightarrow B\}$ and we have $S' = \{A \rightarrow B, AB \rightarrow C, C \rightarrow B\}$.
> 
> For $AB \rightarrow C$ the attribute <b><span style='color:var(--mk-color-red)'>B is redundant</span></b>.
### Finding the Minimal Basis

As mentioned before when [[Functional Dependencies#Canonical & Minimal Cover|finding covers]]:
1) Transform the FDs so that each **right hand side can only contain 1 attribute**
2) **Remove redundant attributes on the left hand side** of each FD
3) **Remove redundant FDs** (*you can raw a graph to help find derived FDs to see who determines what*)

 If you cannot tell if the FD is redundant, if $X \rightarrow Y$ if we remove this FD, then will $\{X\}^{+}$ still contain $Y$ with the remaining FDs:
- If **yes** then the FD is <b><span style='color:var(--mk-color-red)'>redundant</span></b>
- If **no** then it is <b><span style='color:var(--mk-color-green)'>not redundant</span></b>
 
If you **removed the FD**, in the <b><span style='color:var(--mk-color-yellow)'>subsequent checks do not include it</span></b>.

> [!warning] The order of operation matters we cannot do step 3 before step 2

> [!example] Finding a minimal basis
> Lets say we have $S = \{A \rightarrow BD, AB \rightarrow C, C \rightarrow D, BC \rightarrow D\}$
> 
> **Step 1**:
> We can decompose $A \rightarrow BD$ to $A \rightarrow B$ and $A \rightarrow D$.
> 
> Thus we will get $S = \{A \rightarrow B, A \rightarrow D, AB \rightarrow C, C \rightarrow D, BC \rightarrow D\}$.
> 
> **Step 2**:
> We know there is $A \rightarrow B$ this $AB \rightarrow C$ the attribute B is redundant thus $A \rightarrow C$
> 
> For harder ones like $BC \rightarrow D$ we can use closure.
> - If we remove $C$ just check if $\{B\}^{+}$ contains D, which is not the case so C is **not redundant**
> - If we remove $B$ check if $\{C\}^{+}$ contains D, in this case B is **redundant**
>   
> Thus we will get $C \rightarrow D$ and we will end up with, $S = \{A \rightarrow B, A \rightarrow D, A \rightarrow C, C \rightarrow D\}$.
> 
> **Step 3**:
> By transitivity we have $A \rightarrow C$ and $C \rightarrow D$ so $A \rightarrow D$ is redundant because it can be inferred.
> 
> So our minimal basis / cover will be, $S = \{A \rightarrow B, A \rightarrow C, C \rightarrow D\}$.
## Rest of the Steps

Assuming after we found the minimal cover we got $\{BC \rightarrow D, A \rightarrow E, D \rightarrow A, E \rightarrow B\}$.

Following **step 2** no FDs can be combined.

Going to **step 3** create a table for each of the FDs:
1) $T_{1}(B, C, D)$
2) $T_{2}(A, E)$
3) $T_{3}(A, D)$
4) $T_{4}(B, E)$

Going to **step 4**, assuming the key for the original table is $(A, C)$. Then we can see none of the table has this 2 pairs of attributes, so we need to make 1 new table with just A and C
1) $T_{1}(B, C, D)$
2) $T_{2}(A, E)$
3) $T_{3}(A, D)$
4) $T_{4}(B, E)$
5) $T_{5}(A, C)$

Going to **step 5** there are no table which is a subset of another table so there is nothing to be remove

> [!example] If there are subsumed tables
> If we some how have $T_{1}(A, B, D)$ and $T_{2}(A, D)$ then we will remove $T_{2}$.

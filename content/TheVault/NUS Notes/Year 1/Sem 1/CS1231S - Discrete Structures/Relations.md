---
Title: Relations
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - Math/Logic
---
# Definitions
---

**Relations**
> It is a <span style='color:#f7b731'>binary relation from A to B</span> which is also a subset of A x B

If (x, y) appears in the relation set ($R$), it means that<span style='color:#f7b731'> x is related to y by R or x is R-related to y</span>

Symbolically: 
- $x R y$ means (x, y) $\in R$
- $x\not R y$ means (x, y) $\notin R$

**Domain**
> Or $Dom(R)$ is the set of all elements in set A such that $aRb$ for some element in B

It is a set that contains <span style='color:#f7b731'>all the values of A which have a relationship with any element in set B</span>

$Domain \subseteq A$

**Co-domain**
> Or $coDom(R)$ is the set of B

$\text{Co-Domain} = B$

**Range**
> Or $Range(R)$ is the set of all elements in set B such that $aRb$ for some element in A

It is a set that contains <span style='color:#f7b731'>all the values of B which have a relationship with any element in set A</span>

$Range \subseteq \text{Co-domain}$

If a statement says, something <span style='color:#f7b731'>related by R to 1</span>, means $xR1$

**Inverse Relation**
> $R^{-1}$ is the <span style='color:#f7b731'>relation from B to A</span> where $R$ is the relation from A to B

It interchanges all the ordered pairs in the <span style='color:#0fb9b1'>relation set</span> from a (x, y) to (y, x)

Symbolically : 
- $R^{-1} = \{(y,x) \in B \times A : (x,y) \in R\}$
- $\forall x \in A, \forall \in B ((y, x) \in R^{-1} \iff (x, y) \in R)$

**Relation on a Set**
> It is a relation of the same set, basically from A to A

This can be written as $A^{2}$ or $A^n$ 

**N-ary Relations**
> A n-ary relation R is based on the number of sets
# Composition of Relations
---

It is the <span style='color:#f7b731'>combination of 2 relations</span>

Let A, B and C be sets. Let $R \subseteq A \times B$ and $S \subseteq B \times C$, then the <span style='color:#0fb9b1'>composite</span> of R with S is denoted as $S \circ R$;

$\forall x \in A, \forall z \in C (x S\circ R z \iff (\exists y \in B (xRy \land ySz)))$

Basically, x and z are related iff there is a path from x to z via some intermediate element y.
## Characteristics of Composite Relations

**Associative**
$T \circ S \circ R = T \circ (S \circ R) = (T \circ S) \circ R$

**Inverse**
$(S \circ R)^{-1} = R^{-1} \circ S^{-1}$

# Properties of Relations

Let R be a relation on set A ($aRa$)

1) **Reflexive**
	Every element in a, it is related to itself

R is <span style='color:#0fb9b1'>reflexive</span> $\iff \forall x \in A (xRx)$

2) **Symmetric**
	Any 2 elements in set A, if element 1 is related to element 2, then element 2 is also related to element 1.

R is <span style='color:#0fb9b1'>symmetric</span> $\iff \forall x,y \in A (xRy \rightarrow yRx)$

3) **Transitive**
	Any 3 elements, if element 1 is related to element 2, and element 2 is related to element 3, then element 1 is related to element 3

R is <span style='color:#0fb9b1'>transitive</span> $\iff \forall x,y,z \in A (xRy \land yRz \rightarrow xRz)$

**If R is not reflexive it is not transitive as well,**
	Given R = {{1,2}, {2,1}} by transitivity we should expect {1,1} but it does not appear and thus it is not reflexive and transitive.

This <mark class="hltr-orange">cannot be used for elements in the set</mark>.

## Transitive Closure

Let A be some set and R is a relation to set A. <span style='color:#f7b731'>R might not be</span> <span style='color:#0fb9b1'>transitive</span>, therefore the <span style='color:#0fb9b1'>transitive closure</span> of R is the relation $R^{t}$ on A such that is satisfy the following;
1) $R^{t}$ is transitive
2) $R \subseteq R^{t}$
3) If S is any other transitive relation that contains R then $R^{t} \subseteq S$

The above is saying that with a relation, if it is <span style='color:#f7b731'>not transitive, it can be turned into a transitive relation</span>. Thus $R^{t}$ will have additional elements (more arrows) ranging from 0 to n, in order to make it transitive thus R will be a subset of it.

Point 3 is called a <span style='color:#0fb9b1'>minimality clause</span>, which means if <span style='color:#f7b731'>R is a subset of some other set S which is also transitive</span>, thus $R^{t}$ is also the smallest subset of S.

This is the same for, <span style='color:#0fb9b1'>symmetric closure</span> and <span style='color:#0fb9b1'>reflexive closure</span>
## Partitions as Relations

**Relation Induced by a Partition**
> Given a partition (C) of set A, the relation R induced by the partition is defined as;

$\forall x,y \in A, xRy \iff \exists \text{ a component S of C s.t.} \ x,y \in S$

The sets must be <span style='color:#f7b731'>non empty </span>and the union will be the Set A.

A <span style='color:#0fb9b1'>component</span> is the elements in the partition.

Therefore, a partition will have the 3 properties, <span style='color:#0fb9b1'>reflexive</span>, <span style='color:#0fb9b1'>symmetric</span> and <span style='color:#0fb9b1'>transitive</span>, this type of partition is called a <span style='color:#f7b731'>equivalent relation</span>. (**Theorem 8.3.1**)
### Definition of Equivalence Relation

Let A be a set and R a relation on A. R is an equivalence relation if and only if <mark class="hltr-orange">R is reflexive, symmetric and transitive</mark>.

The ~ symbol is used to denote an equivalence relation

## Equivalence Class

A <span style='color:#0fb9b1'>class</span> is a component in a set. It is the<span style='color:#f7b731'> same as</span> a component of <span style='color:#f7b731'>a partition of a set</span>.

Suppose A is a set and ~ is an <span style='color:#0fb9b1'>equivalence relation</span> on A. For each $a \in A$, the equivalence class of a, denoted $[a]$ and called the <span style='color:#f7b731'>class of a</span> for short, is the set of all elements $x \in A$ such that a is ~-related to x ($a\sim x$ another way to write it).

A equivalence class is a subset of A

The equivalence class is denoted as $[a]_{\sim}$
It is symbolically represented as $\forall x \in A (x \in [a]_{\sim}\iff a \sim x)$

The ~ is to be replaced with the equivalence relation letter ($[a]_R$)

Every element in the same class (a) is all related to class a.

Example
Given a class $[0]$ = {0, 4} and another class $[4]$ = {0, 4} they refer to the same set and therefore they are the equivalence class. This means that 0 and 4 are related to one another.

Things to note in <span style='color:#8854d0'>Lemma Rel.1 Equivalence Classes</span>
Let ~ be an equivalence relation on the set A. Then the following are equivalent for all $x, y \in A$
1) $x \sim y$ (Basically xRy where R = the equivalence relation)
2) $[x] = [y]$
3) $[x] \cap [y] = \emptyset$ 
## Congruence

Let $a, b \in \Bbb Z$ and $n \in \Bbb Z^{+}$ Then a is a congruent to b modulo n if and only iff a - b = nk for some $k \in \Bbb Z$, basically n | (a - b), which is $a \equiv b (mod \ n)$.

A congruent mod is <span style='color:#f7b731'>reflexive, symmetric and transitivity</span>.

### Set of Equivalence Classes

Let A be a set and ~ be an equivalence relation on A. Denote by A/~ the set of all equivalence classes with respect to ~, $A / \sim = \{[x]_{\sim} : x \in A\}$

Things to note in <span style='color:#8854d0'>Lemma Rel.2 Equivalence Classes form a partition</span>

Let ~ be an equivalence relation on a set A. Then A/~ is a partition of A.

# Partial Order
---
**Antisymmetric**
> For all values in the set if <span style='color:#f7b731'>x is related to y and y is related to x then x = y</span>. It cannot be x related to y and y related to x

It is symbolically represented as $\forall x,y \in A (xRy \land yRx \rightarrow x = y)$

<span style='color:#0fb9b1'>Antisymmetric</span> <mark class="hltr-orange">is not not symmetric</mark>.

**Asymmetric**
> If x is related to y then y cannot be related to x

It is symbolically represented as $\forall x,y \in A (xRy \rightarrow y \not R x)$

**Partial Order Relation**
> R is a partial order relation if any only if R is <span style='color:#f7b731'>reflexive and antisymmetric and transitive</span>. 

There are two fundamental partial order relations
1) Less than or equal to ( $\preceq$)
2) Subset

**Partially Ordered Set**
>If a set A <span style='color:#f7b731'>has been defined as a partial order relation</span>, then the set A is a partially ordered set also called <span style='color:#0fb9b1'>poset</span>

This is denoted by (A, R)

Partial order can be viewed as a set of tasks
-  x $\preceq$ y is and only if task x must be done before or at the same time as task y
-  Not all elements are comparable, meaning it can be neither x $\preceq$ y nor y $\preceq$ x
-  Therefore it is called partial as there may not be an order between certain elements.

**Strict Partial Order**
> It is Irreflexive (No self loops), antisymmetric and transitive

**Comparable**
> For any element x, y if and only if x $\preceq$ y or y $\preceq$ x

**Compatible**
> There exist a z in the set where x $\preceq$ z and y $\preceq$ z
## Hasse Diagrams

Let $\preceq$ be the partial order on a Set A. The Hassee Diagram of $\preceq$ will be for all distinct $x,y,m \in A$:
	If x $\preceq$ y  and no $m \in A$ is such that x $\preceq$ m $\preceq$ y , then x is placed below y with a line joining them else there is no line.

It is a <span style='color:#0fb9b1'>topological graph</span> of all the nodes in a directed graph. Where if there a line from A to B to C, then there is no line from A to C

To obtain a <span style='color:#0fb9b1'>Hasse Diagram</span>;
1) Start with a directed graph and place all vertices such that all arrows point upwards
2) Remove all loops
3) Remove all arrows implied by the transitive property
4) The direction of the lines

The position of the nodes matter, the <span style='color:#f7b731'>later the order the higher it will be</span> (Starting node will be at the bottom)

**Maximal Element**
> For all elements x in A, either x $\preceq$ c, or x and c are not comparable

Assuming c is the maximal element
Symbolically: $\forall x \in A (c \preceq x \rightarrow c = x)$ 

**Minimal Element**
> For all elements x in A either $c \preceq x$ or c and x are not comparable

Assuming c is the minmal element
Symbolically: $\forall x \in A (x \preceq c \rightarrow c = x)$ 

**Largest Element**
> There can only be one largest element, ie only one maximal element

Symbolically: $\forall x \in A (x \preceq c)$ 

**Smallest Element**
> There can only be one smallest element, ie only one minimal element

Symbolically: $\forall x \in A (c \preceq x)$

If there is a standalone node with no connections, <mark class="hltr-orange">it is both a maximal and minimal element</mark>
## Linearization

Supposed there is partial order relation on Set A and that $x \preceq y$ means <span style='color:#f7b731'>x must be carried out first or at the same time if it equal</span>.

<span style='color:#0fb9b1'>Linearization</span> is a sequence of tasks that lines up all the tasks in order such that <span style='color:#f7b731'>no 2 tasks can be done simultaneously</span>.
### Total Order

It is related to <span style='color:#0fb9b1'>linearization</span>, where when <span style='color:#f7b731'>all the elements are comparable</span> (Is just a straight line in the Hasse diagram) it is called a <span style='color:#0fb9b1'>total order </span>or <span style='color:#0fb9b1'>linear order</span>.

If R is a partial order relation on a set A, and for any two elements x and y in A, either x R y or y R x, then R is a total order relation (or simply total order) on A.

Symbolically: $\forall x,y \in A (xRy \lor yRx) \text{and R is a partial order}$

Let $\preceq$ be a partial order on a set A and A linearization of $\preceq a$ the total order of $\preceq^*$ on A is as such
	$\forall x,y \in A (x \preceq y \rightarrow x \preceq^{*}y)$

### Well-Ordered Set

Let $\preceq$ be a total order on a set A, then A is <span style='color:#0fb9b1'>well-ordered</span> if and only <span style='color:#f7b731'>if every non-empty subset of A contains a smallest element</span>.

Symbolically: $\forall S \in P(A), s \neq \emptyset \rightarrow (\exists x \in S \forall y \in S (s \preceq y))$

Examples:
$(\Bbb N,\le)$ is well ordered
$(\Bbb Z, \le)$ is not well ordered
	Let the subset be {.....,0, 1, 2, 3}, there is no smallest element
$(\Bbb N^{+}, \ge)$ is not well ordered
	Let the subset be {10, 11, 12, .....} there is no element a where a is the largest which is considered the smallest element in this relation

---
Title: Set Theory
Date Created: 28-November-2025
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - Math/Sets
---
# Definitions
---
**Sets**
> <mark class="hltr-orange">Unordered</mark> collection of objects (members / elements)

Sets can be written as a <span style='color:#0fb9b1'>set-roster notation</span>;
- {1,2,3,4,5}
- {1,2,3,4,5,...,100}

In a <span style='color:#0fb9b1'>set</span>, the <span style='color:#f7b731'>order and duplicates do not matter</span>
	{1,2,3} = {2,2,3,3,1,3}

There is a thing called <span style='color:#0fb9b1'>multiset</span> which are the same as sets <span style='color:#f7b731'>but it allows duplicates</span>.

**Set Builder Notation**
> Let U be a set and $P(x)$ be the predicate over U, then <span style='color:#f7b731'>for all elements in U such that P(x) is true</span>.

A <span style='color:#0fb9b1'>set builder notation</span> is used like such, ${x \in U | P(x)}$

**Replacement Notation**
>  Let U be a set and $P(x)$ be the predicate over U, then <span style='color:#f7b731'>the set of all objects of the form P(x) where x ranges over the elements of A</span>.

A <span style='color:#0fb9b1'>replacement notation</span> is used like such, ${P(x) | x \in U}$

**Membership** ($\in$)
> A value which is a <span style='color:#f7b731'>element in the set</span>

Examples:
$\{ 2 \} \in \{1,2,3\}$
$\{ \{ 2 \} \} \in \{1,\{ 2 \},3\}$

**Cardinality** ($|S|$)
> The <span style='color:#f7b731'>size</span> of the set

Examples
$s = \{1,2,3\}$, $|s| = 3$
$s = \{1,\{ 2,3 \} \}$, $|s| = 2$

**Subset and Superset**

A is a <span style='color:#0fb9b1'>subset</span> of B which is written as $A \subseteq B$, if and only if <span style='color:#f7b731'>every element in A is also an element in B</span>.

A <span style='color:#0fb9b1'>superset</span> can be written as $B \supset A$ which means that <span style='color:#f7b731'>B is a superset of A</span>.

**Proper Subset**
> A is a proper subset of B if and only if <span style='color:#f7b731'>A is a subset of B but </span>A $\neq$ B.

It is denoted as $A \subsetneq B$

For A to be a <span style='color:#0fb9b1'>proper subset</span>, A must contain at <span style='color:#f7b731'>least 1 less item from set B</span>.

**Set Equality**
> If 2 sets A and B are equal then, every <span style='color:#f7b731'>element in A is a element in B and vice versa</span>.

Symbolically: $A = B \iff A \subseteq B \land B \subseteq A$ OR $A = B \iff \forall x (x \in A \iff x \in B)$

**Disjoint**
> Two sets are disjoint if and only if there is no element in common

Symbolically: $A \cap B = \emptyset$

Given <span style='color:#f7b731'>N number of sets</span>, <span style='color:#f7b731'>pick any 2</span> and if they are <span style='color:#0fb9b1'>disjoint</span> they are <span style='color:#f7b731'>called mutually disjoint or nonoverlapping</span> if all the sets are disjoint.

**Empty Set**
>  A <span style='color:#f7b731'>set with no element</span>, {} is called a empty set

It is denoted as $\emptyset$ and it is a <span style='color:#f7b731'>subset of every set</span>. A empty set is not a null set

An set with 1 item is called a <span style='color:#0fb9b1'>singleton</span>.

**Ordered Pairs**
> It is an expression in a form of $(x, y)$ and the <span style='color:#f7b731'>order matters</span>.

$(a, b) = (c, d)$ if and only if $a = c \land b = d$

**Cartesian Product**
> The cartesian product of 2 sets A and B is the <span style='color:#f7b731'>set of all</span> <span style='color:#0fb9b1'>ordered pairs</span> (a, b) where a is in A and b is in B

Symbolically: $A x B$ = $\{(a,b) : a \in A \land b \in B\}$  

$A * B * C$ is a cartesian product of <span style='color:#f7b731'>ordered 3 tuples</span>.
$(A * B) * C$ is a cartesian products of <span style='color:#f7b731'>ordered 2 tuples where it will be</span> $((a,b), c)$ 

A <span style='color:#0fb9b1'>cartesian plane</span> is often used to refer to a plane for $\Bbb R * \Bbb R$

The length of $A \times B$ is $\vert A \vert * \vert B \vert$
# Universal Sets
---
A universal set is a set that <span style='color:#f7b731'>captures every possible value of x</span>.

**Union**
> A <span style='color:#0fb9b1'>union</span> of 2 sets denoted as $A \cup B$ is a <span style='color:#f7b731'>set of all elements that are in at least one of A or B</span>.

Union of multiple sets is written as $\bigcup^{n}_{i=0} A_{i}$. 

**Intersection**
>A <span style='color:#0fb9b1'>intersection</span> of 2 sets denoted as $A \cap B$ is a <span style='color:#f7b731'>set of all elements that are common of both A and B</span>.

Union of multiple sets is written as $\bigcap^{n}_{i=0} A_{i}$. 

**Difference / Relative Compliment**
> The <span style='color:#0fb9b1'>difference</span> between 2 sets is denoted by $B - A$ or $B \ \backslash A$, is the <span style='color:#f7b731'>set of all elements that are in B but no in A</span>.

**Compliment**
> Denoted by $\bar A$ or $A^c$ is the set of <span style='color:#f7b731'>all elements in U (Universal Set) that are not in A</span>.

**Exclusive Or** $\oplus$
> A $\oplus$ B, will return <span style='color:#f7b731'>a set with all elements in A and B but not in both</span>. In other terms, it is true if only one of the operands is true.
# Partitions of Sets
---
Supposed a set A is comprised of different subsets ${A_{1}, A_{2}, A_{3} \dots A_{n}}$. Ans supposed that their boundaries are assigned such that these sets are <span style='color:#0fb9b1'>mutually disjoint</span>.

Therefore, A is called a <span style='color:#f7b731'>union of mutually disjoint subsets</span> and the collection of sets is said to be a <span style='color:#0fb9b1'>partition</span> of A.

$\forall x \in A \ \exists! S \in  C (x \in S)$
## Quotient Remainder Theorem

Given any integer n and a positive integer d, there exists a unique integer q and r such that, n = dq + r and $0 \le r \lt d$.

For example:
n = 54 and d = 4
$54 = 4 * 13 + 2$; hence q = 13 and r = 2

## Power Sets

A <span style='color:#0fb9b1'>power set</span> denoted by $P(A)$ is the <span style='color:#f7b731'>set of all possible subsets of A</span>.

Example:
$A = \{x,y\}$ 
$P(A) = \{\emptyset, \{x\}, \{y\}, \{x,y\}\}$

The <span style='color:#0fb9b1'>cardinality</span> of a power set is $2^n$ where n is the number of elements in set A.

Another way is to use [[Counting & Probability#Combinations|combination]] to calculate ${n \choose 0} + {n \choose 1} + {n \choose 2} + \dots + {n \choose n} = 2^{n}$
# Ordered n-tuples and Cartesian Products
---

**Ordered n-tuple**
> It is the same concept as a ordered pair but the <span style='color:#f7b731'>number of elements is determine by n</span>.

**Cartesian Product**
> A cartesian product of n number of sets is a<span style='color:#f7b731'> set of all ordered n-tuples</span>.


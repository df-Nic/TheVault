---
Title: Speaking Mathematically
Date Created: 2023-08-19
Last Updated: 23-January-2026
Tags:
  - CS1231S
  - Math/Logic
---
# Variables
---

They are your algebraic statements where unknowns are given a specific letter.
## Sets

$\Bbb R$ -> The set of all <span style='color:#f7b731'>real numbers</span>.
$\Bbb Z$ -> The set of all <span style='color:#f7b731'>Integers</span>.
	This **includes** negative numbers
$\Bbb Q$ -> The set of all <span style='color:#f7b731'>Rational Numbers</span>.
$\Bbb N$ -> The set of all <span style='color:#f7b731'>Natural Numbers</span>.
	This **includes** 0 but **not** negative numbers
$\Bbb C$ -> The set of all <span style='color:#f7b731'>Complex Numbers</span>.

<b>0 is neither positive or negative</b>
### Superscripts and Subscripts

A <span style='color:#0fb9b1'>Superscript</span> or <span style='color:#0fb9b1'>Subscript</span> <span style='color:#f7b731'>denotes the range</span> in a set.

Examples:
$Z^+$ , just denotes the set of all positive integers
$R^-$ , just denotes the set of all negative real numbers
$Z_{\le 12}$, , just denotes the set of all integers greater than or equal to 12

$\in$ -> Means is an element or a member of

> Note that 0 is <span style='color:#f7b731'>neither negative nor positive</span>.

# Statements
---
## Basic Statements

**Universal Statements** ($\forall$)
> It says a certain property <span style='color:#f7b731'>is true for all elements in the set</span>.

**Conditional Statements** ($\rightarrow$)
> It says if <span style='color:#f7b731'>one thing is true</span> then some <span style='color:#f7b731'>other thing has to be true</span>.

**Existential Statement** ($\exists$)
> It says there is <span style='color:#f7b731'>at least 1 thing</span> for which the property is true.

## Combination of Statements

Each of the 3 types of statements can be combined to form one. The below shows a few.

**Universal Conditional Statement**
> For all items in a set, if one thing is true then the other is true

**Universal Existential Statement**
> For all items in a set, there is at least 1 thing for which the property is true

**Existential Universal Statement**
> There is at least one thing for which the property is true for all items in a set.

# Proofs
---

When writing proofs, it needs to follow these characteristics:
1) Concise, there should be <span style='color:#f7b731'>no irrelevant details</span>.
2) Polished, it must be the <span style='color:#f7b731'>final draft</span> where its revised to be understandable.
3) Argument, every step should be <span style='color:#f7b731'>logical</span> throughout the proof.
## Terminology

**Definition**
> A precise and unambiguous description of a mathematical term. All its properties stated must be true.

**Axiom / Postulate**
> A statement is <mark class="hltr-yellow">assumed to be true</mark> without proof.

**Theorem**
> A mathematical statement proved through rigorous mathematical reasoning. It is usually a major or important result.

**Lemma**
> A <mark class="hltr-yellow">small theorem</mark>, whose purpose is to help prove a theorem.

**Corollary**
> A result that is a <mark class="hltr-yellow">simple deduction from a theorem</mark>. It is just a sub version of a theorem.

**Conjecture**
> A statement is <mark class="hltr-yellow">believed to be true</mark>, but for which there is no proof yet.

**Tautology**
> A <mark class="hltr-yellow">compound statement</mark> which is <mark class="hltr-yellow">always true </mark>, regardless of the individual parts.

## Types of Proofs

**Direct Proof**
> A <span style='color:#f7b731'>logical sequence of statements</span> which are proven to be true to, prove that a statement is true or false

**Proof by Construction**
> It is a form of direct proof where a <span style='color:#f7b731'>value with the correct properties proves</span> that something is true.

**Proof by Counter Example**
> Find a value with the correct properties where it <span style='color:#f7b731'>disproves the statement</span>. 1 example is sufficient

**Proof by Exhaustion / Brute force**
> <span style='color:#f7b731'>Exhaust all possible values</span> and prove if the statement is true or false.

**Proof by Deduction**
> Another type of direct proof where the <span style='color:#f7b731'>number of cases are infinite</span>.

**Proof by Contradiction**
> <span style='color:#f7b731'>Assume that ~S is true</span> and use logical true statements which will lead to a contradiction. Which results in the assumption that ~S is true to be false. 
# Properties of Integers
---
## Terms

**Closure**
> A set is closed where <span style='color:#f7b731'>operations on members of a set will output a set member</span>.
> Addition, subtraction and multiplication are closed. Example: $x + y \in \Bbb Z$ where $x,y \in \Bbb Z$

**Commutativity**
> Numbers which are being operated <span style='color:#f7b731'>can be move or swapped without making any difference</span> to its output. Addition and Multiplication is commutative. Example: $x + y = y + x$, $xy = yx$

**Associativity**
> When more than 2 numbers are operated, the result remains the same <span style='color:#f7b731'>irrespective on how they are grouped</span>. Addition and Multiplication is associative. Example $x * y * z = x * (y * z)$

**Distributivity**
> Multiplying the sum of numbers is the <span style='color:#f7b731'>same as multiplying each number before adding them up</span>. Multiplication is distributive over addition. Example: $x(y + z) = xy + xz$

**Trichotomy**
> For all integers <span style='color:#f7b731'>only one</span> of the following is true, $x = y$ or $x \lt y$ or $x \gt y$

## Definition of Even and Odd Integers

**Even**
> $x$ is even $\iff \exists$ an integer $k$ such that $x = 2k$

**Odd**
> $x$ is even $\iff \exists$ an integer $k$ such that $x = 2k + 1$

## Definition of Divisibility

If $n$ and $d$ are integers and $d \ne 0$, then $n$ is <span style='color:#0fb9b1'>divisible</span> by $d \iff n = d*x$ where x is some integer

In mathematical terms, $d | n \iff \exists k \in \Bbb Z$ such that $n = dk$

Note that the symbol $|$ is <span style='color:#f7b731'>not division but represents divisibility</span>, Thus $a|b$ is either true or false and not a numerical value.
## Definition of Rational and Irrational Numbers

A real number r, is <span style='color:#0fb9b1'>rational</span> if it can be expressed as a <span style='color:#f7b731'>quotient of 2 integers with a non 0 denominator</span>.

In mathematical terms, $r$ is rational $\iff \exists a,b \in \Bbb Z$ such that $r = \frac{a}{b} b \ne 0$

If r is <span style='color:#f7b731'>not rational</span>, then it is <span style='color:#0fb9b1'>irrational</span>.
## Definition of Fraction in Lowest Term

A fraction $\frac{a}{b}$ with a nonzero denominator is said to be the <span style='color:#0fb9b1'>lowest term</span>, if the <span style='color:#f7b731'>largest integer that divides both a and b is 1</span>.

## Definition of Prime and Composite

**Integer**
An integer 𝑛 is <span style='color:#0fb9b1'>prime</span> iff <span style='color:#f7b731'>𝑛>1</span> and for all positive integers 𝑟 and 𝑠, if <span style='color:#f7b731'>𝑛=𝑟𝑠,  then either 𝑟 or 𝑠 equals 𝑛</span>. 

**Composite**
An integer 𝑛 is <span style='color:#0fb9b1'>composite</span> iff <span style='color:#f7b731'>𝑛>1</span> and <span style='color:#f7b731'>𝑛=𝑟𝑠 for some integers  𝑟 and 𝑠 with 1<𝑟<𝑛 and 1<𝑠<𝑛</span>. 


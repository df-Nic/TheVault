---
title: Boolean Algebra
Date Created: 2024-03-08
tags:
  - CS2100
  - Math
---
# Digital Circuits
---
A <span style='color:#0fb9b1'>digital current</span> can be viewed as signal wave, as illustrated when explaining about [[Datapath#Clock Signal|clock signals]]. It consist of <span style='color:#fa8231'>2 voltage levels</span> :
-  **High / True / 1 / Asserted**
- **Low / False / 0 / Desserted**

Some <span style='color:#20bf6b'>advantages</span> of <span style='color:#0fb9b1'>digital circuits</span> are :
1) More **reliable** due to its <span style='color:#f7b731'>simplicity</span> and is <span style='color:#f7b731'>less noise-prone</span>
2) Specified Accuracy
3) Can be abstracted (<span style='color:#0fb9b1'>Boolean Algebra</span>)
4) Ease of design, analysis and simplification of a digital circuit (<span style='color:#0fb9b1'>Digital Logic Design</span>)

**[[Combinatorial Circuits|Types of Circuits]]**
1) **Combinational** - No memory, and output depends on input
2) **Sequential** -With memory and output depends on input and the current state

# Boolean Algebra
---
**Values**
1) True (T or 1)
2) False (F or 0)

**Connectives**
1) Conjunction (`AND`), denoted by $\color {#f7b731} {A . B}$
2) Disjunction (`OR`), denoted by $\color {#f7b731} {A + B}$
3) Negation (`NOT`), denoted by $\color {#f7b731} {A'}$

**Logic Gates**
![[Logic Gates.png|center]]

**Order of Precedence**
>The following the order of precedence with the first being the highest precedence `Not` $\to$ `And` $\to$ `Or`

## Theorems

**Idempotency**
>$X + X = X$ **OR** $X . X = X$

**One /Zero element**
>$X + 1 = 1 + X = 1$ **OR** $X . 0 = 0 . X =0$

**Involution**
>$(X')' = X$ 

**Absorption 1 & 2**
>1) $X + (X.Y) = X$ **OR** $X . (X + Y) = X$
>2) $X + (X' . Y) = X + Y$ **OR** $X.(X' + Y) = X . Y$

**DeMorgans'**
>$(X . Y)' = X' + Y'$ **OR** $(X . Y)' = X' + Y'$

**Consensus**
> $X.Y + X'.Z + Y.Z = X.Y + X'.Z$ **OR** $(X+Y) . (X'+ Z) . (Y + Z) = (X + Y) . (X' + Z)$
## Duality

If the `AND`/`OR` operators **and** the identity elements (**0 / 1**) in a <span style='color:#f7b731'>Boolean equation</span> are <span style='color:#f7b731'>interchanged</span>, it <span style='color:#20bf6b'>still remains valid</span>.

This proves that a Boolean equation is <span style='color:#f7b731'>logically equivalent to its dual</span>, thus no need to prove both sides.

**For example :** Assume the equation $(x + y + z)' = x'.y'. z'$ is valid, then, $(x . y . z)' = x' + y' + z'$ is also valid.

## Compliment Function

A <span style='color:#0fb9b1'>compliment</span> of a function $F$ is denoted as $F'$ can be obtained by <span style='color:#f7b731'>interchanging 1 and 0</span> of $F$ output values.

If the output for the specific input is 0 then the compliment is 1.

To get $F'$ just <span style='color:#f7b731'>use the negation</span> on the whole function $F$.

## Standard Forms

<b><span style='color:#0fb9b1'>Literals</span></b> - It is a Boolean variable on its own ($x$, $x'$)

<b><span style='color:#0fb9b1'>Product Term</span></b> - A single literal or <span style='color:#f7b731'>logical product</span> (AND) of several literals ($x$, $A'.B$, $c.s'.x'.y$)

<b><span style='color:#0fb9b1'>Sum Term</span></b> - A single literal or <span style='color:#f7b731'>logical sum</span> (OR) of several literals ($x$, $A' + B$, $c + s'+ x'+ y$)

<div style="page-break-after: always;"></div>

Certain Boolean expressions are <span style='color:#f7b731'>more desirable</span> in a <span style='color:#f7b731'>implementation</span> view point. <span style='color:#fa8231'>There are 2 standard forms</span> :
1) **Sum-of-Products** (SOP)
>A <span style='color:#0fb9b1'>product term</span> **or** a <span style='color:#0fb9b1'>logical sum</span> of several product terms ($x$, $x + y.z' + C.D$)
2) **Product-of-Sums** (POS)
>A <span style='color:#0fb9b1'>sum term</span> **or** a <span style='color:#0fb9b1'>logical product</span> of several product terms ($x$, $x . y+z' . C+D$)

$X.Y.Z$ or $X + Y + Z$ are <span style='color:#f7b731'>both a SOP and POS</span>.

**Every Boolean expression** can be <b><mark style='background:#f7b731'>expressed in SOP or POS</mark></b> form.

<b><span style='color:#0fb9b1'>Minterm</span></b> - Is a <span style='color:#0fb9b1'>product term</span> consisting of $n$ <span style='color:#f7b731'>literals from all variables</span>.

<b><span style='color:#0fb9b1'>Maxterm</span></b> - Is a <span style='color:#0fb9b1'>sum term</span> consisting of $n$ <span style='color:#f7b731'>literals from all variables</span>.

In general, $n$ variables have $\color {#f7b731} {2^{n}}$ possible <span style='color:#f7b731'>min and max terms</span>.

**Denotation of min and max terms**
![[Denotation of Min and Maxterms.png|center]]

Remember that every<span style='color:#f7b731'> minterm is a compliment of its corresponding maxterm</span> and vice versa, ($(m2)' = M2$).

## Canonical Forms

Another term for this is called <span style='color:#0fb9b1'>normal form</span>, and there are <span style='color:#fa8231'>2 of these forms</span>
1) **Sum-of-minterms** also known as canonical sum-of-products
2) **Sum-of-maxterms** also known as canonical product-of-sums
<div style="page-break-after: always;"></div>

**How to find sum-of-minterms**
![[Finding Sum-of-Minterm.png|center|500]]

**How to find sum-of-maxterms**
![[Finding Sum-of-Maxterm.png|center|500]]

With this, the <span style='color:#f7b731'>conversation between the 2</span> can be done easily like as such :
1) Let use $F2$
2) Then $F2 = \sum{m(1,4,5,6,7)} = \prod{M(0,2,3)}$
3) Notice that whatever number is not in one side will be on the other


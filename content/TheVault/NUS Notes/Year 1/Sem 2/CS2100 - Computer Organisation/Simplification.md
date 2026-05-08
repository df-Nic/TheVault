---
title: Simplification
Date Created: 2024-03-09
tags:
  - CS2100
---
# Function Simplification
---
The reason for <span style='color:#0fb9b1'>simplification</span> is to <span style='color:#f7b731'>reduce logic gates</span>, therefore making it <span style='color:#20bf6b'>cheaper</span>, <span style='color:#20bf6b'>use less power</span> and is sometimes <span style='color:#20bf6b'>faster</span>.

**Techniques for Simplification**
1) **Algebraic** (Uses [[Boolean Algebra#Theorems|theorems]])
2) **Karnaugh Maps** or **K-maps** (Limited to <span style='color:#eb3b5a'>no more than 6 variables</span>)
3) **Quine-McCluskey** (suitable for automation, can handle many variables but is computationally intensive)
## Half Adder

It is a circuit that <span style='color:#f7b731'>add 2 single bits and outputs 2 bits</span>. It follows the <span style='color:#f7b731'>binary addition</span>.

| Input ($X, Y$) |         Output ($S,C$)         |
| :------------: | :----------------------------: |
|     (0, 0)     |       0 + 0  = 0, (0, 0)       |
|     (0, 1)     |       0 + 1 = 1, (0, 1)        |
|     (1, 0)     |       1 + 0 = 1, (0, 1)        |
|     (1, 1)     | 1 + 1 = 0 **Carry(1)**, (1, 0) |
The sum ($S$) and the carry ($C$) can be <span style='color:#fa8231'>in terms of</span> the [[Boolean Algebra#Canonical Forms|sum-of-minterms]] where :
- $S = X'.Y + X.Y' = X \oplus T$, which is just the <span style='color:#f7b731'>XOR operation</span>
- $C = X.Y$

## Gray Code

Another word for <span style='color:#0fb9b1'>gray code</span> is called <span style='color:#0fb9b1'>reflected binary code</span>

**Properties of Gray Code**
- It is <span style='color:#f7b731'>unweighted</span>
- Only a <span style='color:#f7b731'>single bit changes</span> from one value to the next
- It is not restricted to the decimal digits
- Good in <span style='color:#20bf6b'>error detection</span>

For a sequence to be grey code it must have these properties :
- Any sequence the <b><mark style='background:#f7b731'>next term must only differ by 1 bit changed</mark></b>
- There must be <span style='color:#f7b731'>no duplicate values</span>
<div style="page-break-after: always;"></div>

**Generating the Standard Gray Code**
![[Generate the Standard Gray Code.png|center|600]]

# K-Maps

It is an abstract form of a Venn diagram, organised by matrixes of squares where :
- Each square represent a <span style='color:#f7b731'>minterm</span>
- Two <span style='color:#f7b731'>adjacent square</span> represent <span style='color:#f7b731'>minterms that differ by exactly one literal</span>

**Example of a 3 variable K-map**
![[3 Variable K-Map.png|center|]]

There is a <span style='color:#f7b731'>wrap-around</span> in the <span style='color:#0fb9b1'>K-map</span>
![[Neighbours in a K-Map.png|center]]

In general $n$-variable <span style='color:#0fb9b1'>K-map</span> will have $\color {#f7b731} {n}$ neighbours.
<div style="page-break-after: always;"></div>

**For 4 variables**
![[4 Variable K-Map.png|center]]

**For 5 Variables**
![[5 Variable K-Map.png|center|550]]

<div style="page-break-after: always;"></div>

## Converting K-Map to Sum-of-Minterms
![[K-Map to Sum-of-Minterms.png|center|500]]

If the function given is <span style='color:#eb3b5a'>not in sum-of-minterms</span>, then <span style='color:#f7b731'>manipulate</span> it to be a <span style='color:#f7b731'>sum of products</span> ([[Boolean Algebra#Standard Forms|SOP]])
## How to Use K-Maps

The goal of the <span style='color:#0fb9b1'>K-maps</span> is to
- <span style='color:#f7b731'>Group as many</span> cells as possible, **reducing the number of literals**
- <span style='color:#f7b731'>Minimise the number of groups</span> to cover all cells, **reducing the product term**.

**Simplifying using k-map**
![[Simplifying a Function Using K-Map.png|center|600]]

Observe that, for group A, it is a <span style='color:#f7b731'>group of 2</span> which is $2^{1}$. And A has <span style='color:#f7b731'>1 variable less</span>. Therefore in general, when forming groups which is in powers of $2^{n}$, the final result will be $k - n$ variables.

Therefore, <b><mark style='background:#f7b731'>a group must be only have items in powers of 2</mark></b>.

If $n = k$, then the result is <span style='color:#f7b731'>just a constant</span>, not a literal.

**Valid & Invalid Groupings**
![[K-Map Grouping Examples.png|center|550]]

## PIs and EPIs

As mentioned to find the <span style='color:#fa8231'>simplest SOP expression</span> :
- <span style='color:#f7b731'>Minimum</span> number of <span style='color:#f7b731'>literals per product term</span>
- <span style='color:#f7b731'>Minimum</span> number of <span style='color:#f7b731'>product terms</span>

Which can be <span style='color:#fa8231'>achieved</span> by :
- **Bigger groupings** of minterms (<span style='color:#0fb9b1'>Prime Implicants</span>)
- **No redundant** Groupings (<span style='color:#0fb9b1'>Essential Prime Implicants</span>)

<b><span style='color:#0fb9b1'>Implicants</span></b> - A product term that can cover the minterms of the function

<b><span style='color:#0fb9b1'>Prime Implicants</span></b> (**PIs**) - A product term obtained by combining the <b><mark style='background:#f7b731'>maximum possible number of minterms</mark></b> from adjacent squares in the K-map (All possible implicants).

<b><span style='color:#0fb9b1'>Essential Prime Implicants</span></b> (**EPIs**) - A <span style='color:#0fb9b1'>prime implicant</span> but with <span style='color:#fa8231'>one extra condition</span> that at <b><mark style='background:#f7b731'>least 1 midterm is not covered by any other prime implicant</mark></b>.

**Steps to finding Simplified SOP**
1) Find all <span style='color:#f7b731'>prime implicants</span> on the K-map
2) Identify all <span style='color:#f7b731'>essential prime implicants</span>
3) Select the <span style='color:#f7b731'>minimum number of prime implicants to cover the midterms that are not covered</span> by essential prime implicants
<div style="page-break-after: always;"></div>

So far the steps are for **SOP** what about **POS**?

Let $F$ be a function : 
- Then draw the K-map for the function $F$ and then invert it (0 to 1 and 1 to 0), to form the K-map for $F'$
- Then similar as before, find the prime and essential prime implicant
- Form the **SOP** of $F'$
- But now, <span style='color:#f7b731'>compliment everything</span> to get the **POS** of $F$
## Don't-Care Conditions

Certain expressions does not care about certain bit value and it <span style='color:#f7b731'>can be any value</span>. Usually represented by X or b.

These conditions can <span style='color:#f7b731'>simplify the expression further</span> and is denoted by $\sum {d ()}$, thus in the K-map, it can be either 1 or 0, depending on which one results in a simpler expression.

**Example**
![[Don't-Care Condition Example.png|center|550]]
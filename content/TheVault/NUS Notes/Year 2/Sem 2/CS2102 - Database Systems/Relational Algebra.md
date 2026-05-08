---
Title: Relational Algebra
Date Created: 28-November-2025
Last Updated: 10-February-2026
Tags: 
title: Relational Algebra
tags:
  - CS2102
  - Database
---
# Relational Algebra
---
> [!info] Mathematical algebra
> An algebra is a mathematical system <span style='color:var(--mk-color-orange)'>consisting</span> of:
> - **Operands**: Variables or values from which new values can be constructed, <span style='color:var(--mk-color-yellow)'>values used</span>.
> - **Operators**: Symbols denoting procedures that construct new values from the given values, what <span style='color:var(--mk-color-yellow)'>operation</span> to be done.
>   
> One useful thing is that it <span style='color:var(--mk-color-green)'>can do chaining</span>, the output is used as an input for something else.

In SQL we **use something called relational algebra**.

> [!info] Relational algebra
> An algebra system for SQL which <span style='color:var(--mk-color-orange)'>consists</span> of:
> - **Operands**: Relations / tables
> - **Operators**: Transforms from one or more input relations into output relations
>   
> There is <span style='color:var(--mk-color-yellow)'>no nesting</span> in relational algebra.

The tables we used in **relational algebra** are<span style='color:var(--mk-color-yellow)'> materialised tables</span> while the **output** is an <span style='color:var(--mk-color-yellow)'>unmaterialised table</span>.

> [!note] Materialised & unmaterialised table
> A **materialised** table is a <span style='color:var(--mk-color-yellow)'>table stored in the hard disk</span> (*tables in the database*), while for **unmaterialised** tables they are <span style='color:var(--mk-color-yellow)'>stored in memory</span> (*results from a query*).
## Relational Operators

Below is the <span style='color:var(--mk-color-orange)'>main set</span> of operators:
![[Relational Algebra Operators.png|center]]

Relational algebra is based on relations. In turn, **relation is based on set**. So, there is <span style='color:var(--mk-color-yellow)'>no duplicate row in relational algebra</span>, this is <b>not the same as SQL queries</b>.

There is also [[Year 1/Sem 1/CS1231S - Discrete Structures/Propositional Logic|propositional logic]]
![[Propositional Logic.png|center]]

> Remember that $p \rightarrow q \equiv \lnot p \lor q$ 

There is also <span style='color:var(--mk-color-orange)'>relational operators</span>:
- $=$: Equals
- $\neq$: Not equals
- $\gt$, $\lt$: greater / less than
- $\ge$, $\le$: greater / less than or equals to

We will **assume** that <span style='color:var(--mk-color-yellow)'>everything has a total order</span> (*some way to order from smallest to biggest*).

> [!note] Two propositional formulae are equivalent if and only if they have the same truth table.
### Select

We will use $\sigma_{[c]}(R)$, to <span style='color:var(--mk-color-yellow)'>select all rows</span> in relation R (*table R*) that <span style='color:var(--mk-color-yellow)'>satisfies the condition</span> $c$.

> [!info] The $[c]$ is similar to the `WHERE` clause in SQL

> [!example] Find the restaurant name, pizza, and price of the different restaurants that, sells Veggie cheaper than 14 or is named Sizzle Grill.
> Our relational algebra will be: $\sigma[(\text{pizza} = \text{'Veggie'} \land \text{price} \lt 14) \lor (\text{rname} = \text{'Sizzle Grill'})] (\text{sells})$
### Projection

We will use $\pi[l](R)$ to<span style='color:var(--mk-color-yellow)'> keep the columns specified</span> in the ordered list $l$ and in the <span style='color:var(--mk-color-yellow)'>same order</span>.

We also allow dot notation similarly to how in SQL we use `t.attribute`.

> [!info] It is similar to the `SELECT` clause in SQL

> [!example] Find the restaurant name of the different restaurants that, sells Veggie cheaper than 14 or is named Sizzle Grill.
> Our relational algebra will be: $\pi[rname](\sigma[(\text{pizza} = \text{'Veggie'} \land \text{price} \lt 14) \lor (\text{rname} = \text{'Sizzle Grill'})] (\text{sells}))$
### Renaming

We can **rename the table** by using $\rho(R_{1}, R_{2})$, where $R_{1}$ is the <span style='color:var(--mk-color-yellow)'>old table name</span> and $R_{2}$ is the <span style='color:var(--mk-color-yellow)'>new table name</span>.

When **renaming** we <b>do not create a new table / relation in the hard disk</b>.

We can also **rename columns** by doing, $\rho(R_{1}, R_{2}(A_{1} \rightarrow A_{2}))$, where $A_{i}$ is the column name.

Unlike in SQL, we will put $\rho$ <span style='color:var(--mk-color-yellow)'>inside the select operation</span> ($\sigma$).

> [!info] It is similar to the `AS` keyword in SQL
## Set Operators

These are you <span style='color:var(--mk-color-orange)'>3 main set operations</span>:
1) **Union**: $A \cup B$ 
2) **Intersect**: $A \cap B$
3) **Except** or **set difference**: $A - B$

> [!NOTE] The 2 sets must be union-compatible
> Essentially, the **2 sets must have** the <span style='color:var(--mk-color-yellow)'>same column types</span>.

For **2 sets to be equal** we need to <span style='color:var(--mk-color-orange)'>check the following</span>:
1) $\vert A \vert = \vert B \vert$
2) $A \subseteq B$
3) $B \subseteq A$

> [!info] Assignment in relational notation
> Assignment in programming is just `=` but in relational algebra we will use the <span style='color:var(--mk-color-turquoise)'>walrus sign</span> which is $:=$.
> 
> It is <span style='color:var(--mk-color-green)'>useful to break up complex queries</span> into simpler queries.


> [!example] Find the different pizza sold by both Bella Italia and Desert Diner
> $Q1 := π[pizza](σ[rname = 'Bella Italia'](sells))$, $Q2 := π[pizza](σ[rname = 'Desert Diner'](sells))$
> 
> The final result will be, $Q1 \cap Q2$.
### Cross Product

We can do a **cross product** by using $R_{1}  \times R_{2}$, which will attach each row in $R1$ to each row in $R2$, resulting in a $n \times m$ table length.


> [!example] Find all the different pairs of customer name and restaurant name such that they are in the same area.
> **In SQL**:
> ``` SQL
> SELECT c.cname, r.rname
> FROM customer c, restaurant r
> WHERE c.area = r.area;
> ```
> **In relational algebra**: $π[c.cname, r.rname](σ[c.area = r.area]( ρ(customer, c) × ρ(restaurant, r)))$.
> 
> Thus we can <span style='color:var(--mk-color-yellow)'>define the linking conditions in the select clause</span>.
#### Inner Join

We can also do a **inner join**, by using $R_{1} \bowtie_{[c]} R_{2}$ which is shown in the example above as $\sigma[c](R_{1} \times R_{2})$.

> [!summary] Variants of join
> - If we <span style='color:var(--mk-color-yellow)'>exclude the condition</span>, then we are performing a **natural join operator**.
> - We can do **left outer join** by using this $⟕[c]$ 
> - We can do **right outer join** by using this $⟖[c]$ 
> - We can do **full outer join** by using this $⟗[c]$, we can do a **full natural outer join** by <span style='color:var(--mk-color-yellow)'>omitting the condition</span>


> [!example] Find all the different pairs of customer name and restaurant name such that they are in the same area.
> 
> **In relational algebra**: $π[c.cname, r.rname](\sigma[]( ρ(customer, c) ⋈[c.area = r.area] ρ(restaurant, r)))$

Note that for **nested joins** as such $r1 ⋈[c1] r2 ⋈[c2] r3$, we will <b>start from the left</b> then end on the right.
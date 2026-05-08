# Project Overview
---
This will be a <span style='color:var(--mk-color-yellow)'>brownfield project</span>, were we are going to be building up on a pre-existing project SQLancer. In addition we will be following an [[Project Management#Agile Models|agile approach]].
## Scrumban

A **hybrid approach** using both <span style='color:var(--mk-color-turquoise)'>Scrum</span> & <span style='color:var(--mk-color-turquoise)'>Kanban</span>.

> [!note] Scrum Team
> It usually <span style='color:var(--mk-color-yellow)'>consists of product owners as well as developers</span>.

At the **beginning of each sprint** we will do the following:
1) **Sprint review** (*Report the progress towards the product goal*)
2) **Sprint retrospective** (*Reflect on what went well or wrong and how to improve on it*)
3) **Sprint planning** (*Work to be done, how will it be done and what value can it provide*)

We will also required to **get requirements** from the user through [[Project Requirements#User Stories|User stories]].

> [!abstract] Kanban
> A board that <span style='color:var(--mk-color-yellow)'>visualises</span> the **respective tasks and their status**.
> 
> The status are usually (*But not fixed*):
> - **Todo** or **Sprint backlog**
> - **In progress**
> - **Completed**
# SQLancer
---
An overview of SQLancer is that, it will create a database schema with some data, it will then generate queries (*rule-based generators*) and ensure that the result matches the expected result.

> [!example] An interesting bug found
> The **2 values 0.0 and -0.0**, are essentially the same. But when you **look in binary**, it will be <span style='color:var(--mk-color-red)'>different because of the sign bit</span>. In reality, both are the same but some databases will think this is different.
## Test Oracle

We need a way to <span style='color:var(--mk-color-yellow)'>check if the result of a query is correct or not</span>, this is where <span style='color:var(--mk-color-turquoise)'>test oracles</span> come in.

> [!abstract] Naive way of testing
> A simple & naive way of testing is through <span style='color:var(--mk-color-turquoise)'>differential testing</span>.
> 
> Currently there are a lot of databases online and thus we can use the <span style='color:var(--mk-color-yellow)'>same set of queries and check</span> if the results is the same for all the databases. If <span style='color:var(--mk-color-red)'>there is a difference then there is a bug</span>.
> 
> If all the <b><mark style='background:var(--mk-color-red)'>results are the same it does not guarantee there is no bugs</mark></b>, it can be **every database is wrong**.
### Logic Bugs

SQL uses many testing approaches, one **commonly used approach** is the <span style='color:var(--mk-color-turquoise)'>ternary logic partitioning</span> (*TLP*).

> [!info] Query partitioning
> ![[What is Query Partitioning.png|center]]
> 
> Essentially, our queries will <span style='color:var(--mk-color-yellow)'>segment the database</span> into segments and if we <span style='color:var(--mk-color-yellow)'>combine them</span> and it is <span style='color:var(--mk-color-red)'>not equals to the original database then there is a bug</span>.
> 
> This follows the <span style='color:var(--mk-color-turquoise)'>ternary logic</span>, where $\phi$ and not $\phi$ and $\phi$ is null, must make the whole database.
### Performance Bugs

It is <span style='color:var(--mk-color-red)'>difficult to find</span> performance bugs. How would you know that a query which executes in 3 seconds have any bugs. Or sometimes the <span style='color:var(--mk-color-yellow)'>DBMS might trade optimisation time with execution time</span>.

One approach is to use <span style='color:var(--mk-color-turquoise)'>cardinality estimators</span>.

> [!info] Query plan
> Most databases has a keyword called `EXPLAIN`, which shows a query plan for a query. It shows generally how it will execute the query but it also <span style='color:var(--mk-color-yellow)'>shows the estimate number of rows returned</span>.

These **estimators** can be used to check if the query is optimised or not. It has to be <b><mark style='background:var(--mk-color-yellow)'>consistent</mark></b> (*no overestimations*) and <b><mark style='background:var(--mk-color-yellow)'>estimate fewer rows for more restrictive queries</mark></b>. This is known as <span style='color:var(--mk-color-turquoise)'>Cardinality Estimation Restriction Testing</span> (*CERT*).
## Query Generation

We can generate queries but how can we <span style='color:var(--mk-color-orange)'>ensure that future queries are meaningful</span> and not test the same thing again. There is where <span style='color:var(--mk-color-turquoise)'>query plan</span> come in.

> [!faq] How can we use the query plan?
> The query plan (*Query plan guidance or QPG*) **shows how the query will be executed** (*How tables are scanned, filtered, joint, any optimisations etc*).
> 
> What we can do is to <span style='color:var(--mk-color-yellow)'>save this query plan</span> and if future queries <span style='color:var(--mk-color-red)'>does not generate new query plans</span>, we can <span style='color:var(--mk-color-yellow)'>modify the database state</span> (*add new tables/data, remove data, create index, etc*).
> 
> If **new query plans are generated by the same queries** then <span style='color:var(--mk-color-orange)'>something interesting occurred</span> during modification.



---
title: Nested Queries
Date Created: 2025-02-15
Last Updated: 2025-09-28
tags:
  - CS2102
  - Database
  - SQL
  - SQLQueries
---
# Copying a Table
---
Sometimes we will want to **copy a table** (*or a subquery*) if we <span style='color:var(--mk-color-yellow)'>need it frequently</span> or for <span style='color:var(--mk-color-yellow)'>more complex queries</span>.

1) **Create a permanent copy**:

> [!example] Example of making a permanent copy 
> ``` SQL
> CREATE TABLE singapore_customer AS
> 	SELECT *
> 	FROM customers c
> 	WHERE c.country = 'Singapore';
> ```

2) **Create a `temporary` copy**:

Unlike, the previous method, this <span style='color:var(--mk-color-turquoise)'>temporary table</span> exists until the database session ends (*disconnect*).

> [!example] Example of making a temporary copy 
> ``` SQL
> CREATE TEMPORARY TABLE singapore_customer AS
> 	SELECT *
> 	FROM customers c
> 	WHERE c.country = 'Singapore';
> ```

However, when we **copy a table**, it <span style='color:var(--mk-color-red)'>does not change</span> when the **base table has some update**. But is not a good idea because it can be rewritten as a simple query.

> [!summary] `VIEW`
> We can use `VIEW` to create a function of sort which will retrieve the results from the query every time we call it.
> 
> > [!example] Example of using `VIEW`
> > ```SQL
> > CREATE VIEW singapore_customer AS
> > 	SELECT *
> > 	FROM customers c
> > 	WHERE c.country = 'Singapore';
> > ```
> 
> Views can be <span style='color:var(--mk-color-turquoise)'>unmaterialised</span> and <span style='color:var(--mk-color-turquoise)'>materialised</span>. The difference is that **unmaterialised views** <span style='color:var(--mk-color-yellow)'>do not need to be refreshed</span> when the base table updates.
# Splitting Queries
---
1) **Common table expression**
Using `VIEW` creates a perpetual updating copy of a table, however it can be <span style='color:var(--mk-color-yellow)'>used by everyone</span>. But what if we want to **use it for a particular query**, then we can use <span style='color:var(--mk-color-turquoise)'>common table expression</span> (*CTE*), using the clause `WITH`.

> [!example] Example of using CTE 
> ``` SQL
> WITH singapore_customer AS -- This is the CTE
> 	( SELECT *
> 	FROM customers c
> 	WHERE c.country = 'Singapore' )
> SELECT cs.last_name, d.name
> FROM singapore_customer cs, downloads d
> WHERE cs.customerid = d.customerid;
> ```

2) **Using `FROM`**
We can also do the same thing just by using the `FROM` clause.

> [!example] Example of using a subquery in `FROM` clause
> ``` SQL
> SELECT cs.last_name, d.name
> FROM ( SELECT *
> 	FROM customers c
> 	WHERE c.country = 'Singapore') AS cs, downloads d
> WHERE cs.customerid = d.customerid;
> ```

3) **Using `SELECT`**
We can also put a subquery in a `SELECT` clause, but one restriction is that the subquery must <b><span style='color: var(--mk-color-red)'>return only 1 column and 1 row</span></b> for each entry.

This is known as a <span style='color:var(--mk-color-turquoise)'>scalar subquery</span>.

> [!example] Example of a scalar subquery
> ``` SQL
> SELECT (
> 	SELECT COUNT(*) FROM customers c
> 	WHERE c.country = 'Singapore' );
> ```

If the **subquery, returns 0 rows and columns**, then it will return `NULL`.

> [!important] Unsure Readable & Maintainable
> Always try to <span style='color:var(--mk-color-yellow)'>construct simple queries first</span>. As **complex queries** may be <span style='color:var(--mk-color-red)'>unreadable or inefficient</span>.
# Nested Queries
---
1) **Subqueries in the `WHERE` clause**
We will need additional clauses such as `IN`, `ANY` or `ALL` in order for this to work.

> [!example] Example of using a subquery in `WHERE` clause
> ``` SQL
> SELECT d.name
> FROM downloads d
> WHERE d.customerid IN ( -- Or ANY, both are the same
> 	SELECT c.customerid
> 	FROM customers c
> 	WHERE c.country = 'Singapore'
> );
> ```
> In this example we are **unsure how many customers are there**, thus we need to query it.

When using `ALL` usually we will pair it with $\le$ or $\ge$, as `ALL` **checks for everything in the set** (*the 2 just finds the smallest or greatest value respectively*).

> [!info] Limiting results
> We can **limit a queries** results fetched, by doing `LIMIT <number>`. We can also **ignore the first few rows** rows by doing `OFFSET <number>`.
> 
> So `LIMIT 1` and `OFFSET 1` just takes the 2nd value from the resulting query.

2) **Checking if the query `EXISTS` some value**
We can also use subqueries in a `EXISTS` clause.

> [!info] Behavior of `EXISTS`
> It acts like a set of items, and if this **set has something**, it will <span style='color:var(--mk-color-green)'>evaluate to true</span>, if it **has nothing**, it will <span style='color:var(--mk-color-red)'>evaluate to false</span>.

> [!example] Example of using a subquery in `EXISTS` clause
> ``` SQL
> SELECT d.name
> FROM downloads d
> WHERE EXISTS (
> 	SELECT c.customerid
> 	FROM customers c
> 	WHERE d.customerid = c.customerid
> 		AND c.country = 'Singapore'
> );
> ```
> > [!note] Correlated subquery
> > Notice that `d.customerid` is in the inner subquery, this means that the <span style='color:var(--mk-color-yellow)'>query and subquery are correlated</span>.
> >
> > Also the <span style='color:var(--mk-color-yellow)'>columns are also bounded by scope</span>, meaning `c.customerid` <span style='color:var(--mk-color-red)'>cannot be used outside</span>, this is known as <span style='color:var(--mk-color-turquoise)'>lexical scoping</span>.

> [!example] All the customer who downloaded all the versions of Aerified.
> ```SQL
> SELECT c.first_name, c.last_name
> FROM customers c
> WHERE NOT EXISTS (
> 	SELECT *
> 	FROM games g
> 	WHERE g.name = 'Aerified'
> 		AND NOT EXISTS (
> 			SELECT *
> 			FROM downloads d
> 			WHERE d.customerid = c.customerid
> 				AND d.name = g.name
> 				AND d.version = g.version ));
> ```

> [!question] When to use nested queries?
> Nested queries are <span style='color:var(--mk-color-green)'>powerful when combined with negation</span> (*remember [[Queries#Logic & Null|de morgan's law]]*).
> 
> It can also be **necessary** when there are <span style='color:var(--mk-color-yellow)'>aggregation functions on 2 different groupings</span>.

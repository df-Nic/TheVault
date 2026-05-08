---
title: Aggregation & Algebraic Queries
Date Created: 2025-01-27
Last Updated: 2025-09-28
tags:
  - CS2102
  - Database
  - SQL
  - SQLQueries
---
# Aggregate Queries
---
Aggregation functions, takes <span style='color:var(--mk-color-yellow)'>many values and transforms it into one value</span>. We have seen [[Queries#Counting|some examples]] before.

If the **column has no values, it will return null** (*If we don't know the answer, return null*).

> [!important] Ignoring null values
> Most of the <span style='color:var(--mk-color-yellow)'>aggregate functions will ignore</span> (*skip*) <span style='color:var(--mk-color-yellow)'>null values</span> during computation, with the **exception of** `COUNT(*)` this will count the number of rows in a table.

> [!info] Functions for `COUNT`
> When using `COUNT`, we can also use the keyword `ALL`, `COUNT(ALL c.country)`. However this is the <span style='color:var(--mk-color-yellow)'>default option</span> thus its **omitted**.
> 
> We can also use `DISTINCT`, which <span style='color:var(--mk-color-yellow)'>counts the number of unique values</span>. This is [[Queries#Distinct Values|different from putting it at the front]].
## Grouping

To make more meaningful queries, we can <span style='color:var(--mk-color-yellow)'>form logical groups within the data</span> and compute aggregate functions on the **individual groups**.

We can use the `GROUP BY` function to <span style='color:var(--mk-color-yellow)'>group records of similar values</span>. And it <b>must be used with an aggregate function</b>.

> [!example] Count number of people in each country
> ```SQL
> SELECT c.country, COUNT(*)
> FROM customers c
> GROUP BY c.country;
> ```

These **groups are formed** (*logically*) <span style='color:var(--mk-color-yellow)'>after the rows have been filtered</span> by the `WHERE` clause (*From will execute first before this*). In addition, you can also **rename columns** and use it in the `ORDER BY`.

> [!warning] Selecting while grouping
> Besides the aggregate function, we need to also <b><span style='color: var(--mk-color-yellow)'>ensure that the other columns selected is also unique</span></b>.
> 
> A <span style='color:var(--mk-color-green)'>good practice</span> is to `GROUP BY` with **all selected columns**.
## Having

What if we want to **filter out certain groupings**, then we will need to use the `HAVING` function instead of `WHERE`.

> [!failure] Issues with using `WHERE`
> As mentioned previously, the `WHERE` clause will <span style='color:var(--mk-color-yellow)'>execute first</span> before `GROUP BY`. Thus we are <span style='color:var(--mk-color-red)'>not able to remove groupings after formation</span>.
> 
> Also `WHERE` <b><span style='color: var(--mk-color-red)'>clauses does not allow aggregate functions</span></b>. As the <span style='color:var(--mk-color-yellow)'>value will update as rows gets excluded from filtering</span>.

> [!example] Filter out countries who's count is less than 100 
> ```SQL
> SELECT c.country
> FROM customers c
> GROUP BY c.country
> HAVING COUNT(*) >= 100;
> ```

> [!example] Customers who spend the most in each country
> ```SQL
> SELECT c.customerid, c.country, SUM(g.price) AS total -- find total spent by a customer id
> FROM customers c, downloads d, games g -- need these 3 relations
> WHERE c.customerid = d.customerid -- to connect c and d
> 	AND g.name = d.name AND g.version = d.version -- to connect g and d
> GROUP BY c.customerid, c.country -- needed to compute sum
>HAVING SUM(g.price) >= ALL ( -- such that the total spent by customer
> 	SELECT SUM(g2.price) AS total -- is greater than all other customer
> 	FROM customers c2, downloads d2, games g2
> 	WHERE c2.customerid = d2.customerid
> 		AND g2.name = d2.name AND g2.version = d2.version
> 		AND c2.country = c.country -- from the same country
> 	GROUP BY c2.customerid
>);
> ```
# Algebraic Queries
---
**Every single** [[Queries|simple query]]is <span style='color:var(--mk-color-yellow)'>considered as a algebraic query</span>. But not the other way around.
## More on Joining

There are <span style='color:var(--mk-color-orange)'>other ways to join 2 or more tables</span> with **different results** other than cross join.
### Inner Join

An inner join <span style='color:var(--mk-color-yellow)'>does the exact same thing</span> as a [[Queries#Table Joining|cross join]]. The key word is `INNER JOIN` and to specify the condition for the join, use `ON` which will be the <b>same usage for the subsequent joins</b>.

You can omit `INNER` and just use `JOIN` for the same result (*As this is the default option*).

> [!example] Joining tables using inner join
> ```SQL
> SELECT *
> FROM customers c
> INNER JOIN downloads d
> 	ON d.customerid = c.customerid -- you can also do ON true for a cross product --
> INNER JOIN games g
> 	ON d.name = g.name
> 	AND d.version = g.version;
> -- The ON clauses can be extracted out to a WHERE clause -- 
> ```

> [!question] Cross or Inner join?
> There is <span style='color:var(--mk-color-red)'>no added expressiveness or performance gain</span> when using inner join. However **cross join is preferred** as it is <span style='color:var(--mk-color-green)'>easier to read and is optimised by DMBS</span>.
> 
> You can use the `EXPLAIN` function and compare the query plan for a query and they will be the same.
### Natural Join

Similar to cross join, however if there are **multiple columns with the same name and values** (*Thus it has the same meaning*), it will <span style='color:var(--mk-color-yellow)'>remove them</span>.

> [!info] If there is no common attributes, natural join will be equivalent to a cross join

> [!example] Using natural join
> ``` SQL
> SELECT *
> FROM customers c
> 	NATURAL JOIN downloads d
> 	NATURAL JOIN games g;
>  ```
### Outer Join

What if we are interested in data that <span style='color:var(--mk-color-yellow)'>do not match anything in the other table according to the join condition</span> (*Maybe the primary key does not exist in the reference table*). These rows are called <span style='color:var(--mk-color-turquoise)'>dangling</span>.

With the `OUTER JOIN`, and **rows that does not match** the join condition, the columns will all be <span style='color:var(--mk-color-red)'>padded with nulls</span>. We can do a <span style='color:var(--mk-color-orange)'>left, right or full outer join</span> (*Both tables*).

There is also a `NATURAL FULL/LEFT/RIGHT OUTER JOIN` which is <b><span style='color:var(--mk-color-yellow)'>similar to a natural join but for rows that do not match</span></b>.

> [!example] Using outer join
> ``` SQL
> SELECT c.customerid, c.email, d.customerid, d.name, d.version
> FROM customers c LEFT OUTER JOIN downloads d ON c.customerid = d.customerid;
> ```
> > Note that the **position of the table** and using `LEFT` or `RIGHT` will <span style='color:var(--mk-color-yellow)'>make a difference</span> in the result. And `FULL` will do both.

> [!abstract] Anti Join
> It is **same as outer join**, but we only <span style='color:var(--mk-color-yellow)'>filter out the null values</span>.
> 
> ``` SQL
> SELECT c.customerid
> FROM customers c
> 	LEFT OUTER JOIN downloads d
> 		ON c.customerid = d.customerid
> WHERE d.customerid IS NULL; -- This is the filtering for NULL values --
> ```

> [!attention] Further Restrictions
> It is <span style='color:var(--mk-color-red)'>not always correct</span> to place conditions in the `WHERE` clause into the `ON` clause. Any **further restrictions should be placed** in the `WHERE` clause.
## Set Operations

We can <span style='color:var(--mk-color-yellow)'>combine results</span> from 2 queries using set operations.

> [!info] Deduplication
> These set operations will <b><span style='color: var(--mk-color-yellow)'>remove any duplicates</span></b> unless annotated with the keyword `ALL` (*Example `UNION ALL`*).

> [!important] Union-compatible
> The 2 queries <b><span style='color: var(--mk-color-green)'>must be union-compatible</span></b>. Meaning they <span style='color:var(--mk-color-orange)'>must have</span>:
> - **Same number of columns**
> - **Same domain in the same order**
>   
> > [!danger] Even if they are union-compatible it does not mean it is meaningful
### Union

It <span style='color:var(--mk-color-yellow)'>combines the results of the 2 queries</span> ($A \cup B$).

> [!example] Join people who downloaded version 1.0 or 2.0 of Aerified
> ``` SQL
> SELECT d.customerid
> FROM downloads d
> WHERE d.name = 'Aerified' AND d.version = '1.0'
> UNION -- You can add ALL after UNION, to keep duplicates --
> SELECT d.customerid
> FROM downloads d
> WHERE d.name = 'Aerified' AND d.version = '2.0';
> ```
### Intersect

Fetch rows that are <span style='color:var(--mk-color-yellow)'>similar in both results of the 2 queries</span> ($A \cap B$).

> [!example] Join people who downloaded version 1.0 and 2.0 of Aerified
> ``` SQL
> SELECT d.customerid
> FROM downloads d
> WHERE d.name = 'Aerified' AND d.version = '1.0'
> INTERSECT
> SELECT d.customerid
> FROM downloads d
> WHERE d.name = 'Aerified' AND d.version = '2.0';
> ```

We can try to do `d.version = 1.0 AND d.version = 2.0` but it <span style='color:var(--mk-color-red)'>will not work</span> because <span style='color:var(--mk-color-yellow)'>version can be of 1 value</span>. A work around is to use [[Queries#Table Joining|cross join]]and filter using `WHERE`
### Difference

It is the **same as set difference**, it will <span style='color:var(--mk-color-yellow)'>retrieve rows that are in query 1 but not in query 2</span> ($A \backslash B$).

> [!example] Join people who downloaded version 1.0 but not 2.0 of Aerified
> ``` SQL
> SELECT d.customerid
> FROM downloads d
> WHERE d.name = 'Aerified' AND d.version = '1.0'
> EXCEPT
> SELECT d.customerid
> FROM downloads d
> WHERE d.name = 'Aerified' AND d.version = '2.0';
> ```

Unlike intersect and union, `EXCEPT` is <span style='color:var(--mk-color-red)'>not symmetric</span>, the <b>order matters</b>.
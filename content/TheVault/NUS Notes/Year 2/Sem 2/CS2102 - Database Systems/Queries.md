---
title: Queries
Date Created: 2025-01-21
Last Updated: 2025-09-28
tags:
  - CS2102
  - Database
  - SQLQueries
  - SQL
---
# Retrieve Data from a Table
---
In <span style='color:var(--mk-color-purple)'>SQL</span>, the keyword to <span style='color:var(--mk-color-orange)'>retrieve data</span> is `SELECT`, however we also need to <span style='color:var(--mk-color-orange)'>specify the table</span> to retrieve from and the keyword is `FROM`.

> [!example] Selecting from a table
> ```SQL
> SELECT < Column 1 >, < Column 2 >
> FROM < Table-Name >;
> ```

> [!note] Wildcards
> To select <span style='color:var(--mk-color-orange)'>all columns</span> use a **asterisk** (\*).
## Conditions

We can also <span style='color:var(--mk-color-orange)'>filter out</span> certain data entries by using the keyword `WHERE`.

> [!example] Retrieve data whose country is in Singapore
> ```SQL
> SELECT first_name, last_name
> FROM customers
> WHERE country = 'Singapore';
> ```

It <span style='color:var(--mk-color-yellow)'>applies to any Boolean condition</span>, some <span style='color:var(--mk-color-orange)'>Boolean operators</span> in SQL are:
- `AND`
- `OR`
- `NOT`
- `IN (value 1, value 2, ...)`
- `LIKE`
- `BETWEEN .. AND` (*inclusive for both sides*)
- >, <, >=, <=, <> (*not equal to*)

> [!info] Using `LIKE`
> `LIKE` is mainly <span style='color:var(--mk-color-yellow)'>used for matching of strings</span>, and there are 2 special characters, `_` and `%'.
> > [!note] Meaning of `_`
> > `_` means that the string must have a <span style='color:var(--mk-color-yellow)'>specific number of characters</span> based on the number of `_` used.
> 
> > [!note] Meaning of `%`
> `%` means <span style='color:var(--mk-color-yellow)'>any number of characters</span> (*0 or more*).

## Distinct Values

To get <span style='color:var(--mk-color-orange)'>distinct values</span>, use the keyword `DISTINCT`. Note that it <b><span style='color: var(--mk-color-red)'>applies to rows and not individual columns</span></b>.

> [!example] Retrieve distinct names from a table
> ```SQL
> SELECT DISTINCT name, version
> FROM games;
> ```

`DISTINCT` often **results in a sorted result** but it is <b><span style='color: var(--mk-color-red)'>not always guaranteed</span></b>.
# Ordering
---
If you want to **sort** a particular order<span style='color:var(--mk-color-orange)'> in ascending or descending</span> order, use the keyword `ORDER BY`.

> [!example] Order  version in descending order 
> ```SQL
> SELECT name, version
> FROM downloads
> ORDER BY name, version DESC;
> ```
> > [!important] Default ordering
> > The <b>default ordering is ascending</b> and not descending `DESC`.
> > Thus, name in the example above will be in ascending order `ASC`.

> [!warning] Column order
> The <b>order of the column matters</b>, it will **order by the first column**, followed by the second column and so on.

 We can also <span style='color:var(--mk-color-yellow)'>order columns which are not selected</span>, in which case the <span style='color:var(--mk-color-red)'>selected columns will appear in any order</span>. **Same** goes for <span style='color:var(--mk-color-yellow)'>selected columns not stated</span> in the `ORDER BY` condition.

> [!seealso] How does a DBMS sort
> <b><span style='color: var(--mk-color-red)'>Conventional sorting algorithms will not work</span></b>, since in a database it has alot of data and it can <span style='color:var(--mk-color-red)'>exceed memory</span>.
> 
> There are external algorithms which <span style='color:var(--mk-color-yellow)'>sorts based on data from the different files</span>.

> [!error] Combining `DISTINCT` & `ORDER BY`
> There can be <span style='color:var(--mk-color-yellow)'>ambiguity</span> when combining the 2 together.
> 
> **For example**:
> ```SQL
> SELECT DISTINCT version, price
> FROM games
> ORDER BY price ASC;
> ```
> Assuming our table has:
> 
> | version | price |
| :-----: | :---: |
|    1    |  10   |
|    1    |  30   |
|    2    |  20   |
> There can be **2 results**, {1, 10} then {2, 20} or will it be {2, 20} then {1, 30}. In this case <span style='color:var(--mk-color-red)'>SQL will raise an error</span>.
# Table Joining

Instead of selecting from 1 table we can **select from multiple tables** as such, `SELECT * FROM customers, downloads, games`. This however will do a <span style='color:var(--mk-color-red)'>cross product / cartesian product</span> of all possible combinations of rows.

> [!info] `CROSS JOIN`
> `CROSS JOIN` can achieve the same result.
> ```SQL
> SELECT *
> FROM customers
> 	CROSS JOIN downloads
> 	CROSS JOIN games;
> ```
## Meaningful Joins

When joining tables, <span style='color:var(--mk-color-yellow)'>join using the primary and foreign keys</span> to make sense of the data from multiple tables. This can be achieved using the `WHERE` clause and making sure that the <span style='color:var(--mk-color-yellow)'>2 are equal to one another</span>.

> [!example] Combining customers, downloads and games
> ```SQL
> SELECT *
> FROM customers c, downloads d, games g
> WHERE d.customerid = c.customerid
> 	AND d.name = g.name
> 	AND d.version = g.version;
> ```
> > If we **did not link 1 of the primary and foreign key** pairs it will <span style='color:var(--mk-color-yellow)'>do a cross product</span>.

> [!important] Table variables
> Notice that in the example, we did `FROM customer c, ...`, the `c` is known as a <span style='color:var(--mk-color-turquoise)'>table variable</span>. <span style='color:var(--mk-color-red)'>Without it there can be ambiguity</span> between 2 tables with the same column name, which will **result in an error**.
> 
> Thus it is good practice, even without joining to <b><span style='color: var(--mk-color-yellow)'>always assign table variables</span></b>.

# Other Operators
---
## Renaming

The keyword to rename a column is `AS`. It <b><span style='color: var(--mk-color-red)'>does not rename the actual column</span></b> but, whatever <span style='color:var(--mk-color-yellow)'>data will be placed in a renamed column</span>.

> [!example] Displaying price after GST
> ```SQL
> SELECT DISTINCT price * 1.09 AS gst -- add GST of 9% & the column will be named GST--
> FROM games
> ORDER BY gst ASC;
> ```
> >By **default** the name of the column will be "unknown" if we do not modify the values.
## Concatenation

To **concatenate a string** with something use `||`.

> [!example] Concatenate the first & last name 
> ```SQL
> SELECT
> 	first_name || ' ' || last_name AS name,
> FROM downloads
> WHERE price * 0.09 >= 0.3;
> ```
> > It concatenates the first name with a space followed by the last name.
## Rounding

We can **round floating point values** to a specific decimal point using the keyword `ROUND`.

> [!example] Round price to 2 decimal points
> ```SQL
> SELECT
> 	name || ' ' || version AS game,
> 	ROUND(price * 1.09, 2) AS price
> FROM games
> WHERE price * 0.09 >= 0.3;
> ```

> [!important] Difference with `TRUNC`
> For truncation, it just **cuts off at the specified precision**, there is <b><span style='color: var(--mk-color-red)'>no rounding involved</span></b>.
## If-Else

In <span style='color:var(--mk-color-purple)'>SQL</span> we will start an if-else statement using the keyword `CASE`. Afterwards `if`, its keyword will be `WHEN`, else will be `ELSE`. To denote the end of a `CASE` statement, use the keyword `END`.

If the `WHEN` condition is satisfied, to make SQL do something use the keyword `THEN`.

> [!example] Add GST if the amount is significant
> ```SQL
> SELECT name || ' ' || version as games,
> 	CASE
> 		WHEN price * 0.09 >= 0.3 THEN ROUND(price * 1.09, 2) -- Can add more WHEN clauses for else if --
> 		ELSE price
> 	END AS price
> FROM games;
> ```
## Coalesce

Given a set of values, <span style='color:var(--mk-color-yellow)'>return the first instance of a non null value</span>. If <span style='color:var(--mk-color-yellow)'>every value is null, return null</span>.

> [!example] Set all null values in a column to 0
> ```SQL
> SELECT column1, column2,
> 	COALESCE(column2, 0) AS col2 -- For each row if column 2 is NULL, set col2 to be 0--
> FROM example
> WHERE column2 IS NULL;
> ```

> Take note that <b>order matters</b> for `COALESCE`.
## Extract

**Mainly for date domains**, we can <span style='color:var(--mk-color-yellow)'>retrieve part of a date</span> (*For example year*) from a date value.

> [!example] Get year from date of birth
> ```SQL
> SELECT EXTRACT(YEAR FROM dob) AS dob_year,
> FROM customer
> ```

> [!important] If you want to compare dates you can just use conditions
> ```SQL
> SELECT a.date
> FROM table a
> WHERE a.date < 2000 -- Date format is YYYY-MM-DD, follow the format to be more precise
> ```
## Counting

We can **count the number of rows** within a table.

To count everything use `COUNT(*)`, but to <span style='color:var(--mk-color-orange)'>eliminate null values</span>, use `COUNT(column)`.

There are other operations to return <span style='color:var(--mk-color-orange)'>specific statistics</span>:
- `AVG(column)`
- `MIN(column)`
- `MAX(column)`
- `STDDEV(column)`
# Logic & Null
---
To prove that our query is retrieving what we want we will have to <span style='color:var(--mk-color-orange)'>prove it through logical reasoning</span>.

> [!summary] Recap on discrete mathematics
> > [!seealso] De Morgan's Law
> $\lnot(p \land q) \equiv \lnot p \lor \lnot q$ **OR** $\lnot(p \lor q) \equiv \lnot p \land \lnot q$
> 
> > [!seealso] Implication Law
> $p \rightarrow q \equiv \lnot p \lor q$ **OR**  $\lnot(p \rightarrow q) \equiv  p \land \lnot q$
> 
> > These are known as [[Year 1/Sem 1/CS1231S - Discrete Structures/Propositional Logic#Logical Equivalences|logic equivalences]].

Most conditional **operations involving Null** will result in SQL <span style='color:var(--mk-color-yellow)'>returning Null</span>. This is because <span style='color:var(--mk-color-yellow)'>Null can be any value</span>, it is just unknown at the moment.

> [!example] Weird behaviour involving null
> Lets assume we have a table with <b><span style='color: var(--mk-color-green)'>no NULL values</span></b>. And we have this condition `WHERE column <> NULL`.
> 
> Then the <span style='color:var(--mk-color-red)'>result will return nothing</span>, even though we know it is true for all rows.
> 
> Use `IS NULL` /  `IS DISTINCT FROM NULL` or `IS NOT NULL` to **retrieve null / not null values**.
## Truth Table

Below shows the truth table, **inclusive of null values**.

![[Truth Table with NULL Values.png|center]]


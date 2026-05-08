---
title: Creating and Populating Tables with Constraints
Date Created: 2025-01-13
Last Updated: 2025-09-28
tags:
  - CS2102
  - Database
  - SQLQueries
---
# Database Management System
---
Or <span style='color:var(--mk-color-turquoise)'>DBMS</span> for short is **in charge of** <span style='color:var(--mk-color-yellow)'>manipulation</span>, <span style='color:var(--mk-color-yellow)'>querying</span> and <span style='color:var(--mk-color-yellow)'>controlling</span> of data.

> [!abstract] DB Architecture
> There are a few types of database architecture, some of these are:
> 
> 1. **Client-Server**
> A <b><span style='color: var(--mk-color-yellow)'>centralised server</span></b> which manages the control and distribution of data to devices connected to it.
> 
> 2. **Three-Tier**
> It consist of 3 distinct tiers; <span style='color:var(--mk-color-orange)'>clients</span>, <span style='color:var(--mk-color-orange)'>application</span> server and <span style='color:var(--mk-color-orange)'>database server</span>. The clients connect to the <span style='color:var(--mk-color-yellow)'>application server</span> which <b><span style='color: var(--mk-color-yellow)'>restricts what they are allowed to do</span></b> on the database. In addition, the **database server is connected to tons of storages** which <span style='color:var(--mk-color-yellow)'>can be expanded</span>.
## Relational Model

Most DBMS <b>follows the relational model</b>, thus some refer to them as <span style='color:var(--mk-color-turquoise)'>RDBMS</span>.

A database will **consist of 2 components**, a <span style='color:var(--mk-color-orange)'>table</span> and <span style='color:var(--mk-color-orange)'>fields</span>.

> [!info] Tables 
> Data is **organised into tables**, where it is <span style='color:var(--mk-color-yellow)'>comprised of rows</span> (*data entry / records*) and <span style='color:var(--mk-color-yellow)'>columns</span> (*fields*).
> 
> Tables are <b><span style='color: var(--mk-color-yellow)'>multi-sets</span></b> (*Bags*) and <span style='color:var(--mk-color-red)'>not lists or sets</span> as they <span style='color:var(--mk-color-green)'>allow diplicates</span>.

> [!info] Fields
> Each field has its own <span style='color:var(--mk-color-yellow)'>name</span> and <span style='color:var(--mk-color-yellow)'>implicit position</span> (*Order during creation*). More importantly they have a <b><span style='color: var(--mk-color-yellow)'>domain</span></b> which <span style='color:var(--mk-color-yellow)'>represents the data type</span>.
> 
> > `NULL` is a special value for each domain or you can say it is <span style='color:var(--mk-color-yellow)'>universal to all types</span>. And <span style='color:var(--mk-color-red)'>should be avoided</span> as much as possible in the database.
# Table Creation
---
It is good to **impose structural constraints**, ensuring that a <span style='color:var(--mk-color-yellow)'>table captures necessary data</span>. This allows a <span style='color:var(--mk-color-green)'>better understanding of the database schema</span>.

The key word to **create** a table in <span style='color:var(--mk-color-purple)'>postgresql</span> is `CREATE TABLE`.

**Example:**
```sql
CREATE TABLE table_name (
	field_1 VARCHAR(64) PRIMARY KEY, -- CHAR can be used for a fixed length character and string uses ' ' not " "--
	field_2 NUMERIC UNIQUE /* This is a floating point, use INTEGER for non floating */
		CHECK (field_2 > 0),
	field_3 DATE NOT NULL -- The format is in YYYY-MM-DD --
		DEFAULT '2001-01-01'
);
```

> [!attention] Deleting Tables
> The key word to **delete** a table in <span style='color:var(--mk-color-purple)'>postgresql</span> is `DROP TABLE`.
> 
> Do note that there is a difference with `DELETE FROM`. This <b><span style='color: var(--mk-color-red)'>deletes the content but not the table</span></b>.

When **specifying domains** try and <span style='color:var(--mk-color-yellow)'>be as precise as possible</span>, for example do not use floating points for fields that only has whole numbers.
## Constraints

At any point, the database <b><span style='color: var(--mk-color-green)'>has to be in a consistent state</span></b>. And this is based on the <span style='color:var(--mk-color-yellow)'>structural</span> and <span style='color:var(--mk-color-yellow)'>integrity constraints</span> of the schema.

At **any point** if the <span style='color:var(--mk-color-red)'>constraint is voilated</span>, then the operation is <span style='color:var(--mk-color-yellow)'>aborted</span> and <span style='color:var(--mk-color-yellow)'>rolled back</span> to the initial state. It is <span style='color:var(--mk-color-yellow)'>better to defer </span>(*Check after the operation*) the checks as it is <span style='color:var(--mk-color-green)'>easier to handle</span>.


> [!info] ACID Properties
> Any DBMS must <span style='color:var(--mk-color-orange)'>ensure the following 4 properties</span>:
> 
> 1. **Atomicity** - Either an operation is executed successfully or nothing is done at all
> 2. **Consistency** - The database is in a valid state before and after each operation
> 3. **Isolation** - Each operation executes independently to prevent conflicts
> 4. **Durability** - Changes are permanent even in the event of a system failure

> [!tldr] Table vs Column Constraint
> **Both can achieve the same result**, however: 
> 
> <span style='color:var(--mk-color-orange)'>Column constraint</span> is only <span style='color:var(--mk-color-yellow)'>applied to the specified column</span>. It is defined after the domain of a variable.
> 
> <span style='color:var(--mk-color-orange)'>Table constraint</span> is <span style='color:var(--mk-color-yellow)'>applied to one or more columns</span> in the table. It is defined below the last variable in the table.

> [!check] Play the Devil's Advocate
> Given that you designed a database schema with some constraints. It is always <span style='color:var(--mk-color-green)'>good to find a series of operations which can causes volations</span>.
> 
> This is a **good practice to find faults** in the schema and correct it to <span style='color:var(--mk-color-yellow)'>prevent unwanted database states</span>.

> [!info] `DEFERRED`
> We can set the database to **check the validity** of the constraints of a table <span style='color:var(--mk-color-yellow)'>before or after</span> a transaction.
> 
> We can do the following`SET CONSTRAINTS ALL DEFERRED / IMMEDIATE ;` By <span style='color:var(--mk-color-yellow)'>default, it is immediate</span>, which checks before execution. While deferred checks after the transaction.
### Primary Key

It defines a set of columns which <span style='color:var(--mk-color-yellow)'>uniquely identify each record</span>. And <b>1 table is only allows to have 1 primary key</b>.

> [!note] Properties of a Primary Key
> A primary key has <span style='color:var(--mk-color-orange)'>2 properties</span>, they are:
> 1. **Unique** (*Cannot have duplicate values*)
> 2. **Not Null** (*Cannot contain NULL values*)

To apply a primary key constraint to multiple columns, use a <span style='color:var(--mk-color-turquoise)'>composite primary key</span>, which must be <b>declared as a table constraint</b>. In this case a table <span style='color:var(--mk-color-red)'>cannot have two records with the same combination</span> of values.
### Not NULL

It specifies that the <span style='color:var(--mk-color-yellow)'>column cannot have</span> a `NULL` value. This is usually <b>declared as a column constraint</b>.

> [!tldr] Implicit & Explicit NULL
> There are 2 ways to insert null values, either <span style='color:var(--mk-color-orange)'>implicitly</span> or <span style='color:var(--mk-color-orange)'>explicitly</span>.
> 
> For example, we have a table called games with 3 variables, name, version & price.
> 
> **Implicit**:  `INSERT INTO games (name, version) VALUES ('Aerified2', '1.0');`
> 
> **Explicit**: `INSERT INTO games VALUES ('Aerified2', '1.0', NULL);`
### Default

It specifies the <span style='color:var(--mk-color-yellow)'>default value</span> for a particular column in the event it is not provided. This is usually <b>declared as a column constraint</b>.

> By **adding a default constraint**, <span style='color:var(--mk-color-green)'>implicit NULLs are accepted</span> but <span style='color:var(--mk-color-red)'>explicit NULLs are still rejected</span>.
### Unique

It is a constraint that <span style='color:var(--mk-color-yellow)'>no 2 records can have the same value</span> for that specified column. It can be **both a column or a table constraint**.

But for a <span style='color:var(--mk-color-orange)'>table constraint</span> there <span style='color:var(--mk-color-yellow)'>cannot be 2 records with the same combination </span>of values instead.

> A `NULL` value is **treated as a unique value**.
### Foreign Key

It acts as a <span style='color:var(--mk-color-yellow)'>reference to another record in another table</span>. It **checks if a record weather this value exist in another table** before adding it. With this it <span style='color:var(--mk-color-green)'>prevents deletion and updating of values</span>.

The keyword `FOREIGN KEY` is usually used with `REFERENCE` as a <b>table constraint</b>. But you can declare as a <b>column constraint</b> only by just using the `REFERENCE` keyword.

**Example:**
```SQL
CREATE TABLE downloads (
	customerid VARCHAR(16)
		REFERENCES customers (customerid),
	name VARCHAR(32),
	version CHAR(3),
	FOREIGN KEY (name, version)
		REFERENCES games (name, version)
);
```

>The **referenced column** must be a <b>primary key</b> or <b>composite primary key</b>.

> [!attention] Foreign Key & NULL
> With **multiple references**, each of them are <span style='color:var(--mk-color-yellow)'>checked independently</span>. And <span style='color:var(--mk-color-green)'>all constraints must be satisfied</span>.
> 
> If we were to **insert a null value for a foreign key attribute**, it will <b><span style='color: var(--mk-color-red)'>omit the check</span></b> for that reference set.
> 
> Thus we can <span style='color:var(--mk-color-red)'>insert null values</span>, to **prevent this** and a good practice is to add the `NOT NULL` constraint.

> [!abstract] Allowing Deletion & Updating
> To bypass this restriction, we can use the keywords `ON UPDATE/DELETE` and then an option `CASCADE`.
> 
> This will <span style='color:var(--mk-color-yellow)'>automatically update</span> the values of foreign keys upon deletion or updating in the referenced table. Be cautious of this as it can <span style='color:var(--mk-color-red)'>cause a chain reation</span>.
> 
> There are <span style='color:var(--mk-color-orange)'>other options</span> as well:
> - `NO ACTION` (*Default*)
> - `SET DEFAULT`
> - `SET NULL`
### Check

It <span style='color:var(--mk-color-yellow)'>enforces a condition</span> for a particular set of columns. It can be declared as **both a column or table constraint**. But it is preferred to be declared as a table constraint.

The keyword is `CHECK` followed by a constraint (*A Boolean expression*). If any **operation violates this check**, then it will be <span style='color:var(--mk-color-red)'>aborted</span> and <span style='color:var(--mk-color-red)'>rolled back</span>.
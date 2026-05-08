---
title: Relational Databases
Date Created: 2025-09-04
Last Updated: 2025-09-28
tags:
  - CS4225
  - Database/RelationalDatabase
---
# Introduction to Relational Databases
---
In a relational database it is comprised of **table**.

Each <b><span style='color:var(--mk-color-yellow)'>table represents a relation</span></b>. Which is just a collection of tuples or rows.

And each <b><span style='color:var(--mk-color-yellow)'>tuple consists of multiple fields</span></b>.
## Types of Relationships

There are 3 types of relationships between tables:
1) **Many-to-many**
2) **One-to-many**
3) **One-to-one**

>[!tldr] One-to-many
>If **1 value in a column exists multiple times in another table** then it is a one-to-many relationship. 

>[!tldr] Many-to-many
>If **1 value in a column exists multiple times in both tables** then it is a many-to-many relationship. 
## Star Schema

![[DB Star Schema Example.png|center|500]]

A <b><span style='color:var(--mk-color-turquoise)'>star schema</span></b> consist of **2 types of tables**:
1) **Fact table** (*at the center*)
2) **Dimension tables**

This <b><span style='color:var(--mk-color-yellow)'>fact table will store quantitative data</span></b>, things that you want to analyse. It will also contain [[Creating and Populating Tables with Constraints#Foreign Key|foreign keys]] linked to dimension tables.

While the <b><span style='color:var(--mk-color-yellow)'>dimension tables stores descriptive attributes</span></b>, things that give context to a row in the fact table.
<div style="page-break-after: always;"></div>

# Queries in MapReduce
---
## Projection in MapReduce

>[!info] Projection
>
>A [[Relational Algebra#Projection|projection]] is essentially <b><span style='color:var(--mk-color-yellow)'>removing fields from a tuple</span></b> to create a new tuple.
>
>An example query will be `SELECT Name, Age FROM People`.

We can translate this projection as a **map function**:
```python
def map(key, tuple):
	""" Remove the fields of the tuple not in the projection set"""
	emit tuple
```

From the function body, this is a <b><span style='color:var(--mk-color-yellow)'>map-only job</span></b>, there is **no reducer needed** as the final output will be directly used.

>[!success] Very efficient as there is no shuffle stage
>
>The output from the map function is our final output.
## Selection in MapReduce

>[!info] Selection
>
>A [[Relational Algebra#Select|selection]] is essentially <b><span style='color:var(--mk-color-yellow)'>filtering out rows</span></b> based on a condition.
>
>An example query will be `SELECT Name, Age FROM People WHERE Age > 30`.

We can translate this projection as a **map function**:
```python
def map(key, tuple):
	if ("""tuple satisfies predicate"""): # The predicate is our condition
		emit tuple
```

From the function body, this is a <b><span style='color:var(--mk-color-yellow)'>map-only job</span></b>, there is **no reducer needed**.
## Aggregation in MapReduce

>[!info] Aggregation
>
>A [[Aggregation & Algebraic Queries#Aggregate Queries|aggregation]] is essentially <b><span style='color:var(--mk-color-yellow)'>combining a bunch of value into 1</span></b>.
>
>An example query will be `SELECT product_id, AVG(price) FROM sales GROUP BY product_id`.

With aggregation it is more complicated in a sense that now we might require a combiner. Lets take the query as an example `SELECT product_id, AVG(price) FROM sales GROUP BY product_id`.

Our **map & combiner** functions are:
```python
def map(key, tuple):
	emit (tuple.product_id, tuple.price)

def reduce(key, list_of_values):
	emit (key, average(list_of_values)) # The average will be computed here
```

The **key** will be based on what the <b><span style='color:var(--mk-color-yellow)'>query is bring grouped by</span></b>.

>[!note] We can optimise this query with combiners
## Relational Joins in MapReduce

>[!info] Aggregation
>
>A [[Queries#Table Joining|table join]] is essentially <b><span style='color:var(--mk-color-yellow)'>combining the data of 2 tables into 1</span></b>.
>
>These will be your `INNER JOIN`, `OUTER JOIN`, etc.
### Broadcast Join

>[!info] Also known as "Map" Join

![[Broadcast Join Example.png|center|500]]

The idea is that if we have a <b><span style='color:var(--mk-color-yellow)'>small table, copy it into every mapper</span></b>, which will be used when mapping the big table.

>[!note] There is no shuffling involved

For efficiency the <b><span style='color:var(--mk-color-green)'>table will be converted into a hash table</span></b>, so that it will be a simple lookup when mapping.

So it will just take the key we are trying to merge in the big table and then do a <b><span style='color: var(--mk-color-yellow)'>lookup in this hash table and then iterate through the values for that key</span></b>.

>[!important] This small table must be able to fit into memory
### Reduce-Side Join

>[!info] Also known as "Common" Join

![[Reduce-Side Join Example.png|center|500]]

Unlike broadcast join, this <b><span style='color:var(--mk-color-green)'>does not require the dataset to fit in memory</span></b>. However <b><span style='color:var(--mk-color-red)'>it will be slower</span></b>.

Here <b><span style='color:var(--mk-color-yellow)'>2 sets of mappers will operation on 1 table each</span></b>, emitting records with the key as the variable to join by and the value will be the rest of the values.

>[!note] This tuple emitted from `map` can contain a secondary key which is just the table identifier like name

We can then use a [[MapReduce#Secondary Sort|secondary sort]], to ensure that all keys from a table (`X`) <b><span style='color:var(--mk-color-yellow)'>arrive before the other</span></b> (`Y`) (*Basically sort by table X first then Y).

Then all values from table `X` will be <b><span style='color:var(--mk-color-yellow)'>stored in memory</span></b>, then <b><span style='color:var(--mk-color-yellow)'>cross them</span></b> (*cross product*) with values from table `Y`.

>[!success] It takes up less memory as we only hold a single key in memory

>[!info] Secondary sort is an optional optimisation
>
>It benefits in one-to-many joins.


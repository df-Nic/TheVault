---
title: Triggers
Date Created: 2025-03-18
Last Updated: 2025-09-28
tags:
  - CS2102
  - Database
  - SQL
---
# Triggers
---
We can use triggers to <b><span style='color:var(--mk-color-yellow)'>handle complex constraints</span></b> which we [[Creating and Populating Tables with Constraints#Constraints|previously cannot handle]].

However, unlike functions, triggers are an <b><span style='color:var(--mk-color-yellow)'>event condition action</span></b> and they consist of <span style='color:var(--mk-color-orange)'>2 parts</span>:
1) **Trigger**
2) **Trigger function**

![[Trigger Activity Flow.svg|center]]

## Trigger

We can treat a **trigger** as a <b><span style='color:var(--mk-color-yellow)'>listener which calls some function</span></b>.

The **general format** for a trigger is:
```SQL
CREATE TRIGGER <trigger_name>
<event to trigger the function> OR <another event> OR ... ON <existing_table>
<granularity> EXECUTE FUNCTION <function_name>();
```


> [!example] Example of a trigger
> ```SQL
> CREATE TRIGGER score_log -- name of the trigger
> AFTER INSERT OR UPDATE ON Scores -- Some existing table
> FOR EACH ROW EXECUTE FUNCTION
> 	log_score(); -- This is the trigger function name
> ```

<span style='color:var(--mk-color-orange)'>Types of events</span>:
- `INSERT ON table`
- `DELETE ON table`
- `UPDATE [of column] on table`

And with these events we will <span style='color:var(--mk-color-orange)'>include a timing</span> (*`<timing> <event>`*):
- `AFTER`
- `BEFORE`
- `INSTEAD OF`, it can only be defined on [[Nested Queries#Copying a Table|views]]

> [!note] When to use `INSTEAD OF`
> When we do `INSERT` or `DELETE` or `UPDATE` on  a view it will update the original table instead.
> 
> So sometimes we do not want to do thus thus we use a trigger and do `UPDATE table SET ...`. 
> 

![[Return Value Effect for Triggers.svg|center]]

We can have **multiple triggers of the same event for the same table**, thus there will be some <span style='color:var(--mk-color-orange)'>order of activation</span>:
1) `BEFORE` statement-level triggers
2) `BEFORE` row-level triggers
3) `AFTER` row-level triggers
4) `AFTER` statement-level triggers

With in **each of the categories** above, the triggers are <b><span style='color:var(--mk-color-yellow)'>activated in alphabetical order</span></b>.

And if, the `BEFORE` row-level trigger returns `NULL`, the <b><span style='color:var(--mk-color-yellow)'>subsequent triggers of the same row are omitted</span></b>.

And for <span style='color:var(--mk-color-orange)'>granularity</span>:
- `FOR EACH ROW`, triggers the function for rows that were <b><span style='color:var(--mk-color-yellow)'>modified</span></b>
- `FOR EACH STATEMENT`, the <b><span style='color:var(--mk-color-yellow)'>statement that performs the modification</span></b>, trigger function only once

The `FOR EACH STATEMENT` is also known as <b><span style='color:var(--mk-color-turquoise)'>statement level</span></b> trigger and only for this <b>no matter what the event is, returning null will still perform the query</b>.

![[Granularity & Timing.svg|center]]

> [!question] Why execute the function only once?
> - Some times we just want to <b><span style='color:var(--mk-color-yellow)'>prevent an operation from happening</span></b> (`RAISE EXCEPTION`), thus triggering once is enough
> - There are other contextual data available
## Trigger Function

Similar to [[Stored Procedures#SQL Functions & Procedures|functions]], but the return is now `TRIGGER`.

In addition, there are <span style='color:var(--mk-color-orange)'>trigger specific variables</span>:
- `NEW`, the row after the event triggered the function (*if we are deleting NEW is null*)
- `OLD`, the row before the event trigged the function (*if we are inserting OLD is null*)
- `TG_OP`, the operation that caused the trigger function to execute, like insert, delete
- `TG_TABLE_NAME`, the name of the table that the trigger is attached to

> [!important] We can overwrite `OLD` and `NEW` variables using the dot notation

> [!example] Example of a trigger function
> ```SQL
> CREATE OR REPLACE FUNCTION log_score()
> RETURNS TRIGGER AS $$
> BEGIN
> 	INSERT INTO Scores_Log
> 		VALUES (NEW.Name, CURRENT_DATE);
> 	RETURN NULL; -- You can also return an object to insert  or update like RETURN (NEW.Name, CURRENT_DATE)
> END;
> $$ LANGUAGE plpgsql;
> ```
## Trigger Conditions

We can move the **conditions** from inside the trigger function to the <span style='color:var(--mk-color-yellow)'>trigger definition</span>. In general the conditions will be **based on** what is in the `WHERE` clause, which <b><span style='color:var(--mk-color-yellow)'>must return a Boolean</span></b>.

However there are <span style='color:var(--mk-color-orange)'>some subjections</span> to this:
- <b><span style='color:var(--mk-color-red)'>No</span></b> `SELECT` in `WHEN()`
- <b><span style='color:var(--mk-color-red)'>No</span></b> `OLD` in `WHEN()` for inserting
- <b><span style='color:var(--mk-color-red)'>No</span></b> `NEW` in `WHEN()` for deleting
- <b><span style='color:var(--mk-color-red)'>No</span></b> `SELECT` for `INSTEAD OF`

> [!example] Example of a condition in a trigger definition
> ```SQL
> CREATE TRIGGER adi_should_get_full_mark
> BEFORE INSERT ON Scores
> FOR EACH ROW WHEN (NEW.Name = 'Adi')
> EXECUTE FUNCTION give_adi_full_mark();
> ```
### Deferred Trigger

Triggers happen at the end of either the statement or transaction. **Operations consisting of multiple statements** may leave the database in an <b><span style='color:var(--mk-color-red)'>intermediate inconsistent state</span></b>.

We want some sort of <b><span style='color:var(--mk-color-yellow)'>state validity check and a rollback</span></b>, this is known as a <b><span style='color:var(--mk-color-turquoise)'>deferred trigger</span></b>.

We will need to include these <span style='color:var(--mk-color-orange)'>keywords</span>:
- `CONSTRAINT`
- `DEFFERRABLE`
- `INTITALLY DEFERRED` (*check at the end of the transaction*) or `INITIALLY IMMEDIATE`, the default value

`INITIALLY IMMEDIATE` <b><span style='color:var(--mk-color-yellow)'>checks immediately after every transaction even if we group them together</span></b>, we can override this by doing `SET CONSTRAINTS <trigger_name> DEFERRED` followed by our SQL statements.

In addition, they <b>can only work with</b>, `AFTER` and `FOR EACH ROW` and no other.

> [!example] Example of a deferred trigger 
> ```SQL
> CREATE CONSTRAINT TRIGGER balance_check
> AFTER INSERT OR UPDATE OR DELETE ON Account
> DEFERRABLE INITIALLY DEFERRED -- This is to defer the check
> FOR EACH ROW EXECUTE FUNCTION check_balance();
> ```

As mentioned before to roll back we just need to use `RAISE EXCEPTION '< Message >'`, which when executes <b><span style='color:var(--mk-color-yellow)'>roll's back all queries</span></b>.

We can **combine multiple queries / transactions** for the <b><span style='color:var(--mk-color-yellow)'>trigger to check after everything has been completed</span></b>, we can do so by encasing the queries with `BEGIN TRANSACTION` and `COMMIT`.

> [!example] To combine the transactions
> ```SQL
> BEGIN TRANSACTION;
> UPDATE Account SET Balance = Balance – Amount WHERE AID = Account1;
> UPDATE Account SET Balance = Balance + Amount WHERE AID = Account2;
> COMMIT;
> ```

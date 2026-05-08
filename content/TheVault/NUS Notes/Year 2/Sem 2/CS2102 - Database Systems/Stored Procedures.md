---
title: Stored Procedures
Date Created: 2025-03-11
Last Updated: 2025-09-28
tags:
  - CS2102
  - Database
  - SQL
---
# SQL Queries Through Applications
---
Typically the <b><span style='color:var(--mk-color-yellow)'>applications developed will generate the SQL statement</span></b> instead of the users directly writing it.

A <b><span style='color:var(--mk-color-orange)'>typical flow</span></b> is, code queries in application language $\rightarrow$  application will capture input $\rightarrow$ generate the SQL statement based on the inputs $\rightarrow$ send SQL query to DB and retrieve data.

> [!question] Why ask the application to generate the SQL?
> - **Security** reasons
> - **Information hiding** principle (*do not want to expose the database to the user*)

There are <span style='color:var(--mk-color-orange)'>2 types of SQL queries</span> that can be generated:
1) **Static** - The queries are <b><span style='color:var(--mk-color-yellow)'>fixed</span></b> (*coded in manually*)
2) **Dynamic** - The queries are <b><span style='color:var(--mk-color-yellow)'>generated during run time</span></b>

> [!warning] Issues with dynamic SQL statements
> Through they <b><span style='color:var(--mk-color-green)'>provide flexibility</span></b> it has its <span style='color:var(--mk-color-orange)'>shortcomings</span>:
> - <b><span style='color:var(--mk-color-red)'>Security</span></b>
> - <b><span style='color:var(--mk-color-red)'>Performance</span></b> - Each **query is independent** and thus the database will need to parse, plan and execute for every single query

A solution to the issues of dynamic SQL is to use <b><span style='color:var(--mk-color-turquoise)'>prepared SQL</span></b> a **type of dynamic SQL**. It is just an SQL query which is <b><span style='color:var(--mk-color-yellow)'>prepared only once</span></b> (*parsed & planned only once*).

> [!example] Example of a prepared SQL
> ``` C
> EXEC SQL BEGIN DECLARE SECTION;
> 	const char *query = "INSERT INTO test VALUES(?, ?);"; // ? are place holders
> 	
> EXEC SQL END DECLARE SECTION;
> 
> EXEC SQL CONNECT @localhost USER john;
> 
> EXEC SQL PREPARE stmt FROM :query; // Parse, compiled by the DB only once
> 
> EXEC SQL EXECUTE stmt USING 42, 'foobar'; // What value to use for the placeholders
> 
> EXEC SQL DEALLOCATE PREPARE stmt; // Always deallocate when not needed
> 
> EXEC SQL DISCONNECT;
>```

## Statement-Level Interface

![[Statement-Level Interface Idea.png|center]]

We **embed** the SQL query based on the <b><span style='color:var(--mk-color-yellow)'>host's language</span></b> (*what language they used to code*).

This query will <b><span style='color:var(--mk-color-red)'>not be understood</span></b> by the compiler and thus we need to **preprocess** the <b><span style='color:var(--mk-color-yellow)'>query into function calls</span></b> which calls the SQL library (*preprocessor*).

> [!note] Preprocessing in C
> In <span style='color:var(--mk-color-purple)'>C</span>, to **indicate a statement to be processed** we will use the keyword `EXEC SQL <Statement>`.

Finally we can just compile the code as per normal.
### Connecting to the Database

Before we can execute a query we need to **connect to the database**, we can do it as such and we need to specify the username `EXEC SQL CONNECT @localhost USER <user name>`.

After we are done we need to **disconnect** the database <b><span style='color:var(--mk-color-yellow)'>to release the resources</span></b>, `EXEC SQL DISCONNECT`.
### Declaring Variables

We can declare variables to be used in our queries, however these <b><span style='color:var(--mk-color-yellow)'>variables are shared between the host language and SQL</span></b>.

We can do so by using `EXEC SQL BEGIN DECLARE SECTION;` and ending with `EXEC SQL END DECLARE SECTION;`.

These variables during execution acts like a regular C variable, but when executing the query, the library will convert to the corresponding SQL type.

> [!example] Example of declaring variables
> ``` C
> EXEC SQL BEGIN DECLARE SECTION; // Declare variables here
> 	char supplier[30], product[30];
> 	float price;
> EXEC SQL END DECLARE SECTION;
> 
> EXEC SQL CONNECT @localhost USER john;
> // some code that assigns values to supplier, product and price
> 
> EXEC SQL INSERT INTO
> 	Sells (supplName, prodName, price)
> 	VALUES (:supplier, :product, :price); // We do :variable_name to denote using the shared variable 
> 
> EXEC SQL DISCONNECT;
> ```
### Cursors

Usually a query will return a list of results, and a <b><span style='color:var(--mk-color-yellow)'>program will want to process the results row by row</span></b>.

This is where <b><span style='color:var(--mk-color-turquoise)'>cursors</span></b> come in, it <b><span style='color:var(--mk-color-yellow)'>acts as a pointer</span></b> which allows the program to iterate through row by row.

To set a cursor we can do the following `EXEC SQL DECLARE <cursor_name> CURSOR FOR <SQL_statement>`.

> [!example] Example of using a cursor
> ``` C
> // declare variable, connect to database
> // Declare cursor
> EXEC SQL DECLARE cursor CURSOR FOR
> SELECT prodName FROM Sells WHERE supplName = :supplier; // SQL query to execute
> 
> // Open cursor
> EXEC SQL OPEN cursor;
> EXEC SQL WHENEVER NOT FOUND DO BREAK; // If there is no more rows, break the for loop
> 
> for(;;){
> 	EXEC SQL FETCH NEXT FROM cursor INTO :v_product; // Store the data into a variable
> 	printf(">>> product: %s\n", v_product);
> }
> 
> EXEC SQL CLOSE cursor;
> // Disconnect from the database
> ```

> [!info] Client side buffer
> Some databases will limit the number of queries shown, this is known as the **client side buffer**.
> 
> Essentially the database will <b><span style='color:var(--mk-color-yellow)'>fetch the data until the local buffer is full</span></b>. After <b><span style='color:var(--mk-color-yellow)'>iterating through all the data</span></b> with the cursor then it will **fetch the remaining data**.
> 
> If the **buffer size is too large**, it may cause <b><span style='color:var(--mk-color-red)'>unresponsiveness</span></b> depending on the query size.

## Call-Level Interface

![[Call-Level Interface Idea.png|center]]

Instead of writing SQL, we mainly <b><span style='color:var(--mk-color-yellow)'>write everything in the host language</span></b>. Just call the correct functions from the library and it will handle the execution of the SQL query.

> [!example] Some examples of database libraries
> - Java database connectivity (*JDBC*)
> - Open database connectivity (*ODBS*)
> - `psycopg` for <span style='color:var(--mk-color-purple)'>Python</span>


> [!example] Example using the python library `psycopg`
> ``` Python
> import psycopg # Host language library
> product = "some product"
> 
> # Connect to database
> conn = psycopy.connect("host=...")
> 
> # Create cursor
> cursor = conn.cursor()
> 
> # Execute Parameterized Statement
> cursor.execute("SELECT supplName from Sells where prodName = %s", (product,))
> while True:
> 	row = cursor.fetchone()
> 	if row is None:
> 		break
> 	print(f">>> Supplier: {row[0]})
> # Cleanup
> cursor.close()
> conn.commit()
> conn.close()
> ```
# SQL Functions & Procedures
---
For complex tasks with multiple queries, it is <b><span style='color:var(--mk-color-red)'>not efficient</span></b> if we **send the queries from the application to the DB**.

In addition is is <b><span style='color:var(--mk-color-red)'>not modifiable</span></b> as if requirements change, we need to **update the application code** + **redeploy to all users**.

Thus it is better if we <b><span style='color:var(--mk-color-yellow)'>create a function inside the database</span></b> (*in SQL-based procedure language*) which the application just calls.

> [!success] Advantages of using SQL-based procedure language
> - **Reusable**
> - **Ease of maintenance** (*update the function and it will update for all applications*)
> - **Performance**
> - **Security**

To <span style='color:var(--mk-color-orange)'>write the a function</span> in SQL, we will use the following syntax:

``` SQL
CREATE OR REPLACE FUNCTION <function name>
	(<param> <type>, ...) -- Parameters
RETURNS <return type> AS $$ -- Denote return type
	<code> -- The main body function / SQL code
$$ LANGUAGE <language> -- Language used by the code
```

Parameters can be **either** `IN` for input (`IN val int`) and `OUT` for output, (`OUT val int`).

> [!success] Advantages of using SQL functions
> - **Abstractions**
> - Query **simplification**
> - **Reusability**
> - **Easy maintenance**

Here are some return types which will be used:
- Returning **1 row and all columns**, use `table_name`
- Return **multiple rows and all columns** use `SETOF table_name`
- Return a **new table** use `RECORD` and the arguments will need to have $n$ columns of `OUT col_name type`
	- If there is **more than 1 row** we need to use `SETOF RECORD`
	- Or we can use `TABLE` like `TABLE (Mark INT, Count INT)` but then our **arguments will be empty**
- Return nothing then use `VOID` or we can change `FUNCTION`to `PROCEDURE` as a <b><span style='color:var(--mk-color-yellow)'>procedure has no return</span></b>.

> [!info] Procedures
> As mentioned a procedure has no return value, however this <b><span style='color:var(--mk-color-yellow)'>does not mean it cannot output anything</span></b>.
> 
> In the arguments we can specify an `OUT` which the procedure will store a value inside this output variable.
> 
> Another thing is that a procedure, it <b><span style='color:var(--mk-color-green)'>can commit or roll back</span></b> (*control whether to do the transaction or not*) but a <b><span style='color:var(--mk-color-red)'>function cannot</span></b>.
## Control Structures

Just like functions in programing languages we can have **control flow** and **assign variables** which we can do in SQL.
### Declaring Variables

To **declare a variable** we need to use the keyword `DECLARE`. We also need to **denote the start of the function body** by using `BEGIN` & `END`.

We can use <span style='color:var(--mk-color-orange)'>2 symbols</span>:
- `:=`: We can use this to assign to a variable, however if we <b><span style='color:var(--mk-color-yellow)'>want to assign to the ouput table we have to use this</span></b>.
- `=`: We can use this to assign to a variable

> If we are using a select statement do `SELECT < Col > INTO variable From ...`.

> [!example] Example of declaring and using a variable
> ``` SQL
> CREATE OR REPLACE FUNCTION swap(INOUT val1 INT, INOUT val2 INT) -- INOUT means input & output
> RETURNS RECORD AS $$
> DECLARE
> 	temp INT; -- Declare our variables here
> BEGIN
> 	temp := val1;
> 	val1 := val2;
> 	val2 := temp;
> END;
> $$ LANGUAGE plpgsql; -- Posegre procedural SQL
> ```
### Conditionals

We can also include `IF`, `ELSIF` & `ELSE` statements to denote a decision.

> [!example] Example of declaring and using a if statement
> ``` SQL
> CREATE OR REPLACE FUNCTION sort(INOUT val1 INT, INOUT val2 INT)
> RETURNS RECORD AS $$
> DECLARE
> 	temp INT;
> BEGIN
> 	IF val1 > val2 THEN
> 		temp := val1;
> 		val1 := val2;
> 		val2 := temp;
> 		-- Add ELSIF for if else
> 	END IF; -- Denote the end of the If statement
> END;
> $$ LANGUAGE plpgsql;
> ```
### Repetition

#### While Loops

We can also incorporate a `while` loop as such:

> [!example] Example of declaring and using repetition
> ``` SQL
> CREATE OR REPLACE FUNCTION sum_to_x(IN x INT)
> RETURNS INT AS $$
> DECLARE
> 	s INT; temp INT;
> BEGIN
> 	s := 0;
> 	temp := 1;
> LOOP
> 	EXIT WHEN temp > x; -- Exit clause
> 	s := s + temp; temp := temp + 1;
> 	END LOOP;
> END;
> $$ LANGUAGE plpgsql;
> ```

> [!warning] Using while loops in SQL
> Our `while` <b><span style='color:var(--mk-color-yellow)'>loop in SQL is a infinite loop</span></b> (`while (true)`). Thus it is important that we </b><span style='color:var(--mk-color-yellow)'>have a break clause</span></b> inside the loop.
#### For Loops

What if we want to do a `for` loop in some table, we can use the help of a [[Stored Procedures#Cursors|cursor]].

![[Cursor Workflow.png|center]]

> [!example] Example of using a cursor
> ``` SQL
> CREATE OR REPLACE FUNCTION score_gap()
> RETURNS TABLE(name_ TEXT, mark_ INT, gap INT) AS $$
> DECLARE
> 	curs CURSOR FOR (SELECT * FROM Scores ORDER BY Mark DESC);
> 	r RECORD; prev INT;
> BEGIN
> 	prev := -1; OPEN curs;
> 	LOOP
> 		FETCH curs INTO r; -- Send the value at curs into r
> 		EXIT WHEN NOT FOUND; -- Break the loop if the cursor is empty
> 		name_ := r.Name; mark_ := r.Mark; -- variable name cannot be the same as the column name
> 		IF prev >= 0 THEN gap := prev – mark_;
> 		ELSE gap := NULL;
> 		END IF; -- End of IF statement
> 		RETURN NEXT; -- Not returning from the function but basically going to the next line in return the table
> 		prev := r.Mark;
> 	END LOOP; -- End of loop statement
> 	CLOSE curs;
> END;
> $$ LANGUAGE plpgsql
> ```

When we do `FETCH curs INTO r` we are <b><span style='color:var(--mk-color-yellow)'>fetching the next row</span></b>. But there are many <span style='color:var(--mk-color-orange)'>other ways</span> to fetch data:
- `FETCH PRIOR FROM` - To fetch the previous row
- `FETCH FIRST FROM` - Fetch the first row
- `FETCH LAST FROM` - Fetch the last row
- `FETCH ABSOLUTE 3 FROM` - Fetch the 3rd row (*change to fetch from a specific row index*)

**Instead of using a cursor** we can just use `for`.

> [!example] Using a `for` loop instead
> ``` SQL
> CREATE OR REPLACE FUNCTION score_gap()
> RETURNS TABLE(name_ TEXT, mark_ INT, gap INT) AS $$
> DECLARE
> 	r RECORD; prev INT;
> BEGIN
> 	prev := -1;
> 	FOR r IN SELECT * FROM Scores ORDER BY Mark DESC -- Similart to python's for loop
> 	LOOP
> 		name_ := r.Name; mark_ := r.Mark;
> 		IF prev >= 0 THEN gap := prev – mark_;
> 		ELSE gap := NULL;
> 		END IF;
> 		RETURN NEXT;
> 		prev := r.Mark;
> 	END LOOP;
> END;
> $$ LANGUAGE plpgsql
> ```
# SQL Injection Attacks
---
These attacks usually happens when <b><span style='color:var(--mk-color-yellow)'>using dynamic SQL</span></b>. The idea is that the attacker will <b><span style='color:var(--mk-color-red)'>incorporate harmful SQL queries</span></b> which when combined will form a sequence of queries which the database will execute.

> [!question] How does this happen?
> The database <b><span style='color:var(--mk-color-red)'>cannot differentiate inputs from a SQL query</span></b> and thus will just execute whatever it was given.

One way is to **use prepared SQL queries**. When we do `EXEC SQL PREPARE`, we are compiling a query and the <b><span style='color:var(--mk-color-yellow)'>database will know there is a placeholder</span></b>. At runtime when we `EXEC SQL EXECUTE`, the argument will be treated as a <b><span style='color:var(--mk-color-yellow)'>input to the SQL and not part of the SQL statement</span></b>.

Another way is to use **stored functions / procedures**. Similarly to prepared SQL queries the parameters are clearly defined, and thus is treated as a <b><span style='color:var(--mk-color-yellow)'>input to the SQL and not part of the SQL statement</span></b>.


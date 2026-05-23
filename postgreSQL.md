# postgreSQL

- [postgreSQL](#postgresql)
  - [Some Useful Links](#some-useful-links)
  - [Creating, Listing, and Deleting Databases](#creating-listing-and-deleting-databases)
  - [Schemas](#schemas)
  - [Creating, Listing, and Deleting Tables](#creating-listing-and-deleting-tables)
  - [Data Types](#data-types)
  - [Constraints](#constraints)
  - [Inserting Data](#inserting-data)
  - [Importing and Exporting CSV](#importing-and-exporting-csv)
  - [Updating Data](#updating-data)
  - [Deleting Data](#deleting-data)
  - [Queries](#queries)
  - [Some Functions and Operators](#some-functions-and-operators)
  - [Subquery](#subquery)
    - [Subquery](#subquery-1)
    - [Correlated Subquery](#correlated-subquery)
    - [`WHERE IN` Subquery](#where-in-subquery)
    - [`EXISTS`](#exists)
    - [`ANY`](#any)
    - [`ALL`](#all)
  - [Common Table Expression (CTE)](#common-table-expression-cte)
    - [Recursive CTE](#recursive-cte)
  - [Views](#views)
    - [Creating a database view](#creating-a-database-view)
    - [Replacing a database view](#replacing-a-database-view)
    - [Dropping a database view](#dropping-a-database-view)
    - [Creating a materialized view](#creating-a-materialized-view)
    - [Dropping a materialized view](#dropping-a-materialized-view)
  - [Joins](#joins)
    - [Inner Join](#inner-join)
    - [Left Join](#left-join)
    - [Right Join](#right-join)
    - [Full Join](#full-join)
    - [Self-Join](#self-join)
    - [Cross Join](#cross-join)
    - [Natural Join](#natural-join)
    - [`USING`](#using)
  - [Conditional Expressions](#conditional-expressions)
    - [`CASE`](#case)
    - [`IF`](#if)
  - [Sequence](#sequence)
  - [Identity Column](#identity-column)
  - [`ALTER TABLE` Statement](#alter-table-statement)
    - [Renaming a table](#renaming-a-table)
    - [Renaming a column](#renaming-a-column)
    - [Adding new columns to a table](#adding-new-columns-to-a-table)
    - [Changing the column data type](#changing-the-column-data-type)
    - [Applying constraints to columns](#applying-constraints-to-columns)
    - [Dropping columns](#dropping-columns)
    - [Truncating a table](#truncating-a-table)
  - [PL/pgSQL Block and Variables](#plpgsql-block-and-variables)
  - [User-defined Functions](#user-defined-functions)
  - [Special Variable `FOUND`](#special-variable-found)
  - [Exception Handling](#exception-handling)
    - [`RAISE` Statement](#raise-statement)
  - [Stored Procedures](#stored-procedures)
  - [Indexes](#indexes)
    - [Creating an index](#creating-an-index)
    - [Analyzing an index](#analyzing-an-index)
    - [Listing indexes](#listing-indexes)
    - [Dropping an index](#dropping-an-index)
    - [Unique Index](#unique-index)
    - [Expression Index](#expression-index)
    - [Partial Index](#partial-index)
    - [Covering Index](#covering-index)
  - [Denormalized Data Types](#denormalized-data-types)
    - [Composite Types](#composite-types)
    - [`ARRAY` Data Type](#array-data-type)
    - [`XML` Data Type](#xml-data-type)
    - [`ENUM`](#enum)
    - [`RECORD`](#record)
    - [`JSON`](#json)
  - [Cast](#cast)
  - [Triggers](#triggers)
    - [Creating Triggers](#creating-triggers)
    - [Disabling and Enabling Triggers](#disabling-and-enabling-triggers)
    - [Dropping Triggers](#dropping-triggers)
    - [Event Triggers](#event-triggers)
  - [Window functions](#window-functions)
    - [Adding more data to practice window functions](#adding-more-data-to-practice-window-functions)
    - [Intro](#intro)
    - [`ROW_NUMBER()`](#row_number)
    - [`RANK()`](#rank)
    - [`DENSE_RANK()`](#dense_rank)
    - [`PERCENT_RANK()`](#percent_rank)
    - [`NTILE`](#ntile)
    - [`CUME_DIST`](#cume_dist)
    - [`FIRST_VALUE`](#first_value)
    - [`LAST_VALUE`](#last_value)
    - [`LEAD()`](#lead)
    - [`LAG()`](#lag)
    - [`NTH_VALUE ()`](#nth_value-)
    - [`MIN` Window Function](#min-window-function)
    - [`MAX` Window Function](#max-window-function)
    - [`AVG` Window Function](#avg-window-function)
    - [`COUNT` Window Function](#count-window-function)
    - [`SUM` Window Function](#sum-window-function)
  - [Loops](#loops)
    - [`LOOP`](#loop)
    - [`WHILE`](#while)
    - [`FOR`](#for)
    - [Terminating a loop using `EXIT`](#terminating-a-loop-using-exit)
    - [Skipping a loop using `CONTINUE`](#skipping-a-loop-using-continue)

<hr>

## Some Useful Links

- https://www.postgresql.org/
- https://www.pgtutorial.com/
- https://neon.com/postgresql/tutorial
- https://datalemur.com/sql-tutorial
- https://pgexercises.com/
- [FreeCodeCamp Video: Learn PostgreSQL Tutorial - Full Course for Beginners](https://www.youtube.com/watch?v=qw--VYLpxG4)
- [Video Playlist: PostgreSQL for Everybody](https://www.youtube.com/playlist?list=PLlRFEj9H3Oj7Oj3ndXmNS1FFOUyQP-gEa)

<hr>
<hr>

## Creating, Listing, and Deleting Databases

[Creating, Listing, and Deleting Databases](./PSQL_CreateListDelete.md)

<hr>
<hr>

## Schemas

[Schemas](./PSQL_Schemas.md)

<hr>
<hr>

## Creating, Listing, and Deleting Tables

[Creating, Listing, and Deleting Tables](./PSQL_CreateListDeleteTables.md)

<hr>
<hr>

## Data Types

[Data Types](./PSQL_DataTypes.md)

<hr>
<hr>

## Constraints

[Constraints](./PSQL_Constraints.md)

<hr>
<hr>

## Inserting Data

[Inserting Data](./PSQL_InsertingData.md)

<hr>
<hr>

## Importing and Exporting CSV

[Importing and Exporting CSV](./PSQL_ImportingExportingCSV.md)

<hr>
<hr>

## Updating Data

[Updating Data](./PSQL_UpdatingData.md)

<hr>
<hr>

## Deleting Data

[Deleting Data](./PSQL_DeletingData.md)

<hr>
<hr>

## Queries

[Queries](./PSQL_Queries.md)

<hr>
<hr>

## Some Functions and Operators

[Some Functions and Operators](./PSQL_SomeFuncsOps.md)

<hr>
<hr>

## Subquery

### Subquery

PostgreSQL allows us to embed a query within another query. This embedded query is called a _subquery_. The query that contains a subquery is called an _outer query_.

The subquery can be placed in different parts of the SQL code. It could be used with many keywords including `SELECT`, `FROM`, `WHERE`, and `JOIN` depending on what result the subquery returns.

Here is an example of a subquery in a `WHERE` clause:

```sql
SELECT * FROM transactions
WHERE price > (SELECT AVG(price) FROM transactions);
```

Here is an example of a subquery in a `SELECT` statement:

```sql
SELECT
  product_id,
  price,
  (SELECT MAX(price) FROM transactions) max_price
FROM
  transactions;
```

Here is an example of a subquery in a `FROM` clause:

```sql
SELECT amount
FROM (SELECT product_id, price, amount FROM transactions WHERE amount > price);
```

<hr>

### Correlated Subquery

A correlated subquery is a subquery that uses values from an outer query. Unlike a regular subquery that can execute independently, PostgreSQL may have to execute a correlated subquery for every row in the outer query. For this reason, you should avoid using the correlated subquery as much as possible to improve the query performance.

```sql
SELECT user_id, product_id FROM transactions t
WHERE user_id = (SELECT user_id FROM users u WHERE t.user_id = u.user_id);
```

Here is another example, where we find all users whose account balance is above the average account balance of users from the same country:

```sql
SELECT
	username,
	country,
	u1.account_balance
FROM users u1
WHERE account_balance > (
	SELECT AVG(account_balance) FROM users u2
	WHERE u1.country = u2.country
);
```

<hr>

### `WHERE IN` Subquery

The `WHERE ... IN` subquery allows you to check if a value is in a set of values returned by subquery.

```sql
SELECT username, country FROM users
WHERE user_id IN (SELECT user_id FROM transactions);
```

You can use the `NOT IN` operator to filter rows that are not in a list returned by a query.

```sql
SELECT username, country FROM users
WHERE user_id NOT IN (SELECT user_id FROM transactions);
```

<hr>

### `EXISTS`

The `EXISTS` operator returns `true` if the subquery returns any rows or `false` otherwise.

```sql
SELECT username FROM users u
WHERE EXISTS (
	SELECT 1 FROM transactions t
	WHERE u.user_id = t.user_id
);
```

To negate the result of the `EXISTS` operator, we use the `NOT` operator.

```sql
SELECT username FROM users u
WHERE NOT EXISTS (
	SELECT 1 FROM transactions t
	WHERE u.user_id = t.user_id
);
```

<hr>

### `ANY`

The `ANY` operator allows you to compare a value with a set of values returned by a subquery. The `ANY` operator returns true if the comparison returns true for at least one value in the set. The ANY operator returns false if all comparisons are false. If the subquery returns no row, the `ANY` operator always returns true.

In PostgreSQL, `SOME` and `ANY` are synonyms, so you can use them interchangeably.

```sql
SELECT username, account_balance,
FROM users
WHERE account_balance > ANY (
  SELECT price
  FROM transactions
);
```

<hr>

### `ALL`

The `ALL` operator allows you to compare a value with a set of values returned by a subquery. The `ALL` operator returns true if the comparison is true for all values in the set.

```sql
SELECT username, account_balance
FROM users
WHERE account_balance > ALL (
  SELECT price
  FROM transactions
);
```

<hr>
<hr>

## Common Table Expression (CTE)

CTE stands for common table expression. PostgreSQL CTE provides a way to define a temporary table that can be referenced within a `SELECT`, `INSERT`, `UPDATE`, `DELETE`, and `MERGE` statements.

Here’s the syntax for defining a CTE:

```sql
WITH cte_name(column_list) AS (
   -- CTE query
   SELECT ...
)
-- Main query
SELECT select_list
FROM cte_name;
```

- The `WITH` keyword defines a common table expression (CTE). You can think of a CTE as a temporary table within the query.
- The main query is a statement that uses the CTE by referencing the `cte_name`. The main query can be a `SELECT`, `INSERT`, `UPDATE`, `DELETE`, or `MERGE` statement.

Here is an example:

```sql
WITH user_totals AS (
  SELECT
    user_id,
    SUM(amount) AS total_spent
  FROM transactions
  GROUP BY user_id
)
SELECT *
FROM user_totals
WHERE total_spent > 200;
```

<hr>

### Recursive CTE

A recursive CTE is a type of CTE that references itself in its CTE query definition. A recursive CTE has two main parts:

- _Anchor_ member is a query that provides the base result set.
- _Recursive_ member is a query referencing the CTE itself. It will execute repeatedly and build up the final result set. The recursive member has a termination condition that stops execution when it returns no row.

A recursive CTE uses `UNION` or `UNION ALL` to combine result sets returned by the anchor member and recursive member.

Here’s the syntax of a recursive CTE:

```sql
WITH RECURSIVE cte_name (column1, column2, ...) AS (
    -- Anchor member
    SELECT ...
    UNION ALL
    -- Recursive member
    SELECT ...
    FROM cte_name
    WHERE ...
)
SELECT *
FROM cte_name;
```

In this syntax:

- The `WITH RECURSIVE` keyword defines a recursive CTE with a name (`cte_name`).
- An anchor member forms the base result set.
- A recursive member takes the base result set and starts the recursion until it returns no rows.
- The `UNION` (or `UNION ALL`) operator combines the result sets of the anchor member and recursive member into a final result set

The following example uses a recursive CTE to generate a countdown from 3 to 1:

```sql
WITH RECURSIVE count_down (counter) AS (
    -- Anchor member
    SELECT 3 AS counter
    UNION
    -- Recursive member
    SELECT counter - 1
    FROM count_down
    WHERE counter > 1
  )
SELECT * FROM count_down;
```

Here is an example of a recursive CTE to generate next 5 days from a user's signup:

```sql
WITH RECURSIVE next_days(day) AS (
  -- Anchor member: start with Ziya's signup_date
  SELECT signup_date::timestamp
  FROM users
  WHERE username = 'ziya'

  UNION ALL

  -- Recursive member: add 1 day until 5 days total
  SELECT day + INTERVAL '1 day'
  FROM next_days
  WHERE day < (SELECT signup_date::timestamp + INTERVAL '4 days' FROM users WHERE username = 'ziya')
)
SELECT * FROM next_days;
```

<hr>
<hr>

## Views

### Creating a database view

A view is a named query stored in the PostgreSQL database server. A view allows we to query data from it like a regular table but does not store the data physically. Therefore, a view is referred to as a virtual table.

In PostgreSQL, we can create views that store data physically. These views are called _materialized views_.

We use the `CREATE VIEW` statement to create a new view:

```sql
CREATE VIEW view_name
AS
query;
```

The query that defines the view is called the _defining query_. The tables that the defining query references are called _base tables_.

```sql
CREATE VIEW view_name
AS
SELECT username, email, country FROM users;
```

<hr>

### Replacing a database view

If you want to modify an existing view, we can use `CREATE OR REPLACE VIEW` statement:

```sql
CREATE OR REPLACE VIEW view_name
AS query;
```

The `CREATE OR REPLACE VIEW` will create the `view_name` if it does not exist or replace the existing one if it does.

```sql
CREATE OR REPLACE VIEW view_name
AS
SELECT username, email, country, is_active FROM users;
```

<hr>

### Dropping a database view

The `DROP VIEW` allows you to delete a view from the database permanently:

```sql
DROP VIEW IF EXISTS view_name CASCADE;
```

The `CASCADE` option will drop the views (and other objects) that depend on the `view_name` and, in turn, all objects that depend on those objects.

<hr>

### Creating a materialized view

Regular views do not store data. When you query data from them, PostgreSQL retrieves data from the underlying tables. When views have complex defining queries, you’ll encounter performance issues if you query data from them very frequently. To address this issue, PostgreSQL introduces materialized views that physically store the result of queries. These materialized views can significantly improve performance for views with complex queries.

We use the `CREATE MATERIALIZED VIEW` statement to create a materialized view:

```sql
CREATE MATERIALIZED VIEW [IF NOT EXISTS] view_name
AS
query
WITH DATA;
```

We use the `WITH DATA` to load data from underlying tables into the view when we issue the `CREATE MATERIALIZED VIEW` statement.

```sql
CREATE MATERIALIZED VIEW IF NOT EXISTS view_name
AS
SELECT username, email, country FROM users
WITH DATA;
```

Materialized views will not automatically update data from the underlying tables. To replace the data of a materialized view with the new one from a table, we use the `REFRESH MATERIALIZED VIEW view_name;` statement:

<hr>

### Dropping a materialized view

To delete a materialized view, you use the `DROP MATERIALIZED VIEW` statement:

```sql
DROP MATERIALIZED VIEW [ IF EXISTS ] view_name CASCADE;
```

<hr>
<hr>

## Joins

### Inner Join

To select data from two or more tables, you use the `INNER JOIN` clause of the `SELECT` statement. The inner join includes the rows with matching values in the columns.

```sql
SELECT
  table1.column1,
  table2.column2,
FROM
  table1
  INNER JOIN table2 ON table1.column1 = table2.column1
```

Here is an example:

```sql
SELECT DISTINCT username, email FROM users
INNER JOIN transactions ON users.user_id = transactions.user_id;
```

Typing the same table names for every column is tedious. PostgreSQL supports temporary names for tables in a query using table aliases: `table_name AS table_alias`. Since the `AS` keyword is optional, you can ignore it like this: `table_name table_alias`. Then, we use these table aliases to reference the column names from both tables.

```sql
SELECT username, email FROM users AS u
INNER JOIN transactions AS t ON u.user_id = t.user_id;
```

We can join more than 2 tables together:

```sql
SELECT
  u.username,
  u.email,
  p.name
FROM users AS u
INNER JOIN transactions as t ON u.user_id = t.user_id
INNER JOIN products as p ON t.product_id = p.product_id;
```

<hr>

### Left Join

The `LEFT JOIN` clause merges rows from two tables and returns all rows from the left table and matching rows from the right table.

```sql
SELECT
  left_t.username,
  left_t.email,
  right_t.product_id
FROM users AS left_t
LEFT JOIN transactions AS right_t ON left_t.user_id = right_t.user_id;
```

<hr>

### Right Join

The `RIGHT JOIN` includes all rows from the right table and matching rows from the left table.

```sql
SELECT
  left_t.username,
  left_t.email,
  right_t.product_id
FROM users AS left_t
RIGHT JOIN transactions AS right_t ON left_t.user_id = right_t.user_id;
```

<hr>

### Full Join

The `FULL JOIN` merges rows from two tables and returns all rows from both tables. Additionally, the `FULL JOIN` uses NULLs for every column of the table that does not have a matching row.

```sql
SELECT
  u.username,
  u.email,
  t.product_id
FROM users AS u
FULL JOIN transactions AS t ON u.user_id = t.user_id;
```

The `FULL OUTER JOIN` is an alternative syntax of the `FULL JOIN`. Note that the `OUTER` keyword is optional:

```sql
SELECT
  u.username,
  u.email,
  t.product_id
FROM users AS u
FULL OUTER JOIN transactions AS t ON u.user_id = t.user_id;
```

<hr>

### Self-Join

PostgreSQL self-join is a powerful technique that allows you to join a table to itself using an inner join, left join, or right join. The self-join technique can be helpful when you want to compare rows within the same table.

PostgreSQL does not allow you to use the same table multiple times within the same SQL statement. If you do so, PostgreSQL will issue a syntax error. To use the same table multiple times within a statement, you must assign the table different aliases. In this case, PostgreSQL will treat these aliases as separate tables.

Here’s an example of a self-join:

```sql
SELECT
  u1.username AS user1,
  u2.username AS user2,
  u1.country
FROM users u1
INNER JOIN users u2
  ON u1.country = u2.country
  AND u1.user_id < u2.user_id  -- avoid self-matching and duplicate pairs
WHERE u1.country IS NOT NULL;
```

<hr>

### Cross Join

The `CROSS JOIN` combines each row from the first table with every row from the second table and returns combinations of all rows. Unlike other joins like inner join, left join, and full join, a cross join has no condition to match rows from the two tables.

Here’s the syntax of the `CROSS JOIN` clause:

```sql
SELECT
  table1.column1,
  table2.column2,
FROM
  table1
  CROSS JOIN table2;
```

For example:

```sql
SELECT u.username, u.country, p.name FROM users u
CROSS JOIN products p;
```

Alternatively, you can form a cross-join by listing two tables in the `FROM` clause, making the statement more concise but less obvious:

```sql
SELECT
  table1.column1,
  table2.column2,
FROM
  table1, table2;
```

For example:

```sql
SELECT u.username, u.country, p.name FROM users u, products p;
```

If `table1` has n rows and `table2` has m rows, the `CROSS JOIN` will return a result set that has $nxm$ rows. In practice, you use a cross-join when you want to have all possible combinations of rows from both tables.

<hr>

### Natural Join

In PostgreSQL, a `NATURAL JOIN` allows you to join tables based on columns with the same names in both tables. Here’s the syntax of the `NATURAL JOIN`:

```sql
SELECT select_list
FROM table1
NATURAL [INNER, LEFT, RIGHT, FULL] JOIN table2;
```

The `NATURAL JOIN` joins two tables, `table1` and `table2`. These tables need the same column name and compatible types for matching.

For example, both tables here have `user_id` column:

```sql
SELECT u.username, u.country FROM users u
NATURAL INNER JOIN transactions;
```

If you don’t specify a join after the `NATURAL` keyword, PostgreSQL will use an `INNER JOIN` by default. If `table1` and `table2` have no common column, the `NATURAL JOIN` behaves like a `CROSS JOIN`.

<hr>

### `USING`

If you join two tables by comparing values from the same column names using the equal operator (=), you can use the `USING` clause syntax:

```sql
SELECT table1.column1, table2.column2, ...
FROM table1
INNER JOIN table2 USING (column1);
```

In this syntax, we replace the following `ON` clause:

```sql
ON table1.column1 = table2.column1
```

Here is an example:

```sql
SELECT DISTINCT username, email FROM users
INNER JOIN transactions USING (user_id);
```

Or:

```sql
SELECT DISTINCT u.username, u.email, p.name FROM users u
INNER JOIN transactions USING (user_id)
INNER JOIN products p USING (product_id);
```

<hr>
<hr>

## Conditional Expressions

### `CASE`

A `CASE` expression is a powerful tool, allowing you to perform conditional logic within your queries. Here’s the syntax of the `CASE` expression:

```sql
CASE  
  WHEN condition1 THEN result1
  WHEN condition2 THEN result2
  WHEN condition3 THEN result3

  ELSE result
END
```

If no condition is true, the `CASE` expression returns the result of the `ELSE` clause. The `ELSE` clause is optional. If you omit it and no condition returns true, then the `CASE` expression returns NULL.

```sql
SELECT
  username,
  account_balance,
  CASE
    WHEN account_balance >= 1000 THEN 'High'
    WHEN account_balance >= 500 THEN 'Medium'
    WHEN account_balance > 0 THEN 'Low'
    ELSE 'Empty'
  END AS balance_category
FROM users;
```

If you have one condition to evaluate, then you can use an alternative `CASE` expression:

```sql
CASE expression
  WHEN value1 THEN result1
  WHEN value2 THEN result2
  WHEN value3 THEN result3

  ELSE result
END
```

```sql
SELECT
  transaction_id,
  user_id,
  quantity,
  CASE quantity
    WHEN 1 THEN 'Small Order'
    WHEN 2 THEN 'Medium Order'
    WHEN 3 THEN 'Large Order'
    ELSE 'Bulk Order'
  END AS order_size
FROM transactions;
```

---

### `IF`

PL/pgSQL offers three forms of the `IF` statements:

- `IF-THEN`
- `IF-THEN-ELSE`
- `IF-THEN-ELSEIF`

Here’s the syntax of the `IF-THEN-ELSEIF` statement:

```sql
IF condition1 THEN
    statement1;
ELSEIF condition2 THEN
    statement2;
ELSEIF condition3 THEN
    statement3;
[ELSE
    else_statement;]
END IF;
```

<hr>
<hr>

## Sequence

In PostgreSQL, a sequence is a database object that generates unique integer values. To create a new sequence, you use the `CREATE SEQUENCE` statement. Here’s the basic syntax:

```sql
CREATE SEQUENCE sequence_name
    [AS data_type]
    [START WITH start_value]
    [INCREMENT BY increment_value]
    [MINVALUE min_value | NO MINVALUE]
    [MAXVALUE max_value | NO MAXVALUE]
    [CYCLE | NO CYCLE]
    [CACHE cache_value | NO CACHE]
    [OWNED BY table_name.column_name ];
```

In this syntax:

- `sequence_name` defines a sequence name, which must be unique within the database.
- The optional clause `AS data_type` specifies the data type of the sequence. Valid types are `smallint`, `integer`, and `bigint`. `bigint` is the default. The data type determines the default minimum and maximum values of the sequence.
- `START WITH start_value` specifies the starting value of the sequence – the `start_value` defaults to 1.
- `INCREMENT BY increment_value` determines the value you want to increment the sequence. The `increment_value` default is 1.
- `MINVALUE min_value` sets the minimum value of the sequence. Use `NO MINVALUE` to set the default to 1 for ascending and -1 for descending sequences.
- `MAXVALUE max_value` sets the maximum value of the sequence. Use `NO MAXVALUE` to set the default value for `max_value` to the maximum positive integer for ascending and -1 for descending sequences.
- `CYCLE` instructs the sequence should restart for the `MINVALUE` for ascending sequences or `MAXVALUE` for descending sequences when it reaches its limit. Use `NO CYCLE` to throw an error if the sequence value reaches the limit.
- `CACHE cache_value` instructs PostgreSQL to preallocate and store a number of sequence numbers in the memory for faster access—the `cache_value` defaults to 1. Use `NO CACHE` if you want to turn off the cache.
- `OWNED BY table_name.column_name` associates the sequence with a table column.

Here is an example of creating a sequence:

```sql
CREATE SEQUENCE product_seq
	START WITH 1000
	INCREMENT BY 5
	MINVALUE 1000
	NO MAXVALUE
	CACHE 10;
```

PostgreSQL provides some useful functions to work with sequences:

- `nextval('sequence_name')` increments the sequence to its next value and returns that value.
- `currval('sequence_name')` returns the value most recently obtained by the `nextval()` function for the sequence in the current session.
- `setval('sequence_name', value [, is_called])` manually sets the current value of a sequence. `is_called` is a boolean option. When it's `false`, the `nextval` function returns the `value` set with the `setval` function. When it's true, the `nextval` function returns the `value` after the `value` that was set with the `setval` function .
- `lastval()` returns the value that the `nextval()` function has recently generated in the current session.

Here is an example of using the above functions:

```sql
SELECT nextval('product_seq');
SELECT currval('product_seq');
SELECT lastval();
```

We can also use sequences while creating a table or inserting data:

```sql
CREATE TABLE new_products (
	id INT PRIMARY KEY DEFAULT nextval('product_seq'),
	name TEXT NOT NULL,
	key INT
);

INSERT INTO new_products (name, key)
VALUES ('Bluetooth Speaker', setval('product_seq', 1020));
```

To change the sequence, we use the `ALTER SEQUENCE` statement:

```sql
ALTER SEQUENCE [ IF EXISTS ] sequence_name
    [AS data_type]
    [START WITH start_value]
    [RESTART [ [ WITH ] restart_value ]]
    [INCREMENT BY increment_value]
    [MINVALUE min_value | NO MINVALUE]
    [MAXVALUE max_value | NO MAXVALUE]
    [CYCLE | NO CYCLE]
    [CACHE cache_value | NO CACHE]
    [OWNED BY table_name.column_name ];
```

- `start_value` - The optional clause `START WITH` starts changes the recorded start value of the sequence. This has no effect on the current sequence value; it simply sets the value that future `ALTER SEQUENCE RESTART` commands will use.
- The optional clause `RESTART [ WITH restart ]` changes the current value of the sequence. This is similar to calling the `setval` function with `is_called = false`: the specified value will be returned by the next call of `nextval`. Writing `RESTART` with no restart value is equivalent to supplying the start value that was recorded by `CREATE SEQUENCE` or last set by `ALTER SEQUENCE START WITH`.

Here is an example of altering a sequence:

```sql
ALTER SEQUENCE product_seq
    RESTART WITH 2000   -- next call to nextval() will give 2000
    INCREMENT BY 10     -- now each nextval will increase by 10
    MINVALUE 1000       -- minimum value allowed
    MAXVALUE 9999       -- maximum value allowed
    CYCLE               -- wrap around when max is reached
    CACHE 5;            -- store 5 numbers in memory for faster access
```

To list all sequences in a database, WE use the following query:

```sql
SELECT * FROM pg_class
WHERE relkind = 'S';
```

We use the `DROP SEQUENCE` statement to remove a sequence:

```sql
DROP SEQUENCE [IF EXISTS] sequence_name
[CASCADE | RESTRICT];
```

Here is an example:

```SQL
DROP SEQUENCE IF EXISTS product_seq CASCADE;
```

<hr>
<hr>

## Identity Column

In PostgreSQL, the identity column is a special feature that brings convenience by automatically generating unique integers using an implicit sequence.

To define an identity column, you use one of two the following constraints:

- `GENERATED ALWAYS AS IDENTITY`: This ensures the column always uses generated integer numbers. If a column has this constraint, you cannot provide an explicit value in the insert or update statement, except if you use the `OVERRIDING SYSTEM VALUE` in the `INSERT` statement.
- `GENERATED BY DEFAULT AS IDENTITY`: This constraint, similar to the above, offers flexibility by allowing you to provide an explicit integer for insertion.

The following statement shows how to define a column as an identity column as a primary key column:

```sql
CREATE TABLE table_name (
  id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  column1 data_type,
  ...
);
```

Here is how to use `OVERRIDING SYSTEM VALUE` clause in the `INSERT` statement:

```sql
INSERT INTO
  table_name (id, column1)
OVERRIDING SYSTEM VALUE
VALUES
  (1, value1);
```

When you create an identity column for a table, PostgreSQL automatically generates an implicit sequence and associates it with the column. The sequence will have the following naming convention: `<table_name>_<column_name>_seq` For example, PostgreSQL creates the following sequence for the `order_no` column of the `order_schedules` table: `order_schedules_order_no_seq`.

PostgreSQL allows you to configure the sequence when defining an identity column:

```sql
CREATE TABLE order_schedules (
  item_no INT,
  schedule_no INT GENERATED BY DEFAULT AS IDENTITY (INCREMENT 10 START 10),
  PRIMARY KEY (item_no, schedule_no),
  FOREIGN KEY (item_no)
      REFERENCES sales_order_items (item_no)
      ON DELETE CASCADE
);
```

To change a column to an identity column, you can use the `ALTER TABLE` statement:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
ADD GENERATED { ALWAYS | BY DEFAULT }
AS IDENTITY
[sequence_option];
```

The `column_name` must have a `NOT NULL` constraint or you’ll encounter an error.

PostgreSQL allows you to configure the characteristics of an identity column:

- Switching between the `GENERATED ALWAYS` and `GENERATED BY DEFAULT`.
- Change the parameters for the implicit sequence.

Here’s the syntax:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
SET GENERATED { ALWAYS | BY DEFAULT}
[SET sequence_option]
```

To drop a `GENERATED ALWAYS` (or `BY DEFAULT`) `AS IDENTITY` constraint from a column, you use the `ALTER TABLE DROP IDENTITY` statement:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
DROP IDENTITY [ IF EXISTS ];
```

<hr>
<hr>

## `ALTER TABLE` Statement

The `ALTER TABLE` statement allows you to modify the table structure:

```sql
ALTER TABLE table_name
action;
```

Here are the main actions:

- Renaming a table.
- Renaming a column.
- Adding one or more columns to the table.
- Removing a column.
- Applying a constraint to a column.
- Changing the data type of a column.

<hr>

### Renaming a table

You can use the `ALTER TABLE RENAME TO` statement to change the name of an existing table.

```sql
ALTER TABLE table_name
RENAME TO new_table;
```

If the table has dependent objects such as a view and foreign key constraints, renaming the table will automatically change the dependent objects.

```sql
ALTER TABLE products
RENAME TO prods;
```

<hr>

### Renaming a column

To rename a column, we use the `ALTER TABLE ... RENAME COLUMN` statement:

```sql
ALTER TABLE table_name
RENAME COLUMN column_name
TO new_column_name;
```

To make it shorter, we can omit the `COLUMN` keyword in the `RENAME COLUMN`.

If the column we change has references such as views, foreign key constraints, triggers, user-defined functions, and stored procedures, PostgreSQL automatically changes the column names in these objects.

```sql
ALTER TABLE products
RENAME COLUMN bought_at
TO order_date;
```

<hr>

### Adding new columns to a table

Use the `ALTER TABLE...ADD COLUMN` statement to add a new column to a table:

```sql
ALTER TABLE table_name
ADD COLUMN column_name data_type constraint;
```

If you want to add multiple columns at the same time, you can use multiple `ADD COLUMN` clauses:

```sql
ALTER TABLE table_name
ADD COLUMN new_column1 data_type constraint,
ADD COLUMN new_column2 data_type constraint,
ADD COLUMN new_column3 data_type constraint;
```

The `ALTER TABLE ... ADD COLUMN` appends the new column at the end of the column list of the table.

```sql
ALTER TABLE new_products
ADD COLUMN name VARCHAR(100) NOT NULL,
ADD COLUMN bought_at TIMESTAMPTZ(3);
```

PostgreSQL does not allow you to insert a new column at a specified position in the column list like MySQL. But there is a workaround:

1. Rename the existing table to a new one.
2. Recreate the table with the desired column order.
3. Copy data from the old table to the new table.
4. Drop the old table.

Here are 2 examples of copying a column:

```sql
-- copying to an empty table
INSERT INTO new_products(name, bought_at)
SELECT products.name, products.bought_at FROM products;
```

```sql
-- copying to a non-empty table
UPDATE new_products
SET name = products.name
FROM products
WHERE id = products.product_id;
```

<hr>

### Changing the column data type

You use the `ALTER TABLE ... ALTER COLUMN ... SET DATA TYPE` statement to change the data type of a column:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name
SET DATA TYPE new_data_type;
```

Here is an example:

```sql
ALTER TABLE new_products
ALTER COLUMN bought_at
SET DATA TYPE TIMESTAMP(2);
```

<hr>

### Applying constraints to columns

You use the `ALTER TABLE ... ALTER COLUMN ... SET` and `ALTER TABLE ... ALTER COLUMN ... ADD` statements to add a constraint to a column.

The following statement applies a `NOT NULL` constraint to a column:

```sql
ALTER TABLE new_products
ALTER COLUMN bought_at
SET NOT NULL;
```

The following statement adds a `CHECK` constraint to a column:

```sql
ALTER TABLE new_products
ADD CHECK (bought_at < NOW());
```

The following statement adds 2 `CHECK` constraints:

```sql
ALTER TABLE new_products
ADD CHECK (bought_at < NOW()),
ADD CHECK (bought_at > DATE '2025-01-01');
```

The following statement sets the default value to false:

```sql
ALTER TABLE users
ALTER COLUMN is_active
SET DEFAULT false;
```

The following statement adds a unique constraint for one or more columns:

```sql
ALTER TABLE users
ADD UNIQUE (username, email);
```

Here is how to list all the constraints of a table:

```sql
SELECT constraint_name, constraint_type
FROM information_schema.table_constraints
WHERE table_name = 'new_products';
```

Here is how to drop a constraint:

```sql
ALTER TABLE new_products
DROP CONSTRAINT "new_products_bought_at_check1";
```

The `NOT NULL` constraints cannot be dropped using the `DROP CONSTRAINT` syntax; the `DROP NOT NULL` clause must be used instead.

```sql
ALTER TABLE new_products
ALTER COLUMN bought_at DROP NOT NULL;
```

<hr>

### Dropping columns

The `ALTER TABLE ... DROP COLUMN` removes a column from a table:

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

If you remove a column referenced by other objects outside the table, such as views and foreign key constraints, PostgreSQL will return an error. In this case, you can use the `CASCADE` option:

```sql
ALTER TABLE table_name
DROP COLUMN IF EXISTS column_name CASCADE;
```

To drop multiple columns at once, you can use multiple `DROP COLUMN` clauses:

```sql
ALTER TABLE table_name
DROP COLUMN column1,
DROP COLUMN column2,
DROP COLUMN column3;
```

Here is an example:

```sql
ALTER TABLE new_products
DROP COLUMN IF EXISTS name CASCADE,
DROP COLUMN IF EXISTS bought_at CASCADE;
```

<hr>

### Truncating a table

The `TRUNCATE TABLE` statement allows you to remove all rows from a table. Here’s the basic syntax of the `TRUNCATE TABLE` statement. Note that the `TABLE` keyword is optional:

```sql
TRUNCATE TABLE table_name;
```

If the table you want to truncate has identity columns, you can use the `RESTART IDENTITY` option to restart the values of the identity columns:

```sql
TRUNCATE TABLE table_name
RESTART IDENTITY;
```

If you don’t want to restart the values of the identity columns, you can use the `CONTINUE IDENTITY` option:

```sql
TRUNCATE TABLE table_name
CONTINUE IDENTITY;
```

If you truncate a table with foreign key references, you’ll get an error. Fortunately, you can use the `CASCADE` option to automatically truncate the table as well as its foreign key tables in one go:

```sql
TRUNCATE TABLE table_name
CASCADE;
```

To reject the truncation of the foreign key tables, you can ignore the `CASCADE` option or explicitly use the `RESTRICT` option:

```sql
TRUNCATE TABLE table_name
RESTRICT;
```

Note that the `RESTRICT` option is the default.

If you use the `RESTART IDENTITY` and `CASCADE` options at the same time, you need to place the `CASCADE` option after the `RESTART IDENTITY` option:

```sql
TRUNCATE TABLE table_name
RESTART IDENTITY
CASCADE;
```

You can truncate multiple tables in one go using the `TRUNCATE TABLE` statement:

```sql
TRUNCATE TABLE table1, table2, ...;
```

<hr>
<hr>

## PL/pgSQL Block and Variables

PL/pgSQL is a blocked structure programming language. PL/pgSQL organizes code into blocks.

Here’s the syntax of a block:

```sql
[ <<label>> ]
[ DECLARE
    declarations ]
BEGIN
    statements
END [ label ];
```

A block has two main sections:

- Declaration: The declaration section is optional. It is where you declare variables, constants, and cursors.
  - Each statement in the declaration section is terminated with a semicolon (`;`).
  - Besides the assignment operator (`=`), we can use the `:=` operator to assign an initial value to a variable.
  - We can use the `DEFAULT` keyword to specify an initial value of a variable.
- Body: The body section is required. It is where you put the logic of the block, such as SQL statements.

A block may include an optional label appearing at the beginning and end. A block ends with a semicolon (`;`) after the end keyword.

Here is a simple example of a block that displays a message:

```sql
DO
$$
BEGIN
    RAISE NOTICE 'Hello, World';
END;
$$;
```

- The `DO` statement executes the PL/pgSQL block.
- We use the PL/pgSQL block as a dollar-quoted string constant.

Here is the same example, this time with naming the block:

```sql
DO
$$
<<block_name>>
BEGIN
    RAISE NOTICE 'Hello, World';
END block_name;
$$;
```

The following example shows how to define a block with a declaration section. We declare a variable in the declaration section. To declare a variable, you provide the name, data type, and initial value:

```sql
DO
$$
DECLARE
    name VARCHAR = 'Joe';
BEGIN
    RAISE NOTICE 'Hello %', name;
END;
$$;
```

`%` is a placeholder for the string that comes after the comma.

We can also nest blocks:

```sql
DO
$$
DECLARE
	total_q INT DEFAULT 0;
BEGIN
	DECLARE
		safety_stock INT = 10;
		on_hand_q INT = 100;
	BEGIN
		total_q = safety_stock + on_hand_q;
	END;
	RAISE NOTICE 'The total quantity is %', total_q;
END;
$$;
	total_q INT = 0;
BEGIN
	DECLARE
		safety_stock INT =10;
		on_hand_q INT = 100;
	BEGIN
		total_q = safety_stock + on_hand_q;
	END;
	RAISE NOTICE 'The total quantity is %', total_q;
END;
$$;
```

The scope of a variable is within the block and nested blocks of the block where you declare it. For exampe, the variables that we declared in the subblocks above, can only be accessed within the subblock. If we attempt to access them from the outer block, we'll get an error.

Sometimes, we want to define variables whose values cannot be changed. To do that you can declare constants.

Here’s the syntax for declaring a constant:

```sql
constant_name CONSTANT data_type = initial_value;
```

The `CONSTANT` keyword indicates that the value of the `constant_name` cannot be changed after initialization.

Here is an example:

```sql
DO
$$
DECLARE
    pi CONSTANT DEC = 3.14;
    v_radius DEC = 10;
    v_area DEC;
BEGIN
    v_area = pi * v_radius * v_radius;
    RAISE NOTICE 'The area of a circle with the radius % is %', v_radius, v_area;
END;
$$;
```

<hr>
<hr>

## User-defined Functions

PostgreSQL allows us to create a new function using the `CREATE FUNCTION` statement. The following shows the basic syntax of the `CREATE FUNCTION` statement:

```sql
CREATE [OR REPLACE] FUNCTION function_name (parameters)
RETURNS return_type
AS
$$
BEGIN
  -- function body
END
$$
LANGUAGE SQL;
```

- `RETURNS return_type` specifies the data type of a value the function will return. If the function returns no value, the return type is `VOID`.
- `LANGUAGE SQL` specifies that the function is using SQL. PostgreSQL allows us to write user-defined functions in various languages beyond SQL. These are known as procedural languages (PLs). For example, we indicate that we use postgreSQL database system with `plpgSQL`.

To call a user-defined function, we use the `SELECT` statement, followed by the function name and arguments:

```sql
SELECT function_name(arguments);
```

The following example uses the `CREATE FUNCTION` statement to create a function that adds a new product:

```sql
CREATE OR REPLACE FUNCTION add_product(
  product_name VARCHAR,
  order_date TIMESTAMPTZ(3)
)
RETURNS VOID
AS
$$
BEGIN
    INSERT INTO new_products(name, bought_at)
    VALUES(product_name, order_date);
END;
$$
LANGUAGE plpgsql;
```

We cannot use the parameter names the same as the column names of tables used inside the function. If you do so, PostgreSQL will issue an error. The reason is that PostgreSQL will confuse the parameters and column names.

This is how we call the above function:

```sql
SELECT add_product(
    'Mechanical Keyboard',
    NOW()
);
```

PostgreSQL UDFs support variable declaration using the `DECLARE` statement within the function body. In this example, the `get_max_quantity()` function has no parameter and returns a number with the type `DECIMAL` or `DEC` in short.

```sql
CREATE OR REPLACE FUNCTION get_max_quantity()
RETURNS DEC
AS
$$
DECLARE
  result DEC;
BEGIN
  SELECT MAX(quantity) INTO result FROM transactions;
  RETURN result;
END;
$$
LANGUAGE plpgsql;
```

In the above code, we declare the variable using the `DECLARE` statement and assign a value to the variable using the `INTO` keyword. We can use `:=` to assign a simple expression to a variable:

```sql
CREATE OR REPLACE FUNCTION add_five_to_five()
RETURNS DEC
AS
$$
DECLARE
  result DEC := 5;
BEGIN
  result := result + 5;
  RETURN result;
END;
$$
LANGUAGE plpgsql;

SELECT add_five_to_five();
```

The `DROP FUNCTION` statement allows you to remove a user-defined function permanently from the database.

```sql
DROP FUNCTION [IF EXISTS] function_name(parameters);
```

For example:

```sql
DROP FUNCTION IF EXISTS add_product(
	product_name VARCHAR,
	order_date TIMESTAMPTZ(3)
);
```

If a function has dependent objects like operators and triggers, you cannot drop it with the above code. Fortunately, you can drop the function and its dependent objects by using the `CASCADE` option explicitly:

```sql
DROP FUNCTION [IF EXISTS] function_name(parameters) CASCADE;
```

The `RESTRICT` option prevents you from removing a function with dependent objects. The `DROP FUNCTION` statement uses the `RESTRICT` option by default.

To remove multiple functions at once, you can specify a comma-separated list of function names after the `DROP FUNCTION` keyword:

```sql
DROP FUNCTION
    function_name1(parameter),
    function_name2(parameter), ...;
```

Here is an example:

```sql
DROP FUNCTION IF EXISTS
	get_max_quantity,
	add_five
CASCADE;
```

The `returns setof` option allows us to return one or more rows with a predefined structure from a function.

```sql
Here’s the syntax for creating a function that returns a set of rows:

create or replace function function_name(parameters)
returns setof row_structure
as
$$
   -- logic
   -- ...
   -- return one or more rows
   return query select_query;
$$ language plpgsql;
```

<hr>
<hr>

## Special Variable `FOUND`

One way to determine the effects of a command is to check the special variable named `FOUND`, which is of type boolean. `FOUND` starts out false within each PL/pgSQL function call. It is set by each of the following types of statements:

- A `SELECT INTO` statement sets `FOUND` true if a row is assigned, false if no row is returned.

- A `PERFORM` statement sets `FOUND` true if it produces (and discards) one or more rows, false if no row is produced.

- `UPDATE`, `INSERT`, `DELETE`, and `MERGE` statements set `FOUND` true if at least one row is affected, false if no row is affected.

- A `FETCH` statement sets `FOUND` true if it returns a row, false if no row is returned.

- A `MOVE` statement sets `FOUND` true if it successfully repositions the cursor, false otherwise.

- A `FOR` or `FOREACH` statement sets `FOUND` true if it iterates one or more times, else false. `FOUND` is set this way when the loop exits; inside the execution of the loop, `FOUND` is not modified by the loop statement, although it might be changed by the execution of other statements within the loop body.

- `RETURN QUERY` and `RETURN QUERY EXECUTE` statements set `FOUND` true if the query returns at least one row, false if no row is returned.

Other PL/pgSQL statements do not change the state of `FOUND`. Note in particular that `EXECUTE` changes the output of `GET DIAGNOSTICS`, but does not change `FOUND`.

`FOUND` is a local variable within each PL/pgSQL function; any changes to it affect only the current function.

Here is a simple example:

```sql
CREATE OR REPLACE FUNCTION get_user_name(user_id INT)
RETURNS TEXT
LANGUAGE plpgsql
AS $$
DECLARE
    found_name TEXT;
BEGIN
    -- Try to select the name.
    -- If a row is found, FOUND becomes TRUE.
    -- If no row is found, FOUND becomes FALSE (and found_name becomes NULL).
    SELECT name INTO found_name
    FROM users
    WHERE id = user_id;

    -- Check if a row was actually found
    IF FOUND THEN
        RAISE NOTICE 'User found: %', found_name;
        RETURN found_name;
    ELSE
        RAISE EXCEPTION 'User with ID % not found', user_id;
    END IF;
END;
$$;
```

<hr>
<hr>

## Exception Handling

In PL/pgSQL, an exception is an unexpected condition or error during execution. Exceptions may result from issues like constraint violation, division by zero, data not found, or other situations. Here is a list of errors and error messages: [Error Codes](https://www.postgresql.org/docs/current/errcodes-appendix.html).

To handle exceptions, we use the `EXCEPTION` block within the `BEGIN` and `END` keywords of a block:

```sql
DO
$$
DECLARE
   -- declaration
BEGIN
    -- code that may cause exceptions
EXCEPTION
    WHEN exception_name THEN
        -- Handle the specific exception
        RAISE NOTICE 'An error occurred: %', SQLERRM;
    WHEN OTHERS THEN
        -- Handle all other exceptions
        RAISE NOTICE 'An unknown error occurred: %', SQLERRM;
END;
$$
LANGUAGE plpgsql;
```

The `SQLERRM` and `SQLSTATE` are error message variables:

- The `SQLERRM` variable contains the exception’s message.
- The `SQLSTATE` variable holds the error code.

Here is an example:

```sql
CREATE FUNCTION try_divide(x NUMERIC, y NUMERIC)
RETURNS NUMERIC AS
$$
BEGIN
    RETURN x / y;
EXCEPTION
    WHEN division_by_zero THEN
        RAISE NOTICE 'Cannot divide by zero, returning NULL!';
        RETURN NULL;
END;
$$
LANGUAGE plpgsql;
```

---

### `RAISE` Statement

In PL/pgSQL, the `RAISE` statement allows you to debug, inform, warn, and signal errors in your procedures, functions, and triggers.

Here’s the syntax of the `RAISE` statement:

```sql
RAISE [level] 'format' [expression, ...]
```

The level specifies the severity level of the message. The valid levels are as follows:

- `DEBUG`: Use to debug the code.
- `LOG`: Write messages to the PostgreSQL server’s log, but don’t send them to the client.
- `NOTICE`: Return informational messages to the client.
- `WARNING`: Warn the client without interrupting code execution.
- `EXCEPTION`: Issue an error and abort the execution of the current block.

The format is a string that may include one or more placeholders (`%`). The `RAISE` statement will substitute the placeholders with the expression. The number of placeholders and expressions must be the same, or the `RAISE` statement will issue an error.

<hr>
<hr>

## Stored Procedures

A stored procedure is a precompiled set of SQL statements stored and executed on a PostgreSQL database server. To define a stored procedure, we use the `CREATE PROCEDURE` statement with the following syntax:

```sql
CREATE OR REPLACE PROCEDURE procedure_name(parameter_list)
LANGUAGE SQL
BEGIN ATOMIC
    sql_statement1;
END;
```

If we want to execute multiple SQL statements, we place them one after another in the a `BEGIN ATOMIC ... END` block:

```sql
CREATE OR REPLACE PROCEDURE procedure_name(parameter_list)
LANGUAGE SQL
BEGIN ATOMIC
    sql_statement1;
    sql_statement2;
END;
```

Here is an example. In this example, we use `LANGUAGE plpgsql`. This procedural language supports `BEGIN ... END` block. That's what we use instead of `BEGIN ATOMIC ... END` block:

```sql
CREATE OR REPLACE PROCEDURE add_transaction(
  p_user_id INT,
  p_product_id INT,
  p_quantity INT,
  p_price DECIMAL
)
LANGUAGE plpgsql
AS
$$
DECLARE
  total_amount DECIMAL;
BEGIN
  -- Calculate total amount
  total_amount := p_quantity * p_price;

  -- Insert the transaction
  INSERT INTO transactions(user_id, product_id, quantity, price)
  VALUES (p_user_id, p_product_id, p_quantity, p_price);

  -- Update user's account balance
  UPDATE users
  SET account_balance = account_balance - total_amount
  WHERE user_id = p_user_id;
END;
$$;
```

To execute a PostgreSQL stored procedure, we use the `CALL` statement with the following syntax:

```sql
CALL procedure_name(arguments);
```

For example:

```sql
CALL add_transaction(1, 3, 1, 250.00);
```

If a stored procedure is no longer in use, we can remove it from the database using the `DROP PROCEDURE` statement.

```sql
DROP PROCEDURE [IF EXISTS] procedure_name (parameter_list);
```

PostgreSQL will raise an error if we attempt to drop a stored procedure with dependent objects. To remove the stored procedure as well as the objects that depend on it, we use the `CASCADE` option:

```sql
DROP PROCEDURE [IF EXISTS] procedure_name (parameter_list)
CASCADE;
```

We can remove multiple stored procedures using a single `DROP PROCEDURE` statement:

```sql
DROP PROCEDURE
    procedure_name1(parameter_list),
    procedure_name2(parameter_list);
```

<hr>
<hr>

## Indexes

PostgreSQL stores data of a table using a heap file storage model. Each table corresponds to a heap file. Each heap file consists of blocks (or pages). Typically, a block has a size of 8KB by default. Each block contains multiple tuples (or rows). Additionally, PostgreSQL maintains other information that determines which rows are accessible.

When retrieving data from a table, PostgreSQL has to read data from the heap file and load it to the memory for filtering the rows. A full table scan means that PostgreSQL must read all rows from a heap file (table) to memory and search for rows. Most of the time, a full table scan is not efficient because PostgreSQL must read every block, even if only a few rows match the condition.

An index is a separate data structure that allows PostgreSQL to locate rows quickly without scanning the table.

<hr>

### Creating an index

To create an index in PostgreSQL, we use the `CREATE INDEX` statement:

```sql
CREATE INDEX [IF NOT EXISTS] [index_name]
ON tablename (column1, column2);
```

Here is an example:

```sql
CREATE INDEX IF NOT EXISTS idx_transactions_user_product
ON transactions (user_id, product_id);
```

<hr>

### Analyzing an index

When we query the indexed columns, PostgreSQL has a specific software component called a query optimizer that decides whether it should use the index or perform a full table scan. If the number of rows is relatively small, the query optimizer performs a full table scan because it is more efficient than reading the index and locating the data. To check if a query performs a full table scan or utilizes an index, we can use the `EXPLAIN ANALYZE` keywords before a query:

```sql
EXPLAIN ANALYZE query;
```

For example:

```sql
EXPLAIN ANALYZE
SELECT * FROM transactions
WHERE user_id = 2 AND product_id = 5;
```

<hr>

### Listing indexes

To list all the indexes, we can use the below code:

```sql
SELECT * FROM pg_indexes;
```

<hr>

### Dropping an index

To drop an index, we use the below command:

```sql
DROP INDEX [CONCURRENTLY] [IF EXISTS] index_name
[CASCADE | RESTRICT];
```

The `CONCURRENTLY` option is used to delete an index without locking out concurrent selects, inserts, updates, and deletes on the table.

Here is an example of dropping an index:

```sql
DROP INDEX CONCURRENTLY IF EXISTS idx_transactions_user_product;
```

<hr>

### Unique Index

One type of index is unique index. A unique index ensures values in one or more columns are unique across all rows in a table, maintaining the integrity of your data. To create a unique index, you use the `CREATE UNIQUE INDEX` statement:

```sql
CREATE UNIQUE INDEX [index_name]
ON table_name (column1[, column2, ...])
[ NULLS [ NOT ] DISTINCT ];
```

The `NULL NOT DISTINCT` treats NULLs equally, while the `NULLS DISTINCT` considers NULLs as distinct values. The default is `NULLS DISTINCT`, meaning the index column may contain multiple NULLs.

In PostgreSQL, a primary key is a special kind of unique index that:

- Does not allow NULLs.
- Can be applied to one or more columns per table.
- Implies uniqueness inherently

In contrast, a unique index allows NULLs unless you specify `NULL NOT DISTINCT` option.

Here is an example of creating a unique index:

```sql
CREATE UNIQUE INDEX idx_users_email_unique
ON users (email)
NULLS NOT DISTINCT;
```

<hr>

### Expression Index

You can create an expression index based on the results of an expression that involves table columns rather than the columns’ data. When you create an expression index, PostgreSQL evaluates the expression and uses the results for indexing.

To create an expression index, you use the following form of the `CREATE INDEX` statement:

```sql
CREATE INDEX [index_name]
ON table_name(expression);
```

Here is an example of creating an expression index:

```sql
CREATE INDEX idx_users_lower_email
ON users (LOWER(email));
```

Now, the index stores the result of `LOWER(email)` for each row. So, when our query also uses `LOWER(email)`, PostgreSQL can use this index instead of scanning all rows. We can check if PostgreSQL uses the index by running:

```sql
EXPLAIN
SELECT * FROM users
WHERE LOWER(email) = 'ziya@example.com';
```

<hr>

### Partial Index

When you create an index that includes a column or a set of columns, PostgreSQL extracts all data from these columns for indexing. PostgreSQL allows you to include only a subset of data in a table that meets a specified condition in an index. This index is called a partial index.

To create a partial index, you use the following `CREATE INDEX` statement with a `WHERE` clause:

```sql
CREATE INDEX [index_name]
ON table_name (column1, column2)
WHERE condition;
```

Here is an example of creating a partial index:

```sql
CREATE INDEX idx_transactions_large_orders
ON transactions (user_id, product_id)
WHERE quantity > 1;
```

<hr>

### Covering Index

When a query retrieves data based on indexed columns, PostgreSQL looks up the matching rows in the index and accesses the table to retrieve the actual rows. A covering index is a database index that includes all the columns needed to satisfy a query. It allows PostgreSQL to retrieve the required data directly from the index without accessing the table.

To create a covering index, you can use the `CREATE INDEX` statement with an `INCLUDE` clause to specify the extra columns to be stored in the index:

```sql
CREATE INDEX [index_name]
ON table_name(indexed_columns)
INCLUDE(extra_columns);
```

Here is an example:

```sql
CREATE INDEX idx_transactions_user_product_covering
ON transactions (user_id, product_id)
INCLUDE (quantity, price);
```

- `user_id`, `product_id` - These are the indexed columns used for searching/filtering.
- `quantity`, `price` - These are the extra columns stored in the index so PostgreSQL can fetch them without going back to the table.

Here is an example query that would benefit from this index:

```sql
SELECT quantity, price
FROM transactions
WHERE user_id = 2 AND product_id = 4;
```

<hr>
<hr>

## Denormalized Data Types

### Composite Types

A composite type is a list of field names and their data types. A composite type represents the structure of a row or record. For example, the following statement creates a composite type to store shipping details for a product transaction:

```sql
CREATE TYPE shipping_info AS (
  address TEXT,
  city VARCHAR(50),
  postal_code VARCHAR(10)
);
```

PostgreSQL allows you to use composite types in the same way as simple types. Here we create a table that includes a column with a composite type:

```sql
CREATE TABLE shipments (
  shipment_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  transaction_id UUID NOT NULL REFERENCES transactions(transaction_id) ON DELETE CASCADE,
  shipped_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP,
  shipping_details shipping_info
);
```

When inserting data, you can use the `ROW` keyword, to create a composite value as a literal constant and enclose comma-separated field values within parentheses as follows:

```sql
INSERT INTO shipments (transaction_id, shipping_details)
VALUES (
  'd12b2d24-bd05-47a7-bdcd-feda47ec27f8',
  ROW('123 Elm St', 'Baku', '1000')
)
RETURNING *;
```

It’s possible to explicitly specify the fields of the composite column you want to insert using the dot notation:

```sql
INSERT INTO
  shipments (
    transaction_id,
    shipping_details.address,
    shipping_details.city,
    shipping_details.postal_code
  )
VALUES
  ('d12b2d24-bd05-47a7-bdcd-feda47ec27f8', '123 Elm St', 'Baku', '1000')
RETURNING
  *;
```

To access all fields of a composite column, you can use the asterisk shorthand (`*`):

```sql
SELECT
  transaction_id,
  (shipping_details).*
FROM
  shipments;
```

In the `SELECT` statement, if you don’t use the parentheses, PostgreSQL might misinterpret the `shipping_details` as a table name and issue an error.

The following statement updates the address, city, and postal code of the shipment:

```sql
UPDATE shipments
SET
  shipping_details.address = '456 Test st',
  shipping_details.postal_code = '1001'
WHERE
  shipment_id = 1
RETURNING *;
```

You do not use parentheses when you access the field in the `SET` clause of the `UPDATE` statement because the dot notation is sufficient to identify the individual fields within the composite type. Using parentheses here will result in an error.

To update all fields of the shipping_details column at once, you can also use the following syntax:

```sql
UPDATE shipments
SET
  shipping_details = ROW('789 Test st', 'Baku','1002')
WHERE
  shipment_id = 2
RETURNING *;
```

When using the `DELETE` statement to delete a row based on a field of a composite type, you do need to use the parentheses in the `WHERE` clause. The reason is that the `WHERE` clause qualifies the column with the table name. If you don’t use the parentheses, PostgreSQL may misinterpret the composite as a table.

For example, the following statement deletes a row from the `shipments` table where the address of a postal code equals 1000:

```sql
DELETE FROM shipments
WHERE
  (shipping_details).postal_code = '1000'
RETURNING *;
```

Composite types are flexible. However, they do not directly support constraints such as `NOT NULL` and `CHECK` on individual fields. The `NOT NULL` constraint ensures that the whole composite value is `NOT NULL`, not individual fields.

To apply constraints like `NOT NULL` or `CHECK` to individual fields of a composite column, you can create a domain over the composite type and apply constraints to the domain.

A domain is a user-defined data type that is based on another underlying type. Optionally, it can have constraints that restrict its valid values to a subset of what the underlying type would allow. For example:

```sql
CREATE DOMAIN shipment_info_domain
AS shipping_info
CHECK (
  (VALUE).address IS NOT NULL
  AND (VALUE).city IS NOT NULL
  AND (VALUE).postal_code IS NOT NULL
);
```

Change the type of the `shipping_details` column to `shipment_info_domain`:

```sql
ALTER TABLE shipments
ALTER COLUMN shipping_details TYPE shipment_info_domain;
```

The `DROP TYPE` statement allows you to remove one or more user-defined data types from a database.

```sql
DROP TYPE [IF EXISTS] type_name [CASCADE | RESTRICT];
```

If you want to drop more than one type at the same time, you can list them in the `DROP TYPE` statement:

```sql
DROP TYPE type_name1, type_name2, ...;
```

<hr>

### `ARRAY` Data Type

We can use the Array type to store multiple values of the same type in a single column. For every data type, including user-defined type, PostgreSQL creates a corresponding Array data type implicitly. For example, the `INT` type has the `INT[]` array type, `VARCHAR` has the `VARCHAR[]` array type, etc.

Here’s the syntax for defining a column with an array data type:

```sql
column_name datatype[]
```

An array can be one-dimensional or multi-dimensional. The number of bracket squares determines the number of dimensions of an array. For example, the following shows how to define a column with two dimensions:

```sql
column_name datatype [][]
```

Here is an example of creating a table with an array data type:

```sql
CREATE TABLE product_reviews (
  product_id INT PRIMARY KEY REFERENCES products(product_id),
  rating_history INTEGER[] NOT NULL,             -- 1D array
  comment_matrix TEXT[][],                       -- 2D array: e.g., grouped comments
  last_reviewed TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

To construct a value of an array, you can use either curly braces `{}` or the `ARRAY` constructor.

```sql
INSERT INTO product_reviews (
  product_id,
  rating_history,
  comment_matrix
) VALUES (
  1,                              -- Mechanical Keyboard
  ARRAY[5, 4, 4, 3],              -- 1D array: past ratings
  ARRAY[
    ['Great keys', 'Smooth typing'],      -- Usability
    ['Nice design', 'RGB is cool'],       -- Design
    ['Fast shipping', 'Good packaging']   -- Shipping
  ]
)
RETURNING *;
```

PostgreSQL arrays use 1-based indexing i.e., the first array element is 1, the second array element is 2, etc.

The following query retrieves the first rating:

```sql
SELECT rating_history[1] FROM product_reviews;
```

The following `UPDATE` statement modifies the element in a 2-dimensional array:

```sql
UPDATE product_reviews
SET comment_matrix[1][2] = 'Easy to use'
WHERE product_id = 1;
```

We use the `ANY` operator to check if an element exists in an array.

```sql
SELECT product_id, comment_matrix FROM product_reviews
WHERE 'Easy to use' = ANY (comment_matrix);
```

To expand an arrays into a set of rows, we use the `UNNEST` function:

```sql
SELECT
	product_id,
	UNNEST(rating_history) ratings
FROM product_reviews;
```

The `ARRAY_LENGTH` function returns the number of elements in an array: `ARRAY_LENGTH(array, dimension)`. For example, the following query uses the `ARRAY_LENGTH` function to return the number of features for each product:

```sql
SELECT
	ARRAY_LENGTH(comment_matrix, 1) comment_groups,
	ARRAY_LENGTH(comment_matrix, 2) comments_in_group
FROM product_reviews;
```

The `ARRAY_APPEND` appends an element to the end of an array. For example:

```sql
UPDATE product_reviews
SET rating_history = ARRAY_APPEND(rating_history, 3)
WHERE product_id = 1;
```

To delete all occurrences of an element from an array, we use the `ARRAY_REMOVE` function: `ARRAY_REMOVE(array, element)`. The below code removes all occurrences of 3 in the `rating_history` array:

```sql
UPDATE product_reviews
SET rating_history = ARRAY_REMOVE(rating_history, 3)
WHERE product_id = 1;
```

<hr>

### `XML` Data Type

PostgreSQL supports built-in `XML` data type that allows us to store well-formed XML documents and XML fragments. To define a column of the `XML` type, we use the following syntax:

```sql
column_name XML
```

The built-in `XML` data type has the following advantages over using `TEXT` data type to store XML:

- Type safety: PostgreSQL validates XML, ensuring the XML data is valid.
- Built-in functions: PostgreSQL offers built-in functions to help us manipulate XML data effectively.

```sql
INSERT INTO
  xproducts (data)
VALUES
  (
    XMLPARSE(
      DOCUMENT '<?xml version="1.0" encoding="UTF-8"?><product>
    <name>Samsung Galaxy S24</name>
    <price>999.99</price>
    <safety_stock>10</safety_stock>
</product>'
    )
  );
```

In this statement:

- `DOCUMENT` instructs PostgreSQL that the following string is a complete XML document.
- `XMLPARSE` function converts the string into an XML document.

To retrieve the product names from the XML data, we use the `xpath` function:

```sql
SELECT
  xpath('/product/name/text()', data) AS name
FROM
  xproducts;
```

<hr>

### `ENUM`

PostgreSQL allows us to define a column that stores a list of fixed values using an enum. To create an enum, we use the `CREATE TYPE` statement with the following syntax:

```sql
CREATE TYPE enum_name
AS
ENUM(value1, value2, value3);
```

- Enum values are case-sensitive.
- A value in the `ENUM()` is lower than the value that appears after it and higher than before.

Here is an example of creating an enum:

```sql
CREATE TYPE delivery_status AS ENUM (
  'pending',
  'shipped',
  'in_transit',
  'delivered',
  'cancelled'
);
```

To define a column with an enum type, you use the following syntax:

```sql
column_name enum_name
```

The `column_name` can only store values defined in the `enum_name`. If you insert or update a value not in the list, PostgreSQL will issue an error.

```SQL
CREATE TABLE deliveries (
	id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
	user_id INT NOT NULL REFERENCES users(user_id),
	product_id INT NOT NULL REFERENCES products(product_id),
	status delivery_status DEFAULT 'pending',
	updated_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP
);
```

You can use the `ALTER TYPE` statement to add a new value to an existing enum with the following syntax:

```sql
ALTER TYPE enum_name
ADD VALUE [IF NOT EXISTS] new_value
[{BEFORE | AFTER } existing_value];
```

Here is an example on the enum created earlier:

```sql
ALTER TYPE delivery_status
ADD VALUE IF NOT EXISTS 'return_scheduled'
AFTER 'cancelled';
```

If new value's position is not defined, the default position is the end of the list.

The `ENUM_RANGE()` function accepts an enum and returns the enum values as an array:

```sql
ENUM_RANGE(null::enum_name)
```

For example:

```sql
SELECT ENUM_RANGE(NULL::delivery_status);
```

The `ENUM_FIRST` and `ENUM_LAST` functions return the first and last values of an enum:

```sql
SELECT
  ENUM_FIRST(NULL::enum_name) alias,
  ENUM_LAST(NULL::enum_name) alias;
```

For example:

```sql
SELECT
	ENUM_FIRST(NULL::delivery_status),
	ENUM_LAST(NULL::delivery_status);
```

You can use the `ALTER TYPE ... RENAME VALUE` statement to change the value of an enum to the new one:

```sql
ALTER TYPE enum_name
RENAME VALUE existing_value TO new_value;
```

For example:

```sql
ALTER TYPE delivery_status
RENAME VALUE 'pending' TO 'ordered';
```

<hr>

### `RECORD`

The `RECORD` data type represents a single row of a query’s result set. Here’s the syntax for declaring a `RECORD` variable:

```sql
DECLARE
    variable_name RECORD;
```

The `RECORD` type variable does not have a predefined structure. It inherits the structure of the row when you assign a row to it using the `SELECT INTO` or `FOR` statement.

```sql
DO $$
DECLARE
    v_record RECORD;
BEGIN
    SELECT select_list INTO v_record
    FROM table_name
    WHERE condition;
END;
$$;
```

```sql
DO $$
DECLARE
    v_record RECORD;
BEGIN
    FOR v_record IN
        SELECT select_list
        FROM table_name
        WHERE condition
    LOOP
        -- processing each row
    END LOOP;
END;
$$;
```

To access a field in a record, you use the dot notation syntax as follows:

```sql
v_record.field_name
```

<hr>

### `JSON`

PostgreSQL has two built-in data types for storing JSON:

- `JSON`: stores an exact copy of JSON data.
- `JSONB`: stores the JSON data in binary format.

The following table shows key differences between JSON and JSONB types in PostgreSQL:

| Feature           | JSON                                                | JSONB                                                                |
| ----------------- | --------------------------------------------------- | -------------------------------------------------------------------- |
| Storage           | Text                                                | Binary storage format                                                |
| Size              | Bigger because PostgreSQL has to retain whitespace. | Smaller                                                              |
| Indexing          | Full-text search indexes                            | Binary indexes                                                       |
| Query performance | Slower due to parsing                               | Faster due to binary storage                                         |
| Parsing           | Parse each time                                     | Parse once, store in binary format                                   |
| Ordering of keys  | Preserved                                           | Not preserved                                                        |
| Duplicate keys    | Allow duplicate key, the last value is retained     | Do not allow duplicate keys.                                         |
| Use cases         | Only if you want to preserve the order of the keys. | Storing JSON documents where fast querying and indexing are required |

Here is an example of creating a table with `JSON` data type:

```sql
CREATE TABLE user_preferences (
  pref_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  user_id INT REFERENCES users(user_id),
  preferences JSON NOT NULL
);
```

Here is an example of storing JSON data in a table:

```sql
INSERT INTO user_preferences (user_id, preferences)
VALUES
  (1, '{"theme": "dark", "notifications": {"email": true, "sms": false}, "language": "en"}'),
  (2, '{"theme": "light", "notifications": {"email": false, "sms": true}, "language": "tr"}'),
  (4, '{"theme": "dark", "notifications": {"email": true, "sms": true}, "language": "es"}');
```

We use the operator `->` to extract a JSON value by a key. A JSON value is surrounded by double quotes.

```sql
SELECT u.username, p.preferences -> 'theme' theme FROM user_preferences p
JOIN users u ON u.user_id = p.user_id;
```

To return a JSON value as text, we use the operator `->>`.

```sql
SELECT u.username, p.preferences ->> 'theme' theme FROM user_preferences p
JOIN users u ON u.user_id = p.user_id;
```

Here is a more complex example:

```sql
SELECT
  u.username,
  p.preferences -> 'notifications' -> 'email' email
FROM user_preferences p
JOIN users u ON u.user_id = p.user_id;
```

Here is an example of using the JSON data with the `WHERE` clause:

```sql
SELECT
  u.username,
  p.preferences->'notifications'->>'email' AS email_notifications
FROM user_preferences p
JOIN users u ON u.user_id = p.user_id
WHERE p.preferences->'notifications'->>'email' = 'true';
```

The function `jsonb_set` updates a JSON object field with a new value. Here is the syntax:

```sql
UPDATE
  my_table
SET
  json_column = jsonb_set(
    json_column, '{field_name}', '"new_value"'
  )
WHERE
  id = 1;
```

Here is an example:

```sql
UPDATE user_preferences
SET preferences = jsonb_set(preferences::jsonb, '{notifications, sms}', 'true')
WHERE user_id = 1;
```

Here is another example:

```sql
UPDATE user_preferences
SET preferences = jsonb_set(preferences::jsonb, '{theme}', '"dark"')
WHERE user_id = 2;
```

<hr>
<hr>

## Cast

To convert a value of one data type to another, we use the `CAST()` function or cast operator (`::`).

```sql
CAST(value AS target_type);
-- or
value::target_type
```

Here is an example of casting a string to an integer:

```sql
SELECT CAST('10' AS INT) result;
-- or
SELECT '10'::INT result;
```

PostgreSQL can sometimes automatically cast a value to a specific one without requiring the `CAST` function or operator. For example:

```sql
SELECT 1 + '2' result;
```

In this example, PostgreSQL automatically converts the string '2' to an integer and adds it to the number 1.

<hr>
<hr>

## Triggers

### Creating Triggers

In PostgreSQL, a trigger is a user-defined function or procedure invoked automatically when an event such as `INSERT`, `UPDATE`, `DELETE`, or `TRUNCATE` occurs on a table or view.

Triggers include four key components:

- Trigger events
- Trigger timing
- Trigger function
- Trigger scope

Trigger events are events that cause the trigger to fire. In PostgreSQL, the trigger events are:

- `INSERT`
- `UPDATE`
- `DELETE`
- `TRUNCATE`

Trigger timing specifies the time when the triggers fire:

- `BEFORE` – Executes the trigger function before the triggering event.
- `AFTER` – Executes the trigger function after the triggering event.
- `INSTEAD OF` – Executes the trigger function instead of the triggering event.

The trigger function must be defined before the trigger itself can be created. The trigger function must be declared as a function taking no arguments and returning type `TRIGGER`. Inside trigger functions, you can access special variables such as `TG_OP`, `NEW`, and `OLD`.

- The `TG_OP` variable stores the operation that causes the trigger to fire. It can be `'INSERT'`, `'UPDATE'` ,`'DELETE'` and `'TRUNCATE'`.
- The `NEW` variable stores the new row. This variable is available only when the operation is `'INSERT'` or `'UPDATE'`.
- The `OLD` variable stores the old row, available in the `'UPDATE'` or `'DELETE'` operation.

Trigger Scope:

- Row-level: The trigger function executes for every affected row. For example, if you issue an `UPDATE` statement that updates 10 rows, the trigger will fire 10 times, each per row.
- Statement-level: The trigger function executes per SQL statement. For example, if you run an `UPDATE` statement, the statement-level trigger will fire once, regardless of the number of rows updated.

To create a trigger, you follow these steps:

- First, define a user-defined function or procedure to execute when the trigger fires.
- Second, associate the trigger function with a trigger using the `CREATE TRIGGER` statement.

```sql
CREATE [OR REPLACE] TRIGGER trigger_name
{ BEFORE | AFTER | INSTEAD OF }
{ INSERT | DELETE | TRUNCATE | UPDATE [OF column_name, ...] }
ON table_name
[ FOR [ EACH ] { ROW | STATEMENT } ]
[ WHEN condition ]
EXECUTE { FUNCTION | PROCEDURE } function_name(arguments);
```

Here is an example of creating a trigger:

```sql
-- create a table to save logs
CREATE TABLE transaction_log (
  log_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  user_id INT,
  product_id INT,
  quantity INT,
  logged_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP
);

-- trigger function
CREATE OR REPLACE FUNCTION log_new_transaction()
RETURNS TRIGGER AS
$$
BEGIN
  INSERT INTO transaction_log (user_id, product_id, quantity)
  VALUES (NEW.user_id, NEW.product_id, NEW.quantity);

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- trigger
CREATE OR REPLACE TRIGGER after_transaction_insert
AFTER INSERT ON transactions
FOR EACH ROW
EXECUTE FUNCTION log_new_transaction();

-- Insert a sample transaction
INSERT INTO transactions (user_id, product_id, quantity, price)
VALUES (3, 2, 1, 50.00);

SELECT * FROM transactions ORDER BY created_at DESC;

-- Check the log table
SELECT * FROM transaction_log ORDER BY log_id DESC;
```

<hr>

### Disabling and Enabling Triggers

To disable a trigger, you can use the `ALTER TABLE ... DISABLE TRIGGER` statement with the following syntax:

```sql
ALTER TABLE table_name
DISABLE TRIGGER trigger_name | ALL;
```

Here is an example of disabling a trigger:

```sql
ALTER TABLE transactions
DISABLE TRIGGER after_transaction_insert;
```

If you want to turn off all table triggers, you can use the `ALL` keyword instead of disabling a trigger individually.

To enable a trigger, you use the `ALTER TABLE ... ENABLE TRIGGER` statement:

```sql
ALTER TABLE table_name
ENABLE TRIGGER trigger_name | ALL;
```

Here is an example:

```sql
ALTER TABLE transactions
ENABLE TRIGGER after_transaction_insert;
```

<hr>

### Dropping Triggers

The `DROP TRIGGER` statement removes a trigger from a specific table within your database.

Here’s the syntax of the `DROP TRIGGER` statement:

```sql
DROP TRIGGER [IF EXISTS] trigger_name
ON table_name
[CASCADE | RESTRICT];
```

Here is an example:

```sql
DROP TRIGGER IF EXISTS after_transaction_insert
ON transactions
CASCADE;
```

<hr>

### Event Triggers

Unlike regular triggers, event triggers are not associated with a table but a database. Event triggers respond to the database schema change events such as adding a column, dropping a table and so on. Only superusers can create event triggers. Another notable thing is that there is no `CREATE EVENT TRIGGER` statement in the SQL standard.

In PostgreSQL, event triggers can track the following events:

- `ddl_command_start`: fires at the start of any DDL command.
- `ddl_command_end`: fires at the end of any DDL command.
- `sql_drop`: fires after objects are dropped.
- `table_rewrite`: fires when a change in the table’s structure occurs.

You can create event triggers using the `CREATE EVENT TRIGGER` statement:

```sql
CREATE EVENT TRIGGER trigger_name
ON event_name
WHEN condition
EXECUTE FUNCTION function_name();
```

The event trigger function returns `EVENT_TRIGGER` instead of `TRIGGER`. Additionally, it does not have any `RETURN` statement like a regular trigger function.

To turn off an event trigger, you use the `ALTER EVENT TRIGGER` statement:

```sql
ALTER EVENT TRIGGER event_trigger_name
DISABLE;
```

To enable an event trigger, you also use the `ALTER EVENT TRIGGER` statement but with the `ENABLE` option:

```sql
ALTER EVENT TRIGGER event_trigger_name
ENABLE;
```

If you no longer use an event trigger, you can drop it using the `DROP EVENT TRIGGER` statement:

```sql
DROP EVENT TRIGGER event_trigger_name;
```

To get all event triggers, you can query from the `pg_event_trigger` in the PostgreSQL system catalogs:

```sql
SELECT * FROM pg_event_trigger;
```

<hr>
<hr>

## Window functions

### Adding more data to practice window functions

```sql
-- Add extra transactions to users so they have multiple rows
INSERT INTO transactions (user_id, product_id, quantity, price)
VALUES
  (1, 3, 1, 250.00),  -- ziya
  (1, 4, 2, 35.00),   -- ziya

  (4, 3, 1, 250.00),  -- fatima
  (4, 4, 1, 35.00),   -- fatima

  (10, 3, 1, 250.00); -- emine
```

<hr>

### Intro

A window function call represents the application of an aggregate-like function over some portion of the rows selected by a query. Unlike non-window aggregate calls, this is not tied to grouping of the selected rows into a single output row — each row remains separate in the query output. However the window function has access to all the rows that would be part of the current row's group according to the grouping specification (`PARTITION BY` list) of the window function call.

Here’s the basic syntax for a window function:

```sql
function_name (expression) OVER (
    [PARTITION BY expression_list]
    [ORDER BY expression_list]
    [frame_clause]
)
```

In this syntax:

- `function_name`: The window function name such as `MAX`.
- `expression`: The column or expression you want the window function to calculate.
- `PARTITION BY`: This optional clause groups the rows into partitions where the window function applies.
- `ORDER BY`: This clause defines the order of rows within each partition. Note that it differs from the `ORDER BY` clause in the `SELECT` statement.
- `frame_clause`: This clause defines the subset of rows within the partition for the window function to consider.

The optional `frame_clause` can be one of

```sql
{ RANGE | ROWS | GROUPS } frame_start [ frame_exclusion ]
{ RANGE | ROWS | GROUPS } BETWEEN frame_start AND frame_end [ frame_exclusion ]
```

- `ROWS`: This mode allows you to define the frame in terms of physical rows. When you specify `ROWS`, you're telling PostgreSQL to count the exact number of rows from the current row to determine the frame. This mode is ideal when you need a fixed number of rows for your calculation, such as when calculating moving averages or running totals that span a specific row count.
- `RANGE`: Unlike `ROWS`, the `RANGE` mode focuses on the values of the ordering column(s) to define the frame. It groups rows that have the same values as the current row in the ordering column(s), effectively treating rows with identical values as a single entity in the calculation. `RANGE` is particularly useful for dealing with duplicate values in the dataset.

The `frame_start` and `frame_end` can be one of:

```sql
UNBOUNDED PRECEDING
offset PRECEDING
CURRENT ROW
offset FOLLOWING
UNBOUNDED FOLLOWING
```

Whenever we use a window function, it creates a 'window' or a 'partition' depending upon the column mentioned after the `partition by` clause in the `over` clause. And then it applies that window function to each of those partitions and inside these partitions, we can create a subset of records using the `frame_clause`. Therefore, the `frame_clause` specifies a subset. A `frame_start` of `UNBOUNDED PRECEDING` means that the frame starts with the first row of the partition, and similarly a `frame_end` of `UNBOUNDED FOLLOWING` means that the frame ends with the last row of the partition. There is a default frame that SQL uses with every window function. The default frame is a `range between unbounded preceding and current row`.

There are three kinds of window functions in PostgreSQL:

- Ranking Window Functions
  - `ROW_NUMBER`
  - `RANK`
  - `DENSE_RANK`
  - `PERCENT_RANK`
  - `NTILE`
  - `CUME_DIST`
- Value Window Functions
  - `FIRST_VALUE`
  - `LAST_VALUE`
  - `LEAD`
  - `LAG`
  - `NTH_VALUE`
- Aggregate Window Functions

<hr>

### `ROW_NUMBER()`

`ROW_NUMBER` returns the number of the current row starting from 1. Here is the syntax for the `ROW_NUMBER` window function:

```sql
ROW_NUMBER() OVER (
    [PARTITION BY expression_list]
    [ORDER BY expression_list]
    [frame_clause]
)
```

Here is an example:

```sql
SELECT
	u.username,
	t.amount,
	ROW_NUMBER() OVER (
		PARTITION BY t.user_id
		ORDER BY t.amount DESC
	) as tx_rank
FROM transactions t
JOIN users u ON t.user_id = u.user_id
ORDER BY u.username, tx_rank;
```

<hr>

### `RANK()`

`RANK` returns the rank of the current row with gaps. Here’s the syntax of the `RANK()` window function:

```sql
RANK() OVER (
    [PARTITION BY partition_expresion]
    [ORDER BY sort_expression]
    [frame_clause]
)
```

If you omit the optional `PARTITION BY` and `ORDER BY` clauses, the `RANK()` function will treat all the rows as peers and assign them the same rank (1). Therefore, the `RANK()` function works properly only when you have at least the `ORDER BY` clause.

Here is an example:

```sql
SELECT
	u.country,
	u.username,
	t.amount,
	RANK() OVER (
		PARTITION BY u.country
		ORDER BY t.amount DESC
	) AS country_rank
FROM users u
JOIN transactions t ON u.user_id = t.user_id
ORDER BY u.country, country_rank;
```

<hr>

### `DENSE_RANK()`

`DENSE_RANK` returns the rank of the current row without gaps. Here’s the syntax of the `DENSE_RANK()` function:

```sql
DENSE_RANK() OVER (
    [PARTITION BY expression_list]
    [ORDER BY expression_list]
    [frame_clause]
)
```

Here is an example:

```sql
SELECT
	u.country,
	u.username,
	t.amount,
	DENSE_RANK() OVER (
		PARTITION BY u.country
		ORDER BY t.amount DESC
	) AS country_rank
FROM users u
JOIN transactions t ON u.user_id = t.user_id
ORDER BY u.country, country_rank;
```

<hr>

### `PERCENT_RANK()`

`PERCENT_RANK` returns relative rank of each row in a set. Here’s the syntax of the `PERCENT_RANK()` function:

```sql
PERCENT_RANK() OVER (
    [PARTITION BY expression_list]
    [ORDER BY expression_list]
    [frame_clause]
)
```

Here is an example:

```sql
SELECT
	u.country,
	u.username,
	t.amount,
	PERCENT_RANK() OVER (
		PARTITION BY u.country
		ORDER BY t.amount DESC
	) AS country_rank
FROM users u
JOIN transactions t ON u.user_id = t.user_id
ORDER BY u.country, country_rank;
```

<hr>

### `NTILE`

`NTILE` divides rows within into roughly equal-sized buckets and assigns a tile number to each row. Here’s the syntax for the `NTILE()` window function:

```sql
NTILE(num_tiles) OVER (
    [PARTITION BY partition_expression]
    [ORDER BY sort_expression]
    [frame_clause]
)
```

- `num_tiles`: The number of tiles or groups you want to divide the result set into.

Here is an example:

```sql
SELECT
  u.country,
  u.username,
  t.amount,
  NTILE(3) OVER (
  	PARTITION BY u.country
    ORDER BY t.amount DESC
  ) AS buckets
FROM users u
JOIN transactions t ON u.user_id = t.user_id;
```

<hr>

### `CUME_DIST`

`CUME_DIST` returns the cumulative distribution of a value in a set. Here’s the syntax of the `CUME_DIST()` window function:

```sql
CUME_DIST() OVER (
  [PARTITION BY partition_expression]
  [ORDER BY sort_expression]
  [frame_clause]
)
```

Here is an example:

```sql
SELECT
  u.country,
  u.username,
  t.amount,
  CUME_DIST() OVER (
    PARTITION BY u.country
    ORDER BY t.amount
  ) AS cume_distribution
FROM users u
JOIN transactions t ON u.user_id = t.user_id;
```

<hr>

### `FIRST_VALUE`

`FIRST_VALUE` returns the value of the first row in each partition. Here’s the basic syntax of the `FIRST_VALUE` window function:

```sql
FIRST_VALUE (expression) OVER (
    [PARTITION BY partition_expression]
    [ORDER BY sort_expression]
    [frame_clause]
)
```

Here is an example:

```sql
SELECT
  u.username,
  t.amount,
  t.created_at,
  FIRST_VALUE(t.amount) OVER (
    PARTITION BY u.user_id
    ORDER BY t.created_at
  ) AS first_transaction_amount
FROM users u
JOIN transactions t ON u.user_id = t.user_id;
```

<hr>

### `LAST_VALUE`

`LAST_VALUE` returns the value of the last row in each partition. Here’s the basic syntax of the `LAST_VALUE` window function:

```sql
LAST_VALUE (expression) OVER (
     [PARTITION BY partition_expression]
     [ORDER BY sort_expression]
     [frame_clause]
)
```

Here is an example:

```sql
SELECT
  u.username,
  t.amount,
  t.created_at,
  LAST_VALUE(t.amount) OVER (
    PARTITION BY u.user_id
    ORDER BY t.created_at DESC
	ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
  ) AS last_transaction_amount
FROM users u
JOIN transactions t ON u.user_id = t.user_id;
```

<hr>

### `LEAD()`

The `LEAD()` function provides access to a row that follows the current row at a specified physical offset. Here’s the basic syntax of the `LEAD()` window function:

```sql
LEAD(expression [,offset [,default]])
OVER (
    [PARTITION BY partition_expression]
    [ORDER BY sort_expression]
    [frame_clause]
)
```

- `offset`: a positive integer that indicates the number of rows after the current row.
- `default`: the value to return if the row at the offset from the current row does not exist. If you don’t provide a default and the row does not exist, the `LEAD()` function returns NULL.

Here is an example:

```sql
SELECT
  u.username,
  t.amount,
  t.created_at,
  LEAD(t.amount) OVER (
    PARTITION BY u.user_id
	ORDER BY t.created_at
  ) AS next_amount
FROM users u
JOIN transactions t ON u.user_id = t.user_id;
```

<hr>

### `LAG()`

The `LAG()` function allows to access data of the previous row from the current row. Here’s the syntax of the PostgreSQL `LAG` window function:

```sql
LAG(value[, offset [, default]])
OVER (
    [PARTITION BY partition_expression]
    [ORDER BY sort_expression]
    [frame_clause]
)
```

- `offset`: Specifies the number of rows back from the current row you want to retrieve the value. The offset defaults to 1, which accesses the previous row’s value.
- `default`: This is the default value if the previous row does not exist. If you don’t specify a default value, the function returns NULL if the current row is the first row in the partition, which has no previous row.

Here is an example:

```sql
SELECT
  u.username,
  t.amount,
  t.created_at,
  lag(t.amount) OVER (
    PARTITION BY u.user_id
	ORDER BY t.created_at
  ) AS prev_transaction_amount
FROM users u
JOIN transactions t ON u.user_id = t.user_id;
```

<hr>

### `NTH_VALUE ()`

`NTH_VALUE` returns the value of the nth row within a window frame, helpful for accessing specific rows. Here’s the syntax of the `NTH_VALUE()` window function:

```sql
NTH_VALUE(value, n) OVER (
    [PARTITION BY partition_expression]
    [ORDER BY sort_expression]
    [frame_clause]
)
```

`n`: Specifies the row number within the window frame from which the `NTH_VALUE` function retrieves the value. If the nth row does not exist, the `NTH_VALUE()` function returns NULL.

Here is an example:

```sql
SELECT
	u.username,
	t.amount,
	t.created_at,
	NTH_VALUE(t.amount, 2) OVER (
		PARTITION BY u.user_id
		ORDER BY t.created_at
		ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
	) AS second_transaction_amount
FROM transactions t
JOIN users u ON u.user_id = t.user_id;
```

<hr>

### `MIN` Window Function

The `MIN()` window function returns the minimum value in a set of values within a partition.

Here’s the syntax of the `MIN()` window function:

```sql
MIN(value) OVER (
    [PARTITION BY partition_expression]
    [ORDER BY sort_expression]
    [frame_clause]
)
```

Here is an example:

```sql
SELECT
	u.username,
	t.amount,
	t.created_at,
	MIN(t.amount) OVER(
		PARTITION BY t.user_id
	) AS min_amount_for_user
FROM transactions t
JOIN users u ON t.user_id = u.user_id;
```

<hr>

### `MAX` Window Function

The `MAX()` window function returns the maximum value in a set of values within a partition.

Here’s the syntax of the `MAX()` window function:

```sql
MAX(value) OVER (
    [PARTITION BY partition_expression]
    [ORDER BY sort_expression]
    [frame_clause]
)
```

Here is an example:

```sql
SELECT
	u.username,
	t.amount,
	t.created_at,
	MAX(t.amount) OVER(
		PARTITION BY t.user_id
	) AS max_amount_for_user
FROM transactions t
JOIN users u ON t.user_id = u.user_id;
```

<hr>

### `AVG` Window Function

The `AVG()` window function returns the average value in a set of values within a partition.

Here’s the syntax of the `AVG()` window function:

```sql
AVG(value) OVER (
    [PARTITION BY partition_expression]
    [ORDER BY sort_expression]
    [frame_clause]
)
```

Here is an example:

```sql
SELECT
	u.username,
	t.amount,
	t.created_at,
	ROUND(
		AVG(t.amount) OVER(
			PARTITION BY t.user_id
	), 2) AS avg_amount_for_user
FROM transactions t
JOIN users u ON t.user_id = u.user_id;
```

<hr>

### `COUNT` Window Function

The `COUNT()` window function returns the number of rows within a partition. Here’s the syntax of the `COUNT()` window function:

```sql
COUNT(value) OVER (
    [PARTITION BY partition_expression]
    [ORDER BY sort_expression]
    [frame_clause]
)
```

Here is an example:

```sql
SELECT
	u.username,
	t.amount,
	t.created_at,
	COUNT(*) OVER(
		PARTITION BY t.user_id
	) AS user_transaction_count
FROM transactions t
JOIN users u ON t.user_id = u.user_id;
```

<hr>

### `SUM` Window Function

The `SUM()` window function returns the sum of values within a partition.

Here’s the syntax of the `SUM()` window function:

```sql
SUM(value) OVER (
    [PARTITION BY partition_expression]
    [ORDER BY order_expression]
    [frame_clause]
)
```

Here is an example:

```sql
SELECT
	u.username,
	t.amount,
	t.created_at,
	SUM(t.amount) OVER (
	    PARTITION BY t.user_id
	) AS total_spent_by_user
FROM transactions t
JOIN users u ON t.user_id = u.user_id;
```

<hr>
<hr>

## Loops

Looping constructs in PostgreSQL must be used inside a PL/pgSQL code block, which can be:

- An anonymous code block (`DO $$ ... $$;`)
- A PL/pgSQL function (`CREATE FUNCTION ... LANGUAGE plpgsql;`)
- A stored procedure (`CREATE PROCEDURE ... LANGUAGE plpgsql;`)

---

### `LOOP`

The `LOOP` statement allows to execute a code block repeatedly. Here’s the basic syntax of the `LOOP` statement:

```sql
-- optional loop label
<<label>>
LOOP
    statement;
END LOOP [label];
```

Typically, WE use an `IF` statement to terminate the loop based on a condition like this:

```sql
<<label>>
loop
   statements;
   if condition then
      exit;
   end if;
end loop;
```

When we have nested loops, it’s necessary to use loop labels.

---

### `WHILE`

The `WHILE` statement allows you to execute a code block repeatedly if a condition is true. Since the `WHILE` statement evaluates the condition before each iteration, it is known as a pretest loop. Here’s the syntax of the `WHILE` statement:

```sql
[<<label>>]
WHILE condition LOOP
    statements;
END LOOP;
```

---

### `FOR`

The `FOR` loop statement creates a loop that iterates over a range of integers or rows of a result set. Here’s the basic syntax of the `FOR` loop statement that iterates over a range of integers from low to high:

```sql
<<label>>
FOR loop_counter IN low..high LOOP
    statements;
END LOOP [label];
```

By default, the `FOR` loop increments or decrements the loop counter by one after each iteration. If you want to change the step from 1 to another, you can use the `BY` option:

```sql
<<label>>
FOR loop_counter IN low..high [BY step] LOOP
    statements;
END LOOP [label];
```

If you use the `REVERSE` option, the FOR loop will decrement the loop counter after each iteration. Notice that the `high` and `low` are in reversed order.:

```sql
<<label>>
FOR loop_counter IN REVERSE high..low LOOP
    statements;
END LOOP [label];
```

To iterate over the rows of a result set, you use the following `FOR` loop statement:

```sql
[ <<label>> ]
FOR target IN query LOOP
    -- process individual row
END LOOP [ label ];
```

---

### Terminating a loop using `EXIT`

We can specify a condition for terminating the loop using the `IF` and `EXIT` statement:

```sql
<<label>>
LOOP
    statement;
    IF condition THEN
        EXIT;
    END IF;
END LOOP [label];
```

The `EXIT` statement terminates a loop, including `LOOP`, `FOR LOOP`, and `WHILE LOOP`. To terminate based on a condition, you can use the following syntax:

```sql
EXIT loop_label WHEN condition;
```

or:

```sql
EXIT WHEN condition;
```

---

### Skipping a loop using `CONTINUE`

The `CONTINUE` statement skips the remaining statements in the current iteration of a loop and starts a new iteration based on a condition.

We can use `CONTINUE` either this way:

```sql
CONTINUE;
```

or using an optional loop label:

```sql
CONTINUE loop_label;
```

We can use `CONTINUE` with an `IF` clause:

```sql
IF condition THEN
    CONTINUE;
END IF;
```

or use a more concise syntax:

```sql
CONTINUE WHEN condition;
```

---

---

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
  - [Subqueries](#subqueries)
  - [Common Table Expressions](#common-table-expressions)
  - [Views](#views)
  - [Joins](#joins)
  - [Conditional Expressions](#conditional-expressions)
  - [Sequence](#sequence)
  - [Identity Column](#identity-column)
  - [Changing Tables](#changing-tables)
  - [PL/pgSQL Block and Variables](#plpgsql-block-and-variables)
  - [User Defined Functions](#user-defined-functions)
  - [Special Variable Found](#special-variable-found)
  - [Exception Handling](#exception-handling)
  - [Stored Procedures](#stored-procedures)
  - [Index](#index)
  - [Denormalized Data Types](#denormalized-data-types)
  - [Triggers](#triggers)
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

## Subqueries

[Subqueries](./PSQL_Subqueries.md)

<hr>
<hr>

## Common Table Expressions

[Common Table Expressions](./PSQL_CommonTableExpressions.md)

<hr>
<hr>

## Views

[Views](./PSQL_Views.md)

<hr>
<hr>

## Joins

[Joins](./PSQL_Joins.md)

<hr>
<hr>

## Conditional Expressions

[Conditional Expressions](./PSQL_Conditionals.md)

<hr>
<hr>

## Sequence

[Sequence](./PSQL_Sequence.md)

<hr>
<hr>

## Identity Column

[Identity Column](./PSQL_IdentityColumn.md)

<hr>
<hr>

## Changing Tables

[Changing Tables](./PSQL_ChangingTables.md)

<hr>
<hr>

## PL/pgSQL Block and Variables

[PL/pgSQL Block and Variables](./PSQL_PLpgSQLBlockAndVariables.md)

<hr>
<hr>

## User Defined Functions

[User Defined Functions](./PSQL_UserDefinedFunctions.md)

<hr>
<hr>

## Special Variable Found

[Special Variable Found](./PSQL_SpecialVariableFound.md)

<hr>
<hr>

## Exception Handling

[Exception Handling](./PSQL_ExceptionHandling.md)

<hr>
<hr>

## Stored Procedures

[Stored Procedures](./PSQL_StoredProcedures.md)

<hr>
<hr>

## Index

[Index](./PSQL_Index.md)

<hr>
<hr>

## Denormalized Data Types

[Denormalized Data Types](./PSQL_DenormalizedDataTypes.md)

<hr>
<hr>

## Triggers

[Triggers](./PSQL_Triggers.md)

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

# Joins

- [Joins](#joins)
  - [Inner Join](#inner-join)
  - [Left Join](#left-join)
  - [Right Join](#right-join)
  - [Full Join](#full-join)
  - [Self-Join](#self-join)
  - [Cross Join](#cross-join)
  - [Natural Join](#natural-join)
  - [`USING`](#using)

---

---

## Inner Join

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

---

---

## Left Join

The `LEFT JOIN` clause merges rows from two tables and returns all rows from the left table and matching rows from the right table.

```sql
SELECT
  left_t.username,
  left_t.email,
  right_t.product_id
FROM users AS left_t
LEFT JOIN transactions AS right_t ON left_t.user_id = right_t.user_id;
```

---

---

## Right Join

The `RIGHT JOIN` includes all rows from the right table and matching rows from the left table.

```sql
SELECT
  left_t.username,
  left_t.email,
  right_t.product_id
FROM users AS left_t
RIGHT JOIN transactions AS right_t ON left_t.user_id = right_t.user_id;
```

---

---

## Full Join

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

---

---

## Self-Join

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

---

---

## Cross Join

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

---

---

## Natural Join

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

---

---

## `USING`

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

---

---

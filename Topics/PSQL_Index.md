# Indexes

- [Indexes](#indexes)
  - [Creating an index](#creating-an-index)
  - [Analyzing an index](#analyzing-an-index)
  - [Listing indexes](#listing-indexes)
  - [Dropping an index](#dropping-an-index)
  - [Unique Index](#unique-index)
  - [Expression Index](#expression-index)
  - [Partial Index](#partial-index)
  - [Covering Index](#covering-index)

---

---

PostgreSQL stores data of a table using a heap file storage model. Each table corresponds to a heap file. Each heap file consists of blocks (or pages). Typically, a block has a size of 8KB by default. Each block contains multiple tuples (or rows). Additionally, PostgreSQL maintains other information that determines which rows are accessible.

When retrieving data from a table, PostgreSQL has to read data from the heap file and load it to the memory for filtering the rows. A full table scan means that PostgreSQL must read all rows from a heap file (table) to memory and search for rows. Most of the time, a full table scan is not efficient because PostgreSQL must read every block, even if only a few rows match the condition.

An index is a separate data structure that allows PostgreSQL to locate rows quickly without scanning the table.

---

---

## Creating an index

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

---

---

## Analyzing an index

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

---

---

## Listing indexes

To list all the indexes, we can use the below code:

```sql
SELECT * FROM pg_indexes;
```

---

---

## Dropping an index

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

---

---

## Unique Index

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

---

---

## Expression Index

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

---

---

## Partial Index

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

---

---

## Covering Index

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

---

---

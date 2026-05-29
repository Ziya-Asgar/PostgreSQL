# Changing Tables

- [Changing Tables](#changing-tables)
  - [Renaming a table](#renaming-a-table)
  - [Renaming a column](#renaming-a-column)
  - [Adding new columns to a table](#adding-new-columns-to-a-table)
  - [Changing the column data type](#changing-the-column-data-type)
  - [Applying constraints to columns](#applying-constraints-to-columns)
  - [Dropping columns](#dropping-columns)
  - [Truncating a table](#truncating-a-table)

---

---

The `ALTER TABLE` statement allows us to modify the table structure:

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

---

---

## Renaming a table

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

---

---

## Renaming a column

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

---

---

## Adding new columns to a table

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

---

---

## Changing the column data type

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

---

---

## Applying constraints to columns

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

---

---

## Dropping columns

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

---

---

## Truncating a table

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

---

---

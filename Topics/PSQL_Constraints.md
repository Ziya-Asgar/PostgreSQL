# Constraints

- [Constraints](#constraints)
  - [`NOT NULL`](#not-null)
  - [`DEFAULT`](#default)
  - [`CHECK`](#check)
  - [`UNIQUE`](#unique)
  - [Primary and Foreign Keys](#primary-and-foreign-keys)
    - [Primary Key](#primary-key)
    - [Foreign Key](#foreign-key)

---

---

## `NOT NULL`

`NULL` represents the absence of a value, indicating that the data is unknown or missing.

If you compare `NULL` with any value, the comparison returns `NULL`. Even `NULL` is not equal to `NULL`; comparing `NULL` with `NULL` also results in `NULL`.

When you define a column for a table, that column is nullable. It means that you can insert `NULL` into the column. If we want a column to not have a null value (not be empty), we can use the `NOT NULL` constraint:

```sql
CREATE TABLE users (
  user_id INT,
  user_uuid UUID,
  username VARCHAR(50) NOT NULL,
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3),
  last_login_at TIMESTAMPTZ(3),
  membership_duration INTERVAL
);
```

---

---

## `DEFAULT`

We can specify a default value for a column with the flexible `DEFAULT` constraint.

```sql
CREATE TABLE users (
  user_id INT,
  user_uuid UUID,
  username VARCHAR(50) NOT NULL,
  is_active BOOL DEFAULT true,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3),
  last_login_at TIMESTAMPTZ(3),
  membership_duration INTERVAL
);
```

When you insert a row without providing a value for `is_active`, PostgreSQL will use the default value for insertion. You can also use the `DEFAULT` keyword to conveniently represent the default value while inserting data:

```sql
INSERT INTO
  table_name (column1, column2)
VALUES
  (DEFAULT, value2);
```

In PostgreSQL, the `TIMESTAMP` data type is used to store date and time values. When you want a `TIMESTAMP` column to have a default value, you can use the `DEFAULT` constraint with the `CURRENT_TIMESTAMP` function.

```sql
CREATE TABLE users (
  user_id INT,
  user_uuid UUID,
  username VARCHAR(50) NOT NULL,
  is_active BOOL DEFAULT true,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3) DEFAULT CURRENT_TIMESTAMP,
  last_login_at TIMESTAMPTZ(3),
  membership_duration INTERVAL
);
```

---

---

## `CHECK`

`CHECK` constraints maintain data integrity by ensuring that the value in a column must satisfy a Boolean expression. When a column has a `CHECK` constraint, and you attempt to insert or update a value that causes the Boolean expression to be false, PostgreSQL issues a constraint violation and rejects the changes.

```sql
CREATE TABLE users (
  user_id INT,
  user_uuid UUID,
  username VARCHAR(50) NOT NULL,
  is_active BOOL DEFAULT true,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2) CONSTRAINT constraint_name CHECK (account_balance >= 0),
  signup_timestamp TIMESTAMP(3) DEFAULT CURRENT_TIMESTAMP,
  last_login_at TIMESTAMPTZ(3),
  membership_duration INTERVAL
);
```

Note that the `CONSTRAINT constraint_name` is optional. If you omit it, PostgreSQL will automatically generate a constraint name. When a constraint is violated PostgreSQL will issue an error that includes the constraint name. This constraint name helps you detect where the problem is faster.

You use `ALTER TABLE ... ADD CONSTRAINT` statement to add a `CHECK` constraint to an existing table. Here’s the syntax of the statement:

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
CHECK (account_balance >=0 AND account_balance <= 1000000);
```

We can define the `CHECK` constraint as a table constraint. When you add it as a table constraint, it is written after all columns and can involve one or more columns.

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  account_balance DECIMAL(10, 2),
  is_active BOOL,
  CONSTRAINT chk_valid_user CHECK (account_balance >= 0 AND is_active IS NOT NULL)
);
```

To remove a `CHECK` constraint from a table, you use the `ALTER TABLE ... DROP CONSTRAINT` statement:

```sql
ALTER TABLE table_name
DROP CONSTRAINT IF EXISTS constraint_name;
```

---

---

## `UNIQUE`

A `UNIQUE` constraint in PostgreSQL is a mechanism used to ensure that the values in a particular column or a set of columns are unique across all rows in a table. Unlike a primary key, a `UNIQUE` constraint allows NULL values, but it ensures that the combination of values in the constrained columns is unique.

```sql
CREATE TABLE users (
  user_id INT,
  user_uuid UUID,
  username VARCHAR(50) NOT NULL UNIQUE,
  is_active BOOL DEFAULT true,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2) CONSTRAINT constraint_name CHECK (account_balance >= 0),
  signup_timestamp TIMESTAMP(3) DEFAULT CURRENT_TIMESTAMP,
  last_login_at TIMESTAMPTZ(3),
  membership_duration INTERVAL
);
```

You can define a `UNIQUE` constraint as a table constraint. In practice, you often define a `UNIQUE` table constraint when it includes two or more columns:

```sql
CREATE TABLE table_name (
  column1 data_type,
  column2 data_type,
  CONSTRAINT constraint_name UNIQUE (column1, column2)
);
```

---

---

## Primary and Foreign Keys

### Primary Key

A primary key is a column or a set of columns uniquely identifying each row in a table. If a primary key is a single column, you define the `PRIMARY KEY` constraint as a column constraint by adding `PRIMARY KEY` keywords after the primary key column.

```sql
CREATE TABLE users (
  user_id INT PRIMARY KEY,
  user_uuid UUID,
  username VARCHAR(50) NOT NULL UNIQUE,
  is_active BOOL DEFAULT true,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2) CONSTRAINT constraint_name CHECK (account_balance >= 0),
  signup_timestamp TIMESTAMP(3) DEFAULT CURRENT_TIMESTAMP,
  last_login_at TIMESTAMPTZ(3),
  membership_duration INTERVAL
);
```

When a primary key column has two or more columns, you can define the primary key as a table constraint:

```sql
CREATE TABLE table_name(
   column1 data_type,
   column2 data_type,
   column3 data_type,
   PRIMARY KEY (column1, column2)
);
```

In this syntax, the primary key includes column1 and column2. In other words, no two rows will have the same values in column1 and column2. When a primary key consists of two or more columns, it is called a **composite primary key**.

If you have a table that does not have a primary key, you can add one using the following `ALTER TABLE` statement:

```sql
ALTER TABLE table_name
ADD PRIMARY KEY (column1, column2, ...);
```

An auto-increment column is a popular choice for a primary key, due to its simplicity and efficiency. It automatically generates a unique number for each new row inserted into the table, eliminating the need for manual input and ensuring data uniqueness. To define an auto-increment column in PostgreSQL, we use the `GENERATED ALWAYS AS IDENTITY` attribute as follows:

```sql
column_name INT GENERATED ALWAYS AS IDENTITY
```

To define an auto-increment column as a primary key column, you add the `PRIMARY KEY` constraint:

```sql
column_name INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY
```

> Note the use of `SERIAL` is less recommended due to permission and lack of integrity issues.

---

### Foreign Key

A foreign key is a column or set of columns in one table that references the primary key of another table. It serves as a link between the two tables. A table may have multiple foreign key columns. By convention, the foreign key column has the format `table_id`.

The table with the foreign key column is called the child table, while the table with the primary key column that the child table references is known as the referenced or parent table.

When you delete a row in the parent table, you should handle the child table properly to avoid orphaned records. Note that orphaned records are records in a table referencing a non-existent primary key value in another table.

You use the foreign key constraint to set up a foreign key. Here’s the basic syntax for defining a foreign key constraint:

```sql
CONSTRAINT constraint_name
FOREIGN KEY (fk_column)
REFERENCES table(pk_column)
ON DELETE delete_action
ON UPDATE update_action;
```

The `FOREIGN KEY` and `REFERENCES` clauses are mandatory, while the `CONSTRAINT`, `ON DELETE`, and `ON UPDATE` clauses are optional.

Here is one example of creating table with a foreign key column

```sql
-- parent table
CREATE TABLE users (
  user_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  user_uuid UUID NOT NULL,
  username VARCHAR(50) NOT NULL UNIQUE,
  is_active BOOLEAN DEFAULT true,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2) CONSTRAINT chk_account_balance CHECK (account_balance >= 0),
  signup_timestamp TIMESTAMP(3) DEFAULT CURRENT_TIMESTAMP
);

-- child table
CREATE TABLE logins (
  login_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  user_id INT REFERENCES users(user_id),
  login_time TIMESTAMPTZ(3),
  session_duration INTERVAL
);
```

In the above example, we just used the `REFERENCES` keyword. Another approach is below:

```sql
-- parent table
CREATE TABLE users (
  user_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  user_uuid UUID NOT NULL,
  username VARCHAR(50) NOT NULL UNIQUE,
  is_active BOOLEAN DEFAULT true,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2) CONSTRAINT chk_account_balance CHECK (account_balance >= 0),
  signup_timestamp TIMESTAMP(3) DEFAULT CURRENT_TIMESTAMP
);

-- child table
CREATE TABLE logins (
  login_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  user_id INT,
  login_time TIMESTAMPTZ(3),
  session_duration INTERVAL,
  FOREIGN KEY (user_id) REFERENCES users(user_id)
);
```

The `delete_action` can be one of the following:

- `NO ACTION` – issues a constraint violation error. The `NO ACTION` is the default.
- `SET NULL` – sets the values of foreign key column to NULL.
- `CASCADE`– deletes all related rows in the child table.
- `SET DEFAULT` – sets the default values for the foreign key columns in the child table.
- `RESTRICT` works like the `NO ACTION`.

```sql
CREATE TABLE logins(
  login_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  user_id INT,
  login_time TIMESTAMPTZ(3),
  session_duration INTERVAL,
  FOREIGN KEY (user_id) REFERENCES users(user_id)
  ON DELETE CASCADE
);
```

When you drop a table referenced by other tables via foreign key constraints, PostgreSQL will issue an error. To drop the table with a foreign key constraint, you follow these steps:

- First, drop foreign key constraint.
- Second, drop the table

You can do both steps using the `DROP TABLE ... CASCADE` statement.

---

---

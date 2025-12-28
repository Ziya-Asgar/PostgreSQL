# postgreSQL

- [postgreSQL](#postgresql)
  - [Some Useful Links](#some-useful-links)
  - [Listing databases](#listing-databases)
  - [Creating a database](#creating-a-database)
  - [Deleting a database](#deleting-a-database)
  - [Listing tables](#listing-tables)
  - [Creating a table](#creating-a-table)
    - [Generated columns](#generated-columns)
  - [Deleting a table](#deleting-a-table)
  - [Data Types](#data-types)
    - [`BOOLEAN`](#boolean)
    - [`CHAR`](#char)
    - [`VARCHAR`](#varchar)
    - [`TEXT`](#text)
    - [`INTEGER`](#integer)
    - [`DECIMAL`](#decimal)
    - [`DATE`](#date)
    - [`TIME`](#time)
    - [`TIMESTAMP`](#timestamp)
    - [`TIMESTAMP WITH TIME ZONE`](#timestamp-with-time-zone)
    - [`INTERVAL`](#interval)
    - [`UUID`](#uuid)
  - [Constraints](#constraints)
    - [`NOT NULL`](#not-null)
    - [`DEFAULT`](#default)
    - [`CHECK`](#check)
    - [`UNIQUE`](#unique)
    - [Primary and Foreign Keys](#primary-and-foreign-keys)
      - [Primary Key](#primary-key)
      - [Foreign Key](#foreign-key)
  - [Inserting data into tables](#inserting-data-into-tables)
  - [Import and Export a CSV File](#import-and-export-a-csv-file)
    - [Import a CSV File](#import-a-csv-file)
    - [Export to a CSV File](#export-to-a-csv-file)
  - [Updating data](#updating-data)
  - [Deleting data from tables](#deleting-data-from-tables)
  - [Querying a database](#querying-a-database)
    - [Data for queries](#data-for-queries)
    - [Basic queries](#basic-queries)
    - [`DISTINCT` clause](#distinct-clause)
      - [`DISTINCT ON`](#distinct-on)
    - [Column aliases](#column-aliases)
    - [Querying with `WHERE`](#querying-with-where)
    - [Limiting and offsetting during the query](#limiting-and-offsetting-during-the-query)
    - [Querying with `BETWEEN`](#querying-with-between)
    - [Advanced Text Search](#advanced-text-search)
      - [Pattern matching with `LIKE` and `ILIKE`](#pattern-matching-with-like-and-ilike)
      - [Regular Expressions](#regular-expressions)
      - [`SIMILAR TO` Operator](#similar-to-operator)
    - [Full-text Search](#full-text-search)
    - [Grouping and aggregations](#grouping-and-aggregations)
      - [Grouping](#grouping)
      - [Aggregation functions](#aggregation-functions)
      - [`HAVING` clause](#having-clause)
      - [Grouping sets](#grouping-sets)
      - [`GROUPING` function](#grouping-function)
      - [`ROLLUP`](#rollup)
      - [`CUBE`](#cube)
    - [Set Operations](#set-operations)
      - [`UNION` and `UNION ALL`](#union-and-union-all)
      - [`INTERSECT`](#intersect)
      - [`EXCEPT`](#except)
  - [Some useful functions and operators](#some-useful-functions-and-operators)
    - [`IS NULL` Operator](#is-null-operator)
    - [`COALESCE`](#coalesce)
    - [`NULLIF`](#nullif)
    - [`GREATEST`](#greatest)
    - [`LEAST`](#least)
    - [`NOW`](#now)
    - [`EXTRACT`](#extract)
    - [`AGE`](#age)
    - [`DATE_TRUNC`](#date_trunc)
    - [`TO_CHAR`](#to_char)
    - [Concatenation](#concatenation)
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
  - [User-defined Functions](#user-defined-functions)
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

<hr>

## Some Useful Links

- https://www.postgresql.org/
- https://www.pgtutorial.com/
- https://neon.com/postgresql/tutorial
- https://datalemur.com/sql-tutorial
- https://www.youtube.com/watch?v=qw--VYLpxG4

<hr>
<hr>

## Listing databases

To list the existing databases, we use `list` or `\l` command in psql.

To list the databases using a query, we can use the below code:

```sql
SELECT *
FROM pg_catalog.pg_database;
```

That Postgres catalog contains a row for each database in the server.

<hr>
<hr>

## Creating a database

To create a database in postgreSQL, we use:

```sql
CREATE DATABASE db_name;
```

<hr>
<hr>

## Deleting a database

To delete a database, we use:

```sql
DROP DATABASE test;
```

<hr>
<hr>

## Listing tables

To list the existing tables, we use the `\d` command in psql.

Note that if we have sequences (auto incremented columns), `\d` will also show them. In case we have sequences, but want to see the list of tables, we can use the `\dt` command.

To list the tables in PGAdmin tool, we can use the below command:

```sql
SELECT tablename FROM pg_tables WHERE schemaname = 'public';
```

Another way to list all the tables is using this command:

```sql
SELECT table_name FROM INFORMATION_SCHEMA.TABLES
WHERE table_schema LIKE '%public%';
```

To describe the actual table, we use the `\d <table_name>` command in psql.

In PGAdmin tool, we can use the below command to get the details about a table:

```sql
SELECT *
FROM information_schema.COLUMNS
WHERE TABLE_NAME = '<table_name>';
```

<hr>
<hr>

## Creating a table

To create a table, we use the `CREATE TABLE` command. After the `CREATE TABLE table_name` clause, we specify column names as well as data types and optional constraints. Here is the syntax:

```sql
CREATE TABLE table_name (
  column_name data_type constraints_if_any
)
```

Here is an example:

```sql
CREATE TABLE users(
  user_id INT,
  username VARCHAR(50)
);
```

### Generated columns

A generated column is a special column that is always computed from other columns. There are two kinds of generated columns: stored and virtual. A stored generated column is computed when it is written (inserted or updated) and occupies storage as if it were a normal column. A virtual generated column occupies no storage and is computed when it is read. PostgreSQL currently implements only stored generated columns.

To create a generated column, use the `GENERATED ALWAYS AS` clause in `CREATE TABLE`, for example:

```sql
CREATE TABLE transactions (
  quantity INT NOT NULL CHECK (quantity > 0),
  price DECIMAL(8, 2) NOT NULL CHECK (price >= 0),
  amount DECIMAL(10, 2) GENERATED ALWAYS AS (quantity * price) STORED
);
```

The keyword `STORED` must be specified to choose the stored kind of generated column.

A generated column cannot be written to directly. In `INSERT` or `UPDATE` commands, a value cannot be specified for a generated column, but the keyword `DEFAULT` may be specified.

<hr>
<hr>

## Deleting a table

To delete a table, we use:

```sql
DROP TABLE table_name;
```

If you delete a table that does not exist, PostgreSQL will issue an error. However, with the `IF EXISTS` option, PostgreSQL will not issue any errors.

```sql
DROP TABLE IF EXISTS table_name;
```

The `DROP TABLE` statement can drop multiple tables at once.

If a table is referenced by another table, then PostgreSQL might raise an error while deleting the table. To delete the table, together with the columns referring to it, we use the `CASCADE` OPTION:

```sql
DROP TABLE IF EXISTS table_name CASCADE;
```

<hr>
<hr>

## Data Types

### `BOOLEAN`

We use the `BOOLEAN` keyword or `BOOL` to store Boolean data. The boolean type has three values:

- `true`
- `false`
- `NULL`

Besides `true` and `false`, PostgreSQL uses various representations for `true` and `false` in SQL queries:

| True   | False   |
| ------ | ------- |
| `true` | `false` |
| 't'    | 'f'     |
| 'true' | 'false' |
| 'y'    | 'n'     |
| 'yes'  | 'no'    |
| '1'    | '0'     |

Notice that all other values need to be surrounded by single quotes except `true` and `false`.

Here is an example of creating a table with the `BOOLEAN` data type:

```sql
CREATE TABLE users(
  user_id INT,
  username VARCHAR(50),
  is_active BOOL
);
```

<hr>

### `CHAR`

The `CHAR` type, also known as `CHARACTER`, is a fixed-length and blank-padded character type. Here’s the syntax for defining a column with the `CHAR` type:

```sql
column_name CHAR(n)
```

In this syntax, the column_name will store precisely n characters. If you store a string that is less than n, PostgreSQL will pad it with spaces to meet the required length. Note that if you use the `length()` function, PostgreSQL internally trim the spaces before returning the number of characters. To find the size of the stored characters, you can use the `octet_length()` function, which returns the number of bytes.

> In practice, you often use the `CHARACTER VARYING` (`VARCHAR`) type instead of the char type for storing text strings.

If you want a column to have an exact number of characters, no more, no less, you can use a `CHECK` constraint to enforce the rule.

Here is an example of creating a table with the `CHAR` data type:

```sql
CREATE TABLE users(
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50)
);
```

<hr>

### `VARCHAR`

The `CHARACTER VARYING` type, or `VARCHAR`, allows you to store variable-length strings in the database. Unlike the `CHAR` column, PostgreSQL does not pad spaces if the values stored in the `VARCHAR` column have a length of less than n. Here’s the syntax for defining a column with the `CHARACTER VARYING` type:

```sql
column_name CHARACTER VARYING (n)
column_name VARCHAR(n)
```

In this syntax, specify the length specifier (n) that is the maximum number of characters the `VARCHAR` column can store. n is a positive integer and cannot exceed 10,485,760.

If you want to store a string with any length, you can omit the length specifier in the column definition:

```sql
column_name VARCHAR
```

<hr>

### `TEXT`

The `TEXT` data type is a variable-length character data type. The main features of the `TEXT` data type column are:

- Variable length: The `TEXT` column can store strings of any length, up to 1GB. 1GB is the field length limit in PostgreSQL, not only `TEXT` field.
- Trailing spaces: The `TEXT` column retains trailing spaces and does not trim them upon retrieval. These trailing spaces are significant when making comparisons.
- Performance: The `TEXT` type has the same performance as the `VARCHAR` type.

> Note that `VARCHAR`, without a length specifier, behaves like `TEXT`.

Here is an example of creating a table with the `TEXT` data type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT
);
```

<hr>

### `INTEGER`

PostgreSQL supports the following integer data types for storing integers:

- `SMALLINT`
- `INTEGER`. `INT` is the synonym of the `INTEGER` so that we can use them interchangeably.
- `BIGINT`

| Name       | Storage Size | Minimum value              | Maximum value              |
| ---------- | ------------ | -------------------------- | -------------------------- |
| `SMALLINT` | 2 bytes      | -32,768                    | +32,767                    |
| `INTEGER`  | 4 bytes      | -2,147,483,648             | +2,147,483,647             |
| `BIGINT`   | 8 bytes      | -9,223,372,036,854,775,808 | +9,223,372,036,854,775,807 |

<hr>

### `DECIMAL`

`DECIMAL` is a numeric data type that allows you to store exact numeric values with precision. `DEC` and `NUMERIC` are synonyms of the `DECIMAL`, so you can use them interchangeably.

```sql
CREATE TABLE table_name(
  column_name DEC(p,s),
);
```

In this syntax:

- p stands for precision. The precision is the number of significant digits, including integer and fractional parts.
- s stands for scale. The scale is the number of digits to the right of the decimal point. The valid range for scale is from -1000 to 1000.

For example, a `DEC(11,2)` column can store a number with 11 digits, including two digits after the decimal point.

If you omit the scale, it will default to zero: `DEC(p)` is equivalent to `DEC(p,0)`.

However, the precision and scale will default to their above limits if you ignore both precision and scale: `DEC`.

Starting from PostgreSQL 15, you can declare a decimal column with a negative scale: `DEC(p,-s)`. In this syntax, PostgreSQL will round the number to the left of the decimal point.

Besides regular values, the decimal type supports several special values specified in the IEEE 754 standard:

- `Infinity` - represents an infinitely large value.
- `-Infinity` - represents an infinitely small value.
- `NaN` (not-a-number) - represents a value that is not a number, which results from an invalid calculation.

When using these values in SQL statements, you must place them in a single quote like `'Infinity'` , `'-Infinity'`, and `'NaN'`.

Here is an example of creating a table with the `DECIMAL` data type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2)
);
```

<hr>

### `DATE`

We use the `DATE` data type to store date without time.

```sql
CREATE TABLE table_name (
  column_name DATE,
);
```

A date column can store a date between 4713 BC and 5874897 AD. PostgreSQL uses a 4-byte to store a date value. PostgreSQL accepts various date formats, but it is recommended to use ISO 8601, which is yyyy-mm-dd for date input.

Here is an example of create a table with the `DATE` type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_date DATE
);
```

We use the `SET datestyle` command to change the format for the current session. For example, to set the style to ISO with DMY ordering, we execute `SET datestyle TO 'ISO, DMY'`. To see the datestyle setting, we can use `SHOW datestyle;`.

If you want to set the current date as the default value, you can use the `CURRENT_DATE` function as follows:

```sql
CREATE TABLE table_name (
  column_name DATE DEFAULT CURRENT_DATE
);
```

<hr>

### `TIME`

We use the `TIME` data type to store time data (without date) in tables. A time column can store a time value from 00:00:00 to 24:00:00. PostgreSQL uses 8-byte to store a time value. PostgreSQL allows you to store time with fractional seconds precision, up to 6 digits. To use a time value with fractional seconds precision, you use the following format: HH:MM:SS.pppppp. PostgreSQL accepts various time formats, giving you flexibility. However, it is recommended to use ISO 8601, which is HH:MM:SS for time input.

Here is the syntax:

```sql
CREATE TABLE table_name (
    column_name TIME(precision)
);
```

Here is an example of creating a table with the `TIME` data type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_date DATE,
  signup_time TIME(3)
);
```

If you want to set the current time as the default value, you can use the `CURRENT_TIME` function as follows:

```sql
CREATE TABLE table_name(
    column_name TIME DEFAULT CURRENT_TIME,
);
```

To remove the fractional second precision, you pass the precision as zero to the `current_time` function: `SELECT current_time(0);`.

To get the current local time, you use the `localtime` function: `SELECT localtime;`. And without fractional seconds: `SELECT localtime(0);`.

<hr>

### `TIMESTAMP`

The `TIMESTAMP` data type allows you to store both date and time in the database. The `TIMESTAMP` data type does not include any time zone data. It means that when you change the time zone of your PostgreSQL server, the `TIMESTAMP` values stored in the database won't automatically change. PostgreSQL uses 8 bytes to store a `TIMESTAMP` value. The valid range of the `TIMESTAMP` is from 4713 BC to 294276 AD.

Here is an example of creating a table with the `TIMESTAMP` data type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3)
);
```

If you want to set a default value for a `TIMESTAMP` column, you can apply a `DEFAULT` constraint with the default value returned by the `LOCALTIMESTAMP` or `CURRENT_TIMESTAMP` function:

```sql
CREATE TABLE table_name(
  column_name TIMESTAMP DEFAULT LOCALTIMESTAMP
);
```

Note that the `LOCALTIMESTAMP` returns the local date and time based on the local time of the PostgreSQL server. PostgreSQL uses the ISO 8601 standard for both input and output timestamps: yyyy-mm-dd hh:mm:ss

> In practice, you should use the `TIMESTAMP` data type to store timestamps only when you save and retrieve them from the database and you’re not doing any calculations. Otherwise, you should use the `TIMESTAMPTZ` instead.

<hr>

### `TIMESTAMP WITH TIME ZONE`

We can use the `TIMESTAMP WITH TIME ZONE` data type to store time zone-aware timestamp values. `TIMESTAMPTZ` is the shorthand of the `TIMESTAMP WITH TIME ZONE`, so we can use it to save some typing:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3),
  last_login_at TIMESTAMPTZ(3)
);
```

When you insert a timestamp into a `TIMESTAMPTZ` column, PostgreSQL converts it to UTC for storage. This conversion ensures the stored timestamp is consistent and not affected by time zone differences. The `TIMESTAMPTZ` can automatically handle daylight saving time changes and other time zone-related adjustments.

When you retrieve a timestamp from a `TIMESTAMPTZ` column, PostgreSQL converts the stored UTC timestamp back to the time zone of your session. It's important to note that PostgreSQL does not store time zones in the `TIMESTAMPTZ` column but does the time zone conversion when stored and retrieved.

You can set the time zone of your database session using the `SET TIME ZONE` statement. For example:

```sql
SET TIME ZONE 'America/Vancouver';
```

To see the time zone in the database server, we can use this command:

```sql
SHOW TIME ZONE;
```

To get a list of supported time zone names, you use the following statement:

```sql
SELECT * FROM pg_timezone_names;
```

The `CURRENT_TIMESTAMP` function returns the current time with a time zone.

```sql
SELECT CURRENT_TIMESTAMP;
```

<hr>

### `INTERVAL`

Intervals are time durations such as 2 days, 3 hours, 1 year 6 months. We use the `INTERVAL` data type to store intervals. The interval type can store intervals in years, months, hours, minutes, seconds, and milliseconds.

The following statement shows how to create an interval of 2 days: `SELECT INTERVAL '2 days';`.

The following statement shows how to combine multiple units in a single interval: `SELECT INTERVAL '2 days 5 hours 30 minutes';`.

If you have a valid interval string, you explicitly cast it into an `INTERVAL` using the cast operator (`::`): `SELECT '1 day 10 hours'::INTERVAL;`.

Here is an example of creating a table with the `INTERVAL` data type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3),
  last_login_at TIMESTAMPTZ(3),
  membership_duration INTERVAL
);
```

PostgreSQL allows you to specify precision specifications for fractional seconds explicitly: `INTERVAL second(p)`. In this syntax, p is the number of fractional digits you want to retain in the interval.

PostgreSQL provides three functions for adjusting intervals:

- `JUSTIFY_HOURS`: adjust excess hours into days.
- `JUSTIFY_DAYS`: adjust excess days into months while handling leap year accurately.
- `JUSTIFY_INTERVAL`: adjusts months to years and days to months.

For example, the following statements adjust an interval:

```sql
SELECT JUSTIFY_HOURS(INTERVAL '26 hours');
SELECT JUSTIFY_DAYS(INTERVAL '75 days');
SELECT JUSTIFY_INTERVAL(INTERVAL '13 months 30 days');
```

<hr>

### `UUID`

UUID stands for universal unique identifier and is 128 bits long. It guarantees uniqueness across systems and time. PostgreSQL uses the `UUID` type for storing `UUID` values.

Here is an example of creating a table with `UUID`:

```sql
CREATE TABLE users (
  user_id INT,
  user_uuid UUID,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3),
  last_login_at TIMESTAMPTZ(3),
  membership_duration INTERVAL
);
```

Typically, we use the `UUID` as the type of a primary key column of the table:

```sql
CREATE TABLE table_name (
  column_name UUID PRIMARY KEY,
);
```

PostgreSQL provides the `gen_random_uuid()` that allows you to generate a `UUID` value. For example, the following statement generates a `UUID` value: `SELECT gen_random_uuid();`.

You can use the `gen_random_uuid()` function to generate default values for the `UUID` primary key column:

```sql
CREATE TABLE table_name(
   user_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
);
```

<hr>

## Constraints

### `NOT NULL`

NULL represents the absence of a value, indicating that the data is unknown or missing.

If you compare NULL with any value, the comparison returns NULL. Even NULL is not equal to NULL; comparing NULL with NULL also results in NULL.

When you define a column for a table, that column is nullable. It means that you can insert NULL into the column. If we want a column to not have a null value (not be empty), we can use the `NOT NULL` constraint:

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

<hr>

### `DEFAULT`

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

<hr>

### `CHECK`

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

<hr>

### `UNIQUE`

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

<hr>

### Primary and Foreign Keys

#### Primary Key

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

#### Foreign Key

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

<hr>
<hr>

## Inserting data into tables

To insert data into a table, we use the `INSERT INTO table_name` command, specify the columns into which we want to insert data in parentheses, and using the `VALUES()` command, we insert the actual data.

Let's insert data into these tables:

```sql
-- users table
CREATE TABLE users (
  user_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  username VARCHAR(50) NOT NULL UNIQUE,
  email CHAR(50) NOT NULL,
  country VARCHAR(50),
  is_active BOOLEAN DEFAULT true,
  signup_date DATE DEFAULT CURRENT_DATE,
  bio TEXT,
  account_balance DECIMAL(10, 2) CHECK (account_balance >= 0)
);

-- user_activity table
CREATE TABLE user_activity (
  activity_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  user_id INT NOT NULL,
  last_login TIMESTAMPTZ(3),
  total_time_logged INTERVAL,
  CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES users(user_id)
);

-- transactions table
CREATE TABLE transactions (
  transaction_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id INT NOT NULL,
  amount DECIMAL(8, 2) NOT NULL CHECK (amount >= 0),
  description TEXT,
  created_at TIMESTAMP(3) DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_user_tx FOREIGN KEY (user_id) REFERENCES users(user_id)
);
```

Here is an example of inserting data:

```sql
INSERT INTO users (
  username, email, country, is_active, signup_date, bio, account_balance
) VALUES (
  'ziya',
  'ziya@example.com',
  'Azerbaijan',
  true,
  '2025-02-15',
  NULL,
  750.25
);
```

Note that the order of columns listed after the table name does not matter. You can change the column order as you like. But you also need to change the order of values so that they match the columns.

PostgreSQL allows you to insert multiple rows into a table at once. We just need to have more `VALUES()` commands.

To return the inserted row, you add the `RETURNING` clause to the insert statement:

```sql
INSERT INTO user_activity (
  user_id, last_login, total_time_logged
) VALUES (1,  '2025-07-16 10:00:00+03', '5 hours 20 minutes')
RETURNING *;
```

The asterisk (\*) means returning all columns of the inserted row. To select columns to return, you can specify the column names in the `RETURNING` clause:

```sql
INSERT INTO transactions (
  user_id, amount, description
) VALUES (1, 100.00, 'Cloud service subscription')
RETURNING transaction_id, amount, created_at;
```

The `ON CONFLICT` keyword is used to handle unique constraint violations during insert operations. It allows you to specify what action to take when a conflict occurs, such as updating the existing record or doing nothing.

```sql
INSERT INTO users (username, email, country)
VALUES ('kerem', 'kerem@example.com', 'Turkiye')
ON CONFLICT (username)
DO NOTHING;
```

To update the existing record with new values when there is a conflict, we can use the following syntax:

```sql
INSERT INTO users (username, email, country, account_balance)
VALUES ('ziya', 'ziya@example.com', 'Azerbaijan', 900.00)
ON CONFLICT (username)
DO UPDATE SET account_balance = EXCLUDED.account_balance;
```

The `SET` and `WHERE` clauses in `ON CONFLICT DO UPDATE` have access to the existing row using the table's name (or an alias), and to the row proposed for insertion using the special `excluded` table.

<hr>
<hr>

## Import and Export a CSV File

### Import a CSV File

There are various ways to import a CSV file into a PostgreSQL table. One way is to

- Create a new table,
- Then, to import a CSV file into the newly created table, we use `COPY` statement as follows

```sql
COPY table_name(column_name)
FROM 'pathToFile.csv'
DELIMITER ','
CSV HEADER;
```

In case the CSV file contains all columns of the table, we don’t need to specify them explicitly, for example:

```sql
COPY table_name
FROM 'pathToFile.csv'
DELIMITER ','
CSV HEADER;
```

### Export to a CSV File

The `COPY` statement allows to export data from a table to a CSV file.

```sql
COPY table_name
TO 'pathToFile.csv'
DELIMITER ','
CSV HEADER;
```

Sometimes, we may want to export data from some columns of a table to a CSV file. To achieve this, we can specify the column names together with the table name after `COPY` keyword.

```sql
COPY table_name(column_name)
TO 'pathToFile.csv'
DELIMITER ','
CSV HEADER;
```

If we don't want to export the header, which contains the column names of the table, we can remove the `HEADER` flag in the `COPY` statement.

<hr>
<hr>

## Updating data

To update data in PostgreSQL, we use the `UPDATE` and `SET` statements, which allow us to modify existing records in a table.

```sql
UPDATE users
SET account_balance = account_balance + 100
WHERE username = 'hasan';
```

The `UPDATE` statement offers the `RETURNING` clause that returns the updated rows.

```sql
UPDATE users
SET account_balance = account_balance - 100
WHERE username = 'hasan'
RETURNING *;
```

<hr>
<hr>

## Deleting data from tables

The `DELETE` statement permanently removes one or more rows from a table.

```sql
DELETE FROM products
WHERE name = 'test product';
```

The `DELETE` statement has an optional `RETURNING` clause that returns the deleted rows.

```sql
DELETE FROM products
WHERE name = 'test product';
RETURNING *;
```

Here is how to delete all rows from a table:

```sql
DELETE FROM person;
```

<hr>
<hr>

## Querying a database

### Data for queries

These are our tables and data to query:

```sql
-- users table
CREATE TABLE users (
  user_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  username VARCHAR(50) NOT NULL UNIQUE,
  email CHAR(50) NOT NULL,
  country VARCHAR(50),
  is_active BOOLEAN DEFAULT true,
  signup_date DATE DEFAULT CURRENT_DATE,
  bio TEXT,
  account_balance DECIMAL(10, 2) CHECK (account_balance >= 0)
);

-- products table
CREATE TABLE products (
  product_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  name VARCHAR(100) NOT NULL UNIQUE,
  bought_at TIMESTAMPTZ(3)
);

-- transactions table
CREATE TABLE transactions (
  transaction_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id INT NOT NULL,
  product_id INT NOT NULL,
  quantity INT NOT NULL CHECK (quantity > 0),
  price DECIMAL(8, 2) NOT NULL CHECK (price >= 0),
  amount DECIMAL(10, 2) GENERATED ALWAYS AS (quantity * price) STORED,
  created_at TIMESTAMP(3) DEFAULT CURRENT_TIMESTAMP,

  CONSTRAINT fk_user_tx     FOREIGN KEY (user_id)    REFERENCES users(user_id),
  CONSTRAINT fk_product_tx  FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

```sql
INSERT INTO users (username, email, country, is_active, signup_date, bio, account_balance)
VALUES
  ('ziya',    'ziya@example.com',    'Azerbaijan',   true,  '2025-02-15', NULL,                    750.25),
  ('kerem',   'kerem@example.com',   'Turkiye',      true,  '2025-01-10', 'Enjoys coding.',       500.00),
  ('murat',   'murat@example.com',   'Turkiye',      false, '2024-12-20', 'Database admin.',      120.00),
  ('fatima',  'fatima@example.com',  'Kazakhstan',   true,  '2025-03-05', 'Data analyst.',        350.75),
  ('hasan',   'hasan@example.com',   'Uzbekistan',   true,  '2025-06-01', NULL,                    0.00),
  ('aydin',   'aydin@example.com',   'Turkiye',      true,  '2025-04-12', 'Security researcher.',1500.50),
  ('nigar',   'nigar@example.com',   'Turkmenistan', true,  '2025-05-20', NULL,                    275.00),
  ('sara',    'sara@example.com',    NULL,           false, '2025-06-15', 'Intern.',              10.00),
  ('memmed',  'memmed@example.com',  'Azerbaijan',   true,  '2025-01-30', NULL,                    600.00),
  ('emine',   'emine@example.com',   'Turkiye',      true,  '2025-03-22', 'Project manager.',     800.00);

INSERT INTO products (name, bought_at)
VALUES
  ('Mechanical Keyboard', '2025-06-01 14:00:00+00'),
  ('Gaming Mouse',        '2025-06-03 10:30:00+00'),
  ('Monitor 27-inch',     '2025-06-05 09:45:00+00'),
  ('USB-C Hub',           '2025-06-07 11:15:00+00'),
  ('Noise Cancelling Headphones', '2025-06-09 16:20:00+00');

INSERT INTO transactions (user_id, product_id, quantity, price)
VALUES
  (1, 1, 1, 120.00),  -- ziya
  (1, 2, 2, 45.00),   -- ziya

  (2, 3, 1, 250.00),  -- kerem
  (2, 4, 3, 35.00),   -- kerem
  (2, 5, 1, 200.00),  -- kerem

  (4, 1, 1, 120.00),  -- fatima
  (4, 2, 1, 45.00),   -- fatima

  (5, 3, 1, 250.00),  -- hasan

  (6, 5, 1, 200.00),  -- aydin
  (6, 4, 2, 35.00),   -- aydin

  (10, 2, 1, 45.00),  -- emine
  (10, 1, 1, 120.00); -- emine
```

<hr>

### Basic queries

To query a database we use the the `SELECT` and `FROM` keywords specifying columns and the table to take the data from.

```sql
SELECT username, country FROM users
```

To sort the data, we use the `ORDER BY` keyword:

```sql
SELECT username, country FROM users ORDER BY country
```

Use `ASC` to sort rows in ascending order and `DESC` to sort rows in descending order. The `ORDER BY` clause uses the `ASC` by default if you don’t explicitly specify it.

```sql
SELECT username, country FROM users ORDER BY country DESC
```

When it comes to NULL, PostgreSQL provides two options in the `ORDER BY` clause:

```sql
SELECT username, country FROM users ORDER BY country NULLS FIRST;
SELECT username, country FROM users ORDER BY country NULLS LAST;
```

If you have column aliases in the `SELECT` clause, you can use them in the `ORDER BY` clause. The reason is that PostgreSQL evaluates the `SELECT` clause before the `ORDER BY` clause.

```sql
SELECT username, country as c FROM users ORDER BY c;
```

Instead of using the column name or an alias, we can also refer to a column by a number in `ORDER BY`. For example, in the below code, we refer to the `country` column as `2`, as its the second column in the `SELECT` statement:

```sql
SELECT username, country FROM users ORDER BY 2;
```

The `SELECT` statement can also retrieve and transform the data from a table. For example, we can multiply 2 columns:

```sql
SELECT product_id, (quantity * price) FROM transactions;
```

Besides the multiplication operator (\*) you can use other mathematical operators such as addition (+), subtraction (-), and division (/).

If you perform a calculation on columns in the `SELECT` statement, the column is often referred to as a _calculated column_.

<hr>

### `DISTINCT` clause

The `SELECT DISTINCT` clause retrieves unique values from a table:

```sql
SELECT DISTINCT country FROM users;
```

The `SELECT DISTINCT` clause can accept multiple columns. In this case, the `SELECT DISTINCT` clause uses the combination of values in these columns to evaluate the duplicates.

The `GROUP BY` clause groups rows based on the values of one or more columns into groups and applies an aggregate function to each group. The `GROUP BY` clause without an aggregate function has the same effect as the `SELECT DISTINCT` clause.

#### `DISTINCT ON`

A `SELECT DISTINCT ON` clause allows you to select a row for each group defined by the `ON` clause.

```sql
SELECT DISTINCT ON (column1), column2, column3
FROM table_name
ORDER BY column1, column2, column3;
```

This is how it works: We specify a column (column1) inside the parentheses of the `ON` keyword. The column1 will be used to apply the `DISTINCT` clause on. The `SELECT` clause may include other columns (column2, column3) or expressions. The `DISTINCT` clause won't be applied on them. The `ORDER BY` clause sorts rows in each distinct group by column1 and keeps the first row only (only the first row from the other columns get retrieved).

```sql
SELECT DISTINCT ON (country) country, is_active FROM users ORDER BY country;
-- compare it to
SELECT DISTINCT country, is_active FROM users ORDER BY country;
```

> Note that `SELECT DISTINCT ON` is PostgreSQL’s extension to SQL standard. So it may not be available in other database systems.

<hr>

### Column aliases

To assign a meaningful column name to a calculated column (or a regular column), you can use a column alias. A column alias is a temporary column name that you assign to the column in the `SELECT` statement. We can set an alias for a column name using the `AS` keyword:

```sql
SELECT product_id, quantity, price, (quantity * price) AS transaction_amount FROM transactions;
```

Since the `AS` keyword is optional, we can omit it:

```sql
SELECT product_id, quantity, price, (quantity * price) transaction_amount FROM transactions;
```

<hr>

### Querying with `WHERE`

To filter rows from a table based on a condition, you use the `WHERE` clause in the `SELECT` statement:

```sql
SELECT * FROM users
WHERE country = 'Azerbaijan';
```

We can use various operators with the `WHERE` clause:

- `=` - Equal to
- `!=`, `<>` - Not Equal To
- `>` - Greater than
- `>=` - Greater than or equal to
- `<` - Less than
- `<=` - Less than or equal to

We can add more conditions using the `AND` and `OR`:

```sql
SELECT * FROM users
WHERE (country = 'Azerbaijan' OR country = 'Turkiye') AND is_active = 't';
```

Instead of having lots of `OR` keywords in a query, we can use the `IN` keyword. The `IN` operator returns true if a value is in a list of values:

```sql
SELECT * FROM users
WHERE country IN ('Azerbaijan', 'Turkiye', 'Kazakhstan');
```

The `NOT` operator negates the `IN` operator:

```sql
SELECT * FROM users
WHERE country NOT IN ('Azerbaijan', 'Turkiye', 'Kazakhstan');
```

<hr>

### Limiting and offsetting during the query

We can indicate to return no more than specified number of rows using the `LIMIT` keyword:

```sql
SELECT * FROM transactions LIMIT 5;
```

Although the `LIMIT` keyword could be used, the official way of limiting the number of queried rows is this syntex:

```sql
FETCH { FIRST | NEXT } [row_count] {ROW | ROWS } ONLY
```

You can use `FIRST` and `NEXT`, `ROW`, and `ROWS` interchangeably because they are synonyms:

```sql
-- these give the same result
SELECT * FROM transactions FETCH FIRST 5 ROW ONLY;
SELECT * FROM transactions FETCH NEXT 5 ROW ONLY;

SELECT * FROM transactions FETCH FIRST 5 ROWS ONLY;
SELECT * FROM transactions FETCH NEXT 5 ROWS ONLY;
```

To skip some rows before returning a subset of rows, you can use the `OFFSET` clause:

```sql
SELECT * FROM transactions OFFSET 5;
```

<hr>

### Querying with `BETWEEN`

The `BETWEEN` operator is a comparison operator that returns true if a value is between two values:

```sql
SELECT * FROM users
WHERE signup_date BETWEEN DATE '2024-01-01' AND '2025-03-01';
```

The `NOT` operator negates the `BETWEEN` operator:

```sql
SELECT * FROM users
WHERE signup_date NOT BETWEEN DATE '2024-01-01' AND '2025-03-01';
```

<hr>

### Advanced Text Search

#### Pattern matching with `LIKE` and `ILIKE`

`LIKE` operator is used for pattern matching in SQL queries, allowing you to filter records based on whether the value in a column matches a given pattern. It uses two wildcards:

- the percent sign (`%`) which represents zero, or more characters, and
- the underscore (`_`) which represents a single character.

```sql
SELECT * FROM users
WHERE email LIKE '%.com%';
```

The following `SELECT` statement uses the `LIKE` operator to find the products with the name containing exactly 5 characters:

```sql
SELECT * FROM users
WHERE username LIKE '_____';
```

If we want to have a case-insensitive query, we can use the `ILIKE` operator:

```sql
SELECT DISTINCT country FROM users
WHERE country ILIKE '%u%';
```

The `NOT` operator negates the result of the `LIKE` and `ILIKE` operators:

```sql
SELECT DISTINCT country FROM users
WHERE country NOT ILIKE '%u%';;
```

PostgreSQL provides some operators that replicate the functionality of `LIKE`, `NOT LIKE`, `ILIKE`, and `NOT ILIKE` operators.

| Operator | Meaning     |
| -------- | ----------- |
| `~~`     | `LIKE`      |
| `~~*`    | `ILIKE`     |
| `!~~`    | `NOT LIKE`  |
| `!~~*`   | `NOT ILIKE` |

For example:

```sql
SELECT * FROM users
WHERE email ~~ '%.com%';
```

The string you want to find may contain the wildcard characters `%` and `_` such as 100% . To treat the wildcard characters as regular characters, you can use the `ESCAPE` option in the `LIKE` and `ILIKE` operators:

```sql
SELECT price FROM transactions
WHERE price::TEXT LIKE '%120$%%' ESCAPE '$';
```

In this example, we use the `$` character as an escape character. We specify the escape character `$` before `%` so the `LIKE` operator treats the character `%` that immediately follows 120 as a regular character. We also cast the `price` column to the `TEXT` data type to be able to use the `LIKE` operator on it.

#### Regular Expressions

PostgreSQL supports POSIX regular expressions, a standardized set of regular expressions defined by POSIX (Portable Operating System Interface).

_Character Classes:_

- `\d` matches any digit. It is equivalent to `[0-9]`
- `\s` matches any whitespace character.
- `\w` matches any word character, including letters, digits, and underscores. It is equivalent to `[a-zA-Z0-9_]`.

The uppercase letter negates the meaning of the character classes:

- `\D` matches any non-digit character, equivalent to `[^0-9]`.
- `\S` matches any non-whitespace character.
- `\W` matches any non-word character.

_Anchors:_

Anchors match a position instead of characters:

- `^` matches the beginning of a string.
- `$` matches the end of a string.

_Quantifiers:_

Quantifiers match the number of instances of a character set:

- `*` matches zero or more.
- `+` matches one or more.
- `?` matches zero or one.
- `{n}` matches exactly n times.
- `{n,}` matches at least n times.
- `{n,m}` matches a range from n to m times, where n < m.

_Sets & Ranges:_

- Use `[]` to create a set that matches any character in the set. For example, `[abc]` matches a, b, or c.
- Use a hyphen `-` within the square brackets `[]` to create a range. For example, `[a-z]` is a range of characters from a to z. `[0-9]` is a range of digits from 0 to 9.
- Use `^` inside `[]` to exclude a set or range. For example, the set `[^0-9]` matches any character except a digit.

_Alternation:_

- Use `|` to represent alternation, which is like the `OR` operator. For example, the regular expression `a|b` matches a or b.

PostgreSQL allows you to use POSIX regular expressions with the following operators:

- `~` matches a pattern.
- `~*` case-insensitively matches a pattern.
- `!~` does not match a pattern.
- `!~*` case-insensitively does not match a pattern.

For example, the following query uses the match operator (`~`) to find products whose names contain three digits:

```sql
SELECT * FROM products
WHERE name ~ '\d+';
```

The following query uses the case-insensitive match operator (`~*`) to find products with names that contain “mouse” or “keyboard”:

```sql
SELECT * FROM products
WHERE name ~* 'mouse|keyboard';
```

#### `SIMILAR TO` Operator

The `SIMILAR TO` operator returns true if the regular expression matches the whole string. It differs from the expected behavior of matching a string with a regular expression, which can match any part of a string.

```sql
SELECT * FROM products
WHERE name SIMILAR TO '%\d+%';
```

To negate the `SIMILAR TO` operator, you use the `NOT` operator:

```sql
SELECT * FROM products
WHERE name NOT SIMILAR TO '%\d+%';
```

Like the `LIKE` operator, you can use the `ESCAPE` option to define an escape character in the pattern when using the `SIMILAR TO` operator:

```sql
SELECT
  column1,
  column2
FROM
  table_name
WHERE
  column1 SIMILAR TO pattern ESCAPE escape_character;
```

<hr>

### Full-text Search

In PostgreSQL, full-text search is a powerful feature that allows you to carry complex searches on text. For example, if you find documents that contain the word “advance,” the full-text search will return the documents with the words "advance" , "advancing" , and "advanced".

A _document_ is the basic unit of text you want to search through in a full-text search. It can be a column of a table or a combination of columns from multiple tables.

PostgreSQL provides two specific data types to support full-text searches: `tsvector` and `tsquery`.

`tsvector` represents a document optimized for text search by storing a sorted list of distinct normalized words. The technical term of the normalized words are **lexemes**. Lexemes are words without variations, such as "teaches" and "teaching" words have the lexeme "teach".

To convert a regular string to a `tsvector`, you use the `to_tsvector` function. For example:

```sql
SELECT
  to_tsvector('teaches'),
  to_tsvector('teaching');
```

PostgreSQL uses the `tsquery` data type to represent full-text search queries.

To convert a string to a `tsquery` value, you use the `to_tsquery` function. For example:

```sql
SELECT to_tsquery('"blue" & "elephant" |"dolphin"');
```

PostgreSQL uses the match operator (`@@`) to match a `tsvector` against a `tsquery` to determine if the text the `tsvector` represents contains the terms specified in the `tsquery`:

For example:

```sql
SELECT
  to_tsvector('The big blue elephant jumps over the lazy dog.') @@ to_tsquery('elephant') result;
-- result is true
```

It’s possible to use a value of `CHAR`, `VARCHAR`, and `TEXT` with the match operator. In this case, PostgreSQL will implicitly convert the text to the `tsvector` before matching with the `tsquery`.

<hr>

### Grouping and aggregations

#### Grouping

The `GROUP BY` clause allows you to group rows into groups based on values of one or more columns.

```sql
SELECT country FROM users GROUP BY country;
```

It’s crucial to note that the columns in the `SELECT` clause must appear in the `GROUP BY` clause. You’ll encounter an error if you specify a column in the `SELECT` clause that does not appear in the `GROUP BY` clause.

#### Aggregation functions

The `GROUP BY` clause is more useful when used with aggregate functions. PostgreSQL provides several aggregate functions that compute a single result from multiple input rows. These functions include `COUNT`, `SUM`, `MAX`, `MIN`, and `AVG` which respectively return the number of rows, the sum of a selected column, the largest value, the smallest value, and the average value for a specific column.

```sql
SELECT country, COUNT(*) FROM users GROUP BY country;

SELECT MAX(amount) FROM transactions;
```

#### `HAVING` clause

The `HAVING` clause is used to filter the results of a `GROUP BY` operation. It works similarly to the `WHERE` clause but is applied after the grouping and aggregation functions like `SUM()`, `COUNT()`, `AVG()`, etc., have been evaluated.

```sql
SELECT country, COUNT(*) FROM users
GROUP BY country
HAVING COUNT(*) > 1
ORDER BY 2 DESC;
```

#### Grouping sets

The `GROUPING SETS` is an advanced feature of the `GROUP BY` clause. The `GROUPING SETS` enables multiple groupings within the same query without using multiple queries or the `UNION` operator. Here’s the general syntax:

```sql
SELECT country, is_active, COUNT(account_balance) FROM users
GROUP BY
  GROUPING SETS (
    (country, is_active),
    (country),
    (is_active),
    ()
  )
ORDER BY
  country NULLS LAST,
  is_active NULLS LAST;
```

The query creates four grouping sets:

- The (`country`, `is_active`) defines a grouping that groups rows by `country` and `is_active`.
- The (`country`) defines a grouping that groups rows by `country`.
- The (`is_active`) defines a grouping that groups rows by `is_active`.
- The `()` defines a grouping that represents the aggregation of overall rows.

#### `GROUPING` function

We might be confused with the result of `GROUPING SETs`. To alleviate the situation and understand which row is the result of which grouping, we can use the `GROUPING` function. It takes a column and returns 0 if the column is part of the current grouping set.

```sql
SELECT
  country,
  is_active,
  GROUPING(country) country_groupping,
  GROUPING(is_active) is_active_groupping,
  COUNT(account_balance)
FROM users
GROUP BY
  GROUPING SETS (
    (country, is_active),
    (country),
    (is_active),
    ()
  )
ORDER BY
  country NULLS LAST,
  is_active NULLS LAST;
```

#### `ROLLUP`

The `GROUP BY` clause can only generate a single level of aggregation. To generate multiple levels of aggregation, you use the `ROLLUP` option of the `GROUP BY` clause.

```sql
SELECT
	country,
	is_active,
	COUNT(*),
	GROUPING (country) c_group,
	GROUPING (is_active) act_group
FROM users
GROUP BY
	ROLLUP (country, is_active)
ORDER BY
	c_group, act_group;
```

In this syntax, the `ROLLUP(country, is_active)` generates the three groupings:

- `(country, is_active)`: Regular groupings that include aggregate data by values of both `country` and `is_active`.
- `(country, NULL)`: Subtotal per country.
- `(NULL, NULL)`: Grand total.

The `ROLLUP` assumes a hierarchical relationship between `country` and `is_active`.

#### `CUBE`

The `GROUP BY` clause allows you to group rows and calculate an aggregation of a single grouping set.

To calculate aggregations of all possible combinations of a set of columns, you can use the `GROUP BY` clause with the `CUBE` option.

```sql
SELECT
	country,
	is_active,
	COUNT(*),
	GROUPING(country) c_group,
	GROUPING(is_active) act_group
FROM users
GROUP BY
	CUBE (country, is_active)
ORDER BY c_group, act_group;
```

The following table explains the differences between `GROUPING SETS`, `ROLLUP`, and `CUBE`:

| Option          | Description                                                                |
| --------------- | -------------------------------------------------------------------------- |
| `CUBE`          | Generates all possible combinations of specified columns.                  |
| `ROLLUP`        | Generates hierarchical summaries.                                          |
| `GROUPING SETS` | Generates specified grouping sets instead of generating all possibilities. |

<hr>

### Set Operations

#### `UNION` and `UNION ALL`

You can use the `UNION` operator to append the result set of the second query to the result set of the first query.

To sort the result set returned by the `UNION` operator, you can use an `ORDER BY` clause. However, you need to place the `ORDER BY` clause at the end of the second query:

```sql
SELECT username AS name
FROM users

UNION

SELECT name
FROM products;
```

We may want an additional column to label which dataset a row comes from. To do that, we specify the fixed value and a column alias as follows:

```sql
SELECT username AS name, 'users table' AS source FROM users
UNION
SELECT name, 'products table' AS source FROM products;
```

The `UNION` operator removes duplicate rows. The `UNION ALL` operator appends the second query’s result set to the first query’s result set and keeps the duplicate row in the final result set:

```sql
-- compare this
SELECT user_id FROM users
UNION ALL
SELECT user_id FROM transactions
ORDER BY 1;

-- to this
SELECT user_id FROM users
UNION
SELECT user_id FROM transactions
ORDER BY 1;
```

Both `SELECT` statements need to adhere to the following rules:

- Having the same number of columns in the result sets.
- The corresponding columns have compatible data types.

#### `INTERSECT`

The `INTERSECT` operator returns the common records of result sets of two queries. In other words, it returns the intersection of two result sets.

```sql
SELECT user_id FROM users
INTERSECT
SELECT user_id FROM transactions
ORDER BY user_id;
```

Both `SELECT` statements need to adhere to the following rules:

- Having the same number of columns in the result sets.
- The corresponding columns have compatible data types.

To sort the result set of a query that involves the `INTERSECT` operator, you place the `ORDER BY` clause in the last query.

To include duplicate rows in the result, you can use the `INTERSECT ALL` operator:

```sql
SELECT user_id FROM users
INTERSECT ALL
SELECT user_id FROM transactions
ORDER BY user_id;
```

#### `EXCEPT`

The `EXCEPT` operator returns the rows from the first result set that are not present in the second. Unlike the `UNION` and `INTERSECT` operators, the order of the `SELECT` statements is important when using the `EXCEPT` operator because it will directly impact the query result.

```sql
SELECT user_id FROM users
EXCEPT
SELECT user_id FROM transactions;
```

Both `SELECT` statements need to adhere to the following rules:

- Having the same number of columns in the result sets.
- The corresponding columns have compatible data types.

If you want to sort the result set returned by the `EXCEPT` operator, you can place the `ORDER BY` clause in the second `SELECT` statement.

To retain the duplicate rows in the final result set, you use the `EXCEPT ALL` operator.

<hr>
<hr>

## Some useful functions and operators

### `IS NULL` Operator

To check if a value is NULL, we cannot compare it with NULL using the equal to operator. To compare a value with NULL, we use the `IS NULL` operator.

```sql
SELECT bio, bio IS NULL FROM users;

SELECT username FROM users
WHERE bio IS NULL;
```

To negate the result of the `IS NULL` operator, we use the `IS NOT NULL` operator.

```sql
SELECT bio, bio IS NOT NULL FROM users;

SELECT username FROM users
WHERE bio IS NOT NULL;
```

If we want to handle NULL using functions instead of the `IS NULL` operator, we can use the `NULLIF`, `ISNULL`, and `COALESCE` functions.

<hr>

### `COALESCE`

`COALESCE` function returns the first non-null value among its arguments. If all arguments are NULL, it returns NULL. This function is particularly useful for replacing NULL values with alternative values for display purposes without updating the actual data.

```sql
SELECT email, COALESCE(bio, 'N/A') FROM users;
```

<hr>

### `NULLIF`

The PostgreSQL `NULLIF` function returns NULL if two arguments are equal; otherwise, it returns the first argument.

```sql
SELECT NULLIF(2, 9);
SELECT NULLIF(2, 2);
```

Note that the `NULLIF` function compares the results of two expressions using the equal operator (=). This means that the results of both expressions must be comparable. In other words, they must have a compatible data type for comparison.

> The psql program displays blank for NULL by default. To use the NULL literal string to represent NULL, you can use the following command: `\pset null NULL`.

<hr>

### `GREATEST`

The `GREATEST` function accepts a list of values and returns the largest value. The `GREATEST` function ignores NULL. It’ll return NULL if all expressions evaluate to NULL.

> In SQL standard, the `GREATEST` function returns NULL if any expression evaluates to NULL. Some databases behave this way like MySQL.

The following example uses the `GREATEST` function to find the latest date in a list of date literals:

```sql
SELECT GREATEST ('2025-01-01', '2025-02-01', '2025-03-01', NULL) latest;
```

<hr>

### `LEAST`

The `LEAST` function accepts a list of values and returns the smallest value. The `LEAST` function ignores NULL. It’ll return NULL if all expressions evaluate to NULL.

> In SQL standard, the `LEAST` function returns NULL if any expression evaluates to NULL. Some database systems behave this way such as MySQL.

```sql
SELECT LEAST (1, 2, 3, 4, NULL) smallest;
```

<hr>

### `NOW`

The `NOW()` function returns the current date and time with timezone, which is an alias for the `current_timestamp` function.

```sql
SELECT NOW();
```

We can also use the `NOW()` function to return either the date or the time:

```sql
SELECT NOW()::DATE;
SELECT NOW()::TIME;
```

<hr>

### `EXTRACT`

The `EXTRACT()` function is used to retrieve specific components such as year, month, or day from date/time values.

```sql
SELECT EXTRACT(YEAR FROM NOW()) ;
SELECT EXTRACT(MONTH FROM NOW()) ;
SELECT EXTRACT(WEEK FROM NOW()) ;
SELECT EXTRACT(DAY FROM NOW()) ;
SELECT EXTRACT(DOW FROM NOW()) ;
SELECT EXTRACT(CENTURY FROM NOW()) ;
```

The `EXTRACT()` function is also used to extract hour, minute, and second.

```sql
SELECT EXTRACT(HOUR FROM NOW());
SELECT EXTRACT(MINUTE FROM NOW());
SELECT EXTRACT(SECOND FROM NOW());
```

The second includes the fraction part. To remove it, you can cast the seconds to integers using the cast operator `::`.

```sql
SELECT EXTRACT(SECOND FROM NOW()):: INT s;
```

We can extract data from an `INTERVAL` as well:

```sql
SELECT EXTRACT(DAY FROM INTERVAL '2 days 5 hours');
```

<hr>

### `AGE`

The `AGE()` function calculates the difference between two dates, returning the result in years, months, and days.

```sql
-- bought_at - NOW()
SELECT AGE(NOW(), bought_at) in_inventory FROM products;
```

It can also be used to find the age between a specific date and the current date. If only one date is passed, it compares that date with the current date to determine the age.

<hr>

### `DATE_TRUNC`

The `DATE_TRUNC()` function truncates a `TIMESTAMP`, a `TIMESTAMP WITH TIME ZONE`, or an `INTERVAL` value to a specified precision. Here’s the basic syntax of the DATE_TRUNC function:

```sql
DATE_TRUNC(field, source [,time_zone])
```

`field` specifies the to which precision to truncate the source. Here are the valid values for the field:

- `"millennium"`
- `"century"`
- `"decade"`
- `"year"`
- `"quarter"`
- `"month"`
- `"week"`
- `"day"`
- `"hour"`
- `"minute"`
- `"second"`
- `"milliseconds"`
- `"microseconds"`

Here are some examples:

```sql
SELECT DATE_TRUNC('year', TIMESTAMP '2025-10-23 16:20:30');
SELECT DATE_TRUNC('month', TIMESTAMP '2025-10-23 16:20:30');
SELECT DATE_TRUNC('day', TIMESTAMP '2025-10-23 16:20:30');
SELECT DATE_TRUNC('hour', TIMESTAMP '2025-10-23 16:20:30');
SELECT DATE_TRUNC('minute', TIMESTAMP '2025-10-23 16:20:30');
```

<hr>

### `TO_CHAR`

We can use the `TO_CHAR()` function to convert a timestamp or a numeric value to a string. Here is an example of using `TO_CHAR` while converting the `DATE` type to a desired string format:

```sql
SELECT
  username,
  to_char (signup_date, 'Month dd, yyyy') formatted_date
FROM
  users
ORDER BY
  signup_date;
```

We can also extract the parts of the day in a desired format using the `TO_CHAR()` function.

```sql
SELECT to_char(date '2025-12-27', 'Day');
SELECT to_char(date '2025-12-27', 'DAY');
SELECT to_char(date '2025-12-27', 'day');
SELECT to_char(date '2025-12-27', 'DY');
SELECT to_char(date '2025-12-27', 'Dy');
SELECT to_char(date '2025-12-27', 'dy');
```

<hr>

### Concatenation

To concatenate two strings into a single string, we use the concatenation operator `||`:

```sql
SELECT username || ' from ' || country FROM users;
```

Besides the concatenation operator, PostgreSQL offers the `CONCAT()` function that concatenates multiple strings into a single one:

```sql
SELECT CONCAT(username, ' from ', country) FROM users;
```

To concatenate strings with a separator, we use the `CONCAT_WS()` function. The first argument to the `CONCAT_WS()` function is the separator. Note that WS stands for With Separator.

```sql
SELECT CONCAT_WS(' from ', username, country) FROM users;
```

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

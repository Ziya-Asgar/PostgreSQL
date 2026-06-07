# Some Functions and Operators

- [Some Functions and Operators](#some-functions-and-operators)
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
  - [`FORMAT` Function](#format-function)
  - [`PERFORM`](#perform)
  - [`EXECUTE`](#execute)
  - [`PREPARE`](#prepare)
  - [Concatenation](#concatenation)
  - [Cast](#cast)

---

---

## `IS NULL` Operator

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

---

---

## `COALESCE`

`COALESCE` function returns the first non-null value among its arguments. If all arguments are NULL, it returns NULL. This function is particularly useful for replacing NULL values with alternative values for display purposes without updating the actual data.

```sql
SELECT email, COALESCE(bio, 'N/A') FROM users;
```

---

---

## `NULLIF`

The PostgreSQL `NULLIF` function returns NULL if two arguments are equal; otherwise, it returns the first argument.

```sql
SELECT NULLIF(2, 9);
SELECT NULLIF(2, 2);
```

Note that the `NULLIF` function compares the results of two expressions using the equal operator (=). This means that the results of both expressions must be comparable. In other words, they must have a compatible data type for comparison.

> The psql program displays blank for NULL by default. To use the NULL literal string to represent NULL, you can use the following command: `\pset null NULL`.

---

---

## `GREATEST`

The `GREATEST` function accepts a list of values and returns the largest value. The `GREATEST` function ignores NULL. It’ll return NULL if all expressions evaluate to NULL.

> In SQL standard, the `GREATEST` function returns NULL if any expression evaluates to NULL. Some databases behave this way like MySQL.

The following example uses the `GREATEST` function to find the latest date in a list of date literals:

```sql
SELECT GREATEST ('2025-01-01', '2025-02-01', '2025-03-01', NULL) latest;
```

---

---

## `LEAST`

The `LEAST` function accepts a list of values and returns the smallest value. The `LEAST` function ignores NULL. It’ll return NULL if all expressions evaluate to NULL.

> In SQL standard, the `LEAST` function returns NULL if any expression evaluates to NULL. Some database systems behave this way such as MySQL.

```sql
SELECT LEAST (1, 2, 3, 4, NULL) smallest;
```

---

---

## `NOW`

The `NOW()` function returns the current date and time with timezone, which is an alias for the `current_timestamp` function.

```sql
SELECT NOW();
```

We can also use the `NOW()` function to return either the date or the time:

```sql
SELECT NOW()::DATE;
SELECT NOW()::TIME;
```

---

---

## `EXTRACT`

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

---

---

## `AGE`

The `AGE()` function calculates the difference between two dates, returning the result in years, months, and days.

```sql
-- bought_at - NOW()
SELECT AGE(NOW(), bought_at) in_inventory FROM products;
```

It can also be used to find the age between a specific date and the current date. If only one date is passed, it compares that date with the current date to determine the age.

---

---

## `DATE_TRUNC`

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

---

---

## `TO_CHAR`

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

---

---

## `FORMAT` Function

The `FORMAT()` function returns a formatted string based on a template. Here’s the syntax of the `FORMAT()` function:

```sql
FORMAT(format_string, format_argument1, format_argument2, ...)
```

The `format_string` may include one or more format specifiers:

- `%s` formats the argument as a string.
- `%I` formats the argument as an SQL identifier, such as a table name with proper quoting.
- `%L` formats the argument as an SQL literal.

The format specifiers `%I` and `%L` can be handy for constructing dynamic SQL statements.

Here is an example with `%s`:

```sql
SELECT
  FORMAT('Hello, %s', 'pgtutorial.com');
```

The following example uses the `FORMAT` function with the `%I` specifiers to return a dynamic SQL statement:

```sql
SELECT
  FORMAT(
    'SELECT %I, %I FROM %I',
    'product_name',
    'price',
    'products'
  ) sql_statement;
```

The following query uses the `FORMAT` function with the `%L` for formatting literals:

```sql
SELECT
  FORMAT(
    'SELECT %I, %I FROM %I WHERE %I = %L',
    'product_name',
    'price',
    'products',
    'product_name',
    'Apple iPhone 15'
  ) sql_statement;
```

---

---

## `PERFORM`

Sometimes it is useful to evaluate an expression or `SELECT` query but discard the result, for example when calling a function that has side-effects but no useful result value like calling a function that updates data, or logs an event. To do this in PL/pgSQL, we use the `PERFORM` statement:

```sql
-- First, we define a simple function that logs a message. It returns void (nothing useful to capture).
CREATE OR REPLACE FUNCTION send_notification(message TEXT)
RETURNS void
LANGUAGE plpgsql
AS $$
BEGIN
    RAISE NOTICE 'Notification sent: %', message;
END;
$$;

-- Now, we create a function that calls send_notification using PERFORM.
CREATE OR REPLACE FUNCTION process_user_registration(user_name TEXT)
RETURNS void
LANGUAGE plpgsql
AS $$
BEGIN
    -- Perform the action of sending a notification
    -- The result is discarded immediately
    PERFORM send_notification('Welcome to the system, ' || user_name || '!');

    RAISE NOTICE 'Registration process for % completed.', user_name;
END;
$$;

SELECT process_user_registration('Alice');
```

If we used just `SELECT send_notification(...)`, PostgreSQL would throw an error because PL/pgSQL requires queries that return rows to be handled with `INTO` (to store the result) or `PERFORM` (to discard it).

---

---

## `EXECUTE`

The `EXECUTE` statement in PL/pgSQL is used to run dynamic SQL commands. Unlike standard PL/pgSQL commands where the SQL text is fixed at compile time, `EXECUTE` takes a string containing the SQL command and runs it at runtime.

Because the command is built as a string, you must be careful to sanitize inputs (using functions like `quote_ident`, `quote_nullable`, or `quote_literal`) to prevent SQL injection attacks. `quote_ident`, `quote_literal`, and `quote_nullable` are helper functions in PostgreSQL designed to make Dynamic SQL safe. When you build a SQL command as a string using `EXECUTE` (e.g., `'SELECT * FROM ' || table_name`), you risk SQL Injection if the variable contains malicious text (like `users; DROP TABLE users;--`). These functions automatically escape special characters and add the necessary quotes to ensure the input is treated strictly as data or an identifier, not as executable code. Please note that using the `FORMAT` function is preferable, as it has built-in escaping using `%s`, `%I`, and `%L`.

Here is a simple function that creates a new table with a name provided by the user:

```sql
CREATE OR REPLACE FUNCTION create_dynamic_table(table_name TEXT)
RETURNS void
LANGUAGE plpgsql
AS $$
BEGIN
    -- Build the command string using quote_ident for safety
    -- This ensures the table name is properly escaped
    EXECUTE 'CREATE TABLE ' || quote_ident(table_name) || ' (id INT, data TEXT)';

    RAISE NOTICE 'Table % created successfully.', table_name;
END;
$$;

SELECT create_dynamic_table('users_data');
```

We can also use the `USING` clause in the `EXECUTE` statement to pass values (literals) to a dynamic SQL command safely. To do this, we add `$1`, `$2`, etc. to a command string and these symbols refer to values supplied in the `USING` clause. This method is often preferable to inserting data values into the command string as text:

```sql
CREATE OR REPLACE function insert_user_data(target_table text, user_name text, user_age int)
RETURNS void
LANGUAGE plpgsql
AS $$
BEGIN
    -- 1. quote_ident is used for the table name (an identifier) because it cannot be a parameter ($1).
    -- 2. $1 and $2 are placeholders for the data values (literals).
    -- 3. USING provides the actual values for $1 and $2 at runtime.
    EXECUTE format('INSERT INTO %I (name, age) VALUES ($1, $2)', target_table)
    USING user_name, user_age;

    RAISE NOTICE 'Inserted user % (age %)' into %', user_name, user_age, target_table;
END;
$$;

SELECT insert_user_data('users_data', 'Bob', 25);
```

---

---

## `PREPARE`

The `PREPARE` statement enables us to prepare a statement with a unique name and execute it repeatedly using the `EXECUTE` command.

Here is the syntax for the `PREPARE` statement:

```sql
PREPARE name [ ( data_type [, ...] ) ] AS statement
```

Here is an example:

```sql
PREPARE fooplan (int, text, bool, numeric) AS
    INSERT INTO foo VALUES($1, $2, $3, $4);
EXECUTE fooplan(1, 'Hunter Valley', 't', 200.00);
```

Prepared statements only last for the duration of the current database session. When the session ends, the prepared statement is forgotten, so it must be recreated before being used again. This also means that a single prepared statement cannot be used by multiple simultaneous database clients; however, each client can create their own prepared statement to use. Prepared statements can be manually cleaned up using the `DEALLOCATE` command.

---

---

## Concatenation

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

---

---

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

---

---

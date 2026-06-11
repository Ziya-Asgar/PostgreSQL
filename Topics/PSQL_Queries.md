# Querying a database

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

---

---

## Data for queries

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

---

---

## Basic queries

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

---

---

## `DISTINCT` clause

The `SELECT DISTINCT` clause retrieves unique values from a table:

```sql
SELECT DISTINCT country FROM users;
```

The `SELECT DISTINCT` clause can accept multiple columns. In this case, the `SELECT DISTINCT` clause uses the combination of values in these columns to evaluate the duplicates.

The `GROUP BY` clause groups rows based on the values of one or more columns into groups and applies an aggregate function to each group. The `GROUP BY` clause without an aggregate function has the same effect as the `SELECT DISTINCT` clause.

---

### `DISTINCT ON`

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

---

---

## Column aliases

To assign a meaningful column name to a calculated column (or a regular column), you can use a column alias. A column alias is a temporary column name that you assign to the column in the `SELECT` statement. We can set an alias for a column name using the `AS` keyword:

```sql
SELECT product_id, quantity, price, (quantity * price) AS transaction_amount FROM transactions;
```

Since the `AS` keyword is optional, we can omit it:

```sql
SELECT product_id, quantity, price, (quantity * price) transaction_amount FROM transactions;
```

---

---

## Querying with `WHERE`

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

---

---

## Limiting and offsetting during the query

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

---

---

## Querying with `BETWEEN`

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

---

---

## Advanced Text Search

### Pattern matching with `LIKE` and `ILIKE`

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

---

### Regular Expressions

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

### `SIMILAR TO` Operator

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

---

---

## Full-text Search

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

---

---

## Grouping and aggregations

### Grouping

The `GROUP BY` clause allows you to group rows into groups based on values of one or more columns.

```sql
SELECT country FROM users GROUP BY country;
```

It’s crucial to note that the columns in the `SELECT` clause must appear in the `GROUP BY` clause. You’ll encounter an error if you specify a column in the `SELECT` clause that does not appear in the `GROUP BY` clause.

---

### Aggregation functions

The `GROUP BY` clause is more useful when used with aggregate functions. PostgreSQL provides several aggregate functions that compute a single result from multiple input rows. These functions include `COUNT`, `SUM`, `MAX`, `MIN`, and `AVG` which respectively return the number of rows, the sum of a selected column, the largest value, the smallest value, and the average value for a specific column.

```sql
SELECT country, COUNT(*) FROM users GROUP BY country;

SELECT MAX(amount) FROM transactions;
```

One of the useful aggregation functions is `STRING_AGG()`. It concatenates a list of strings and places a separator between them. It does not add the separator at the end of the string.

The following shows the syntax of the `STRING_AGG()` function:

```sql
STRING_AGG ( expression, separator [order_by_clause] )
```

---

### `HAVING` clause

The `HAVING` clause is used to filter the results of a `GROUP BY` operation. It works similarly to the `WHERE` clause but is applied after the grouping and aggregation functions like `SUM()`, `COUNT()`, `AVG()`, etc., have been evaluated.

```sql
SELECT country, COUNT(*) FROM users
GROUP BY country
HAVING COUNT(*) > 1
ORDER BY 2 DESC;
```

---

### Grouping sets

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

---

### `GROUPING` function

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

---

### `ROLLUP`

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

---

### `CUBE`

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

---

---

## Set Operations

### `UNION` and `UNION ALL`

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

---

### `INTERSECT`

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

---

### `EXCEPT`

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

---

---

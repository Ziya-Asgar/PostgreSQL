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

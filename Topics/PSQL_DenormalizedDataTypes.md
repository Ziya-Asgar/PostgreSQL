# Denormalized Data Types

- [Denormalized Data Types](#denormalized-data-types)
  - [Composite Types](#composite-types)
  - [`ARRAY` Data Type](#array-data-type)
  - [`XML` Data Type](#xml-data-type)
  - [`ENUM`](#enum)
  - [`RECORD`](#record)
  - [`JSON`](#json)

---

---

## Composite Types

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

---

---

## `ARRAY` Data Type

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

---

---

## `XML` Data Type

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

---

---

## `ENUM`

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

---

---

## `RECORD`

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

---

---

## `JSON`

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

---

---

# User-defined Functions

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

The `returns setof` option allows us to return one or more rows with a predefined structure from a function.

```sql
Here’s the syntax for creating a function that returns a set of rows:

create or replace function function_name(parameters)
returns setof row_structure
as
$$
   -- logic
   -- ...
   -- return one or more rows
   return query select_query;
$$ language plpgsql;
```

---

---

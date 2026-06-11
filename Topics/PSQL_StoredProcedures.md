# Stored Procedures

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

---

---

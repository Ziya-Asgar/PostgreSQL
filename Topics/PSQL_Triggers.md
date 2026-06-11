# Triggers

- [Triggers](#triggers)
  - [Creating Triggers](#creating-triggers)
  - [Disabling and Enabling Triggers](#disabling-and-enabling-triggers)
  - [Dropping Triggers](#dropping-triggers)
  - [Event Triggers](#event-triggers)

---

---

## Creating Triggers

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

---

---

## Disabling and Enabling Triggers

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

---

---

## Dropping Triggers

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

---

---

## Event Triggers

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

---

---

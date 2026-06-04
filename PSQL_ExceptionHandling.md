# Exception Handling

- [Exception Handling](#exception-handling)
  - [Intro](#intro)
  - [`RAISE` Statement](#raise-statement)

---

---

## Intro

In PL/pgSQL, an exception is an unexpected condition or error during execution. Exceptions may result from issues like constraint violation, division by zero, data not found, or other situations. Here is a list of errors and error messages: [Error Codes](https://www.postgresql.org/docs/current/errcodes-appendix.html).

To handle exceptions, we use the `EXCEPTION` block within the `BEGIN` and `END` keywords of a block:

```sql
DO
$$
DECLARE
   -- declaration
BEGIN
    -- code that may cause exceptions
EXCEPTION
    WHEN exception_name THEN
        -- Handle the specific exception
        RAISE NOTICE 'An error occurred: %', SQLERRM;
    WHEN OTHERS THEN
        -- Handle all other exceptions
        RAISE NOTICE 'An unknown error occurred: %', SQLERRM;
END;
$$
LANGUAGE plpgsql;
```

The `SQLERRM` and `SQLSTATE` are error message variables:

- The `SQLERRM` variable contains the exception’s message.
- The `SQLSTATE` variable holds the error code.

Here is an example:

```sql
CREATE FUNCTION try_divide(x NUMERIC, y NUMERIC)
RETURNS NUMERIC AS
$$
BEGIN
    RETURN x / y;
EXCEPTION
    WHEN division_by_zero THEN
        RAISE NOTICE 'Cannot divide by zero, returning NULL!';
        RETURN NULL;
END;
$$
LANGUAGE plpgsql;
```

---

---

## `RAISE` Statement

In PL/pgSQL, the `RAISE` statement allows you to debug, inform, warn, and signal errors in your procedures, functions, and triggers.

Here’s the syntax of the `RAISE` statement:

```sql
RAISE [level] 'format' [expression, ...]
```

The level specifies the severity level of the message. The valid levels are as follows:

- `DEBUG`: Use to debug the code.
- `LOG`: Write messages to the PostgreSQL server’s log, but don’t send them to the client.
- `NOTICE`: Return informational messages to the client.
- `WARNING`: Warn the client without interrupting code execution.
- `EXCEPTION`: Issue an error and abort the execution of the current block.

The format is a string that may include one or more placeholders (`%`). The `RAISE` statement will substitute the placeholders with the expression. The number of placeholders and expressions must be the same, or the `RAISE` statement will issue an error.

---

---

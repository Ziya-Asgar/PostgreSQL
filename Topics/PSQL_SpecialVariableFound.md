# Special Variable `FOUND`

One way to determine the effects of a command is to check the special variable named `FOUND`, which is of type boolean. `FOUND` starts out false within each PL/pgSQL function call. It is set by each of the following types of statements:

- A `SELECT INTO` statement sets `FOUND` true if a row is assigned, false if no row is returned.

- A `PERFORM` statement sets `FOUND` true if it produces (and discards) one or more rows, false if no row is produced.

- `UPDATE`, `INSERT`, `DELETE`, and `MERGE` statements set `FOUND` true if at least one row is affected, false if no row is affected.

- A `FETCH` statement sets `FOUND` true if it returns a row, false if no row is returned.

- A `MOVE` statement sets `FOUND` true if it successfully repositions the cursor, false otherwise.

- A `FOR` or `FOREACH` statement sets `FOUND` true if it iterates one or more times, else false. `FOUND` is set this way when the loop exits; inside the execution of the loop, `FOUND` is not modified by the loop statement, although it might be changed by the execution of other statements within the loop body.

- `RETURN QUERY` and `RETURN QUERY EXECUTE` statements set `FOUND` true if the query returns at least one row, false if no row is returned.

Other PL/pgSQL statements do not change the state of `FOUND`. Note in particular that `EXECUTE` changes the output of `GET DIAGNOSTICS`, but does not change `FOUND`.

`FOUND` is a local variable within each PL/pgSQL function; any changes to it affect only the current function.

Here is a simple example:

```sql
CREATE OR REPLACE FUNCTION get_user_name(user_id INT)
RETURNS TEXT
LANGUAGE plpgsql
AS $$
DECLARE
    found_name TEXT;
BEGIN
    -- Try to select the name.
    -- If a row is found, FOUND becomes TRUE.
    -- If no row is found, FOUND becomes FALSE (and found_name becomes NULL).
    SELECT name INTO found_name
    FROM users
    WHERE id = user_id;

    -- Check if a row was actually found
    IF FOUND THEN
        RAISE NOTICE 'User found: %', found_name;
        RETURN found_name;
    ELSE
        RAISE EXCEPTION 'User with ID % not found', user_id;
    END IF;
END;
$$;
```

---

---

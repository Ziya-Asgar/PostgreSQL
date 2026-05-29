# Sequence

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

---

---

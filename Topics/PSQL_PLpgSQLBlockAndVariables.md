# PL/pgSQL Block and Variables

PL/pgSQL is a blocked structure programming language. PL/pgSQL organizes code into blocks.

Here’s the syntax of a block:

```sql
[ <<label>> ]
[ DECLARE
    declarations ]
BEGIN
    statements
END [ label ];
```

A block has two main sections:

- Declaration: The declaration section is optional. It is where you declare variables, constants, and cursors.
  - Each statement in the declaration section is terminated with a semicolon (`;`).
  - Besides the assignment operator (`=`), we can use the `:=` operator to assign an initial value to a variable.
  - We can use the `DEFAULT` keyword to specify an initial value of a variable.
- Body: The body section is required. It is where you put the logic of the block, such as SQL statements.

A block may include an optional label appearing at the beginning and end. A block ends with a semicolon (`;`) after the end keyword.

Here is a simple example of a block that displays a message:

```sql
DO
$$
BEGIN
    RAISE NOTICE 'Hello, World';
END;
$$;
```

- The `DO` statement executes the PL/pgSQL block.
- We use the PL/pgSQL block as a dollar-quoted string constant.

Here is the same example, this time with naming the block:

```sql
DO
$$
<<block_name>>
BEGIN
    RAISE NOTICE 'Hello, World';
END block_name;
$$;
```

The following example shows how to define a block with a declaration section. We declare a variable in the declaration section. To declare a variable, you provide the name, data type, and initial value:

```sql
DO
$$
DECLARE
    name VARCHAR = 'Joe';
BEGIN
    RAISE NOTICE 'Hello %', name;
END;
$$;
```

`%` is a placeholder for the string that comes after the comma.

We can also nest blocks:

```sql
DO
$$
DECLARE
	total_q INT DEFAULT 0;
BEGIN
	DECLARE
		safety_stock INT = 10;
		on_hand_q INT = 100;
	BEGIN
		total_q = safety_stock + on_hand_q;
	END;
	RAISE NOTICE 'The total quantity is %', total_q;
END;
$$;
	total_q INT = 0;
BEGIN
	DECLARE
		safety_stock INT =10;
		on_hand_q INT = 100;
	BEGIN
		total_q = safety_stock + on_hand_q;
	END;
	RAISE NOTICE 'The total quantity is %', total_q;
END;
$$;
```

The scope of a variable is within the block and nested blocks of the block where you declare it. For exampe, the variables that we declared in the subblocks above, can only be accessed within the subblock. If we attempt to access them from the outer block, we'll get an error.

Sometimes, we want to define variables whose values cannot be changed. To do that you can declare constants.

Here’s the syntax for declaring a constant:

```sql
constant_name CONSTANT data_type = initial_value;
```

The `CONSTANT` keyword indicates that the value of the `constant_name` cannot be changed after initialization.

Here is an example:

```sql
DO
$$
DECLARE
    pi CONSTANT DEC = 3.14;
    v_radius DEC = 10;
    v_area DEC;
BEGIN
    v_area = pi * v_radius * v_radius;
    RAISE NOTICE 'The area of a circle with the radius % is %', v_radius, v_area;
END;
$$;
```

---

---

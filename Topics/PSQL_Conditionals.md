# Conditional Expressions

- [Conditional Expressions](#conditional-expressions)
  - [`CASE`](#case)
  - [`IF`](#if)

---

---

## `CASE`

A `CASE` expression is a powerful tool, allowing you to perform conditional logic within your queries. Here’s the syntax of the `CASE` expression:

```sql
CASE  
  WHEN condition1 THEN result1
  WHEN condition2 THEN result2
  WHEN condition3 THEN result3

  ELSE result
END
```

If no condition is true, the `CASE` expression returns the result of the `ELSE` clause. The `ELSE` clause is optional. If you omit it and no condition returns true, then the `CASE` expression returns NULL.

```sql
SELECT
  username,
  account_balance,
  CASE
    WHEN account_balance >= 1000 THEN 'High'
    WHEN account_balance >= 500 THEN 'Medium'
    WHEN account_balance > 0 THEN 'Low'
    ELSE 'Empty'
  END AS balance_category
FROM users;
```

If you have one condition to evaluate, then you can use an alternative `CASE` expression:

```sql
CASE expression
  WHEN value1 THEN result1
  WHEN value2 THEN result2
  WHEN value3 THEN result3

  ELSE result
END
```

```sql
SELECT
  transaction_id,
  user_id,
  quantity,
  CASE quantity
    WHEN 1 THEN 'Small Order'
    WHEN 2 THEN 'Medium Order'
    WHEN 3 THEN 'Large Order'
    ELSE 'Bulk Order'
  END AS order_size
FROM transactions;
```

---

---

## `IF`

PL/pgSQL offers three forms of the `IF` statements:

- `IF-THEN`
- `IF-THEN-ELSE`
- `IF-THEN-ELSEIF`

Here’s the syntax of the `IF-THEN-ELSEIF` statement:

```sql
IF condition1 THEN
    statement1;
ELSEIF condition2 THEN
    statement2;
ELSEIF condition3 THEN
    statement3;
[ELSE
    else_statement;]
END IF;
```

---

---

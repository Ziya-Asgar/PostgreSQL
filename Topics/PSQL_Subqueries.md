# Subqueries

- [Subqueries](#subqueries)
  - [Subquery](#subquery)
  - [Correlated Subquery](#correlated-subquery)
  - [`WHERE IN` Subquery](#where-in-subquery)
  - [`EXISTS`](#exists)
  - [`ANY`](#any)
  - [`ALL`](#all)

---

---

## Subquery

PostgreSQL allows us to embed a query within another query. This embedded query is called a _subquery_. The query that contains a subquery is called an _outer query_.

The subquery can be placed in different parts of the SQL code. It could be used with many keywords including `SELECT`, `FROM`, `WHERE`, and `JOIN` depending on what result the subquery returns.

Here is an example of a subquery in a `WHERE` clause:

```sql
SELECT * FROM transactions
WHERE price > (SELECT AVG(price) FROM transactions);
```

Here is an example of a subquery in a `SELECT` statement:

```sql
SELECT
  product_id,
  price,
  (SELECT MAX(price) FROM transactions) max_price
FROM
  transactions;
```

Here is an example of a subquery in a `FROM` clause:

```sql
SELECT amount
FROM (SELECT product_id, price, amount FROM transactions WHERE amount > price);
```

---

---

## Correlated Subquery

A correlated subquery is a subquery that uses values from an outer query. Unlike a regular subquery that can execute independently, PostgreSQL may have to execute a correlated subquery for every row in the outer query. For this reason, you should avoid using the correlated subquery as much as possible to improve the query performance.

```sql
SELECT user_id, product_id FROM transactions t
WHERE user_id = (SELECT user_id FROM users u WHERE t.user_id = u.user_id);
```

Here is another example, where we find all users whose account balance is above the average account balance of users from the same country:

```sql
SELECT
	username,
	country,
	u1.account_balance
FROM users u1
WHERE account_balance > (
	SELECT AVG(account_balance) FROM users u2
	WHERE u1.country = u2.country
);
```

---

---

## `WHERE IN` Subquery

The `WHERE ... IN` subquery allows you to check if a value is in a set of values returned by subquery.

```sql
SELECT username, country FROM users
WHERE user_id IN (SELECT user_id FROM transactions);
```

You can use the `NOT IN` operator to filter rows that are not in a list returned by a query.

```sql
SELECT username, country FROM users
WHERE user_id NOT IN (SELECT user_id FROM transactions);
```

---

---

## `EXISTS`

The `EXISTS` operator returns `true` if the subquery returns any rows or `false` otherwise.

```sql
SELECT username FROM users u
WHERE EXISTS (
	SELECT 1 FROM transactions t
	WHERE u.user_id = t.user_id
);
```

To negate the result of the `EXISTS` operator, we use the `NOT` operator.

```sql
SELECT username FROM users u
WHERE NOT EXISTS (
	SELECT 1 FROM transactions t
	WHERE u.user_id = t.user_id
);
```

---

---

## `ANY`

The `ANY` operator allows you to compare a value with a set of values returned by a subquery. The `ANY` operator returns true if the comparison returns true for at least one value in the set. The ANY operator returns false if all comparisons are false. If the subquery returns no row, the `ANY` operator always returns true.

In PostgreSQL, `SOME` and `ANY` are synonyms, so you can use them interchangeably.

```sql
SELECT username, account_balance,
FROM users
WHERE account_balance > ANY (
  SELECT price
  FROM transactions
);
```

---

---

## `ALL`

The `ALL` operator allows you to compare a value with a set of values returned by a subquery. The `ALL` operator returns true if the comparison is true for all values in the set.

```sql
SELECT username, account_balance
FROM users
WHERE account_balance > ALL (
  SELECT price
  FROM transactions
);
```

---

---

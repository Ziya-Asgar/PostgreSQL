# Common Table Expressions (CTE)

- [Common Table Expressions (CTE)](#common-table-expressions-cte)
  - [Ordinary CTE](#ordinary-cte)
  - [Recursive CTE](#recursive-cte)

---

---

## Ordinary CTE

CTE stands for common table expression. PostgreSQL CTE provides a way to define a temporary table that can be referenced within a `SELECT`, `INSERT`, `UPDATE`, `DELETE`, and `MERGE` statements.

Here’s the syntax for defining a CTE:

```sql
WITH cte_name(column_list) AS (
   -- CTE query
   SELECT ...
)
-- Main query
SELECT select_list
FROM cte_name;
```

- The `WITH` keyword defines a common table expression (CTE). You can think of a CTE as a temporary table within the query.
- The main query is a statement that uses the CTE by referencing the `cte_name`. The main query can be a `SELECT`, `INSERT`, `UPDATE`, `DELETE`, or `MERGE` statement.

Here is an example:

```sql
WITH user_totals AS (
  SELECT
    user_id,
    SUM(amount) AS total_spent
  FROM transactions
  GROUP BY user_id
)
SELECT *
FROM user_totals
WHERE total_spent > 200;
```

---

---

## Recursive CTE

A recursive CTE is a type of CTE that references itself in its CTE query definition. A recursive CTE has two main parts:

- _Anchor_ member is a query that provides the base result set.
- _Recursive_ member is a query referencing the CTE itself. It will execute repeatedly and build up the final result set. The recursive member has a termination condition that stops execution when it returns no row.

A recursive CTE uses `UNION` or `UNION ALL` to combine result sets returned by the anchor member and recursive member.

Here’s the syntax of a recursive CTE:

```sql
WITH RECURSIVE cte_name (column1, column2, ...) AS (
    -- Anchor member
    SELECT ...
    UNION ALL
    -- Recursive member
    SELECT ...
    FROM cte_name
    WHERE ...
)
SELECT *
FROM cte_name;
```

In this syntax:

- The `WITH RECURSIVE` keyword defines a recursive CTE with a name (`cte_name`).
- An anchor member forms the base result set.
- A recursive member takes the base result set and starts the recursion until it returns no rows.
- The `UNION` (or `UNION ALL`) operator combines the result sets of the anchor member and recursive member into a final result set

The following example uses a recursive CTE to generate a countdown from 3 to 1:

```sql
WITH RECURSIVE count_down (counter) AS (
    -- Anchor member
    SELECT 3 AS counter
    UNION
    -- Recursive member
    SELECT counter - 1
    FROM count_down
    WHERE counter > 1
  )
SELECT * FROM count_down;
```

Here is an example of a recursive CTE to generate next 5 days from a user's signup:

```sql
WITH RECURSIVE next_days(day) AS (
  -- Anchor member: start with Ziya's signup_date
  SELECT signup_date::timestamp
  FROM users
  WHERE username = 'ziya'

  UNION ALL

  -- Recursive member: add 1 day until 5 days total
  SELECT day + INTERVAL '1 day'
  FROM next_days
  WHERE day < (SELECT signup_date::timestamp + INTERVAL '4 days' FROM users WHERE username = 'ziya')
)
SELECT * FROM next_days;
```

---

---

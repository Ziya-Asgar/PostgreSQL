# Updating data

To update data in PostgreSQL, we use the `UPDATE` and `SET` statements, which allow us to modify existing records in a table.

```sql
UPDATE users
SET account_balance = account_balance + 100
WHERE username = 'hasan';
```

The `UPDATE` statement offers the `RETURNING` clause that returns the updated rows.

```sql
UPDATE users
SET account_balance = account_balance - 100
WHERE username = 'hasan'
RETURNING *;
```

---

---

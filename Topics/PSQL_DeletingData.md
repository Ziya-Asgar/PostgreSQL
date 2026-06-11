# Deleting Data from Tables

The `DELETE` statement permanently removes one or more rows from a table.

```sql
DELETE FROM products
WHERE name = 'test product';
```

The `DELETE` statement has an optional `RETURNING` clause that returns the deleted rows.

```sql
DELETE FROM products
WHERE name = 'test product';
RETURNING *;
```

Here is how to delete all rows from a table:

```sql
DELETE FROM person;
```

---

---

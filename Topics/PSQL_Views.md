# Views

- [Views](#views)
  - [Creating a database view](#creating-a-database-view)
  - [Replacing a database view](#replacing-a-database-view)
  - [Dropping a database view](#dropping-a-database-view)
  - [Creating a materialized view](#creating-a-materialized-view)
  - [Dropping a materialized view](#dropping-a-materialized-view)

---

---

## Creating a database view

A view is a named query stored in the PostgreSQL database server. A view allows we to query data from it like a regular table but does not store the data physically. Therefore, a view is referred to as a virtual table.

In PostgreSQL, we can create views that store data physically. These views are called _materialized views_.

We use the `CREATE VIEW` statement to create a new view:

```sql
CREATE VIEW view_name
AS
query;
```

The query that defines the view is called the _defining query_. The tables that the defining query references are called _base tables_.

```sql
CREATE VIEW view_name
AS
SELECT username, email, country FROM users;
```

---

---

## Replacing a database view

If you want to modify an existing view, we can use `CREATE OR REPLACE VIEW` statement:

```sql
CREATE OR REPLACE VIEW view_name
AS query;
```

The `CREATE OR REPLACE VIEW` will create the `view_name` if it does not exist or replace the existing one if it does.

```sql
CREATE OR REPLACE VIEW view_name
AS
SELECT username, email, country, is_active FROM users;
```

---

---

## Dropping a database view

The `DROP VIEW` allows you to delete a view from the database permanently:

```sql
DROP VIEW IF EXISTS view_name CASCADE;
```

The `CASCADE` option will drop the views (and other objects) that depend on the `view_name` and, in turn, all objects that depend on those objects.

---

---

## Creating a materialized view

Regular views do not store data. When you query data from them, PostgreSQL retrieves data from the underlying tables. When views have complex defining queries, you’ll encounter performance issues if you query data from them very frequently. To address this issue, PostgreSQL introduces materialized views that physically store the result of queries. These materialized views can significantly improve performance for views with complex queries.

We use the `CREATE MATERIALIZED VIEW` statement to create a materialized view:

```sql
CREATE MATERIALIZED VIEW [IF NOT EXISTS] view_name
AS
query
WITH DATA;
```

We use the `WITH DATA` to load data from underlying tables into the view when we issue the `CREATE MATERIALIZED VIEW` statement.

```sql
CREATE MATERIALIZED VIEW IF NOT EXISTS view_name
AS
SELECT username, email, country FROM users
WITH DATA;
```

Materialized views will not automatically update data from the underlying tables. To replace the data of a materialized view with the new one from a table, we use the `REFRESH MATERIALIZED VIEW view_name;` statement:

---

---

## Dropping a materialized view

To delete a materialized view, you use the `DROP MATERIALIZED VIEW` statement:

```sql
DROP MATERIALIZED VIEW [ IF EXISTS ] view_name CASCADE;
```

---

---

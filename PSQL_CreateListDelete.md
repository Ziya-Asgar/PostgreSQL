# Creating, Listing, and Deleting Databases

- [Creating, Listing, and Deleting Databases](#creating-listing-and-deleting-databases)
  - [Listing databases](#listing-databases)
  - [Creating a database](#creating-a-database)
  - [Deleting a database](#deleting-a-database)

---

---

## Listing databases

To list the existing databases, we use `list` or `\l` command in psql.

To list the databases using a query, we can use the below code:

```sql
SELECT *
FROM pg_catalog.pg_database;
```

That Postgres catalog contains a row for each database in the server.

---

---

## Creating a database

To create a database in postgreSQL, we use:

```sql
CREATE DATABASE db_name;
```

---

---

## Deleting a database

To delete a database, we use:

```sql
DROP DATABASE test;
```

---

---

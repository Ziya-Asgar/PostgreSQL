# Schemas

- [Schemas](#schemas)

---

---

## Intro

A schema is a named collection of database objects, including tables, views, indexes, data types, functions, stored procedures, and operators. A schema allows you to organize database objects within a database. A database may contain one or more schemas. However, a schema belongs to only one database.
PostgreSQL automatically creates a schema called `public` for every new database.

---

---

## Listing and Accessing Schemas

The following statement returns all schemas from the current database:

```sql
SELECT *
FROM pg_catalog.pg_namespace
ORDER BY nspname;
```

To access an object in a schema, we need to write the object by using the following syntax:

```sql
schema_name.object_name
```

There is an even more general syntax

```sql
database_name.schema_name.table_name
```

When you reference a table using its name only, PostgreSQL searches for the table by using the schema search path, which is a list of schemas to look in. To view the current search path, you use the `SHOW` command in psql tool:

```sql
SHOW search_path;
```

In the default setup this returns:

```sql
 search_path
--------------
 "$user", public
```

The first element in the `search_path` specifies that a schema with the same name as the current user is to be searched. If no such schema exists, the entry is ignored. The second element refers to the public schema.

PostgreSQL will access the first matching table in the schema search path. If there is no match, it will return an error, even if the name exists in another schema in the database. The first schema in the search path is called the current schema.

The `current_schema()` function returns the current schema:

```sql
SELECT current_schema();
```

To add the new schema to the search path, you use the following command:

```sql
SET search_path TO new_schema, public;
```

---

---

## Creating Schemas

To create a new schema, you use the `CREATE SCHEMA` statement:

```sql
CREATE SCHEMA [IF NOT EXISTS] new_schema;
```

PostgreSQL allows to create a schema and a list of objects such as tables and views using a single statement as follows:

```sql
CREATE SCHEMA schema_name
    CREATE TABLE table_name1 (...)
    CREATE TABLE table_name2 (...)
    CREATE VIEW view_name1
        SELECT select_list FROM table_name1;
```

---

---

## Changing Schemas

The `ALTER SCHEMA` statement allows you to change the definition of a schema. For example, you can rename a schema as follows:

```sql
ALTER SCHEMA schema_name
RENAME TO new_name;
```

---

---

## Deleting Schemas

The `DROP SCHEMA` removes a schema and all of its objects from a database. The following illustrates the syntax of the `DROP SCHEMA` statement:

```sql
DROP SCHEMA [IF EXISTS] schema_name1 [,schema_name2,...]
[CASCADE | RESTRICT];
-- if the schema is not empty and you want to remove the schema and its objects, you must use the `CASCADE` option:
```

---

---

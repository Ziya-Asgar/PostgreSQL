# Creating, Listing, and Deleting Tables

- [Creating, Listing, and Deleting Tables](#creating-listing-and-deleting-tables)
  - [Creating a table](#creating-a-table)
    - [`CREATE TABLE`](#create-table)
    - [Generated columns](#generated-columns)
    - [`CREATE TABLE AS`](#create-table-as)
  - [Listing tables](#listing-tables)
  - [Deleting a table](#deleting-a-table)

---

---

## Creating a table

### `CREATE TABLE`

To create a table, we use the `CREATE TABLE` command. After the `CREATE TABLE table_name` clause, we specify column names as well as data types and optional constraints. Here is the syntax:

```sql
CREATE TABLE table_name (
  column_name data_type constraints_if_any
)
```

Here is an example:

```sql
CREATE TABLE users(
  user_id INT,
  username VARCHAR(50)
);
```

---

### Generated columns

A generated column is a special column that is always computed from other columns. There are two kinds of generated columns: stored and virtual. A stored generated column is computed when it is written (inserted or updated) and occupies storage as if it were a normal column. A virtual generated column occupies no storage and is computed when it is read. PostgreSQL currently implements only stored generated columns.

To create a generated column, use the `GENERATED ALWAYS AS` clause in `CREATE TABLE`, for example:

```sql
CREATE TABLE transactions (
  quantity INT NOT NULL CHECK (quantity > 0),
  price DECIMAL(8, 2) NOT NULL CHECK (price >= 0),
  amount DECIMAL(10, 2) GENERATED ALWAYS AS (quantity * price) STORED
);
```

The keyword `STORED` must be specified to choose the stored kind of generated column.

A generated column cannot be written to directly. In `INSERT` or `UPDATE` commands, a value cannot be specified for a generated column, but the keyword `DEFAULT` may be specified.

---

### `CREATE TABLE AS`

`CREATE TABLE AS` creates a table and fills it with data computed by a `SELECT` command. The table columns have the names and data types associated with the output columns of the `SELECT` (except that you can override the column names by giving an explicit list of new column names).

`CREATE TABLE AS` bears some resemblance to creating a view, but it is really quite different: it creates a new table and evaluates the query just once to fill the new table initially. The new table will not track subsequent changes to the source tables of the query. In contrast, a view re-evaluates its defining SELECT statement whenever it is queried.

Here is an example:

```sql
CREATE TABLE films_recent AS
  SELECT * FROM films WHERE date_prod >= '2002-01-01';
```

To copy a table completely, the short form using the `TABLE` command can also be used:

```sql
CREATE TABLE films2 AS
  TABLE films;
```

---

---

## Listing tables

To list the existing tables, we use the `\d` command in psql.

Note that if we have sequences (auto incremented columns), `\d` will also show them. In case we have sequences, but want to see the list of tables, we can use the `\dt` command.

To list the tables in PGAdmin tool, we can use the below command:

```sql
SELECT tablename FROM pg_tables WHERE schemaname = 'public';
```

Another way to list all the tables is using this command:

```sql
SELECT table_name FROM INFORMATION_SCHEMA.TABLES
WHERE table_schema LIKE '%public%';
```

To describe the actual table, we use the `\d <table_name>` command in psql.

In PGAdmin tool, we can use the below command to get the details about a table:

```sql
SELECT *
FROM information_schema.COLUMNS
WHERE TABLE_NAME = '<table_name>';
```

---

---

## Deleting a table

To delete a table, we use:

```sql
DROP TABLE table_name;
```

If you delete a table that does not exist, PostgreSQL will issue an error. However, with the `IF EXISTS` option, PostgreSQL will not issue any errors.

```sql
DROP TABLE IF EXISTS table_name;
```

The `DROP TABLE` statement can drop multiple tables at once.

If a table is referenced by another table, then PostgreSQL might raise an error while deleting the table. To delete the table, together with the columns referring to it, we use the `CASCADE` OPTION:

```sql
DROP TABLE IF EXISTS table_name CASCADE;
```

---

---

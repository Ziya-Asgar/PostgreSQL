# Import and Export a CSV File

- [Import and Export a CSV File](#import-and-export-a-csv-file)
  - [Import a CSV File](#import-a-csv-file)
  - [Export to a CSV File](#export-to-a-csv-file)

---

---

## Import a CSV File

There are various ways to import a CSV file into a PostgreSQL table. One way is to

- Create a new table,
- Then, to import a CSV file into the newly created table, we use `COPY` statement as follows

```sql
COPY table_name(column_name)
FROM 'pathToFile.csv'
DELIMITER ','
CSV HEADER;
```

In case the CSV file contains all columns of the table, we don’t need to specify them explicitly, for example:

```sql
COPY table_name
FROM 'pathToFile.csv'
DELIMITER ','
CSV HEADER;
```

---

---

## Export to a CSV File

The `COPY` statement allows to export data from a table to a CSV file.

```sql
COPY table_name
TO 'pathToFile.csv'
DELIMITER ','
CSV HEADER;
```

Sometimes, we may want to export data from some columns of a table to a CSV file. To achieve this, we can specify the column names together with the table name after `COPY` keyword.

```sql
COPY table_name(column_name)
TO 'pathToFile.csv'
DELIMITER ','
CSV HEADER;
```

If we don't want to export the header, which contains the column names of the table, we can remove the `HEADER` flag in the `COPY` statement.

---

---

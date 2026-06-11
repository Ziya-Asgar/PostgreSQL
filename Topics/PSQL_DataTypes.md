# Data Types

- [Data Types](#data-types)
  - [`BOOLEAN`](#boolean)
  - [`CHAR`](#char)
  - [`VARCHAR`](#varchar)
  - [`TEXT`](#text)
  - [`INTEGER`](#integer)
  - [`DECIMAL`](#decimal)
  - [`DATE`](#date)
  - [`TIME`](#time)
  - [`TIMESTAMP`](#timestamp)
  - [`TIMESTAMP WITH TIME ZONE`](#timestamp-with-time-zone)
  - [`INTERVAL`](#interval)
  - [`UUID`](#uuid)

---

---

## `BOOLEAN`

We use the `BOOLEAN` keyword or `BOOL` to store Boolean data. The boolean type has three values:

- `true`
- `false`
- `NULL`

Besides `true` and `false`, PostgreSQL uses various representations for `true` and `false` in SQL queries:

| True   | False   |
| ------ | ------- |
| `true` | `false` |
| 't'    | 'f'     |
| 'true' | 'false' |
| 'y'    | 'n'     |
| 'yes'  | 'no'    |
| '1'    | '0'     |

Notice that all other values need to be surrounded by single quotes except `true` and `false`.

Here is an example of creating a table with the `BOOLEAN` data type:

```sql
CREATE TABLE users(
  user_id INT,
  username VARCHAR(50),
  is_active BOOL
);
```

---

---

## `CHAR`

The `CHAR` type, also known as `CHARACTER`, is a fixed-length and blank-padded character type. Here’s the syntax for defining a column with the `CHAR` type:

```sql
column_name CHAR(n)
```

In this syntax, the column_name will store precisely n characters. If you store a string that is less than n, PostgreSQL will pad it with spaces to meet the required length. Note that if you use the `length()` function, PostgreSQL internally trim the spaces before returning the number of characters. To find the size of the stored characters, you can use the `octet_length()` function, which returns the number of bytes.

> In practice, you often use the `CHARACTER VARYING` (`VARCHAR`) type instead of the char type for storing text strings.

If you want a column to have an exact number of characters, no more, no less, you can use a `CHECK` constraint to enforce the rule.

Here is an example of creating a table with the `CHAR` data type:

```sql
CREATE TABLE users(
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50)
);
```

---

---

## `VARCHAR`

The `CHARACTER VARYING` type, or `VARCHAR`, allows you to store variable-length strings in the database. Unlike the `CHAR` column, PostgreSQL does not pad spaces if the values stored in the `VARCHAR` column have a length of less than n. Here’s the syntax for defining a column with the `CHARACTER VARYING` type:

```sql
column_name CHARACTER VARYING (n)
column_name VARCHAR(n)
```

In this syntax, specify the length specifier (n) that is the maximum number of characters the `VARCHAR` column can store. n is a positive integer and cannot exceed 10,485,760.

If you want to store a string with any length, you can omit the length specifier in the column definition:

```sql
column_name VARCHAR
```

---

---

## `TEXT`

The `TEXT` data type is a variable-length character data type. The main features of the `TEXT` data type column are:

- Variable length: The `TEXT` column can store strings of any length, up to 1GB. 1GB is the field length limit in PostgreSQL, not only `TEXT` field.
- Trailing spaces: The `TEXT` column retains trailing spaces and does not trim them upon retrieval. These trailing spaces are significant when making comparisons.
- Performance: The `TEXT` type has the same performance as the `VARCHAR` type.

> Note that `VARCHAR`, without a length specifier, behaves like `TEXT`.

Here is an example of creating a table with the `TEXT` data type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT
);
```

---

---

## `INTEGER`

PostgreSQL supports the following integer data types for storing integers:

- `SMALLINT`
- `INTEGER`. `INT` is the synonym of the `INTEGER` so that we can use them interchangeably.
- `BIGINT`

| Name       | Storage Size | Minimum value              | Maximum value              |
| ---------- | ------------ | -------------------------- | -------------------------- |
| `SMALLINT` | 2 bytes      | -32,768                    | +32,767                    |
| `INTEGER`  | 4 bytes      | -2,147,483,648             | +2,147,483,647             |
| `BIGINT`   | 8 bytes      | -9,223,372,036,854,775,808 | +9,223,372,036,854,775,807 |

---

---

## `DECIMAL`

`DECIMAL` is a numeric data type that allows you to store exact numeric values with precision. `DEC` and `NUMERIC` are synonyms of the `DECIMAL`, so you can use them interchangeably.

```sql
CREATE TABLE table_name(
  column_name DEC(p,s),
);
```

In this syntax:

- `p` stands for precision. The precision is the number of significant digits, including integer and fractional parts.
- `s` stands for scale. The scale is the number of digits to the right of the decimal point. The valid range for scale is from -1000 to 1000.

For example, a `DEC(11,2)` column can store a number with 11 digits, including two digits after the decimal point.

If you omit the scale, it will default to zero: `DEC(p)` is equivalent to `DEC(p,0)`.

However, the precision and scale will default to their above limits if you ignore both precision and scale: `DEC`.

Starting from PostgreSQL 15, you can declare a decimal column with a negative scale: `DEC(p,-s)`. In this syntax, PostgreSQL will round the number to the left of the decimal point.

Besides regular values, the decimal type supports several special values specified in the IEEE 754 standard:

- `Infinity` - represents an infinitely large value.
- `-Infinity` - represents an infinitely small value.
- `NaN` (not-a-number) - represents a value that is not a number, which results from an invalid calculation.

When using these values in SQL statements, you must place them in a single quote like `'Infinity'` , `'-Infinity'`, and `'NaN'`.

Here is an example of creating a table with the `DECIMAL` data type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2)
);
```

---

---

## `DATE`

We use the `DATE` data type to store date without time.

```sql
CREATE TABLE table_name (
  column_name DATE,
);
```

A date column can store a date between 4713 BC and 5874897 AD. PostgreSQL uses a 4-byte to store a date value. PostgreSQL accepts various date formats, but it is recommended to use ISO 8601, which is yyyy-mm-dd for date input.

Here is an example of create a table with the `DATE` type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_date DATE
);
```

We use the `SET datestyle` command to change the format for the current session. For example, to set the style to ISO with DMY ordering, we execute `SET datestyle TO 'ISO, DMY'`. To see the datestyle setting, we can use `SHOW datestyle;`.

If you want to set the current date as the default value, you can use the `CURRENT_DATE` function as follows:

```sql
CREATE TABLE table_name (
  column_name DATE DEFAULT CURRENT_DATE
);
```

---

---

## `TIME`

We use the `TIME` data type to store time data (without date) in tables. A time column can store a time value from 00:00:00 to 24:00:00. PostgreSQL uses 8-byte to store a time value. PostgreSQL allows you to store time with fractional seconds precision, up to 6 digits. To use a time value with fractional seconds precision, you use the following format: HH:MM:SS.pppppp. PostgreSQL accepts various time formats, giving you flexibility. However, it is recommended to use ISO 8601, which is HH:MM:SS for time input.

Here is the syntax:

```sql
CREATE TABLE table_name (
    column_name TIME(precision)
);
```

Here is an example of creating a table with the `TIME` data type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_date DATE,
  signup_time TIME(3)
);
```

If you want to set the current time as the default value, you can use the `CURRENT_TIME` function as follows:

```sql
CREATE TABLE table_name(
    column_name TIME DEFAULT CURRENT_TIME,
);
```

To remove the fractional second precision, you pass the precision as zero to the `current_time` function: `SELECT current_time(0);`.

To get the current local time, you use the `localtime` function: `SELECT localtime;`. And without fractional seconds: `SELECT localtime(0);`.

---

---

## `TIMESTAMP`

The `TIMESTAMP` data type allows you to store both date and time in the database. The `TIMESTAMP` data type does not include any time zone data. It means that when you change the time zone of your PostgreSQL server, the `TIMESTAMP` values stored in the database won't automatically change. PostgreSQL uses 8 bytes to store a `TIMESTAMP` value. The valid range of the `TIMESTAMP` is from 4713 BC to 294276 AD.

Here is an example of creating a table with the `TIMESTAMP` data type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3)
);
```

If you want to set a default value for a `TIMESTAMP` column, you can apply a `DEFAULT` constraint with the default value returned by the `LOCALTIMESTAMP` or `CURRENT_TIMESTAMP` function:

```sql
CREATE TABLE table_name(
  column_name TIMESTAMP DEFAULT LOCALTIMESTAMP
);
```

Note that the `LOCALTIMESTAMP` returns the local date and time based on the local time of the PostgreSQL server. PostgreSQL uses the ISO 8601 standard for both input and output timestamps: yyyy-mm-dd hh:mm:ss

> In practice, you should use the `TIMESTAMP` data type to store timestamps only when you save and retrieve them from the database and you’re not doing any calculations. Otherwise, you should use the `TIMESTAMPTZ` instead.

---

---

## `TIMESTAMP WITH TIME ZONE`

We can use the `TIMESTAMP WITH TIME ZONE` data type to store time zone-aware timestamp values. `TIMESTAMPTZ` is the shorthand of the `TIMESTAMP WITH TIME ZONE`, so we can use it to save some typing:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3),
  last_login_at TIMESTAMPTZ(3)
);
```

When you insert a timestamp into a `TIMESTAMPTZ` column, PostgreSQL converts it to UTC for storage. This conversion ensures the stored timestamp is consistent and not affected by time zone differences. The `TIMESTAMPTZ` can automatically handle daylight saving time changes and other time zone-related adjustments.

When you retrieve a timestamp from a `TIMESTAMPTZ` column, PostgreSQL converts the stored UTC timestamp back to the time zone of your session. It's important to note that PostgreSQL does not store time zones in the `TIMESTAMPTZ` column but does the time zone conversion when stored and retrieved.

You can set the time zone of your database session using the `SET TIME ZONE` statement. For example:

```sql
SET TIME ZONE 'America/Vancouver';
```

To see the time zone in the database server, we can use this command:

```sql
SHOW TIME ZONE;
```

To get a list of supported time zone names, you use the following statement:

```sql
SELECT * FROM pg_timezone_names;
```

The `CURRENT_TIMESTAMP` function returns the current time with a time zone.

```sql
SELECT CURRENT_TIMESTAMP;
```

---

---

## `INTERVAL`

Intervals are time durations such as 2 days, 3 hours, 1 year 6 months. We use the `INTERVAL` data type to store intervals. The interval type can store intervals in years, months, hours, minutes, seconds, and milliseconds.

The following statement shows how to create an interval of 2 days: `SELECT INTERVAL '2 days';`.

The following statement shows how to combine multiple units in a single interval: `SELECT INTERVAL '2 days 5 hours 30 minutes';`.

If you have a valid interval string, you explicitly cast it into an `INTERVAL` using the cast operator (`::`): `SELECT '1 day 10 hours'::INTERVAL;`.

Here is an example of creating a table with the `INTERVAL` data type:

```sql
CREATE TABLE users (
  user_id INT,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3),
  last_login_at TIMESTAMPTZ(3),
  membership_duration INTERVAL
);
```

PostgreSQL allows you to specify precision specifications for fractional seconds explicitly: `INTERVAL second(p)`. In this syntax, p is the number of fractional digits you want to retain in the interval.

PostgreSQL provides three functions for adjusting intervals:

- `JUSTIFY_HOURS`: adjust excess hours into days.
- `JUSTIFY_DAYS`: adjust excess days into months while handling leap year accurately.
- `JUSTIFY_INTERVAL`: adjusts months to years and days to months.

For example, the following statements adjust an interval:

```sql
SELECT JUSTIFY_HOURS(INTERVAL '26 hours');
SELECT JUSTIFY_DAYS(INTERVAL '75 days');
SELECT JUSTIFY_INTERVAL(INTERVAL '13 months 30 days');
```

---

---

## `UUID`

UUID stands for universal unique identifier and is 128 bits long. It guarantees uniqueness across systems and time. PostgreSQL uses the `UUID` type for storing `UUID` values.

Here is an example of creating a table with `UUID`:

```sql
CREATE TABLE users (
  user_id INT,
  user_uuid UUID,
  username VARCHAR(50),
  is_active BOOL,
  email CHAR(50),
  bio TEXT,
  account_balance DECIMAL(10, 2),
  signup_timestamp TIMESTAMP(3),
  last_login_at TIMESTAMPTZ(3),
  membership_duration INTERVAL
);
```

Typically, we use the `UUID` as the type of a primary key column of the table:

```sql
CREATE TABLE table_name (
  column_name UUID PRIMARY KEY,
);
```

PostgreSQL provides the `gen_random_uuid()` that allows you to generate a `UUID` value. For example, the following statement generates a `UUID` value: `SELECT gen_random_uuid();`.

You can use the `gen_random_uuid()` function to generate default values for the `UUID` primary key column:

```sql
CREATE TABLE table_name(
   user_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
);
```

---

---

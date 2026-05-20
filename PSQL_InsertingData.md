# Inserting Data Into Tables

To insert data into a table, we use the `INSERT INTO table_name` command, specify the columns into which we want to insert data in parentheses, and using the `VALUES()` command, we insert the actual data.

Let's insert data into these tables:

```sql
-- users table
CREATE TABLE users (
  user_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  username VARCHAR(50) NOT NULL UNIQUE,
  email CHAR(50) NOT NULL,
  country VARCHAR(50),
  is_active BOOLEAN DEFAULT true,
  signup_date DATE DEFAULT CURRENT_DATE,
  bio TEXT,
  account_balance DECIMAL(10, 2) CHECK (account_balance >= 0)
);

-- user_activity table
CREATE TABLE user_activity (
  activity_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  user_id INT NOT NULL,
  last_login TIMESTAMPTZ(3),
  total_time_logged INTERVAL,
  CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES users(user_id)
);

-- transactions table
CREATE TABLE transactions (
  transaction_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id INT NOT NULL,
  amount DECIMAL(8, 2) NOT NULL CHECK (amount >= 0),
  description TEXT,
  created_at TIMESTAMP(3) DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_user_tx FOREIGN KEY (user_id) REFERENCES users(user_id)
);
```

Here is an example of inserting data:

```sql
INSERT INTO users (
  username, email, country, is_active, signup_date, bio, account_balance
) VALUES (
  'ziya',
  'ziya@example.com',
  'Azerbaijan',
  true,
  '2025-02-15',
  NULL,
  750.25
);
```

Note that the order of columns listed after the table name does not matter. You can change the column order as you like. But you also need to change the order of values so that they match the columns.

PostgreSQL allows you to insert multiple rows into a table at once. We just need to have more `VALUES()` commands.

To return the inserted row, you add the `RETURNING` clause to the insert statement:

```sql
INSERT INTO user_activity (
  user_id, last_login, total_time_logged
) VALUES (1,  '2025-07-16 10:00:00+03', '5 hours 20 minutes')
RETURNING *;
```

The asterisk (\*) means returning all columns of the inserted row. To select columns to return, you can specify the column names in the `RETURNING` clause:

```sql
INSERT INTO transactions (
  user_id, amount, description
) VALUES (1, 100.00, 'Cloud service subscription')
RETURNING transaction_id, amount, created_at;
```

The `ON CONFLICT` keyword is used to handle unique constraint violations during insert operations. It allows you to specify what action to take when a conflict occurs, such as updating the existing record or doing nothing.

```sql
INSERT INTO users (username, email, country)
VALUES ('kerem', 'kerem@example.com', 'Turkiye')
ON CONFLICT (username)
DO NOTHING;
```

To update the existing record with new values when there is a conflict, we can use the following syntax:

```sql
INSERT INTO users (username, email, country, account_balance)
VALUES ('ziya', 'ziya@example.com', 'Azerbaijan', 900.00)
ON CONFLICT (username)
DO UPDATE SET account_balance = EXCLUDED.account_balance;
```

The `SET` and `WHERE` clauses in `ON CONFLICT DO UPDATE` have access to the existing row using the table's name (or an alias), and to the row proposed for insertion using the special `excluded` table.

---

---

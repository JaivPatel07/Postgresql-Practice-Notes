# 🐘 02 - The SELECT Statement

For practice, I use the **dvdrental** database. It is a sample database provided by PostgreSQL. It contains tables related to a DVD rental store, such as customers, rentals, films, and actors. You can use this database to practice your SQL skills and explore various queries.

---

## 📜 The SELECT Statement Clauses

The `SELECT` statement has the following clauses:

*   Select distinct rows using `DISTINCT` operator.
*   Sort rows using `ORDER BY` clause.
*   Filter rows using `WHERE` clause.
*   Select a subset of rows from a table using `LIMIT` or `FETCH` clause.
*   Group rows into groups using `GROUP BY` clause.
*   Filter groups using `HAVING` clause.
*   Join with other tables using joins such as `INNER JOIN`, `LEFT JOIN`, `FULL OUTER JOIN`, `CROSS JOIN` clauses.
*   Perform set operations using `UNION`, `INTERSECT`, and `EXCEPT`.

---

## 🏗️ The FROM Clause

The `FROM` clause is optional.
*   **Example:** `SELECT 'Hello, PostgreSQL' AS message;`

PostgreSQL evaluates the `FROM` clause **before** the `SELECT` clause in the `SELECT` statement.

> **Note:** The semicolon is not a part of the SQL statement; semicolons are used to separate two or more SQL statements.

---

## ⭐ Asterisk (*)

However, using the asterisk (`*`) in the `SELECT` statement is considered a bad practice when you embed SQL statements in the application code, such as Python, Java, or PHP for the following reasons:

1.  **Database performance:** Suppose you have a table with many columns and substantial data, the `SELECT` statement with the asterisk (`*`) shorthand will select data from all the columns of the table, potentially retrieving more data than required for the application.
2.  **Application performance:** Retrieving unnecessary data from the database increases the traffic between the PostgreSQL server and the application server. Consequently, this can result in slower response times and reduced scalability for your applications.

For these reasons, it is recommended to explicitly specify the column names in the `SELECT` clause whenever possible. This ensures that only the necessary data is retrieved from the database, contributing to more efficient and optimized queries.

---

## 💡 Examples

### 1. Concatenation
The following example uses the `SELECT` statement to return the full names and emails of all customers from the `customer` table:

```sql
SELECT
   first_name || ' ' || last_name,
   email
FROM
   customer;
```

**Output:**
```text
?column?        |                  email
------------------------+------------------------------------------
 Jared Ely             | jared.ely@example.com
 Mary Smith            | mary.smith@example.com
 Patricia Johnson      | patricia.johnson@example.com
...
```

In this example, we used the concatenation operator || to concatenate the first name, space, and last name of every customer.

### 2. Column Aliases
Notice the first column of the output doesn't have a name but `?column?`. To assign a name to a column temporarily in the query, you can use a **column alias**:

```sql
SELECT
   first_name || ' ' || last_name full_name,
   email
FROM
   customer;
```

**Output:**
```text
full_name       |                  email
------------------------+------------------------------------------
 Jared Ely             | jared.ely@example.com
 Mary Smith            | mary.smith@example.com
 Patricia Johnson      | patricia.johnson@example.com
...
```

### 3. SELECT NOW()

```sql
SELECT NOW();
```

In this example, we use the `NOW()` function in the `SELECT` statement. It'll return the current date and time of the PostgreSQL server.

*(Ref: Neon PostgreSQL Tutorial https://neon.com/postgresql/postgresql-tutorial/postgresql-select)*


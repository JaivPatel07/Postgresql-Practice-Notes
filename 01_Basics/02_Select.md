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

# The SELECT DISTINCT Clause

The `SELECT DISTINCT` clause is used to remove duplicate rows from a result set. It retains only one unique row for each group of duplicates.

---

## 📜 Syntax

### On a Single Column

```sql
SELECT
  DISTINCT column1
FROM
  table_name;
```

### On Multiple Columns

When you specify multiple columns, `DISTINCT` evaluates uniqueness based on the **combination of values** in those columns.

```sql
SELECT
   DISTINCT column1, column2
FROM
   table_name;
```

---

## 💡 Examples

Let's use the `film` and `customer` tables from the `dvdrental` database for our examples.

### 1. DISTINCT on a Single Column

To get a unique list of release years from the `film` table:

```sql
SELECT
  DISTINCT release_year
FROM
  film
ORDER BY
  release_year;
```
This query returns a list of all unique years in which films were released, sorted in ascending order.

### 2. DISTINCT on Multiple Columns

To get the unique combinations of first and last names from the `customer` table:

```sql
SELECT
   DISTINCT first_name,
   last_name
FROM
   customer
ORDER BY
   first_name,
   last_name;
```
This query will return unique pairs of `first_name` and `last_name`. If there are two customers named 'John Smith', only one 'John Smith' will appear in the result.

---

## ✨ DISTINCT ON (PostgreSQL Specific)

PostgreSQL also provides the `DISTINCT ON (expression)` clause, which is a more powerful and flexible way to remove duplicates. It keeps the "first" row of each group of duplicates, based on the ordering defined in the `ORDER BY` clause.

**Important:** The expression in `DISTINCT ON` must match the first expression in the `ORDER BY` clause.

### Example: Get the latest rental for each customer

```sql
SELECT
  DISTINCT ON (customer_id) customer_id,
  rental_id,
  rental_date
FROM
  rental
ORDER BY
  customer_id,
  rental_date DESC;
```
**How it works:**
1.  The query partitions rows by `customer_id`.
2.  Within each partition, it orders the rentals by `rental_date` from newest to oldest.
3.  `DISTINCT ON (customer_id)` then picks the **first row** from each partition, which corresponds to the latest rental for that customer.

---

## 🎯 Summary

1.  Use `SELECT DISTINCT` to remove duplicate rows from your query results.
2.  `DISTINCT` can be applied to one or more columns.
3.  When using multiple columns, uniqueness is determined by the combination of values.
4.  PostgreSQL offers a powerful `DISTINCT ON (expression)` clause to select a specific unique row from a group based on a defined order.


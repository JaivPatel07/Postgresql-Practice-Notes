# 🐘 04 - The SELECT DISTINCT Clause

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
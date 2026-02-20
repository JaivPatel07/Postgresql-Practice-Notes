# 🐘 02 - The GROUP BY Clause

The `GROUP BY` clause divides rows returned from a `SELECT` statement into groups. For each group, you can apply an **aggregate function** like `SUM()` or `COUNT()` to perform a calculation on the group.

---

## 📜 Syntax

```sql
SELECT
   column_1,
   column_2,
   ...,
   aggregate_function(column_3)
FROM
   table_name
GROUP BY
   column_1,
   column_2,
   ...;
```

**Key Points:**
1.  List the columns you want to group by in the `GROUP BY` clause.
2.  Any column in the `SELECT` list that is **not** inside an aggregate function **must** be in the `GROUP BY` clause.
3.  The `GROUP BY` clause returns one summary row for each group.

---

## 🏗️ Order of Evaluation

PostgreSQL evaluates clauses in the following order:
1.  `FROM`
2.  `WHERE`
3.  `GROUP BY`
4.  `HAVING`
5.  `SELECT`
6.  `DISTINCT`
7.  `ORDER BY`
8.  `LIMIT`

---

## 💡 Examples

### 1. `GROUP BY` with `SUM()`
To find the total amount paid by each customer:

```sql
SELECT
  customer_id,
  SUM(amount)
FROM
  payment
GROUP BY
  customer_id
ORDER BY
  customer_id;
```

**Output:**
```text
customer_id |  sum
-------------+--------
           1 | 114.70
           2 | 123.74
           3 | 130.76
...
```
**Explanation:** The query groups rows by `customer_id` and then uses `SUM(amount)` to calculate the total payment for each customer group.

### 2. `GROUP BY` with `COUNT()`
To count the number of payments processed by each staff member:

```sql
SELECT
	staff_id,
	COUNT(payment_id)
FROM
	payment
GROUP BY
	staff_id;
```

**Output:**
```text
 staff_id | count
----------+-------
        1 |  7292
        2 |  7304
```

### 3. `GROUP BY` with `JOIN`
To get the full name of each customer and their total payment amount, sorted from highest to lowest:

```sql
SELECT
  c.first_name || ' ' || c.last_name AS full_name,
  SUM(p.amount) AS total_amount
FROM
  payment p
INNER JOIN
  customer c ON p.customer_id = c.customer_id
GROUP BY
  full_name
ORDER BY
  total_amount DESC;
```

**Output:**
```text
full_name       | amount
-----------------------+--------
 Eleanor Hunt          | 211.55
 Karl Seal             | 208.58
 Marion Snyder         | 194.61
...
```

### 4. `GROUP BY` with Multiple Columns
To see how many rentals each customer made on a specific date:

```sql
SELECT
    customer_id,
    CAST(rental_date AS DATE) AS rental_day,
    COUNT(rental_id) AS rentals_on_day
FROM
    rental
GROUP BY
    customer_id,
    rental_day
ORDER BY
    customer_id,
    rental_day;
```
**Explanation:** This query groups rows first by `customer_id` and then by the `rental_day`. It then counts the number of rentals for each unique combination of customer and day.

---

## 🎯 Summary

1.  `GROUP BY` is used to group rows that have the same values into summary rows.
2.  It is almost always used with **aggregate functions** (`COUNT`, `SUM`, `AVG`, `MAX`, `MIN`).
3.  Columns in the `SELECT` list must either be in an aggregate function or in the `GROUP BY` clause.
4.  `GROUP BY` is evaluated after `WHERE` but before `HAVING` and `SELECT`.
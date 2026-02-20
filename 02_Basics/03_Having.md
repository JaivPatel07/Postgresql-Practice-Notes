# 🐘 03 - The HAVING Clause

The `HAVING` clause is used to filter groups created by the `GROUP BY` clause. It specifies a search condition for a group or an aggregate.

---

## 🤔 WHERE vs. HAVING

This is a common point of confusion. Here's the key difference:

| Clause | Purpose | When it runs | Can use aggregates? |
| :--- | :--- | :--- | :--- |
| `WHERE` | Filters **rows** | **Before** grouping | ❌ No |
| `HAVING`| Filters **groups** | **After** grouping | ✅ Yes |

> In short: Use `WHERE` to filter individual records, and `HAVING` to filter the results of aggregate functions.

---

## 📜 Syntax

SELECT
  column1,
  aggregate_function(column2)
FROM
  table_name
GROUP BY
  column1
HAVING
  condition;
```

---

## 🏗️ Order of Evaluation

PostgreSQL evaluates clauses in the following order:
1.  `FROM`
2.  `WHERE`
3.  `GROUP BY`
4.  `HAVING`
5.  `SELECT`
6.  `ORDER BY`
7.  `LIMIT`

> **⚠️ Important:** Because `HAVING` is evaluated **before** `SELECT`, you **cannot** use column aliases defined in the `SELECT` clause inside the `HAVING` clause.

---

## 💡 Examples

### 1. `HAVING` with `SUM()`
Find customers who have spent more than $100 in total.

SELECT
  customer_id,
  SUM(amount)
FROM
  payment
GROUP BY
  customer_id
HAVING
  SUM(amount) > 100
ORDER BY
  SUM(amount) DESC;
```

**Output:**
```text
 customer_id |   sum
-------------+--------
         148 | 211.55
         526 | 208.58
         178 | 194.61
...
```
**Explanation:**
1.  The query first groups payments by `customer_id` and calculates the `SUM(amount)` for each.
2.  The `HAVING` clause then filters these groups, keeping only those where the total sum is greater than 100.

### 2. `HAVING` with `COUNT()`
Find staff members who have handled more than 7,300 payments.

```sql
SELECT
    staff_id,
    COUNT(payment_id)
FROM
    payment
GROUP BY
    staff_id
HAVING
    COUNT(payment_id) > 7300;
```

**Output:**
```text
 staff_id | count
----------+-------
        2 |  7304
(1 row)
```

---

## 🎯 Summary

1.  `HAVING` is used to filter groups based on a condition.
2.  It is almost always used with the `GROUP BY` clause.
3.  `WHERE` filters rows before grouping; `HAVING` filters groups after grouping.
4.  You can use aggregate functions inside the `HAVING` clause, but not in the `WHERE` clause.
5.  Column aliases from the `SELECT` list cannot be used in the `HAVING` clause.
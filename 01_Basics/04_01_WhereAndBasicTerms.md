# 🐘 05 - Filtering Data (WHERE, LIMIT, OFFSET)

The `SELECT` statement returns all rows from one or more columns in a table. To retrieve rows that satisfy a specified condition, you use a `WHERE` clause.

---

## 🔍 1. The WHERE Clause

The `WHERE` clause allows you to filter rows based on a specific condition. Only rows that satisfy the condition (evaluate to `True`) are returned.

### 📜 Syntax

```sql
SELECT
  select_list
FROM
  table_name
WHERE
  condition
ORDER BY
  sort_expression;
```

**Key Points:**
1.  Place the `WHERE` clause right after the `FROM` clause.
2.  The condition must evaluate to `True`, `False`, or `Unknown` (NULL).

### 🏗️ Order of Evaluation

PostgreSQL evaluates the query in this order:
1.  `FROM`
2.  `WHERE`
3.  `SELECT`
4.  `ORDER BY`

> **⚠️ Important:** Because `WHERE` runs **before** `SELECT`, you **cannot** use column aliases (defined in `SELECT`) inside the `WHERE` clause.

---

## 🧮 2. Comparison Operators

| Operator | Description |
| :--- | :--- |
| `=` | Equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |
| `<>` or `!=` | Not equal |
| `AND` | Logical operator AND |
| `OR` | Logical operator OR |
| `IN` | Return true if a value matches any value in a list |
| `BETWEEN` | Return true if a value is between a range |
| `LIKE` | Return true if a value matches a pattern |
| `IS NULL` | Return true if a value is NULL |
| `NOT` | Negate the result of other operators |

---

## 🧠 3. Boolean Logic (AND, OR)

In PostgreSQL, a boolean value can be `TRUE`, `FALSE`, or `NULL`.

*   **True representations:** `true`, `'t'`, `'true'`, `'y'`, `'yes'`, `'1'`
*   **False representations:** `false`, `'f'`, `'false'`, `'n'`, `'no'`, `'0'`

### AND Operator
Returns `TRUE` only if **both** expressions are true.

| Exp 1 | Exp 2 | Result |
| :--- | :--- | :--- |
| ✅ True | ✅ True | ✅ **True** |
| ✅ True | ❌ False | ❌ False |
| ✅ True | ❓ Null | ❓ Null |
| ❌ False | ❓ Null | ❌ False |
| ❓ Null | ❓ Null | ❓ Null |

### OR Operator
Returns `TRUE` if **any** of the expressions is true.

| Exp 1 | Exp 2 | Result |
| :--- | :--- | :--- |
| ✅ True | ✅ True | ✅ **True** |
| ✅ True | ❌ False | ✅ **True** |
| ✅ True | ❓ Null | ✅ **True** |
| ❌ False | ❌ False | ❌ False |
| ❌ False | ❓ Null | ❓ Null |
| ❓ Null | ❓ Null | ❓ Null |

---

## ✂️ 4. LIMIT and OFFSET (Pagination)

`LIMIT` and `OFFSET` are used to retrieve a subset of rows, commonly for pagination.

### 📜 Syntax

```sql
SELECT
  select_list
FROM
  table_name
ORDER BY
  sort_expression
LIMIT
  row_count
OFFSET
  row_to_skip;
```

### 💡 Key Rules
1.  **LIMIT**: Constrains the number of rows returned.
    *   If `row_count` is `0`, returns empty set.
    *   If `row_count` is `NULL`, returns all rows (same as no LIMIT).
2.  **OFFSET**: Skips a number of rows before returning.
    *   If `row_to_skip` is `0`, behaves like no OFFSET.
3.  **Evaluation**: PostgreSQL evaluates `OFFSET` before `LIMIT`.
4.  **Ordering**: Always use `ORDER BY` with `LIMIT/OFFSET`. Without it, the order of rows is unpredictable.

### 💡 Example

```sql
-- Get 5 customers, skipping the first 10
SELECT customer_id, first_name
FROM customer
ORDER BY customer_id
LIMIT 5 OFFSET 10;
```

---

## 🎯 Summary

1.  **WHERE**: Filters rows based on conditions.
2.  **Operators**: Use standard comparison (`=`, `>`, `<`) and logical (`AND`, `OR`) operators.
3.  **LIMIT**: Restricts result size.
4.  **OFFSET**: Skips rows for pagination.
5.  **Best Practice**: Always combine `LIMIT` with `ORDER BY`.
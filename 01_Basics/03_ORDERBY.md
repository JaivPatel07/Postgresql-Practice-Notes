# 🐘 03 - The ORDER BY Clause

When you query data from a table, the `SELECT` statement returns rows in an unspecified order. To sort the rows of the result set, you use the `ORDER BY` clause in the `SELECT` statement.

The `ORDER BY` clause allows you to sort rows returned by a `SELECT` clause in ascending or descending order based on a sort expression.

---

## 📜 Syntax

```sql
SELECT
  select_list
FROM
  table_name
ORDER BY
  sort_expression1 [ASC | DESC],
  sort_expression2 [ASC | DESC],
  ...;
```

**In this syntax:**
1.  Specify a **sort expression** (column or expression) after the `ORDER BY` keywords.
2.  If you want to sort by multiple columns, separate them with a comma (`,`).
3.  Use `ASC` to sort in **ascending** order (default).
4.  Use `DESC` to sort in **descending** order.

---

## 🏗️ Order of Evaluation

PostgreSQL evaluates the clauses in the `SELECT` statement in the following order:
1.  `FROM`
2.  `SELECT`
3.  `ORDER BY`

Because `ORDER BY` is evaluated **after** `SELECT`, you can use **column aliases** defined in the `SELECT` clause inside the `ORDER BY` clause.

---

## 💡 Examples

### 1. Sorting by a Single Column
Sort customers by their first name in ascending order:

```sql
SELECT
   first_name,
   last_name
FROM
   customer
ORDER BY
   first_name ASC;
```

### 2. Sorting by Multiple Columns
Sort customers by first name (ascending), then by last name (descending) for those with the same first name:

```sql
SELECT
   first_name,
   last_name
FROM
   customer
ORDER BY
   first_name ASC,
   last_name DESC;
```

### 3. Sorting by Expressions (Length)
The `LENGTH()` function returns the length of a string. You can sort by the result of this function.

```sql
SELECT
  first_name,
  LENGTH(first_name) AS len
FROM
  customer
ORDER BY
  len DESC;
```

---

## 🧩 Handling NULL Values

In the database world, `NULL` indicates missing or unknown data. When sorting, you can specify where `NULL` values appear using `NULLS FIRST` or `NULLS LAST`.

**Syntax:**
```sql
ORDER BY sort_expression [ASC | DESC] [NULLS FIRST | NULLS LAST]
```

**Default Behavior:**
*   `ASC` order: `NULLS LAST` is the default.
*   `DESC` order: `NULLS FIRST` is the default.

---

## 🎯 Summary

1.  Use `ORDER BY` to sort result sets.
2.  `ASC` sorts ascending (default), `DESC` sorts descending.
3.  You can sort by multiple columns or expressions.
4.  `ORDER BY` is evaluated after `SELECT`, so aliases work.
5.  Use `NULLS FIRST` or `NULLS LAST` to control `NULL` placement.
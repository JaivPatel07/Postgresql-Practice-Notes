# 🐘 01 - Joins in PostgreSQL

A **Join** is used to combine rows from two or more tables based on a related column between them.

PostgreSQL supports several types of joins:
*   **Inner Join**
*   **Left Join**
*   **Right Join**
*   **Full Outer Join**
*   Cross Join
*   Natural Join
*   Self Join

**Output:**
```text
 a | fruit_a | b | fruit_b
---+---------+---+------------
 2 | Orange  | 1 | Orange
 1 | Apple   | 2 | Apple
   |         | 3 | Watermelon
   |         | 4 | Pear
```

**Explanation:**
*   The query returns all rows from the right table (`basket_b`).
*   'Watermelon' and 'Pear' are in `basket_b` but not `basket_a`, so `basket_a` columns are `NULL`.


## 🛠️ Setup: Sample Tables

Let's create two tables, `basket_a` and `basket_b`, to demonstrate how joins work.

```sql
CREATE TABLE basket_a (
    a INT PRIMARY KEY,
    fruit_a VARCHAR (100) NOT NULL
);

CREATE TABLE basket_b (
    b INT PRIMARY KEY,
    fruit_b VARCHAR (100) NOT NULL
);

INSERT INTO basket_a (a, fruit_a)
VALUES
    (1, 'Apple'),
    (2, 'Orange'),
    (3, 'Banana'),
    (4, 'Cucumber');

INSERT INTO basket_b (b, fruit_b)
VALUES
    (1, 'Orange'),
    (2, 'Apple'),
    (3, 'Watermelon'),
    (4, 'Pear');
```

**Output:**
```text
 a | fruit_a | b | fruit_b
---+---------+---+------------
 2 | Orange  | 1 | Orange
 1 | Apple   | 2 | Apple
   |         | 3 | Watermelon
   |         | 4 | Pear
```

**Explanation:**
*   The query returns all rows from the right table (`basket_b`).
*   'Watermelon' and 'Pear' are in `basket_b` but not `basket_a`, so `basket_a` columns are `NULL`.


## 1. Inner Join

The **Inner Join** returns rows when there is a match in **both** tables.

### 📜 Syntax & Example

```sql
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
INNER JOIN basket_b
    ON fruit_a = fruit_b;
```

**Output:**
```text
a | fruit_a | b | fruit_b
---+---------+---+---------
 1 | Apple   | 2 | Apple
 2 | Orange  | 1 | Orange
```

**Explanation:**
*   It compares `fruit_a` with `fruit_b`.
*   Only 'Apple' and 'Orange' exist in both tables, so only those rows are returned.

---

## 2. Left Join

The **Left Join** returns all rows from the **left** table (`basket_a`), and the matched rows from the right table (`basket_b`). If there is no match, the result is `NULL` on the right side.

### 📜 Syntax & Example

```sql
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
LEFT JOIN basket_b
    ON fruit_a = fruit_b;
```

---

## 3. Right Join

The **Right Join** is the reverse of the Left Join. It returns all rows from the **right** table (`basket_b`), and the matched rows from the left table (`basket_a`).

### 📜 Syntax & Example

```sql
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
RIGHT JOIN basket_b
    ON fruit_a = fruit_b;
```

---

## 4. Full Outer Join

The **Full Outer Join** returns all rows when there is a match in **either** left or right table. Rows that do not have a match in the other table will contain `NULL`.

### 📜 Syntax & Example

```sql
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
FULL OUTER JOIN basket_b
    ON fruit_a = fruit_b;
```

---

## 🎯 Summary

| Join Type | Description |
| :--- | :--- |
| **INNER JOIN** | Returns records that have matching values in both tables. |
| **LEFT JOIN** | Returns all records from the left table, and the matched records from the right table. |
| **RIGHT JOIN** | Returns all records from the right table, and the matched records from the left table. |
| **FULL JOIN** | Returns all records when there is a match in either left or right table. |

!Join Types Visualization
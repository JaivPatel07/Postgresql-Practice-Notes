# 🐘 06 - Advanced Filtering Operators

This guide covers powerful operators that go beyond basic comparisons, allowing you to create more specific and efficient queries.

---

## 1. The FETCH Clause

The `FETCH` clause is the standard SQL way to retrieve a portion of rows, similar to PostgreSQL's `LIMIT` clause. It is often used with `OFFSET` for pagination.

### 📜 Syntax

```sql
OFFSET row_to_skip {ROW | ROWS}
FETCH {FIRST | NEXT} [row_count] {ROW | ROWS} ONLY
```

**Key Points:**
*   `OFFSET`: Skips a specified number of rows. Defaults to `0`.
*   `FETCH`: Retrieves the next `row_count` rows. Defaults to `1`.
*   `ROW` and `ROWS` are synonyms. `FIRST` and `NEXT` are synonyms.
*   **Best Practice**: Always use `ORDER BY` with `FETCH` to ensure a predictable result.

> **Note:** While `FETCH` is standard SQL, `LIMIT` is simpler and more common in PostgreSQL. Use `FETCH` if you need your code to be compatible with other database systems.

### 💡 Example

```sql
-- Get 5 films after skipping the first 5
SELECT film_id, title
FROM film
ORDER BY title
OFFSET 5 ROWS
FETCH FIRST 5 ROW ONLY;
```

---

## 2. The IN Operator

The `IN` operator checks if a value matches any value in a given list. It's a concise and efficient alternative to multiple `OR` conditions.

### 📜 Syntax
```sql
value IN (value1, value2, ...)
value NOT IN (value1, value2, ...)
```

### 💡 Example
Find all customers with `customer_id` 1, 2, or 3.

```sql
-- Using IN is cleaner and faster
SELECT customer_id, first_name, last_name
FROM customer
WHERE customer_id IN (1, 2, 3);

-- This is the same as:
-- WHERE customer_id = 1 OR customer_id = 2 OR customer_id = 3;
```

---

## 3. The BETWEEN Operator

The `BETWEEN` operator checks if a value falls within a specified range. The range is **inclusive**, meaning it includes both the start and end values.

### 📜 Syntax
```sql
value BETWEEN low AND high
value NOT BETWEEN low AND high
```

### 💡 Example
Find all payments with an amount between $8 and $9.

```sql
SELECT customer_id, payment_id, amount
FROM payment
WHERE amount BETWEEN 8 AND 9
ORDER BY amount;

-- This is the same as:
-- WHERE amount >= 8 AND amount <= 9;
```

---

## 4. The LIKE Operator (Pattern Matching)

The `LIKE` operator is used for pattern matching in strings. It's incredibly useful when you only know part of a value.

### Wildcards
*   `%` (Percent sign): Matches any sequence of zero or more characters.
*   `_` (Underscore): Matches any single character.

### 💡 Examples
```sql
-- Find customers whose first name starts with 'Jen'
SELECT first_name, last_name FROM customer
WHERE first_name LIKE 'Jen%';

-- Find customers whose first name contains 'er'
SELECT first_name, last_name FROM customer
WHERE first_name LIKE '%er%';

-- Find customers whose first name has 'a' as the second letter
SELECT first_name, last_name FROM customer
WHERE first_name LIKE '_a%';
```

### ILIKE (Case-Insensitive)
PostgreSQL provides `ILIKE` for case-insensitive pattern matching.

```sql
-- Matches 'Jen', 'jen', 'jEn', etc.
SELECT first_name, last_name FROM customer
WHERE first_name ILIKE 'jen%';
```

### ESCAPE Clause
To search for a literal `%` or `_`, use the `ESCAPE` clause to define an escape character.

```sql
-- Suppose you have a table with film titles like 'Film_A' and 'Film_B'
-- To find titles containing a literal underscore, you can do this:
SELECT title FROM film
WHERE title LIKE '%#_%' ESCAPE '#';
```

---

## 5. The IS NULL Operator

`NULL` represents an unknown or missing value. It is special and cannot be compared using standard operators like `=` or `!=`.

> **⚠️ Important:** Any comparison with `NULL` (e.g., `column = NULL` or `NULL = NULL`) results in `NULL`, not `TRUE` or `FALSE`.

To check for `NULL` values, you must use `IS NULL` or `IS NOT NULL`.

### 📜 Syntax
```sql
value IS NULL
value IS NOT NULL
```

### 💡 Example
Find customers who do not have a `last_name` recorded.

```sql
SELECT customer_id, first_name
FROM customer
WHERE last_name IS NULL;
```

---

## 🎯 Summary

1.  **FETCH**: A standard SQL way to limit rows, similar to `LIMIT`.
2.  **IN**: Checks if a value exists in a list. More readable and faster than multiple `OR`s.
3.  **BETWEEN**: Checks if a value is within an inclusive range.
4.  **LIKE / ILIKE**: Performs pattern matching on strings using wildcards (`%`, `_`).
5.  **IS NULL**: The correct way to check for `NULL` values.
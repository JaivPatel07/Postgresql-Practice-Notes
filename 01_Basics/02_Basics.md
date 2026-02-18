# 🐘 02 - Core SQL Mastery in PostgreSQL

Welcome! This section covers the fundamental building blocks of SQL in PostgreSQL. We'll explore how to define table structures, manipulate data, and retrieve specific information.

---

## 🏗️ 1. SQL Command Categories: DDL vs DML

SQL commands are grouped into categories. The two most important are DDL and DML.

| Category | Full Name | Purpose | Example Commands |
| :--- | :--- | :--- | :--- |
| **DDL** | Data Definition Language | Defines or modifies the database **structure** (the blueprint). | `CREATE`, `ALTER`, `DROP` |
| **DML** | Data Manipulation Language | Manages the **data** within the tables. | `INSERT`, `UPDATE`, `DELETE`, `SELECT` |

### DDL (Data Definition Language)
Think of DDL as the architect's tools for building the database schema.

- **`CREATE`**: Builds a new object (like a table).
  ```sql
  -- Creates a new table to store employee information
  CREATE TABLE employees (
      id SERIAL PRIMARY KEY,
      name VARCHAR(100),
      department VARCHAR(50)
  );
  ```
- **`ALTER`**: Modifies an existing object's structure.
  ```sql
  -- Adds a new 'salary' column to the employees table
  ALTER TABLE employees ADD COLUMN salary NUMERIC(10, 2);
  ```
- **`DROP`**: Deletes an entire object. **Warning: Use with caution!**
  ```sql
  -- Deletes the employees table completely
  DROP TABLE employees;
  ```

### DML (Data Manipulation Language)
Think of DML as the tools for adding, changing, or removing the contents of the database.

- **`INSERT`**: Adds new rows (records) into a table.
  ```sql
  -- Adds a new employee record
  INSERT INTO employees (name, department, salary)
  VALUES ('Ravi Kumar', 'Engineering', 60000);
  ```
- **`UPDATE`**: Modifies existing rows.
  ```sql
  -- Changes the salary for the employee named 'Ravi Kumar'
  UPDATE employees
  SET salary = 65000
  WHERE name = 'Ravi Kumar';
  ```
- **`DELETE`**: Removes rows from a table.
  ```sql
  -- Removes the employee record for 'Ravi Kumar'
  DELETE FROM employees
  WHERE name = 'Ravi Kumar';
  ```
- **`SELECT`**: Retrieves data from one or more tables. This is the most common SQL command.
  ```sql
  -- Retrieves the name and salary of all employees
  SELECT name, salary FROM employees;
  ```

---

## 📊 2. PostgreSQL Data Types

When creating a table, you must specify a data type for each column. This tells the database what kind of data to expect.

| Category | Data Type | Description | Example Usage |
| :--- | :--- | :--- | :--- |
| **Numeric** | `INT` / `BIGINT` | For whole numbers. `BIGINT` for very large numbers. | `age INT` |
| | `NUMERIC(p, s)` | For exact decimal numbers. `p`=total digits, `s`=digits after decimal. | `price NUMERIC(8, 2)` |
| | `REAL` / `DOUBLE PRECISION` | For floating-point (inexact) numbers. | `temperature REAL` |
| **Character** | `VARCHAR(n)` | For variable-length text up to `n` characters. **Most common text type.** | `name VARCHAR(100)` |
| | `TEXT` | For text of unlimited length. | `article_content TEXT` |
| **Date/Time** | `DATE` | Stores only the date (YYYY-MM-DD). | `birth_date DATE` |
| | `TIMESTAMP` | Stores both date and time. | `created_at TIMESTAMP` |
| **Boolean** | `BOOLEAN` | Stores `TRUE` or `FALSE` values. | `is_active BOOLEAN` |
| **Auto-Increment** | `SERIAL` | An auto-incrementing integer, perfect for primary keys. | `id SERIAL` |

---

## 🛡️ 3. Constraints: Enforcing Data Rules

Constraints are rules applied to columns to ensure data integrity and accuracy.

| Constraint | Purpose |
| :--- | :--- |
| `NOT NULL` | Ensures a column cannot have a `NULL` (empty) value. |
| `UNIQUE` | Ensures all values in a column are different from each other. |
| `PRIMARY KEY` | A combination of `NOT NULL` and `UNIQUE`. Uniquely identifies each row in a table. |
| `FOREIGN KEY` | Links a row in one table to a row in another table, creating a relationship. |
| `CHECK` | Ensures that all values in a column satisfy a specific condition. |
| `DEFAULT` | Sets a default value for a column when no value is specified. |

**Example: A table with multiple constraints**
```sql
CREATE TABLE products (
    product_id SERIAL PRIMARY KEY, -- Automatically unique and not null
    product_code VARCHAR(20) NOT NULL UNIQUE, -- Must be provided and must be unique
    name VARCHAR(100) NOT NULL,
    price NUMERIC(10, 2) CHECK (price > 0), -- Price must be positive
    status VARCHAR(10) DEFAULT 'active', -- Defaults to 'active' if not provided
    category_id INT REFERENCES categories(id) -- Links to a 'categories' table
);
```

---

## 🔍 4. Filtering Data with `WHERE`

The `WHERE` clause is used to filter records and extract only those that fulfill a specified condition.

### Basic Operators (`=`, `>`, `<`, `<>`)
```sql
-- Select employees with a salary greater than 50000
SELECT * FROM employees WHERE salary > 50000;
```

### `AND` / `OR`
- `AND`: Displays a record if **all** conditions are true.
- `OR`: Displays a record if **any** of the conditions are true.
```sql
-- Select employees from the 'Engineering' department with a salary > 60000
SELECT * FROM employees
WHERE department = 'Engineering' AND salary > 60000;
```

### `BETWEEN`
Selects values within a given range (inclusive).
```sql
-- Select employees with a salary between 50000 and 70000
SELECT * FROM employees
WHERE salary BETWEEN 50000 AND 70000;
```

### `IN`
Specifies multiple possible values for a column.
```sql
-- Select employees from the 'Engineering' or 'Marketing' departments
SELECT * FROM employees
WHERE department IN ('Engineering', 'Marketing');
```

### `LIKE`
Used for pattern matching in strings.
- `%`: Represents zero, one, or multiple characters.
- `_`: Represents a single character.
```sql
-- Select employees whose name starts with 'A'
SELECT * FROM employees WHERE name LIKE 'A%';

-- Select employees whose name has 'a' as the second letter
SELECT * FROM employees WHERE name LIKE '_a%';
```

---

## 📈 5. Sorting Data with `ORDER BY`

The `ORDER BY` clause sorts the result set in ascending or descending order.

- **`ASC`**: Ascending order (A-Z, 0-9). This is the default.
- **`DESC`**: Descending order (Z-A, 9-0).

```sql
-- Sort employees by salary from highest to lowest
SELECT name, salary FROM employees
ORDER BY salary DESC;

-- Sort employees by name alphabetically
SELECT name, salary FROM employees
ORDER BY name ASC; -- ASC is optional here
```

---

## 🎯 Summary & Interview Tips

- **DDL vs. DML**: DDL builds the house (`CREATE TABLE`), DML furnishes it (`INSERT` data). This is a classic interview question.
- **`VARCHAR` vs. `TEXT`**: Use `VARCHAR(n)` when you have a known length limit (e.g., postal code). Use `TEXT` for long-form content.
- **`PRIMARY KEY`**: The single most important column in a table for identifying records. `SERIAL` is its best friend.
- **`WHERE` is your filter**: Master the `WHERE` clause to retrieve precisely the data you need.
- **`ORDER BY` is for presentation**: Use it to make your output readable and organized.
- **Always be careful with `DROP` and `DELETE` without a `WHERE` clause!** There is often no undo button.
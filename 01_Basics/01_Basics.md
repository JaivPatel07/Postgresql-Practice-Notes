# 🐘 01 - Database Fundamentals

Welcome to the start of your PostgreSQL journey! Before writing queries, let's understand the core concepts of databases.

---

## 🗄️ 1. What is a Database?

A **database** is an organized collection of data stored electronically. Think of it as a digital filing cabinet.

It allows you to:
*   **Store** data securely.
*   **Retrieve** specific information quickly.
*   **Update** records easily.
*   **Manage** huge amounts of data efficiently.

**Real-life Example:**
A **Pharmacy System** stores:
*   💊 Medicine Names
*   💰 Prices
*   📅 Expiry Dates
*   📦 Stock Quantity

---

## ⚙️ 2. DBMS vs. RDBMS

Software that manages databases is called a **DBMS** (Database Management System).

| Feature | DBMS (File System) | RDBMS (Relational) |
| :--- | :--- | :--- |
| **Full Form** | Database Management System | **Relational** Database Management System |
| **Structure** | Stores data as files. | Stores data in **Tables** (Rows & Columns). |
| **Relationships** | No relationship between data. | Tables are linked using **Keys**. |
| **Examples** | XML, File Systems | **PostgreSQL**, MySQL, SQL Server, Oracle |

> **Note:** PostgreSQL is an **RDBMS**. It stores data in tables and uses SQL (Structured Query Language).

---

## 🐘 3. Why PostgreSQL?

PostgreSQL (often called "Postgres") is one of the most advanced open-source databases in the world.

*   **Open Source:** Free to use.
*   **ACID Compliant:** Ensures data validity despite errors or power failures.
*   **Extensible:** You can write your own code to extend functionality.
*   **Standard SQL:** Follows strict SQL standards, making it great for learning.

---

## 🏗️ 4. Basic Terminology

Let's break down the structure of an RDBMS using a `students` table.

### 1. Table
A structured list of data.
*   **Example:** The entire grid below is the `students` table.

### 2. Column (Field)
A vertical category of data.
*   **Example:** `name`, `age` are columns.

### 3. Row (Record)
A horizontal entry representing one item.
*   **Example:** `1 | Ravi | 20` is one row.

| id (PK) | name | age |
| :--- | :--- | :--- |
| 1 | Ravi | 20 |
| 2 | Neha | 21 |

---

## 🔑 5. Keys: The "Relational" Part

Keys are special columns used to identify rows and link tables together.

### 🥇 Primary Key (PK)
*   **Uniquely identifies** every row in a table.
*   Cannot be `NULL` (empty).
*   Cannot have duplicates.
*   **Example:** `student_id` (Two students can have the name "Ravi", but they will have different IDs).

### 🔗 Foreign Key (FK)
*   Links two tables together.
*   It points to the **Primary Key** of another table.

**Example Relationship:**

**Table A: Students**
| student_id (PK) | name |
| :--- | :--- |
| 101 | Ravi |
| 102 | Neha |

**Table B: Orders**
| order_id | item | student_id (FK) |
| :--- | :--- | :--- |
| 1 | Laptop | 101 |
| 2 | Mouse | 102 |

> Here, `student_id` in the **Orders** table connects the order back to the student in the **Students** table.

---

## 🌍 6. Why do we need Databases?

Imagine managing a bank without a database.
*   ❌ **Spreadsheets:** Hard to manage millions of users.
*   ❌ **Security:** Anyone could delete a file.
*   ❌ **Speed:** Searching a text file takes forever.

**With a Database:**
*   ✅ **Organized:** Structured storage.
*   ✅ **Fast:** Find one record among millions in milliseconds.
*   ✅ **Secure:** Strict access rules.
*   ✅ **Scalable:** Can grow to petabytes of data.

---

## 🎯 Summary

1.  **Database**: Electronic data storage.
2.  **RDBMS**: Stores data in tables (Rows & Columns).
3.  **PostgreSQL**: A powerful, open-source RDBMS.
4.  **Primary Key**: Unique ID for a row.
5.  **Foreign Key**: Links tables together.
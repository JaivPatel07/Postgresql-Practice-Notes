# 01 - Database Basics

---

# 1. What is a Database?

A **database** is an organized collection of data stored electronically.

It allows users to:
- Store data
- Retrieve data
- Update data
- Delete data
- Manage large amounts of information efficiently

Example:
A pharmacy system storing:
- Medicine name
- Price
- Expiry date
- Stock quantity

---

# 2. What is DBMS?

DBMS (Database Management System) is software that manages databases.

It provides:
- Data storage
- Data security
- Data retrieval
- Backup & recovery
- Multi-user access

Examples of DBMS:
- MySQL
- PostgreSQL
- Oracle
- SQL Server

---

# 3. What is RDBMS?

RDBMS (Relational Database Management System) stores data in the form of tables.

Each table:
- Has rows (records)
- Has columns (attributes)
- Follows relational model
- Uses SQL for operations

PostgreSQL is an RDBMS.

---

# 4. What is PostgreSQL?

PostgreSQL is:
- Open-source
- Advanced RDBMS
- ACID compliant
- Highly extensible
- Supports SQL standards

It is widely used for:
- Web applications
- Backend systems
- Data engineering
- AI applications (with extensions like vector search)

---

# 5. Basic Terminology

## Table
A structured collection of related data.

Example: students table

| id | name  | age |
|----|-------|-----|
| 1  | Ravi  | 20  |
| 2  | Neha  | 21  |

---

## Row (Record)
A single entry in a table.

Example:
1 | Ravi | 20

---

## Column (Field)
A specific attribute of data.

Example:
name column stores student names.

---

## Primary Key

A column that:
- Uniquely identifies each row
- Cannot be NULL
- Cannot have duplicate values

Example:
id column in students table.

---

## Foreign Key

A column that:
- References primary key of another table
- Creates relationship between tables

Example:

students table:
id | name

orders table:
order_id | student_id

Here, student_id is a foreign key referencing students.id

---

# 6. Why Databases are Important in Real Applications

Without database:
- Data would be messy
- No security
- No relationships
- No performance optimization

With database:
- Organized storage
- Fast searching
- Data integrity
- Scalability

---

# Summary

Database → Stores data  
DBMS → Manages database  
RDBMS → Stores data in tables  
PostgreSQL → Advanced open-source RDBMS  
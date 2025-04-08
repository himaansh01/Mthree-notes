# SQL Learning Notes – 10-02-2025

## Introduction to SQL

Think of a wardrobe with different sections for clothes. SQL works similarly—it helps manage and organize data in a structured way.

### 🗂 Example Analogy:
- **Sections** = Tables (e.g., Shirts, Jeans)
- **Racks** = Columns (e.g., Color, Size, Type)

Want to find all pink shirts? Instead of manually searching:
```sql
SELECT * FROM Shirts WHERE Color = 'Pink';
```
SQL helps efficiently **store, retrieve, and manage data**.

---

## Understanding Tables and Rows

In SQL:
- **Table** = Group of related data (like all shirts)
- **Row** = One item (a specific shirt)
- **Column** = A property (color, size, etc.)

### Example Table: Shirts

| ID | Color | Size  | Type   |
|----|-------|-------|--------|
| 1  | Red   | Small | Casual |
| 2  | Blue  | Medium| Formal |
| 3  | Pink  | Large | Casual |

Query for pink shirts:
```sql
SELECT * FROM Shirts WHERE Color = 'Pink';
```

---

## 1. What is a Database?
A **database** is a structured way to store large amounts of information for easy access and management.

## 2. What is a DBMS?
A **Database Management System (DBMS)** is software used to manage and interact with databases.

## 3. Types of DBMS
- **Relational (RDBMS)** – Uses tables (e.g., MySQL, PostgreSQL)
- **NoSQL** – Uses key-value, documents, or graphs (e.g., MongoDB)

---

## 4. Example Query

Retrieve pink shirts from a large collection:
```sql
SELECT * FROM supboard WHERE color = 'pink';
```

---

## 5. Creating a Table

```sql
CREATE TABLE supboard (
    id INT PRIMARY KEY,
    type VARCHAR(50),
    color VARCHAR(20),
    rack_number INT
);
```

---

## 6. Installing MySQL Workbench

1. Go to the [MySQL Workbench installation guide](https://www.geeksforgeeks.org/how-to-install-sql-workbench-for-mysql-on-windows/)
2. Download and install.
3. Connect and start writing SQL queries.

---

## 7. DDL (Data Definition Language)

- **Create Table**
```sql
CREATE TABLE employees (id INT, name VARCHAR(50), salary INT);
```

- **Alter Table**
```sql
ALTER TABLE employees ADD COLUMN department VARCHAR(50);
```

- **Drop Table**
```sql
DROP TABLE employees;
```

---

## 8. DML (Data Manipulation Language)

- **Insert**
```sql
INSERT INTO employees (id, name, salary) VALUES (1, 'John', 50000);
```

- **Update**
```sql
UPDATE employees SET salary = 55000 WHERE id = 1;
```

- **Delete**
```sql
DELETE FROM employees WHERE id = 1;
```

---

## 9. DELETE vs. TRUNCATE

| Feature               | DELETE       | TRUNCATE    |
|-----------------------|--------------|-------------|
| Removes specific rows?| ✅ Yes       | ❌ No        |
| Supports rollback?    | ✅ Yes       | ❌ No        |
| Performance           | Slower       | Faster      |

---

## 10. Cloning Tables

- **Deep Copy** (Structure + Data)
```sql
CREATE TABLE new_table AS SELECT * FROM old_table;
```

- **Shallow Copy** (Only Structure)
```sql
CREATE TABLE new_table LIKE old_table;
```

---

## 11. Describe Table

```sql
DESC employees;
```

---

## 12. Temporary Tables

Used within a session; deleted automatically after.
```sql
CREATE TEMPORARY TABLE temp_table AS SELECT * FROM employees;
```

---

## 13. Views

A **view** is a virtual table created from a query:
```sql
CREATE VIEW high_salary AS
SELECT * FROM employees WHERE salary > 60000;
```

---

## 14. CHAR vs. VARCHAR

| Feature   | CHAR        | VARCHAR     |
|-----------|-------------|-------------|
| Storage   | Fixed length| Variable    |
| Speed     | Faster      | Slower      |
| Padding   | Adds spaces | No padding  |

---

## 15. SQL Clauses

- **ORDER BY**
```sql
SELECT * FROM employees ORDER BY salary DESC;
```

- **HAVING**
```sql
SELECT department, COUNT(*) 
FROM employees 
GROUP BY department 
HAVING COUNT(*) > 5;
```

- **WHERE**
```sql
SELECT * FROM employees WHERE salary > 50000;
```

- **LIMIT**
```sql
SELECT * FROM employees LIMIT 5;
```

- **DISTINCT**
```sql
SELECT DISTINCT department FROM employees;
```

---

## 16. Constraints

- **Primary Key**
```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    salary INT
);
```

- **UNIQUE**
```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

- **NOT NULL**
```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL
);
```

---

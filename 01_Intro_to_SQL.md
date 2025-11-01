# 🧠 Introduction to SQL (Structured Query Language)

## 🔹 What is SQL?
SQL (Structured Query Language) is a **standard language** used to store, manipulate, and retrieve data from **Relational Database Management Systems (RDBMS)** such as Oracle, MySQL, PostgreSQL, SQL Server, etc.

It allows you to:
- Create and manage database structures.
- Insert, update, delete, and query data.
- Control access and manage transactions.

---

## 🔹 History & Standards
| Year | Event |
|------|--------|
| 1970 | Dr. E. F. Codd introduced the relational model. |
| 1974 | First SQL version developed by IBM (called SEQUEL). |
| 1986 | ANSI standardized SQL. |
| 1989–1999 | SQL enhancements like joins, triggers, procedures, and recursive queries. |

---

## 🔹 What is an RDBMS?
**RDBMS (Relational Database Management System)** stores data in tables (rows and columns) and enforces relationships among them using keys.

**Examples:** Oracle, MySQL, PostgreSQL, MS SQL Server, SQLite.

**Key Features:**
- Data stored in tabular form  
- Data integrity through keys and constraints  
- SQL support for querying and transaction management  

---

## 🔹 SQL Language Categories

| Category | Description | Examples |
|-----------|--------------|-----------|
| **DDL** (Data Definition Language) | Defines database structure | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` |
| **DML** (Data Manipulation Language) | Manipulates data in tables | `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `MERGE` |
| **DCL** (Data Control Language) | Controls user access | `GRANT`, `REVOKE` |
| **TCL** (Transaction Control Language) | Manages transactions | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

---

## 🔹 SQL Syntax Overview
Every SQL command follows this general pattern:

```sql
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column_name;
````

* **SQL keywords** are *not case-sensitive* (`SELECT` = `select`).
* **Semicolon (;)** ends a statement.
* **Comments**:

  ```sql
  -- This is a single-line comment
  /* This is a
     multi-line comment */
  ```

---

## 🔹 SQL Table Structure

A **table** is made up of:

* **Columns (fields):** Define data types (e.g., `VARCHAR2`, `NUMBER`, `DATE`)
* **Rows (records):** Actual data values

**Example:**

| emp_id | emp_name | dept | salary |
| ------ | -------- | ---- | ------ |
| 101    | Ramesh   | HR   | 45000  |
| 102    | Sneha    | IT   | 55000  |

---

## 🔹 Basic Example — Creating and Querying Data

### Step 1: Create a Table

```sql
CREATE TABLE employees (
  emp_id NUMBER PRIMARY KEY,
  emp_name VARCHAR2(100),
  dept VARCHAR2(50),
  salary NUMBER(10,2)
);
```

### Step 2: Insert Data

```sql
INSERT INTO employees (emp_id, emp_name, dept, salary)
VALUES (101, 'Ramesh', 'HR', 45000);

INSERT INTO employees VALUES (102, 'Sneha', 'IT', 55000);
```

### Step 3: Query Data

```sql
SELECT emp_name, salary
FROM employees
WHERE dept = 'IT';
```

**Output:**

| emp_name | salary |
| -------- | ------ |
| Sneha    | 55000  |

---

## 🔹 Understanding Keys and Constraints

| Constraint      | Description                       | Example                                   |
| --------------- | --------------------------------- | ----------------------------------------- |
| **PRIMARY KEY** | Unique identifier for each record | `emp_id NUMBER PRIMARY KEY`               |
| **FOREIGN KEY** | Links records between tables      | `dept_id REFERENCES departments(dept_id)` |
| **UNIQUE**      | No duplicate values allowed       | `email VARCHAR2(100) UNIQUE`              |
| **NOT NULL**    | Field must have a value           | `name VARCHAR2(50) NOT NULL`              |
| **CHECK**       | Restricts column values           | `salary NUMBER CHECK(salary > 0)`         |
| **DEFAULT**     | Provides a default value          | `status VARCHAR2(10) DEFAULT 'ACTIVE'`    |

---

## 🔹 Real-world Example — Employee & Department Tables

```sql
CREATE TABLE departments (
  dept_id NUMBER PRIMARY KEY,
  dept_name VARCHAR2(50)
);

CREATE TABLE employees (
  emp_id NUMBER PRIMARY KEY,
  emp_name VARCHAR2(100) NOT NULL,
  dept_id NUMBER,
  salary NUMBER(10,2),
  FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);

INSERT INTO departments VALUES (1, 'HR');
INSERT INTO departments VALUES (2, 'IT');

INSERT INTO employees VALUES (101, 'Ramesh', 1, 45000);
INSERT INTO employees VALUES (102, 'Sneha', 2, 55000);
INSERT INTO employees VALUES (103, 'Ravi', 2, 60000);

SELECT e.emp_name, d.dept_name, e.salary
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id;
```

**Output:**

| emp_name | dept_name | salary |
| -------- | --------- | ------ |
| Ramesh   | HR        | 45000  |
| Sneha    | IT        | 55000  |
| Ravi     | IT        | 60000  |

---

## 🔹 Common Mistakes

❌ Using string literals without quotes
✅ `'string_value'` not `string_value`

❌ Forgetting `WHERE` in an `UPDATE` or `DELETE`
✅ Always test with `SELECT` first before modifying rows

❌ Using `SELECT *` unnecessarily
✅ Always specify required columns for better performance

---

## 🔹 Practice Questions

1. Create a table `students` with columns: `id`, `name`, `age`, `grade`.
2. Insert at least 3 records into the table.
3. Write a query to display all students aged above 18.
4. Add a new column `city` to the table.
5. Delete all students whose grade is less than 40.

---

## 🔹 Summary

✅ SQL is the backbone of data management in relational databases.
✅ You can define, manipulate, control, and secure data using various SQL commands.
✅ Always practice with examples to build confidence.

---

## 🔹 Next Topic

👉 **[Data Types in SQL](./02_Data_Types.md)**
Learn about different data types like `NUMBER`, `VARCHAR2`, `DATE`, and how they are used efficiently.

---

**🧾 Author:** Sapna Usare
**📁 Topic:** SQL Basics
**📘 Repository:** SQL & PL/SQL Notes
**📅 Last Updated:** {{CURRENT_DATE}}

# 📘 01 — Introduction to SQL (Oracle Database)

[← Back to README](../README.md) | [Next → 02_Data_Types.md](./02_Data_Types.md)

---

## 🏁 What is SQL?

**SQL (Structured Query Language)** is the standard language used to **store, retrieve, and manipulate data** in a **Relational Database Management System (RDBMS)**.  
In Oracle Database, SQL is used to communicate with the database engine to perform all data-related operations.

Oracle’s SQL engine is ANSI-compliant but includes **Oracle-specific features** such as:
- The `DUAL` table  
- Pseudocolumns (`ROWNUM`, `ROWID`)  
- Oracle data types (`VARCHAR2`, `NUMBER`, `DATE`, etc.)  
- SQL functions (`NVL`, `DECODE`, `SYSDATE`, etc.)

---

## ⚙️ How SQL Works in Oracle

When you execute a SQL statement in Oracle, it goes through three main phases:

1. **Parsing** – Oracle checks the SQL syntax and validates object names in the data dictionary.  
2. **Execution** – The SQL engine executes the parsed statement.  
3. **Fetching** – The results are returned to the user or program.

---

## 💡 Key Features of SQL

- SQL is **non-procedural** — you describe *what* data to retrieve, not *how* to retrieve it.  
- It supports operations on **one or more tables** simultaneously.  
- It can **define**, **manipulate**, **control**, and **query** data.  
- SQL commands are **not case-sensitive** (though data values are).

---

## 🧩 SQL Command Categories in Oracle

| Category | Description | Common Commands |
|-----------|--------------|-----------------|
| **DDL (Data Definition Language)** | Defines the structure of database objects | `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` |
| **DML (Data Manipulation Language)** | Modifies data inside tables | `INSERT`, `UPDATE`, `DELETE`, `MERGE` |
| **DCL (Data Control Language)** | Controls access permissions | `GRANT`, `REVOKE` |
| **TCL (Transaction Control Language)** | Manages transactions | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |
| **DQL (Data Query Language)** | Retrieves data from the database | `SELECT` |

---

## 🗂️ Common SQL Objects in Oracle

| Object | Description |
|---------|--------------|
| **Table** | Stores data in rows and columns |
| **View** | Logical view of one or more tables |
| **Sequence** | Generates unique numeric values |
| **Synonym** | Alias name for a table, view, or sequence |
| **Index** | Improves query performance |
| **Schema** | Logical collection of database objects owned by a user |

---

## 🧮 Basic SQL Example

```sql
SELECT first_name, last_name, salary
FROM employees
WHERE department_id = 10;
````

This retrieves employee details from the `EMPLOYEES` table whose department ID is 10.

---

## 🧱 Using the DUAL Table in Oracle

The **`DUAL` table** is a special **one-row, one-column** table present in all Oracle databases.
It is used to **evaluate expressions, functions, or pseudo-columns**.

```sql
SELECT SYSDATE AS current_date FROM dual;
SELECT 10 + 20 AS sum_result FROM dual;
```

**Output:**

```
CURRENT_DATE
-------------
01-NOV-25

SUM_RESULT
-----------
30
```

---

## 🧭 SQL vs PL/SQL

| Feature   | SQL                        | PL/SQL                                      |
| --------- | -------------------------- | ------------------------------------------- |
| Type      | Declarative Language       | Procedural Language                         |
| Execution | One statement at a time    | Block of statements                         |
| Usage     | Query and manipulate data  | Write logic, loops, conditions              |
| Example   | `SELECT * FROM employees;` | `BEGIN DBMS_OUTPUT.PUT_LINE('Hello'); END;` |

---

## 🖥️ Running SQL in Oracle SQL Developer

1. Open **Oracle SQL Developer**.
2. Click ➕ to **create a new connection**:

   * Username: `system` or your schema user
   * Password: your password
   * Connection type: `Basic`
3. Click **Test** → **Connect**.
4. Open a new SQL Worksheet (`Ctrl + Shift + N`).
5. Type and execute your SQL command (`Ctrl + Enter`).

---

## 🧠 Practice Exercises

1. Display the system date using the `DUAL` table.
2. Write a query to display all employees whose salary is greater than 5000.
3. Show all department names from the `DEPARTMENTS` table.
4. Display your name and current date using a single SQL query.

---

## 🏁 Summary

* SQL is the foundation of Oracle Database operations.
* It includes DDL, DML, DCL, TCL, and DQL commands.
* The `DUAL` table and `SYSDATE` function are unique Oracle features.
* SQL Developer is a popular tool to run and test your SQL scripts.

---

## 🔗 Next Steps

👉 Continue to the next file to learn about **Oracle SQL Data Types**:
**[02_Data_Types.md →](./02_Data_Types.md)**

---

*Created by [Sapna Usare](https://github.com/sapna-usare) — Oracle SQL & PL/SQL Learning Repository* 💾
# 📘 03 — DDL (Data Definition Language) in Oracle

[← Back to 02_Data_Types.md](./02_Data_Types.md) | [Next → 04_DML_Commands.md](./04_DML_Commands.md)

---

## 🧩 Introduction

**DDL (Data Definition Language)** statements are used to **define, modify, or remove** database objects such as tables, views, sequences, indexes, and synonyms.

In Oracle, when a DDL command is executed:
- It performs an **auto-commit** (cannot be rolled back).
- It **changes the structure**, not the data.
- Examples include:  
  - `CREATE`  
  - `ALTER`  
  - `DROP`  
  - `TRUNCATE`  
  - `RENAME`

---

## 🧱 1. CREATE Command

Used to **create** new database objects like tables, views, or sequences.

### 🟢 a) Creating a Table

```sql
CREATE TABLE employees (
    emp_id        NUMBER(5)      PRIMARY KEY,
    emp_name      VARCHAR2(50)   NOT NULL,
    job_title     VARCHAR2(30),
    salary        NUMBER(8,2),
    hire_date     DATE DEFAULT SYSDATE,
    dept_id       NUMBER(4)
);
````

✅ **Explanation:**

* `emp_id` is a **primary key**.
* `salary` allows 8 digits with 2 after the decimal.
* `hire_date` defaults to current date.
* `dept_id` references another table (can later add a foreign key).

---

### 🟢 b) Creating a Table Using Subquery

Copies structure and data from another table.

```sql
CREATE TABLE sales_backup AS
SELECT * FROM sales;
```

To copy only structure (no data):

```sql
CREATE TABLE sales_structure AS
SELECT * FROM sales WHERE 1=2;
```

---

### 🟢 c) Creating Other Objects

#### i. Creating a Sequence

Generates sequential numeric values (e.g., employee IDs).

```sql
CREATE SEQUENCE emp_seq
START WITH 100
INCREMENT BY 1
NOCACHE
NOCYCLE;
```

#### ii. Creating a View

```sql
CREATE VIEW emp_view AS
SELECT emp_name, salary FROM employees WHERE salary > 5000;
```

#### iii. Creating a Synonym

```sql
CREATE SYNONYM emp FOR employees;
```

---

## ⚙️ 2. ALTER Command

Used to **modify** the structure of an existing object.

### 🟡 a) Add a New Column

```sql
ALTER TABLE employees
ADD email VARCHAR2(100);
```

### 🟡 b) Modify Column Data Type or Size

```sql
ALTER TABLE employees
MODIFY emp_name VARCHAR2(100);
```

### 🟡 c) Rename a Column

```sql
ALTER TABLE employees
RENAME COLUMN job_title TO designation;
```

### 🟡 d) Drop a Column

```sql
ALTER TABLE employees
DROP COLUMN dept_id;
```

### 🟡 e) Add or Drop Constraints

```sql
ALTER TABLE employees
ADD CONSTRAINT fk_dept FOREIGN KEY (dept_id) REFERENCES departments(department_id);

ALTER TABLE employees
DROP CONSTRAINT fk_dept;
```

---

## ❌ 3. DROP Command

Used to **remove** database objects permanently.

```sql
DROP TABLE employees;
DROP VIEW emp_view;
DROP SEQUENCE emp_seq;
DROP SYNONYM emp;
```

⚠️ **Note:** Once dropped, data and structure are permanently deleted.

---

## 🧹 4. TRUNCATE Command

Removes **all rows** from a table but keeps its structure.

```sql
TRUNCATE TABLE employees;
```

🧠 **Key Points:**

* Faster than `DELETE`.
* Cannot use `WHERE` clause.
* Auto-committed.
* Cannot be rolled back.

---

## 🔁 5. RENAME Command

Used to **rename** a table or any schema object.

```sql
RENAME employees TO emp_master;
```

---

## 🧾 6. Viewing Metadata in Oracle

Oracle provides system views to check objects and structures.

| View Name          | Description                           |
| ------------------ | ------------------------------------- |
| `USER_TABLES`      | Lists tables owned by the user        |
| `USER_TAB_COLUMNS` | Shows columns and data types          |
| `USER_CONSTRAINTS` | Displays table constraints            |
| `USER_OBJECTS`     | Lists all objects created by the user |

```sql
SELECT table_name FROM user_tables;
SELECT column_name, data_type FROM user_tab_columns WHERE table_name = 'EMPLOYEES';
```

---

## ⚖️ 7. DROP vs TRUNCATE vs DELETE

| Feature               | DROP  | TRUNCATE | DELETE                 |
| --------------------- | ----- | -------- | ---------------------- |
| Removes Structure?    | ✅ Yes | ❌ No     | ❌ No                   |
| Removes Data?         | ✅ Yes | ✅ Yes    | ✅ Yes (with condition) |
| Rollback Possible?    | ❌ No  | ❌ No     | ✅ Yes                  |
| Auto-commit?          | ✅ Yes | ✅ Yes    | ❌ No                   |
| WHERE Clause Allowed? | ❌ No  | ❌ No     | ✅ Yes                  |

---

## 🧠 Practice Exercises

1. Create a table `department` with columns:

   * `dept_id` NUMBER(5)
   * `dept_name` VARCHAR2(30)
   * `location` VARCHAR2(30)

2. Add a column `manager_id` later.

3. Modify `dept_name` to `VARCHAR2(50)`.

4. Rename the table to `departments_master`.

5. Truncate all data from `departments_master`.

6. Drop the table completely.

7. Create a sequence and use it in an `INSERT` statement.

---

## 🏁 Summary

* **DDL** commands define and modify database structure.
* Every DDL operation is **auto-committed**.
* Major DDL commands: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, and `RENAME`.
* Use system views (`USER_TABLES`, `USER_OBJECTS`) to verify your objects.
* Use caution with `DROP` and `TRUNCATE` — both are irreversible.

---

## 🔗 Next Steps

👉 Continue to the next file to learn about **Oracle DML (Data Manipulation Language)** commands:
**[04_DML_Commands.md →](./04_DML_Commands.md)**

---

*Created by [Sapna Usare](https://github.com/sapna-usare) — Oracle SQL & PL/SQL Learning Repository* 💾
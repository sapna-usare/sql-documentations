# 📘 02 — Oracle SQL Data Types

[← Back to 01_Intro_to_SQL.md](./01_Intro_to_SQL.md) | [Next → 03_DDL_Commands.md](./03_DDL_Commands.md)

---

## 🧩 Introduction

Every column in an Oracle database table is assigned a **data type**, which defines the kind of values that can be stored in it (numbers, text, dates, etc.).  
Oracle provides a rich set of **built-in data types** to handle different kinds of data efficiently.

---

## 🗃️ Categories of Data Types in Oracle

| Category | Description | Example Data Types |
|-----------|--------------|--------------------|
| **Character / String** | Stores text data | `CHAR`, `VARCHAR2`, `NCHAR`, `NVARCHAR2`, `CLOB`, `NCLOB` |
| **Numeric** | Stores numeric values | `NUMBER`, `FLOAT`, `BINARY_FLOAT`, `BINARY_DOUBLE` |
| **Date/Time** | Stores date and time values | `DATE`, `TIMESTAMP`, `INTERVAL YEAR TO MONTH`, `INTERVAL DAY TO SECOND` |
| **Large Objects (LOBs)** | Stores large data such as text, images, or files | `BLOB`, `CLOB`, `BFILE`, `NCLOB` |
| **RAW / LONG** | Stores raw binary data | `RAW`, `LONG`, `LONG RAW` |

---

## 🧾 1. Character Data Types

### 🟢 **CHAR(size)**
- Fixed-length character data type.  
- Maximum size: **2000 bytes**.  
- If actual data is smaller, Oracle **pads** spaces to the right.

```sql
CREATE TABLE demo_char (
    code CHAR(5)
);

INSERT INTO demo_char VALUES ('A');
-- 'A    ' → Stored with trailing spaces
````

---

### 🟢 **VARCHAR2(size)**

* Variable-length character data type.
* Maximum size: **4000 bytes**.
* Recommended over `CHAR` for most use cases.

```sql
CREATE TABLE demo_varchar2 (
    name VARCHAR2(50)
);

INSERT INTO demo_varchar2 VALUES ('Sapna Usare');
```

🧠 **Note:**
Oracle recommends **`VARCHAR2`** instead of `VARCHAR`.
The `VARCHAR` type is accepted but treated internally as `VARCHAR2`.

---

### 🟢 **NCHAR(size)** and **NVARCHAR2(size)**

* Used for storing **Unicode (national character set)** data.
* Supports multilingual data (e.g., Hindi, Telugu, etc.).

```sql
CREATE TABLE demo_nchar (
    lang_text NVARCHAR2(50)
);
```

---

### 🟢 **CLOB / NCLOB**

* **Character Large Object** types.
* Used for large text data (up to 4 GB).
* `NCLOB` supports Unicode.

```sql
CREATE TABLE demo_clob (
    content CLOB
);
```

---

## 🔢 2. Numeric Data Types

### 🟣 **NUMBER(p,s)**

* Stores **fixed or floating-point numbers**.
* `p` → precision (total digits), `s` → scale (digits after decimal).
* Default precision: up to 38 digits.

```sql
CREATE TABLE demo_number (
    salary NUMBER(8,2)
);

INSERT INTO demo_number VALUES (45678.99);
```

### 🟣 **FLOAT(p)**

* Stores approximate numeric values.
* Equivalent to `NUMBER` but allows floating-point representation.

```sql
CREATE TABLE demo_float (
    value FLOAT(10)
);
```

### 🟣 **BINARY_FLOAT / BINARY_DOUBLE**

* Store **floating-point numbers** using binary precision.
* Faster mathematical computation but less exact for monetary data.

```sql
CREATE TABLE demo_binary (
    speed BINARY_DOUBLE
);
```

---

## 📅 3. Date and Time Data Types

### 🟠 **DATE**

* Stores both **date and time** up to seconds.
* Format: `DD-MON-YY` or `DD-MON-RR`.
* Default display format: `DD-MON-RR`.

```sql
CREATE TABLE demo_date (
    hire_date DATE
);

INSERT INTO demo_date VALUES (SYSDATE);
```

### 🟠 **TIMESTAMP**

* Stores date and time **including fractional seconds**.

```sql
CREATE TABLE demo_timestamp (
    event_time TIMESTAMP
);
```

### 🟠 **INTERVAL YEAR TO MONTH / DAY TO SECOND**

* Used for **time duration** calculations.

```sql
SELECT TO_DATE('2024-01-01','YYYY-MM-DD') + INTERVAL '2' MONTH AS result FROM dual;
```

---

## 🧱 4. Large Object (LOB) Data Types

| Type      | Description                                    |
| --------- | ---------------------------------------------- |
| **CLOB**  | Character Large Object (up to 4GB of text)     |
| **BLOB**  | Binary Large Object (up to 4GB of binary data) |
| **NCLOB** | National character LOB (Unicode)               |
| **BFILE** | External binary file stored outside database   |

```sql
CREATE TABLE demo_lob (
    doc_id NUMBER,
    doc_file BLOB
);
```

---

## ⚙️ 5. RAW and LONG Data Types

* **RAW(size)** → Stores binary or byte data (max 2000 bytes).
* **LONG / LONG RAW** → Legacy types (max 2 GB).

  > 🔸 *Avoid using `LONG`; use LOBs instead.*

```sql
CREATE TABLE demo_raw (
    image RAW(100)
);
```

---

## 🔁 6. Data Type Conversion Functions

Oracle provides built-in functions to convert between data types.

| Function      | Purpose                           | Example                              |
| ------------- | --------------------------------- | ------------------------------------ |
| `TO_CHAR()`   | Converts date/number to character | `TO_CHAR(SYSDATE, 'DD-MON-YYYY')`    |
| `TO_DATE()`   | Converts string to date           | `TO_DATE('01-11-2025','DD-MM-YYYY')` |
| `TO_NUMBER()` | Converts string to number         | `TO_NUMBER('12345')`                 |

---

## ⚖️ 7. CHAR vs VARCHAR2

| Feature         | CHAR                           | VARCHAR2                         |
| --------------- | ------------------------------ | -------------------------------- |
| Storage         | Fixed-length                   | Variable-length                  |
| Performance     | Slightly faster for fixed data | More efficient for varying sizes |
| Padding         | Adds spaces automatically      | No padding                       |
| Recommended for | Fixed-size codes               | Names, addresses, etc.           |

---

## 🧠 Practice Exercises

1. Create a table `student_info` with the following columns:

   * `roll_no` (NUMBER)
   * `name` (VARCHAR2(50))
   * `dob` (DATE)
   * `grade` (CHAR(1))

2. Insert 3 sample rows using `SYSDATE` for date.

3. Display the date in format: `DD-MON-YYYY`.

4. Create another table using a `CLOB` column to store remarks.

5. Try using `TO_CHAR` and `TO_DATE` functions in queries.

---

## 🏁 Summary

* Oracle supports rich data types for text, numbers, dates, and binary data.
* Use `VARCHAR2` for variable-length strings and `NUMBER` for numeric data.
* Use `CLOB`/`BLOB` for large data storage.
* Conversion functions (`TO_CHAR`, `TO_DATE`, `TO_NUMBER`) help switch between types.

---

## 🔗 Next Steps

👉 Continue to the next file to learn about **Oracle DDL (Data Definition Language)** commands:
**[03_DDL_Commands.md →](./03_DDL_Commands.md)**

---

*Created by [Sapna Usare](https://github.com/sapna-usare) — Oracle SQL & PL/SQL Learning Repository* 💾
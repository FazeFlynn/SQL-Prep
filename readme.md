# SQl P

### 1. **Introduction to SQL**
- **What is SQL?**  
  Structured Query Language (SQL) is a standard language used to interact with databases, enabling tasks such as creating databases, retrieving data, updating records, etc.

- **What is a Database?**  
  A structured data storage system that includes schemas, tables, queries, views, etc.

- **Does SQL Support Programming?**  
  SQL is a command language, not a programming language. It lacks constructs like loops and conditional statements.

---

### 2. **SQL Data Types**
- **CHAR vs. VARCHAR2**  
  - `CHAR`: Fixed-length storage. Example: `CHAR(5)` always stores exactly 5 characters.  
  - `VARCHAR2`: Variable-length storage. Example: `VARCHAR2(5)` stores up to 5 characters.

---

### 3. **SQL Commands**
- **Data Definition Language (DDL):** Includes `CREATE`, `DROP`, `ALTER`.  
- **Data Manipulation Language (DML):** Includes `INSERT`, `DELETE`, `SELECT`, `UPDATE`.

---

### 4. **Views in SQL**
- **Definition:** A virtual table based on a result-set of an SQL query.  
- **Syntax:**
  ```sql
  CREATE VIEW view_name AS
  SELECT column1, column2 
  FROM table_name
  WHERE condition;
  ```

---

### 5. **Keys in SQL**
- **Primary Key:** Uniquely identifies each row in a table.  
- **Foreign Key:** Links two tables, referencing the primary key in another table.

---

### 6. **Constraints**
- **Default Constraint:** Sets a default value for a column if no value is provided.  
- **Data Integrity:** Ensures correctness and consistency of data in a database.

---

### 7. **Normalization and Denormalization**
- **Normalization:** Reduces redundancy and anomalies.  
- **Denormalization:** Optimizes performance by adding redundancy.

---

### 8. **Functions in SQL**
- **Aggregate Functions:** Includes `SUM`, `AVG`, `COUNT`, `MIN`, `MAX`.  
- **Scalar Functions:** Operates on single values, e.g., `UPPER`, `LOWER`, `INITCAP`.

---

### 9. **Joins in SQL**
- **Types of Joins:**
  - `INNER JOIN`: Returns rows with matching values in both tables.
  - `LEFT JOIN`: Includes all rows from the left table.
  - `RIGHT JOIN`: Includes all rows from the right table.
  - `FULL JOIN`: Combines results of `LEFT` and `RIGHT JOIN`.

---

### 10. **Indexes**
- **Definition:** A structure to enhance query performance.  
- **Attributes:** Access time, insertion time, deletion time, space overhead.

---

### 11. **Advanced Features**
- **Triggers:** Automatically executes a specified action when a database event occurs.  
- **Stored Procedures:** Precompiled SQL statements executed as a single unit.  
- **User-Defined Functions (UDFs):** Custom functions for specific operations.

---

### 12. **Transactions**
- **ACID Properties:** Atomicity, Consistency, Isolation, Durability.  
- **Commands:**  
  - `COMMIT`: Saves all changes.  
  - `ROLLBACK`: Reverts changes to a previous state.

---

### 13. **Operators**
- **Types:**
  - Arithmetic Operators: `+`, `-`, `*`, `/`.  
  - Logical Operators: `AND`, `OR`, `NOT`.  
  - Comparison Operators: `=`, `>`, `<`, `>=`, `<=`.

---

### 14. **SQL Security**
- **SQL Injection:** A hacking technique that exploits vulnerabilities in SQL queries.

---


$$
\text{End Of File}
$$
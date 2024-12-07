# SQL Prac

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
---
---

## Problem Statements

Here’s a collection of SQL problem statements with their solutions, covering concepts from basic to advanced. Each query is explained concisely to help you understand the logic.

---

### **1. Basic SQL Queries**
#### Problem: Retrieve all data from the `Employees` table.
**Query:**
```sql
SELECT * FROM Employees;
```
- Retrieves all rows and columns from the table.

#### Problem: Select employees whose salary is greater than 50,000.
**Query:**
```sql
SELECT EmployeeID, Name, Salary 
FROM Employees 
WHERE Salary > 50000;
```
- Filters rows where the `Salary` column value is greater than 50,000.

---

### **2. Filtering and Sorting**
#### Problem: Find employees whose name starts with 'A' and sort them by salary in descending order.
**Query:**
```sql
SELECT Name, Salary 
FROM Employees 
WHERE Name LIKE 'A%' 
ORDER BY Salary DESC;
```
- The `LIKE` operator filters rows with names starting with 'A'.  
- `ORDER BY DESC` sorts results in descending order.

---

### **3. Aggregations**
#### Problem: Find the total salary paid to employees in each department.
**Query:**
```sql
SELECT DepartmentID, SUM(Salary) AS TotalSalary 
FROM Employees 
GROUP BY DepartmentID;
```
- `GROUP BY` groups data by `DepartmentID`.  
- `SUM(Salary)` calculates the total salary for each group.

#### Problem: Find the maximum salary in the company.
**Query:**
```sql
SELECT MAX(Salary) AS MaxSalary 
FROM Employees;
```
- `MAX(Salary)` retrieves the highest salary value.

---

### **4. Joins**
#### Problem: Retrieve employee names along with their department names.
**Tables:**
- `Employees(EmployeeID, Name, DepartmentID)`
- `Departments(DepartmentID, DepartmentName)`

**Query:**
```sql
SELECT E.Name, D.DepartmentName 
FROM Employees E 
INNER JOIN Departments D 
ON E.DepartmentID = D.DepartmentID;
```
- Combines `Employees` and `Departments` using `INNER JOIN` based on `DepartmentID`.

---

### **5. Subqueries**
#### Problem: Find employees earning more than the average salary.
**Query:**
```sql
SELECT Name, Salary 
FROM Employees 
WHERE Salary > (SELECT AVG(Salary) FROM Employees);
```
- Subquery calculates the average salary.  
- Outer query filters employees with a salary above the calculated average.

---

### **6. Set Operations**
#### Problem: Find employees who work in either the HR or IT departments.
**Query:**
```sql
SELECT Name 
FROM Employees 
WHERE DepartmentID IN (SELECT DepartmentID FROM Departments WHERE DepartmentName IN ('HR', 'IT'));
```
- Subquery retrieves `DepartmentID` for 'HR' and 'IT'.  
- Outer query selects employees belonging to these departments.

---

### **7. Window Functions**
#### Problem: Rank employees based on their salary within each department.
**Query:**
```sql
SELECT Name, DepartmentID, Salary, 
       RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS Rank
FROM Employees;
```
- `RANK()` assigns a rank to employees based on salary.  
- `PARTITION BY` groups data by `DepartmentID`.

---

### **8. Advanced Features**
#### Problem: Create a view to list employees and their department names.
**Query:**
```sql
CREATE VIEW EmployeeDepartments AS
SELECT E.Name, D.DepartmentName 
FROM Employees E 
INNER JOIN Departments D 
ON E.DepartmentID = D.DepartmentID;
```
- Creates a virtual table to simplify future queries.

---

### **9. Data Manipulation**
#### Problem: Insert a new employee record into the `Employees` table.
**Query:**
```sql
INSERT INTO Employees (EmployeeID, Name, Salary, DepartmentID) 
VALUES (101, 'John Doe', 75000, 2);
```
- Adds a new row to the `Employees` table.

#### Problem: Update the salary of an employee with ID = 101.
**Query:**
```sql
UPDATE Employees 
SET Salary = 80000 
WHERE EmployeeID = 101;
```
- Modifies the salary for the specified employee.

#### Problem: Delete employees with a salary below 30,000.
**Query:**
```sql
DELETE FROM Employees 
WHERE Salary < 30000;
```
- Removes rows where the condition is met.

---

### **10. Transactions**
#### Problem: Commit a transaction to increase all salaries by 10%.
**Query:**
```sql
BEGIN TRANSACTION;
UPDATE Employees 
SET Salary = Salary * 1.10;
COMMIT;
```
- Begins a transaction, updates salaries, and saves the changes.

#### Problem: Roll back a transaction if an error occurs.
**Query:**
```sql
BEGIN TRANSACTION;
UPDATE Employees 
SET Salary = Salary * 1.10;
ROLLBACK;
```
- Reverts changes if the transaction fails.

---

### **11. Handling Null Values**
#### Problem: Replace null salaries with a default value of 40,000.
**Query:**
```sql
SELECT Name, COALESCE(Salary, 40000) AS Salary 
FROM Employees;
```
- `COALESCE` replaces null values with 40,000.

---

### **12. Recursive Queries**
#### Problem: Find the management hierarchy starting from a specific employee.
**Query:**
```sql
WITH RECURSIVE EmployeeHierarchy AS (
    SELECT EmployeeID, ManagerID, Name 
    FROM Employees 
    WHERE EmployeeID = 1
    UNION ALL
    SELECT E.EmployeeID, E.ManagerID, E.Name 
    FROM Employees E 
    INNER JOIN EmployeeHierarchy EH 
    ON E.ManagerID = EH.EmployeeID
)
SELECT * FROM EmployeeHierarchy;
```
- Recursively retrieves employees and their managers.

---

### **13. Indexing**
#### Problem: Create an index on the `Salary` column for faster searches.
**Query:**
```sql
CREATE INDEX idx_salary ON Employees(Salary);
```
- Speeds up queries filtering by `Salary`.









---

$$
\text{End Of File}
$$
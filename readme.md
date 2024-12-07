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


## Complex Problem Statements

Here are some complex SQL queries designed to help sharpen your SQL skills. These queries cover advanced concepts such as subqueries, joins, window functions, recursive queries, and aggregation.

---

### **1. Find the Second Highest Salary in a Table**
**Problem:** Retrieve the second-highest salary from the `Employees` table.

**Query:**
```sql
SELECT MAX(Salary) AS SecondHighestSalary
FROM Employees
WHERE Salary < (SELECT MAX(Salary) FROM Employees);
```
**Explanation:**  
- The inner query finds the maximum salary.  
- The outer query retrieves the highest salary below the maximum.

---

### **2. Find Departments with More Than 5 Employees**
**Problem:** List department names where more than 5 employees work.

**Query:**
```sql
SELECT D.DepartmentName, COUNT(E.EmployeeID) AS EmployeeCount
FROM Employees E
JOIN Departments D ON E.DepartmentID = D.DepartmentID
GROUP BY D.DepartmentName
HAVING COUNT(E.EmployeeID) > 5;
```
**Explanation:**  
- `JOIN` links employees to their departments.  
- `GROUP BY` groups by department.  
- `HAVING` filters groups with more than 5 employees.

---

### **3. Retrieve Employees With a Salary Greater Than Their Department's Average**
**Problem:** List employees earning above the average salary of their respective departments.

**Query:**
```sql
SELECT E.Name, E.Salary, E.DepartmentID
FROM Employees E
WHERE E.Salary > (
    SELECT AVG(Salary)
    FROM Employees
    WHERE DepartmentID = E.DepartmentID
);
```
**Explanation:**  
- The subquery calculates the average salary for each department.  
- The outer query compares each employee's salary with their department's average.

---

### **4. Identify Duplicate Records in a Table**
**Problem:** Find duplicate employee names in the `Employees` table.

**Query:**
```sql
SELECT Name, COUNT(*)
FROM Employees
GROUP BY Name
HAVING COUNT(*) > 1;
```
**Explanation:**  
- Groups rows by `Name`.  
- `HAVING COUNT(*) > 1` filters names that appear more than once.

---

### **5. Retrieve Top 3 Salaries in Each Department**
**Problem:** Rank employees by salary within each department and retrieve the top 3.

**Query:**
```sql
SELECT Name, DepartmentID, Salary
FROM (
    SELECT Name, DepartmentID, Salary,
           RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS Rank
    FROM Employees
) Ranked
WHERE Rank <= 3;
```
**Explanation:**  
- `RANK()` assigns a rank to employees within each department based on salary.  
- The outer query filters rows where the rank is less than or equal to 3.

---

### **6. Find Employees Reporting to the Same Manager**
**Problem:** List pairs of employees who share the same manager.

**Query:**
```sql
SELECT E1.Name AS Employee1, E2.Name AS Employee2, E1.ManagerID
FROM Employees E1
JOIN Employees E2 ON E1.ManagerID = E2.ManagerID
WHERE E1.EmployeeID < E2.EmployeeID;
```
**Explanation:**  
- Self-join matches employees with the same `ManagerID`.  
- `E1.EmployeeID < E2.EmployeeID` ensures no duplicate pairs.

---

### **7. Recursive Query: Find an Employee Hierarchy**
**Problem:** Display the hierarchy of employees starting from the CEO.

**Query:**
```sql
WITH RECURSIVE EmployeeHierarchy AS (
    SELECT EmployeeID, Name, ManagerID
    FROM Employees
    WHERE ManagerID IS NULL
    UNION ALL
    SELECT E.EmployeeID, E.Name, E.ManagerID
    FROM Employees E
    INNER JOIN EmployeeHierarchy EH ON E.ManagerID = EH.EmployeeID
)
SELECT * FROM EmployeeHierarchy;
```
**Explanation:**  
- The recursive query starts with the CEO (no manager).  
- It then finds employees reporting to each level of the hierarchy.

---

### **8. Identify Gaps in Sequential Data**
**Problem:** Find missing order numbers in a sequence from the `Orders` table.

**Query:**
```sql
SELECT O1.OrderNo + 1 AS MissingOrderNo
FROM Orders O1
LEFT JOIN Orders O2 ON O1.OrderNo + 1 = O2.OrderNo
WHERE O2.OrderNo IS NULL;
```
**Explanation:**  
- Checks for gaps by joining `OrderNo` + 1 in one table to `OrderNo` in another.  
- Filters where no match is found.

---

### **9. Count Employees With the Same Job Title in a Department**
**Problem:** Count employees with the same job title within each department.

**Query:**
```sql
SELECT DepartmentID, JobTitle, COUNT(*) AS EmployeeCount
FROM Employees
GROUP BY DepartmentID, JobTitle
HAVING COUNT(*) > 1;
```
**Explanation:**  
- Groups data by department and job title.  
- `HAVING` ensures only groups with more than one employee are shown.

---

### **10. Compare Monthly Sales Between Two Years**
**Problem:** Compare monthly sales for 2023 and 2024.

**Query:**
```sql
SELECT EXTRACT(MONTH FROM SaleDate) AS Month, 
       SUM(CASE WHEN EXTRACT(YEAR FROM SaleDate) = 2023 THEN Amount ELSE 0 END) AS Sales2023,
       SUM(CASE WHEN EXTRACT(YEAR FROM SaleDate) = 2024 THEN Amount ELSE 0 END) AS Sales2024
FROM Sales
GROUP BY EXTRACT(MONTH FROM SaleDate);
```
**Explanation:**  
- Extracts the month from `SaleDate` for grouping.  
- Conditional aggregation sums sales separately for 2023 and 2024.

---

### **11. Retrieve Employees Without Managers in Their Department**
**Problem:** List employees who do not have a manager in their department.

**Query:**
```sql
SELECT E.Name, E.DepartmentID
FROM Employees E
WHERE E.ManagerID NOT IN (
    SELECT EmployeeID
    FROM Employees
    WHERE DepartmentID = E.DepartmentID
);
```
**Explanation:**  
- Subquery finds all managers in each department.  
- Outer query filters employees whose `ManagerID` is not in this list.










---

$$
\text{End Of File}
$$
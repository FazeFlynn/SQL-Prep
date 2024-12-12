# SQL Prac

<!-- =========================================================== -->

### **SQL Operations: Comprehensive Guide**

---

### **1. Database Operations**
#### **Definition:** SQL operations to create, modify, and delete databases.

- **Create Database**
  ```sql
  CREATE DATABASE DatabaseName;
  ```
  Creates a new database.

- **Use Database**
  ```sql
  USE DatabaseName;
  ```
  Selects a database for operations.

- **Modify Database**
  ```sql
  ALTER DATABASE DatabaseName MODIFY NAME = NewDatabaseName;
  ```
  Renames an existing database.

- **Delete Database**
  ```sql
  DROP DATABASE DatabaseName;
  ```
  Deletes an existing database.

---

### **2. Table Operations**
#### **Definition:** SQL operations to create, modify, and delete tables.

- **Create Table**
  ```sql
  CREATE TABLE TableName (
      Column1 DataType Constraints,
      Column2 DataType Constraints
  );
  ```
  Example with Constraints:
  ```sql
  CREATE TABLE Employees (
      EmployeeID INT PRIMARY KEY AUTO_INCREMENT,
      Name VARCHAR(100) NOT NULL,
      DepartmentID INT,
      Salary DECIMAL(10, 2) DEFAULT 0.00
  );
  ```

 #### Adding primary key after by altering the table

 ```sql
ALTER TABLE TableName
ADD CONSTRAINT ConstraintName PRIMARY KEY (ColumnName);
 ``` 

`Setting auto increment`

```sql
CREATE TABLE Employees (
    EmployeeID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100)
) AUTO_INCREMENT = 200; -- Starts from 200

```

`OR - Alter after creating the column`

```sql
ALTER TABLE Employees AUTO_INCREMENT = 200;
```


- **Modify Table (Add/Drop Columns)**
  ```sql
  ALTER TABLE TableName ADD ColumnName DataType;
  ALTER TABLE TableName DROP COLUMN ColumnName;
  ```
  Adds or removes a column.

- **Modify Column**
  ```sql
  ALTER TABLE TableName MODIFY ColumnName NewDataType;
  ```
  Changes the data type or size of a column.

- **Delete Table**
  ```sql
  DROP TABLE TableName;
  ```
  Deletes an existing table.

---

<!-- ================================================================================= -->

#### Renaming tables and columns

- **Using `RENAME TABLE` (in MySQL):**
```sql
RENAME TABLE old_table_name TO new_table_name;
```

- **Using `ALTER TABLE` (in PostgreSQL and MySQL):**
```sql
ALTER TABLE old_table_name RENAME TO new_table_name;
```
`Renaming Columns`

To rename columns in SQL, the process can differ slightly between different database systems. Below are the methods for renaming columns in some common relational databases:

---

### **1. Renaming a Column**

**Syntax:**
```sql
ALTER TABLE table_name CHANGE old_column_name new_column_name column_definition;
```
- `column_definition` must include the data type of the column.

#### **Example:**
If you have a table `students` and want to rename the column `studID` to `studentID`:
```sql
ALTER TABLE students CHANGE studID studentID INT;
```
- **Important**: You need to specify the column’s data type (`INT` in this example) while renaming the column.


<!-- =========================================================================== -->
---

### **3. Data (Record) Operations**
#### **Definition:** SQL operations to manipulate records in tables.

- **Insert Data**
  ```sql
  INSERT INTO TableName (Column1, Column2) VALUES (Value1, Value2);
  ```
  Inserts a new row.

- **Update Data**
  ```sql
  UPDATE TableName
  SET Column1 = NewValue1
  WHERE Condition;
  ```
  Modifies existing data.

- **Delete Data**
  ```sql
  DELETE FROM TableName
  WHERE Condition;
  ```
  Removes rows matching a condition.

- **Retrieve Data**
  ```sql
  SELECT Column1, Column2 FROM TableName WHERE Condition;
  ```
  Retrieves specific rows.

---

### **4. Views**
#### **Definition:** A virtual table created using SQL queries.

- **Create View**
  ```sql
  CREATE VIEW ViewName AS
  SELECT Column1, Column2
  FROM TableName
  WHERE Condition;
  ```
  Example:
  ```sql
  CREATE VIEW HighSalaryEmployees AS
  SELECT Name, Salary
  FROM Employees
  WHERE Salary > 50000;
  ```

- **Modify View**
  ```sql
  CREATE OR REPLACE VIEW ViewName AS
  SELECT Column1, Column2
  FROM TableName
  WHERE Condition;
  ```
  Updates the definition of a view.

- **Delete View**
  ```sql
  DROP VIEW ViewName;
  ```
  Removes an existing view.

---

### **5. Indexes**
#### **Definition:** Structures to improve the speed of data retrieval.

- **Create Index**
  ```sql
  CREATE INDEX IndexName ON TableName(ColumnName);
  ```

- **Unique Index**
  ```sql
  CREATE UNIQUE INDEX IndexName ON TableName(ColumnName);
  ```

- **Drop Index**
  ```sql
  DROP INDEX IndexName ON TableName;
  ```

---

### **6. Constraints**
#### **Definition:** Rules applied to columns for data integrity.

- **Primary Key**
  ```sql
  CREATE TABLE Example (
      ID INT PRIMARY KEY
  );
  ```

- **Foreign Key**
  ```sql
  CREATE TABLE Orders (
      OrderID INT PRIMARY KEY,
      CustomerID INT,
      FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
  );
  ```

- **Unique**
  ```sql
  CREATE TABLE Example (
      Email VARCHAR(255) UNIQUE
  );
  ```

- **Check**
  ```sql
  CREATE TABLE Example (
      Age INT CHECK (Age >= 18)
  );
  ```

- **Default**
  ```sql
  CREATE TABLE Example (
      Status VARCHAR(50) DEFAULT 'Active'
  );
  ```

- **Not Null**
  ```sql
  CREATE TABLE Example (
      Name VARCHAR(100) NOT NULL
  );
  ```

---

### **7. Auto-Increment**
#### **Definition:** Automatically generates unique values for a column.

- **Example:**
  ```sql
  CREATE TABLE Employees (
      EmployeeID INT AUTO_INCREMENT PRIMARY KEY,
      Name VARCHAR(100)
  );
  ```

---

### **8. Stored Procedures**
#### **Definition:** A group of SQL statements executed as a unit.

- **Create Procedure**
  ```sql
  CREATE PROCEDURE ProcedureName()
  BEGIN
      SELECT * FROM TableName;
  END;
  ```

- **Execute Procedure**
  ```sql
  CALL ProcedureName();
  ```

- **Drop Procedure**
  ```sql
  DROP PROCEDURE ProcedureName;
  ```

---

### **9. Transactions**
#### **Definition:** A series of operations executed as a single unit.

- **Begin Transaction**
  ```sql
  BEGIN TRANSACTION;
  ```

- **Commit**
  ```sql
  COMMIT;
  ```

- **Rollback**
  ```sql
  ROLLBACK;
  ```

---

### **10. Triggers**
#### **Definition:** Automatically executes a function in response to certain events.

- **Create Trigger**
  ```sql
  CREATE TRIGGER TriggerName
  AFTER INSERT ON TableName
  FOR EACH ROW
  BEGIN
      INSERT INTO AuditLog (Action) VALUES ('Insert Operation');
  END;
  ```

- **Drop Trigger**
  ```sql
  DROP TRIGGER TriggerName;
  ```


---

<!-- ==================================================== -->

### **Difference Between DROP, DELETE, and TRUNCATE**


### **1. DROP Command**
#### **Definition:**  
The `DROP` command removes an **entire database object** (like a table, database, view, etc.). Once dropped, the object and its data are permanently removed, and it cannot be recovered unless backed up.

#### **Key Characteristics:**
- Deletes the table structure and all its data permanently.
- Cannot be rolled back.
- Frees up the storage space allocated to the object.

#### **Example:**
```sql
DROP TABLE Employees;
```
- Removes the `Employees` table entirely, including its structure and data.

#### **Use Case:**
When you want to permanently delete a table or database.

---

### **2. DELETE Command**
#### **Definition:**  
The `DELETE` command removes specific rows from a table based on a condition. The table structure and the remaining data are unaffected.

#### **Key Characteristics:**
- Deletes rows based on a condition (`WHERE` clause).  
- If no `WHERE` clause is provided, deletes all rows but keeps the table structure.
- Can be rolled back (if inside a transaction).  
- Triggers associated with the table are activated.

#### **Example:**
```sql
DELETE FROM Employees WHERE DepartmentID = 2;
```
- Deletes only rows where `DepartmentID` is `2`.

#### **Use Case:**
When you want to remove specific rows from a table.

---

### **3. TRUNCATE Command**
#### **Definition:**  
The `TRUNCATE` command removes **all rows** from a table without logging individual row deletions. It resets the table to an empty state but retains the table structure.

#### **Key Characteristics:**
- Deletes all rows in the table.  
- Cannot have a `WHERE` clause.  
- Cannot be rolled back (not logged like `DELETE`).  
- Faster than `DELETE` because it doesn’t log each row deletion.  
- Resets auto-increment counters (if any).

#### **Example:**
```sql
TRUNCATE TABLE Employees;
```
- Removes all rows from the `Employees` table but keeps the structure intact.

#### **Use Case:**
When you want to quickly clear all data from a table without removing its structure.

---

### **Key Differences**

| Feature                  | DROP                          | DELETE                          | TRUNCATE                       |
|--------------------------|-------------------------------|---------------------------------|--------------------------------|
| **Purpose**              | Deletes the entire object.    | Deletes specific rows.          | Deletes all rows.              |
| **Structure**            | Removes the table structure.  | Retains the structure.          | Retains the structure.         |
| **Condition (`WHERE`)**  | Not allowed.                 | Allowed.                       | Not allowed.                  |
| **Rollback Support**     | No                           | Yes (if within a transaction). | No                            |
| **Speed**                | Fast                         | Slower (row-by-row logging).   | Very fast.                    |
| **Auto-increment Reset** | Not applicable.              | No.                            | Yes.                          |
| **Trigger Activation**   | No                           | Yes.                           | No.                           |

---

### **Examples in Context**

#### Scenario: Remove a specific employee's data.
```sql
DELETE FROM Employees WHERE EmployeeID = 101;
```
- Removes only the employee with `EmployeeID = 101`.

#### Scenario: Empty a table but keep its structure for reuse.
```sql
TRUNCATE TABLE Employees;
```
- Clears all rows from the `Employees` table.

#### Scenario: Permanently remove a table and its data.
```sql
DROP TABLE Employees;
```
- Deletes the `Employees` table entirely.

---

### **Conclusion**
- Use `DROP` to permanently delete a table or database.  
- Use `DELETE` to remove specific rows while retaining the table structure.  
- Use `TRUNCATE` to quickly remove all rows from a table without affecting its structure.  








<!-- ============================================================= -->
---

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

# Windows Functions Comprehensive


### **Comprehensive Guide to Window Functions in SQL**

#### **Overview of Window Functions**
Window functions allow you to perform calculations across a set of table rows that are related to the current row. Unlike aggregate functions, window functions do not group the result set. Instead, they perform calculations across a "window" of rows.

Window functions are often used for tasks like ranking, cumulative totals, moving averages, and more. 

---

### **Basic Syntax of Window Functions**
```sql
<window_function> OVER (
  [PARTITION BY partition_columns]
  [ORDER BY order_columns]
  [ROWS window_specification]
)
```

- **`<window_function>`**: This is the specific window function, such as `RANK()`, `ROW_NUMBER()`, `SUM()`, etc.
- **`PARTITION BY`**: Divides the result set into partitions (groups of rows) to which the window function will be applied.
- **`ORDER BY`**: Orders rows within each partition.
- **`ROWS`**: Defines a window frame (optional), e.g., to define a specific range of rows for the calculation.

---

### **Types of Window Functions**

1. **Ranking Functions**
   - These functions assign a rank to each row within the result set, based on the specified order.
   
   - **ROW_NUMBER()**: Assigns a unique number to each row.
   - **RANK()**: Assigns a rank to rows with ties, but the next rank(s) are skipped.
   - **DENSE_RANK()**: Similar to `RANK()`, but no gaps are left in ranks.
   - **NTILE(n)**: Divides the result set into `n` buckets and assigns a bucket number to each row.

2. **Aggregate Functions**
   - These functions compute aggregated values but over a defined window (as opposed to summarizing the entire result set).
   
   - **SUM()**: Calculates the sum of a window of rows.
   - **AVG()**: Calculates the average of a window of rows.
   - **MIN()**: Returns the minimum value in the window.
   - **MAX()**: Returns the maximum value in the window.
   - **COUNT()**: Returns the count of rows in the window.

3. **Value Functions**
   - These functions return specific values for a window frame.
   
   - **LEAD()**: Returns the value of the next row.
   - **LAG()**: Returns the value of the previous row.
   - **FIRST_VALUE()**: Returns the first value in the window.
   - **LAST_VALUE()**: Returns the last value in the window.

---

### **Examples of Window Functions**

#### **1. `ROW_NUMBER()`**
Assigns a unique row number to each row in the result set.

**Query:**
```sql
SELECT Name, DepartmentID, Salary,
       ROW_NUMBER() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS RowNum
FROM Employees;
```

**Explanation:**
- `ROW_NUMBER()` assigns a unique sequential number within each department (`PARTITION BY DepartmentID`), ordered by `Salary` in descending order.

**Sample Table (`Employees`):**
| Name    | DepartmentID | Salary |
|---------|--------------|--------|
| Alice   | 1            | 50000  |
| Bob     | 1            | 70000  |
| Charlie | 1            | 70000  |
| David   | 2            | 40000  |
| Eva     | 2            | 60000  |
| Frank   | 2            | 50000  |

**Output:**
| Name    | DepartmentID | Salary | RowNum |
|---------|--------------|--------|--------|
| Bob     | 1            | 70000  | 1      |
| Charlie | 1            | 70000  | 2      |
| Alice   | 1            | 50000  | 3      |
| Eva     | 2            | 60000  | 1      |
| Frank   | 2            | 50000  | 2      |
| David   | 2            | 40000  | 3      |

---

#### **2. `RANK()`**
Assigns a rank to each row, skipping ranks in case of ties.

**Query:**
```sql
SELECT Name, DepartmentID, Salary,
       RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS Rank
FROM Employees;
```

**Explanation:**
- `RANK()` assigns the same rank to rows with the same salary and skips the next rank.

**Output:**
| Name    | DepartmentID | Salary | Rank |
|---------|--------------|--------|------|
| Bob     | 1            | 70000  | 1    |
| Charlie | 1            | 70000  | 1    |
| Alice   | 1            | 50000  | 3    |
| Eva     | 2            | 60000  | 1    |
| Frank   | 2            | 50000  | 2    |
| David   | 2            | 40000  | 3    |

---

#### **3. `DENSE_RANK()`**
Similar to `RANK()`, but no gaps are left in the ranks.

**Query:**
```sql
SELECT Name, DepartmentID, Salary,
       DENSE_RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS DenseRank
FROM Employees;
```

**Explanation:**
- `DENSE_RANK()` assigns the same rank to rows with the same salary but without skipping any ranks.

**Output:**
| Name    | DepartmentID | Salary | DenseRank |
|---------|--------------|--------|-----------|
| Bob     | 1            | 70000  | 1         |
| Charlie | 1            | 70000  | 1         |
| Alice   | 1            | 50000  | 2         |
| Eva     | 2            | 60000  | 1         |
| Frank   | 2            | 50000  | 2         |
| David   | 2            | 40000  | 3         |

---

#### **4. `NTILE()`**
Divides the result set into `n` buckets and assigns a bucket number.

**Query:**
```sql
SELECT Name, DepartmentID, Salary,
       NTILE(3) OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS Quartile
FROM Employees;
```

**Explanation:**
- `NTILE(3)` divides the rows within each department into 3 roughly equal groups (quartiles).

**Output:**
| Name    | DepartmentID | Salary | Quartile |
|---------|--------------|--------|----------|
| Bob     | 1            | 70000  | 1        |
| Charlie | 1            | 70000  | 1        |
| Alice   | 1            | 50000  | 2        |
| Eva     | 2            | 60000  | 1        |
| Frank   | 2            | 50000  | 2        |
| David   | 2            | 40000  | 3        |

---

#### **5. `LEAD()`**
Returns the value of the next row in the result set.

**Query:**
```sql
SELECT Name, Salary,
       LEAD(Salary, 1) OVER (ORDER BY Salary DESC) AS NextSalary
FROM Employees;
```

**Explanation:**
- `LEAD(Salary, 1)` returns the salary of the next employee (ordered by `Salary DESC`).

**Output:**
| Name    | Salary | NextSalary |
|---------|--------|------------|
| Bob     | 70000  | 70000      |
| Charlie | 70000  | 50000      |
| Alice   | 50000  | 40000      |
| Eva     | 60000  | 50000      |
| Frank   | 50000  | 40000      |
| David   | 40000  | NULL       |

---

#### **6. `LAG()`**
Returns the value of the previous row in the result set.

**Query:**
```sql
SELECT Name, Salary,
       LAG(Salary, 1) OVER (ORDER BY Salary DESC) AS PrevSalary
FROM Employees;
```

**Explanation:**
- `LAG(Salary, 1)` returns the salary of the previous employee (ordered by `Salary DESC`).

**Output:**
| Name    | Salary | PrevSalary |
|---------|--------|------------|
| Bob     | 70000  | NULL       |
| Charlie | 70000  | 70000      |
| Alice   | 50000  | 70000      |
| Eva     | 60000  | 50000      |
| Frank   | 50000  | 60000      |
| David   | 40000  | 50000      |

---

#### **7. `FIRST_VALUE()` and `LAST_VALUE()`**
Returns the first or last value in the window.

**Query:**
```sql
SELECT Name, Salary,
       FIRST_VALUE(Salary) OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS FirstSalary,
       LAST_VALUE(Salary) OVER (PARTITION BY DepartmentID ORDER BY Salary DESC ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS LastSalary
FROM Employees;
```

**Explanation:**
- `FIRST_VALUE(Salary)` returns the first salary value in the department (after sorting).
- `LAST_VALUE(Salary)` returns the last salary value in the department.

**Output:**
| Name    | Salary | FirstSalary | LastSalary |
|---------|--------|-------------|------------|
| Bob     | 70000  | 70000       | 50000      |
| Charlie | 70000  | 70000       | 50000      |
| Alice   | 50000  | 70000       | 50000      |
| Eva     | 60000  | 60000       | 40000      |
| Frank   | 50000  | 60000       | 40000      |
| David   | 40000  | 60000       | 40000      |

---

### **Conclusion**
- **Window Functions** allow for advanced data analysis within SQL without collapsing the result set (as with aggregates).
- Key functions include `RANK()`, `ROW_NUMBER()`, `LEAD()`, `LAG()`, `SUM()`, `AVG()`, and others.
- Window functions can partition data (`PARTITION BY`), order it (`ORDER BY`), and define the window frame (`ROWS`).







---

$$
\text{End Of File}
$$
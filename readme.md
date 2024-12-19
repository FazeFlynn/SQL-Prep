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
---

# 200 Short SQL Interview Questions Compilation



### **1. What is SQL?**
SQL (Structured Query Language) is a standard language for managing and manipulating relational databases, including creating, updating, deleting, and querying data.

---

### **2. What are the types of SQL commands?**
1. **DDL (Data Definition Language):** `CREATE`, `ALTER`, `DROP`.  
2. **DML (Data Manipulation Language):** `INSERT`, `UPDATE`, `DELETE`.  
3. **DQL (Data Query Language):** `SELECT`.  
4. **TCL (Transaction Control Language):** `COMMIT`, `ROLLBACK`.  
5. **DCL (Data Control Language):** `GRANT`, `REVOKE`.

---

### **3. What is the difference between `DELETE` and `TRUNCATE`?**
| **DELETE**               | **TRUNCATE**                 |
|--------------------------|------------------------------|
| Deletes specific rows.   | Deletes all rows.            |
| Can use `WHERE`.         | Cannot use `WHERE`.          |
| Slower (logs each row).  | Faster (no row-level logging). |
| Can be rolled back.      | Cannot be rolled back.       |

---

### **4. What are constraints in SQL?**
Constraints enforce rules on data. Common constraints:
- **NOT NULL:** Prevents null values.  
- **UNIQUE:** Ensures unique values in a column.  
- **PRIMARY KEY:** Combines `NOT NULL` and `UNIQUE`.  
- **FOREIGN KEY:** Links two tables.  
- **CHECK:** Validates column data.  
- **DEFAULT:** Sets a default value for a column.

---

### **5. What is a primary key?**
A primary key uniquely identifies each row in a table. It cannot have `NULL` values and must be unique.

---

### **6. What is a foreign key?**
A foreign key is a column in one table that refers to the primary key of another table, establishing a relationship between the two.

---

### **7. What is the difference between `INNER JOIN` and `OUTER JOIN`?**
| **INNER JOIN**            | **OUTER JOIN**            |
|---------------------------|---------------------------|
| Returns matching rows.    | Returns matching + non-matching rows. |
| Excludes unmatched data.  | Includes unmatched data with `NULL`. |

---

### **8. What is a view in SQL?**
A view is a virtual table based on the result of a `SELECT` query. Example:
```sql
CREATE VIEW employee_view AS
SELECT Name, Department FROM Employees;
```

---

### **9. How to find duplicate rows in a table?**
```sql
SELECT Column1, COUNT(*) 
FROM TableName 
GROUP BY Column1 
HAVING COUNT(*) > 1;
```

---

### **10. What is the difference between `RANK()` and `ROW_NUMBER()`?**
- **`RANK()`**: Assigns the same rank for ties but skips ranks.  
- **`ROW_NUMBER()`**: Assigns a unique number to each row.

---

### **11. What is indexing in SQL?**
Indexing improves the speed of data retrieval. Types:
1. **Clustered Index:** Reorders the table.  
2. **Non-Clustered Index:** Creates a separate structure for lookups.

---

### **12. Write a query to find the second-highest salary.**
```sql
SELECT MAX(Salary) AS SecondHighest
FROM Employees
WHERE Salary < (SELECT MAX(Salary) FROM Employees);
```

---

### **13. What is the difference between `HAVING` and `WHERE`?**
- **`WHERE`**: Filters rows before grouping.  
- **`HAVING`**: Filters groups after aggregation.

---

### **14. What are aggregate functions?**
Functions that perform calculations on multiple rows:
- `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`.

---

### **15. What is the difference between `DROP` and `TRUNCATE`?**
- **`DROP`**: Deletes the table structure and data.  
- **`TRUNCATE`**: Deletes all rows but keeps the table structure.

---

### **16. What is a stored procedure?**
A stored procedure is a precompiled set of SQL statements that can be executed as a single unit.

**Example:**
```sql
CREATE PROCEDURE GetEmployees()
AS
BEGIN
    SELECT * FROM Employees;
END;
```

---

### **17. What are window functions?**
Functions that perform calculations across a window of rows without collapsing the result set.  
Example:
```sql
SELECT Name, Salary, 
       RANK() OVER (PARTITION BY DepartmentID ORDER BY Salary DESC) AS Rank
FROM Employees;
```

---

### **18. What is a transaction?**
A transaction is a sequence of SQL statements executed as a single unit of work. Properties:
- **Atomicity, Consistency, Isolation, Durability (ACID).**

---

### **19. How do you handle NULL values in SQL?**
Use functions like:
- `IS NULL`: Check for NULL.
- `COALESCE(value1, value2)`: Returns the first non-NULL value.

---

### **20. What is SQL injection?**
SQL injection is a security vulnerability that allows attackers to manipulate queries. Use **prepared statements** to prevent it:
```sql
SELECT * FROM Users WHERE Username = ? AND Password = ?;
```

---

### **21. What is a `CASE` statement in SQL?**
It adds conditional logic to queries.  
Example:
```sql
SELECT Name, 
       CASE 
           WHEN Salary > 50000 THEN 'High'
           ELSE 'Low'
       END AS SalaryCategory
FROM Employees;
```

---

### **22. What is normalization?**
Normalization is the process of organizing data to reduce redundancy and improve integrity. Common forms:
1. **1NF:** Remove duplicate columns.  
2. **2NF:** Ensure no partial dependency.  
3. **3NF:** Remove transitive dependencies.

---

### **23. Write a query to fetch common rows from two tables.**
```sql
SELECT Name 
FROM TableA 
INTERSECT 
SELECT Name 
FROM TableB;
```

---

### **24. How to fetch the current date in SQL?**
```sql
SELECT CURRENT_DATE; -- MySQL, PostgreSQL
```

---

### **25. Explain the `LIMIT` and `OFFSET` clauses.**
- **`LIMIT`**: Limits the number of rows returned.
- **`OFFSET`**: Skips rows before returning the result.

**Example:**
```sql
SELECT * FROM Employees LIMIT 10 OFFSET 5;
```

---



### **26. What is a surrogate key?**
A surrogate key is a unique identifier for a record, generated by the system (e.g., `AUTO_INCREMENT` in MySQL).

---

### **27. What is the difference between `COALESCE` and `ISNULL`?**
- **`COALESCE`:** Returns the first non-NULL value from multiple inputs.  
- **`ISNULL`:** Checks if a single value is `NULL`.

---

### **28. Write a query to find the nth highest salary.**
```sql
SELECT DISTINCT Salary 
FROM Employees 
ORDER BY Salary DESC 
LIMIT 1 OFFSET n-1;
```

---

### **29. What is the difference between `UNION` and `UNION ALL`?**
- **`UNION`:** Eliminates duplicate rows.  
- **`UNION ALL`:** Includes duplicates.

---

### **30. What is the difference between a view and a materialized view?**
- **View:** A virtual table that executes a query each time it’s accessed.  
- **Materialized View:** Stores the query result physically.

---

### **31. How do you create a unique index?**
```sql
CREATE UNIQUE INDEX idx_name ON Employees (Email);
```

---

### **32. What is the purpose of the `GROUP BY` clause?**
It groups rows sharing the same value in specified columns for aggregation functions.

**Example:**
```sql
SELECT DepartmentID, AVG(Salary) 
FROM Employees 
GROUP BY DepartmentID;
```

---

### **33. What is a CTE (Common Table Expression)?**
A temporary result set defined using `WITH`.  

**Example:**
```sql
WITH CTE AS (
    SELECT Name, Salary FROM Employees WHERE Salary > 50000
)
SELECT * FROM CTE;
```

---

### **34. Write a query to fetch even and odd rows.**
**Odd Rows:**
```sql
SELECT * FROM Employees WHERE MOD(EmployeeID, 2) = 1;
```
**Even Rows:**
```sql
SELECT * FROM Employees WHERE MOD(EmployeeID, 2) = 0;
```

---

### **35. What is a cross join?**
A `CROSS JOIN` combines every row from two tables (Cartesian product).  

**Example:**
```sql
SELECT * 
FROM TableA CROSS JOIN TableB;
```

---

### **36. How do you delete duplicate rows?**
```sql
DELETE FROM Employees 
WHERE EmployeeID NOT IN (
    SELECT MIN(EmployeeID) 
    FROM Employees 
    GROUP BY Name, DepartmentID
);
```

---

### **37. What is a composite key?**
A composite key is a primary key made up of two or more columns to uniquely identify a row.

**Example:**
```sql
CREATE TABLE Orders (
    OrderID INT,
    ProductID INT,
    PRIMARY KEY (OrderID, ProductID)
);
```

---

### **38. What is the difference between `NOW()` and `CURRENT_TIMESTAMP`?**
Both return the current date and time, but behavior may differ slightly in some databases.  
- **`NOW()`**: MySQL.  
- **`CURRENT_TIMESTAMP`**: Standard SQL.

---

### **39. How to copy a table structure without data?**
```sql
CREATE TABLE new_table LIKE old_table; -- MySQL
```

---

### **40. What is the difference between `DELETE` and `DROP`?**
- **`DELETE`:** Removes rows but retains the table.  
- **`DROP`:** Removes the table entirely.

---

### **41. How do you fetch the highest salary in each department?**
```sql
SELECT DepartmentID, MAX(Salary) 
FROM Employees 
GROUP BY DepartmentID;
```

---

### **42. What is the difference between `IN` and `EXISTS`?**
- **`IN`:** Checks values within a list.  
- **`EXISTS`:** Checks if a subquery returns rows.

---

### **43. What is the use of the `CAST()` function?**
Converts data types.
```sql
SELECT CAST(123.45 AS INT);
```

---

### **44. How to calculate the percentage in a query?**
```sql
SELECT Name, (Salary / SUM(Salary) OVER()) * 100 AS Percentage 
FROM Employees;
```

---

### **45. How do you find employees without a manager?**
```sql
SELECT * FROM Employees WHERE ManagerID IS NULL;
```

---

### **46. Write a query to list all tables in a database.**
```sql
SHOW TABLES; -- MySQL
```

---

### **47. What is a self join?**
A join where a table is joined with itself.  
**Example:**
```sql
SELECT A.Name, B.Name AS Manager 
FROM Employees A 
JOIN Employees B ON A.ManagerID = B.EmployeeID;
```

---

### **48. What is a correlated subquery?**
A subquery that depends on the outer query.  
**Example:**
```sql
SELECT Name, Salary 
FROM Employees E1 
WHERE Salary > (SELECT AVG(Salary) FROM Employees E2 WHERE E1.DepartmentID = E2.DepartmentID);
```

---

### **49. How do you update multiple columns?**
```sql
UPDATE Employees 
SET Name = 'John', Salary = 60000 
WHERE EmployeeID = 101;
```

---

### **50. How do you rename a column in SQL?**
```sql
ALTER TABLE Employees RENAME COLUMN old_name TO new_name; -- PostgreSQL
```


---

### **51. How do you fetch the last N rows from a table?**
```sql
SELECT * 
FROM Employees 
ORDER BY EmployeeID DESC 
LIMIT N;
```

---

### **52. What is the difference between `CHAR` and `VARCHAR`?**
- **`CHAR`**: Fixed-length storage.  
- **`VARCHAR`**: Variable-length storage.

---

### **53. Write a query to swap values of two columns in a table.**
```sql
UPDATE Employees 
SET Column1 = Column2, Column2 = Column1;
```

---

### **54. How do you add a new column to a table?**
```sql
ALTER TABLE Employees ADD Address VARCHAR(255);
```

---

### **55. What is the difference between a clustered and non-clustered index?**
- **Clustered:** Reorders the actual table rows.  
- **Non-Clustered:** Creates a separate structure for lookup.

---

### **56. How to remove duplicate rows but keep one?**
```sql
DELETE FROM Employees 
WHERE EmployeeID NOT IN (
    SELECT MIN(EmployeeID) 
    FROM Employees 
    GROUP BY Name, DepartmentID
);
```

---

### **57. Write a query to calculate the cumulative sum.**
```sql
SELECT Name, Salary, 
       SUM(Salary) OVER (ORDER BY Salary) AS CumulativeSalary 
FROM Employees;
```

---

### **58. What are the differences between `CASE` and `IF` in SQL?**
- **`CASE`**: Used in queries for conditional logic.  
- **`IF`**: Used in stored procedures/functions for flow control.

---

### **59. How do you find the length of a string in SQL?**
```sql
SELECT LENGTH('Hello'); -- MySQL
```

---

### **60. Write a query to get the current database name.**
```sql
SELECT DATABASE(); -- MySQL
```

---

### **61. What is the use of the `GROUP_CONCAT()` function?**
Combines values into a single string.
```sql
SELECT GROUP_CONCAT(Name) FROM Employees;
```

---

### **62. Write a query to fetch employees with salaries between 30K and 50K.**
```sql
SELECT * 
FROM Employees 
WHERE Salary BETWEEN 30000 AND 50000;
```

---

### **63. How to check if a column exists in a table?**
```sql
SHOW COLUMNS FROM Employees LIKE 'ColumnName'; -- MySQL
```

---

### **64. What is the purpose of `HAVING` without `GROUP BY`?**
Filters rows after aggregate functions.
```sql
SELECT COUNT(*) 
FROM Employees 
HAVING COUNT(*) > 10;
```

---

### **65. Write a query to fetch the nth row of a table.**
```sql
SELECT * 
FROM Employees 
ORDER BY EmployeeID 
LIMIT 1 OFFSET N-1;
```

---

### **66. How do you change a column's data type?**
```sql
ALTER TABLE Employees 
MODIFY Salary DECIMAL(10, 2); -- MySQL
```

---

### **67. What is a JSON data type in SQL?**
A data type used to store JSON objects in databases like MySQL and PostgreSQL.

**Example:**
```sql
SELECT JSON_EXTRACT(data, '$.key') FROM table_name;
```

---

### **68. Write a query to find the total count of rows in a table.**
```sql
SELECT COUNT(*) FROM Employees;
```

---

### **69. How do you concatenate two columns in SQL?**
```sql
SELECT CONCAT(FirstName, ' ', LastName) AS FullName 
FROM Employees;
```

---

### **70. What is the difference between `EXCEPT` and `NOT IN`?**
- **`EXCEPT`**: Removes rows from one query present in another.  
- **`NOT IN`**: Filters rows not present in a subquery.

---

### **71. Write a query to find employees hired in the current year.**
```sql
SELECT * 
FROM Employees 
WHERE YEAR(HireDate) = YEAR(CURDATE());
```

---

### **72. What is a sequence in SQL?**
A database object that generates numeric values sequentially.

**Example:**
```sql
CREATE SEQUENCE seq START WITH 1 INCREMENT BY 1;
```

---

### **73. How do you fetch random rows from a table?**
```sql
SELECT * 
FROM Employees 
ORDER BY RAND() 
LIMIT 5;
```

---

### **74. Write a query to find the median salary of employees.**
```sql
SELECT AVG(Salary) 
FROM (SELECT Salary FROM Employees ORDER BY Salary LIMIT 2 OFFSET (SELECT COUNT(*) FROM Employees) / 2 - 1) AS MedianSubquery;
```

---

### **75. How do you reset an auto-increment column?**
```sql
ALTER TABLE Employees AUTO_INCREMENT = 1;
```

---


---

### **76. How do you fetch common records between two tables?**
```sql
SELECT * FROM TableA INTERSECT SELECT * FROM TableB;
```

---

### **77. What is the difference between `FETCH` and `OFFSET`?**
- **`FETCH`**: Limits the number of rows returned.  
- **`OFFSET`**: Skips a specified number of rows.

---

### **78. Write a query to find all tables in a database with a specific column.**
```sql
SELECT TABLE_NAME 
FROM INFORMATION_SCHEMA.COLUMNS 
WHERE COLUMN_NAME = 'ColumnName';
```

---

### **79. What is the `BIT` data type?**
Stores binary data as 0 or 1, useful for boolean values.

---

### **80. Write a query to drop a primary key constraint.**
```sql
ALTER TABLE Employees DROP PRIMARY KEY;
```

---

### **81. How do you find the second-largest value without using `LIMIT`?**
```sql
SELECT MAX(Salary) 
FROM Employees 
WHERE Salary < (SELECT MAX(Salary) FROM Employees);
```

---

### **82. What are stored functions in SQL?**
Functions that return a value and are used in queries.

**Example:**
```sql
CREATE FUNCTION GetFullName (FirstName VARCHAR(50), LastName VARCHAR(50))
RETURNS VARCHAR(100)
RETURN CONCAT(FirstName, ' ', LastName);
```

---

### **83. What is a partitioned table?**
A table divided into smaller, manageable pieces (partitions) for performance optimization.

---

### **84. How do you disable foreign key checks in MySQL?**
```sql
SET FOREIGN_KEY_CHECKS = 0;
```

---

### **85. What are magic tables in SQL Server?**
Temporary tables (`INSERTED`, `DELETED`) used within triggers.

---

### **86. Write a query to find rows with NULL values in a column.**
```sql
SELECT * FROM Employees WHERE ColumnName IS NULL;
```

---

### **87. How to remove a column from a table?**
```sql
ALTER TABLE Employees DROP COLUMN ColumnName;
```

---

### **88. What is the `MERGE` statement?**
Combines `INSERT`, `UPDATE`, and `DELETE` into one statement.

**Example:**
```sql
MERGE INTO TargetTable T
USING SourceTable S
ON T.ID = S.ID
WHEN MATCHED THEN UPDATE SET T.Name = S.Name
WHEN NOT MATCHED THEN INSERT (ID, Name) VALUES (S.ID, S.Name);
```

---

### **89. Write a query to find duplicate rows in a table.**
```sql
SELECT Name, COUNT(*) 
FROM Employees 
GROUP BY Name 
HAVING COUNT(*) > 1;
```

---

### **90. How do you calculate the difference between two dates?**
```sql
SELECT DATEDIFF('2024-12-31', '2024-01-01') AS Difference;
```

---

### **91. How to add a unique constraint to an existing column?**
```sql
ALTER TABLE Employees ADD CONSTRAINT unique_constraint_name UNIQUE (ColumnName);
```

---

### **92. What is the difference between `==` and `=` in SQL?**
- **`=`**: Used for comparison in SQL.  
- **`==`**: Not valid in SQL; used in some programming languages.

---

### **93. Write a query to rename a table.**
```sql
ALTER TABLE old_table_name RENAME TO new_table_name;
```

---

### **94. What is the difference between scalar and aggregate functions?**
- **Scalar:** Operates on individual rows (e.g., `LEN()`, `ABS()`).  
- **Aggregate:** Operates on groups of rows (e.g., `SUM()`, `COUNT()`).

---

### **95. Write a query to retrieve unique combinations of two columns.**
```sql
SELECT DISTINCT Column1, Column2 FROM TableName;
```

---

### **96. What is the use of `WITH TIES` in `TOP` queries?**
Returns additional rows that tie for the last position.  
```sql
SELECT TOP 3 WITH TIES * FROM Employees ORDER BY Salary DESC;
```

---

### **97. How do you check if a table exists in a database?**
```sql
SELECT TABLE_NAME 
FROM INFORMATION_SCHEMA.TABLES 
WHERE TABLE_NAME = 'TableName';
```

---

### **98. Write a query to pivot rows into columns.**
```sql
SELECT DepartmentID, 
       MAX(CASE WHEN Gender = 'Male' THEN Salary ELSE NULL END) AS MaleSalary,
       MAX(CASE WHEN Gender = 'Female' THEN Salary ELSE NULL END) AS FemaleSalary
FROM Employees
GROUP BY DepartmentID;
```

---

### **99. How do you fetch records where a column starts with 'A'?**
```sql
SELECT * FROM Employees WHERE Name LIKE 'A%';
```

---

### **100. What is the difference between `NVL()` and `COALESCE()`?**
- **`NVL()`**: Replaces `NULL` with a specified value (Oracle-specific).  
- **`COALESCE()`**: Replaces `NULL` with the first non-NULL value in multiple arguments (Standard SQL).

---


### **101. What is a composite index?**
An index on multiple columns to speed up queries involving those columns.

---

### **102. How do you check the current SQL version?**
```sql
SELECT VERSION(); -- MySQL
```

---

### **103. Write a query to get the day of the week for a date.**
```sql
SELECT DAYNAME('2024-12-31'); -- MySQL
```

---

### **104. What is a lateral join?**
A `LATERAL` join allows a subquery to reference columns from the outer query.  
```sql
SELECT * FROM Employees E CROSS JOIN LATERAL (SELECT MAX(Salary) FROM Salaries S WHERE S.EmployeeID = E.ID);
```

---

### **105. How do you remove a foreign key constraint?**
```sql
ALTER TABLE Employees DROP FOREIGN KEY fk_name;
```

---

### **106. Write a query to reverse a string.**
```sql
SELECT REVERSE('Hello'); -- MySQL
```

---

### **107. What is the use of the `LIMIT` clause?**
Restricts the number of rows returned.  
```sql
SELECT * FROM Employees LIMIT 10;
```

---

### **108. How do you check table dependencies?**
```sql
SELECT REFERENCED_TABLE_NAME 
FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE 
WHERE TABLE_NAME = 'TableName';
```

---

### **109. What is the difference between `TRIM()`, `LTRIM()`, and `RTRIM()`?**
- **`TRIM()`**: Removes spaces from both sides.  
- **`LTRIM()`**: Removes spaces from the left.  
- **`RTRIM()`**: Removes spaces from the right.

---

### **110. How do you calculate the difference between two times?**
```sql
SELECT TIMEDIFF('10:30:00', '08:00:00'); -- MySQL
```

---

### **111. What are system tables in SQL?**
System tables store metadata about the database (e.g., `INFORMATION_SCHEMA.TABLES`).

---

### **112. Write a query to convert a string to uppercase.**
```sql
SELECT UPPER('hello'); -- MySQL
```

---

### **113. What is a derived table?**
A subquery that acts as a temporary table in a `FROM` clause.  
```sql
SELECT * FROM (SELECT Name, Salary FROM Employees) AS DerivedTable;
```

---

### **114. How do you find the first three characters of a string?**
```sql
SELECT SUBSTRING('Hello', 1, 3); -- MySQL
```

---

### **115. Write a query to find employees earning more than their manager.**
```sql
SELECT E.Name 
FROM Employees E 
JOIN Employees M ON E.ManagerID = M.EmployeeID 
WHERE E.Salary > M.Salary;
```

---

### **116. How do you list indexes on a table?**
```sql
SHOW INDEX FROM TableName; -- MySQL
```

---

### **117. What is the `EXPLAIN` command?**
It shows the execution plan of a query for optimization.  
```sql
EXPLAIN SELECT * FROM Employees WHERE Salary > 50000;
```

---

### **118. How do you create a full-text index?**
```sql
CREATE FULLTEXT INDEX ft_index ON Employees (Name);
```

---

### **119. Write a query to generate random numbers.**
```sql
SELECT RAND(); -- MySQL
```

---

### **120. How do you add comments in SQL?**
- Single-line: `-- Comment`  
- Multi-line: `/* Comment */`

---

### **121. What is the `IFNULL()` function?**
Replaces `NULL` with a specified value.  
```sql
SELECT IFNULL(Salary, 0) FROM Employees;
```

---

### **122. How do you check query execution time?**
```sql
SET profiling = 1; 
SELECT * FROM Employees; 
SHOW PROFILES; -- MySQL
```

---

### **123. Write a query to remove duplicates from a column.**
```sql
ALTER TABLE Employees ADD UNIQUE (ColumnName);
```

---

### **124. How do you split a string in SQL?**
Split functions vary by database; MySQL uses `SUBSTRING_INDEX()`:
```sql
SELECT SUBSTRING_INDEX('John,Doe,Developer', ',', 2);
```

---

### **125. What is the difference between `COUNT(*)` and `COUNT(ColumnName)`?**
- **`COUNT(*)`**: Counts all rows.  
- **`COUNT(ColumnName)`**: Counts non-NULL values in the column.

---

### **126. How do you rename an index?**
```sql
ALTER TABLE Employees RENAME INDEX old_index_name TO new_index_name; -- MySQL
```

---

### **127. What is the difference between `STORED` and `VIRTUAL` columns?**
- **`STORED`**: Physically stored in the table.  
- **`VIRTUAL`**: Calculated on the fly.

---

### **128. Write a query to get the last character of a string.**
```sql
SELECT RIGHT('Hello', 1); -- MySQL
```

---

### **129. How do you list triggers in a database?**
```sql
SHOW TRIGGERS; -- MySQL
```

---

### **130. What is the purpose of the `AS` keyword?**
Used to create aliases for columns or tables.  
```sql
SELECT Name AS EmployeeName FROM Employees;
```

---


### **131. What is a correlated subquery?**  
A subquery that depends on the outer query for its values.  
```sql
SELECT Name FROM Employees E WHERE Salary > (SELECT AVG(Salary) FROM Employees WHERE DepartmentID = E.DepartmentID);
```

---

### **132. Write a query to get the difference in months between two dates.**  
```sql
SELECT TIMESTAMPDIFF(MONTH, '2023-01-01', '2024-12-31'); -- MySQL
```

---

### **133. How do you retrieve the current user?**  
```sql
SELECT USER(); -- MySQL
```

---

### **134. What is the difference between `STORED PROCEDURE` and `FUNCTION`?**  
- **Procedure:** Doesn’t return a value, used for tasks.  
- **Function:** Returns a value, used in queries.

---

### **135. How do you retrieve duplicate values with their counts?**  
```sql
SELECT Name, COUNT(*) FROM Employees GROUP BY Name HAVING COUNT(*) > 1;
```

---

### **136. What is the difference between `LEFT JOIN` and `RIGHT JOIN`?**  
- **LEFT JOIN:** Returns all rows from the left table and matching rows from the right.  
- **RIGHT JOIN:** Returns all rows from the right table and matching rows from the left.

---

### **137. How do you create a new database?**  
```sql
CREATE DATABASE TestDB;
```

---

### **138. Write a query to find the highest salary in each department.**  
```sql
SELECT DepartmentID, MAX(Salary) FROM Employees GROUP BY DepartmentID;
```

---

### **139. What is the difference between `BETWEEN` and `IN`?**  
- **`BETWEEN`:** Checks if a value is within a range.  
- **`IN`:** Checks if a value exists in a list.

---

### **140. How do you fetch a column with an alias?**  
```sql
SELECT Name AS EmployeeName FROM Employees;
```

---

### **141. Write a query to fetch employees with no department.**  
```sql
SELECT * FROM Employees WHERE DepartmentID IS NULL;
```

---

### **142. How do you list all databases in MySQL?**  
```sql
SHOW DATABASES;
```

---

### **143. What is the use of `DISTINCT`?**  
Eliminates duplicate rows from the result set.  
```sql
SELECT DISTINCT DepartmentID FROM Employees;
```

---

### **144. Write a query to count NULL values in a column.**  
```sql
SELECT COUNT(*) - COUNT(ColumnName) AS NullCount FROM Employees;
```

---

### **145. How do you concatenate multiple rows into a single string?**  
```sql
SELECT GROUP_CONCAT(Name) FROM Employees; -- MySQL
```

---

### **146. What is the `IF` statement in SQL?**  
```sql
SELECT Name, IF(Salary > 50000, 'High', 'Low') AS SalaryCategory FROM Employees;
```

---

### **147. How do you fetch all records except the top N?**  
```sql
SELECT * FROM Employees ORDER BY Salary LIMIT N, 18446744073709551615; -- MySQL
```

---

### **148. What is the difference between `CROSS JOIN` and `SELF JOIN`?**  
- **CROSS JOIN:** Produces a Cartesian product.  
- **SELF JOIN:** Joins a table to itself.

---

### **149. Write a query to get the 3rd highest salary without using `LIMIT`.**  
```sql
SELECT DISTINCT Salary FROM Employees ORDER BY Salary DESC OFFSET 2 ROWS FETCH NEXT 1 ROW ONLY;
```

---

### **150. How do you create a temporary table?**  
```sql
CREATE TEMPORARY TABLE TempTable AS SELECT * FROM Employees;
```

---

### **151. Write a query to update a column conditionally.**  
```sql
UPDATE Employees SET Salary = Salary + 1000 WHERE DepartmentID = 2;
```

---

### **152. What is a cascade delete?**  
Automatically deletes rows in child tables when a parent row is deleted.  
```sql
FOREIGN KEY (DepartmentID) REFERENCES Departments(ID) ON DELETE CASCADE;
```

---

### **153. How do you return the last inserted ID?**  
```sql
SELECT LAST_INSERT_ID(); -- MySQL
```

---

### **154. What is the difference between `NOW()` and `SYSDATE()`?**  
- **`NOW()`**: Captures the timestamp when the query starts.  
- **`SYSDATE()`**: Captures the timestamp when executed.

---

### **155. Write a query to find the first non-NULL value.**  
```sql
SELECT COALESCE(Column1, Column2, 'Default') FROM Employees;
```

---

### **156. How do you extract the year from a date?**  
```sql
SELECT YEAR(HireDate) FROM Employees; -- MySQL
```

---

### **157. Write a query to return rows where a column contains a substring.**  
```sql
SELECT * FROM Employees WHERE Name LIKE '%John%';
```

---

### **158. How do you check if a table is empty?**  
```sql
SELECT COUNT(*) FROM Employees;
```

---

### **159. What is the `CAST` function?**  
Converts data types.  
```sql
SELECT CAST(Salary AS CHAR) FROM Employees;
```

---

### **160. Write a query to create an index on multiple columns.**  
```sql
CREATE INDEX idx_name ON Employees (DepartmentID, Salary);
```

---


### **161. How do you check the size of a database?**  
```sql
SELECT table_schema AS DatabaseName, SUM(data_length + index_length) AS SizeInBytes 
FROM information_schema.TABLES 
GROUP BY table_schema;
```

---

### **162. What is a recursive CTE?**  
A Common Table Expression that refers to itself.  
```sql
WITH RECURSIVE CTE AS (
    SELECT 1 AS Number
    UNION ALL
    SELECT Number + 1 FROM CTE WHERE Number < 10
)
SELECT * FROM CTE;
```

---

### **163. How do you drop a column with constraints?**  
```sql
ALTER TABLE Employees DROP COLUMN Name CASCADE;
```

---

### **164. Write a query to find employees whose names end with 'e'.**  
```sql
SELECT * FROM Employees WHERE Name LIKE '%e';
```

---

### **165. How do you fetch the current time in SQL?**  
```sql
SELECT CURRENT_TIME; -- MySQL
```

---

### **166. Write a query to fetch duplicate salaries.**  
```sql
SELECT Salary, COUNT(*) FROM Employees GROUP BY Salary HAVING COUNT(*) > 1;
```

---

### **167. What is an updatable view?**  
A view that allows `INSERT`, `UPDATE`, or `DELETE` operations if it meets certain conditions.

---

### **168. Write a query to delete all rows from a table without logging.**  
```sql
TRUNCATE TABLE Employees;
```

---

### **169. How do you fetch the last day of the current month?**  
```sql
SELECT LAST_DAY(CURDATE()); -- MySQL
```

---

### **170. What is the `UUID()` function?**  
Generates a unique identifier.  
```sql
SELECT UUID(); -- MySQL
```

---

### **171. Write a query to remove leading and trailing spaces.**  
```sql
SELECT TRIM('   Hello   '); -- MySQL
```

---

### **172. How do you fetch the maximum value of a column?**  
```sql
SELECT MAX(Salary) FROM Employees;
```

---

### **173. Write a query to fetch all employees except the lowest salary.**  
```sql
SELECT * FROM Employees WHERE Salary > (SELECT MIN(Salary) FROM Employees);
```

---

### **174. What is the difference between `FLOAT` and `DECIMAL`?**  
- **FLOAT:** Approximate numeric values.  
- **DECIMAL:** Exact numeric values.

---

### **175. Write a query to calculate the average salary by department.**  
```sql
SELECT DepartmentID, AVG(Salary) FROM Employees GROUP BY DepartmentID;
```

---

### **176. How do you fetch non-matching records between two tables?**  
```sql
SELECT * FROM TableA A LEFT JOIN TableB B ON A.ID = B.ID WHERE B.ID IS NULL;
```

---

### **177. Write a query to drop a materialized view.**  
```sql
DROP MATERIALIZED VIEW ViewName;
```

---

### **178. How do you copy data from one table to another?**  
```sql
INSERT INTO Table2 SELECT * FROM Table1;
```

---

### **179. What is the `DECODE()` function?**  
Performs conditional queries, similar to `CASE`.  
```sql
SELECT DECODE(Salary, 50000, 'Low', 100000, 'High', 'Average') FROM Employees;
```

---

### **180. Write a query to create a trigger for auditing changes.**  
```sql
CREATE TRIGGER AuditTrigger AFTER UPDATE ON Employees
FOR EACH ROW INSERT INTO AuditLog (EmployeeID, OldSalary, NewSalary) VALUES (OLD.ID, OLD.Salary, NEW.Salary);
```

---

### **181. How do you check foreign key constraints in MySQL?**  
```sql
SELECT * FROM INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS;
```

---

### **182. Write a query to find all employees with salaries greater than the average salary.**  
```sql
SELECT * FROM Employees WHERE Salary > (SELECT AVG(Salary) FROM Employees);
```

---

### **183. What is a stored-generated column?**  
A column whose value is computed based on other columns.  
```sql
CREATE TABLE Test (A INT, B INT, C INT AS (A + B));
```

---

### **184. Write a query to fetch the nth highest salary using a CTE.**  
```sql
WITH CTE AS (
    SELECT Salary, ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum
    FROM Employees
)
SELECT Salary FROM CTE WHERE RowNum = N;
```

---

### **185. How do you fetch all records that do not contain 'John'?**  
```sql
SELECT * FROM Employees WHERE Name NOT LIKE '%John%';
```

---

### **186. Write a query to find employees hired after 2020.**  
```sql
SELECT * FROM Employees WHERE HireDate > '2020-12-31';
```

---

### **187. What is the difference between `ISNULL()` and `NULLIF()`?**  
- **`ISNULL()`**: Replaces `NULL` with a value.  
- **`NULLIF()`**: Returns `NULL` if two values are equal.

---

### **188. Write a query to drop all rows from a table but keep the structure.**  
```sql
TRUNCATE TABLE Employees;
```

---

### **189. How do you change the default value of a column?**  
```sql
ALTER TABLE Employees ALTER COLUMN Status SET DEFAULT 'Active';
```

---

### **190. Write a query to convert a number to a string.**  
```sql
SELECT CAST(Salary AS CHAR) FROM Employees; -- MySQL
```

---

### **191. How do you find the length of a column value?**  
```sql
SELECT LENGTH(Name) AS Length FROM Employees; -- MySQL
```

---

### **192. Write a query to get the name and the highest salary in the company.**  
```sql
SELECT Name, Salary FROM Employees WHERE Salary = (SELECT MAX(Salary) FROM Employees);
```

---

### **193. What is a Cartesian product in SQL?**  
A result of a `CROSS JOIN`, combining all rows from two tables.

---

### **194. Write a query to find employees with salaries in a given list.**  
```sql
SELECT * FROM Employees WHERE Salary IN (50000, 75000, 100000);
```

---

### **195. How do you fetch records where a column has special characters?**  
```sql
SELECT * FROM Employees WHERE Name LIKE '%[^a-zA-Z0-9]%';
```

---

### **196. Write a query to find the employee with the longest name.**  
```sql
SELECT Name FROM Employees ORDER BY LENGTH(Name) DESC LIMIT 1;
```

---

### **197. How do you delete all rows where a column is NULL?**  
```sql
DELETE FROM Employees WHERE ColumnName IS NULL;
```

---

### **198. Write a query to calculate the percentage of total salary for each employee.**  
```sql
SELECT Name, (Salary / (SELECT SUM(Salary) FROM Employees)) * 100 AS SalaryPercentage FROM Employees;
```

---

### **199. How do you rename a constraint in SQL?**  
```sql
ALTER TABLE Employees RENAME CONSTRAINT old_constraint_name TO new_constraint_name; -- PostgreSQL
```

---

### **200. Write a query to list employees grouped by their first letter of the name.**  
```sql
SELECT LEFT(Name, 1) AS Initial, COUNT(*) AS EmployeeCount FROM Employees GROUP BY LEFT(Name, 1);
```

---

# Comprehensive Topics

**Full hierarchical structure of SQL joins**, categorized and organized for better understanding:

---

### **1. Joins Overview**
Joins in SQL can be divided into two main categories:
1. **Standard Joins**: Include INNER, OUTER (LEFT, RIGHT, FULL), and CROSS joins.  
2. **Specialized Joins**: Include SELF JOIN, EQUI JOIN, NON-EQUI JOIN, NATURAL JOIN, and LATERAL JOIN.

---

### **2. Standard Joins (Primary Categories)**

#### **2.1. INNER JOIN**
- Returns rows where there is a match in both tables.  
- **Variations:**
  - **Equi Join**: Matches rows using `=` operator.
  - **Non-Equi Join**: Matches rows using conditions other than `=` (e.g., `<`, `>`, `BETWEEN`).

#### **2.2. OUTER JOIN**
- Returns matched and unmatched rows from one or both tables.
- **Types:**
  1. **LEFT JOIN (LEFT OUTER JOIN):** Returns all rows from the left table and matched rows from the right table.  
  2. **RIGHT JOIN (RIGHT OUTER JOIN):** Returns all rows from the right table and matched rows from the left table.  
  3. **FULL JOIN (FULL OUTER JOIN):** Returns all rows from both tables, matched and unmatched.

#### **2.3. CROSS JOIN**
- Produces a Cartesian product of two tables (all possible combinations of rows).

---

### **3. Specialized Joins (Derived Categories)**

#### **3.1. SELF JOIN**
- A join where a table is joined with itself.
- Typically uses INNER JOIN or OUTER JOIN logic.

#### **3.2. NATURAL JOIN**
- Matches rows automatically using columns with the same name and compatible data types in both tables.
- **Limitations:** Avoids explicit `ON` condition, making it less flexible.

#### **3.3. LATERAL JOIN**
- A special type of join that allows a subquery in the `FROM` clause to reference columns from preceding tables.  
- Typically implemented using `CROSS APPLY` or `OUTER APPLY` in some databases.

#### **3.4. ANTI JOIN (Simulated with NOT IN or NOT EXISTS)**
- Returns rows from one table that **do not** have a match in the other table.
- Simulated using:
  ```sql
  SELECT * FROM TableA
  WHERE TableA.ID NOT IN (SELECT TableB.ID FROM TableB);
  ```

#### **3.5. SEMI JOIN (Simulated with EXISTS)**
- Returns rows from one table where matches exist in the other table.
- Simulated using:
  ```sql
  SELECT * FROM TableA
  WHERE EXISTS (SELECT 1 FROM TableB WHERE TableB.ID = TableA.ID);
  ```

---

### **4. Full Hierarchical Structure of Joins**

```
SQL Joins
│
├── Standard Joins
│   ├── INNER JOIN
│   │   ├── Equi Join (uses "=" for matching)
│   │   └── Non-Equi Join (uses "<", ">", "BETWEEN", etc.)
│   ├── OUTER JOIN
│   │   ├── LEFT JOIN (LEFT OUTER JOIN)
│   │   ├── RIGHT JOIN (RIGHT OUTER JOIN)
│   │   └── FULL JOIN (FULL OUTER JOIN)
│   └── CROSS JOIN (Cartesian Product)
│
├── Specialized Joins
│   ├── SELF JOIN (Table joined with itself)
│   ├── NATURAL JOIN (Automatic column matching)
│   ├── LATERAL JOIN (Uses CROSS APPLY / OUTER APPLY)
│   ├── ANTI JOIN (Simulated with NOT IN or NOT EXISTS)
│   └── SEMI JOIN (Simulated with EXISTS)
```

---

### **Comparison of Join Types**

| **Join Type**          | **Description**                                         | **Example Usage**                                       |
|-------------------------|---------------------------------------------------------|--------------------------------------------------------|
| **INNER JOIN**          | Matches rows in both tables.                           | `Employees INNER JOIN Departments ON ...`             |
| **LEFT JOIN**           | All rows from the left table and matched rows from right.| `Employees LEFT JOIN Departments ON ...`              |
| **RIGHT JOIN**          | All rows from the right table and matched rows from left.| `Employees RIGHT JOIN Departments ON ...`             |
| **FULL JOIN**           | All rows from both tables, matched and unmatched.      | `Employees FULL JOIN Departments ON ...`              |
| **CROSS JOIN**          | Cartesian product of two tables.                      | `Employees CROSS JOIN Departments`                    |
| **SELF JOIN**           | Join a table to itself.                                | Compare rows within the same table.                   |
| **NATURAL JOIN**        | Matches using same-named columns.                     | Avoids explicit `ON` condition.                       |
| **LATERAL JOIN**        | References outer query columns in subqueries.          | `CROSS APPLY` for row-wise subquery results.           |
| **ANTI JOIN**           | Rows in one table not present in another.             | Simulated using `NOT IN` or `NOT EXISTS`.             |
| **SEMI JOIN**           | Rows in one table that have matches in another.       | Simulated using `EXISTS`.                             |

---

### **Key Points to Remember**
1. **INNER JOIN**: Most commonly used; returns matching rows.  
2. **OUTER JOIN**: Useful for preserving unmatched rows.  
3. **SELF JOIN**: Used for hierarchical data or relationships within the same table.  
4. **LATERAL JOIN**: Allows subqueries to reference outer query columns.  
5. **CROSS JOIN**: Should be avoided unless explicitly needed (e.g., generating combinations).  
6. **ANTI JOIN** and **SEMI JOIN**: Useful for filtering data.

---


### **What is a Join?**
A **join** in SQL combines rows from two or more tables based on a related column between them. It allows you to retrieve data spread across multiple tables by establishing a relationship.

---

### **Types of Joins**
Joins are categorized into **five main types**:
1. **INNER JOIN**  
2. **LEFT JOIN (LEFT OUTER JOIN)**  
3. **RIGHT JOIN (RIGHT OUTER JOIN)**  
4. **FULL JOIN (FULL OUTER JOIN)**  
5. **CROSS JOIN**

---

### **1. INNER JOIN**
- Combines rows from two tables where there is a **match** in the specified columns.
- Rows without matches are excluded.

**Syntax:**
```sql
SELECT table1.column1, table2.column2 
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:**
**Tables:**

**Employees Table**  
| EmployeeID | Name  | DepartmentID |
|------------|-------|--------------|
| 1          | Alice | 101          |
| 2          | Bob   | 102          |
| 3          | Charlie | 103        |

**Departments Table**  
| DepartmentID | DepartmentName |
|--------------|----------------|
| 101          | HR             |
| 102          | IT             |

**Query:**
```sql
SELECT Employees.Name, Departments.DepartmentName
FROM Employees
INNER JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

**Output:**
| Name  | DepartmentName |
|-------|----------------|
| Alice | HR             |
| Bob   | IT             |

---

### **2. LEFT JOIN (LEFT OUTER JOIN)**
- Returns all rows from the **left table** and the matched rows from the right table.
- If no match exists, `NULL` is returned for the columns from the right table.

**Syntax:**
```sql
SELECT table1.column1, table2.column2 
FROM table1
LEFT JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:**
**Query:**
```sql
SELECT Employees.Name, Departments.DepartmentName
FROM Employees
LEFT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

**Output:**
| Name     | DepartmentName |
|----------|----------------|
| Alice    | HR             |
| Bob      | IT             |
| Charlie  | NULL           |

---

### **3. RIGHT JOIN (RIGHT OUTER JOIN)**
- Returns all rows from the **right table** and the matched rows from the left table.
- If no match exists, `NULL` is returned for the columns from the left table.

**Syntax:**
```sql
SELECT table1.column1, table2.column2 
FROM table1
RIGHT JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:**
**Query:**
```sql
SELECT Employees.Name, Departments.DepartmentName
FROM Employees
RIGHT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

**Output:**
| Name   | DepartmentName |
|--------|----------------|
| Alice  | HR             |
| Bob    | IT             |
| NULL   | Sales          |

---

### **4. FULL JOIN (FULL OUTER JOIN)**
- Combines the result of both **LEFT JOIN** and **RIGHT JOIN**.
- Returns all rows from both tables. If no match exists, `NULL` is returned for unmatched columns.

**Syntax:**
```sql
SELECT table1.column1, table2.column2 
FROM table1
FULL JOIN table2
ON table1.common_column = table2.common_column;
```

**Example:**
**Query:**
```sql
SELECT Employees.Name, Departments.DepartmentName
FROM Employees
FULL JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

**Output:**
| Name     | DepartmentName |
|----------|----------------|
| Alice    | HR             |
| Bob      | IT             |
| Charlie  | NULL           |
| NULL     | Sales          |

---

### **5. CROSS JOIN**
- Combines each row from the first table with **every row** in the second table (Cartesian product).
- No condition is required.

**Syntax:**
```sql
SELECT table1.column1, table2.column2 
FROM table1
CROSS JOIN table2;
```

**Example:**
**Query:**
```sql
SELECT Employees.Name, Departments.DepartmentName
FROM Employees
CROSS JOIN Departments;
```

**Output:**
| Name     | DepartmentName |
|----------|----------------|
| Alice    | HR             |
| Alice    | IT             |
| Bob      | HR             |
| Bob      | IT             |
| Charlie  | HR             |
| Charlie  | IT             |

---

### **Self Join**
- A self join is when a table is joined with itself.
- Useful for hierarchical or relational data.

**Syntax:**
```sql
SELECT A.column1, B.column2 
FROM table A
INNER JOIN table B
ON A.common_column = B.common_column;
```

**Example:**
**Employees Table:**  
| EmployeeID | Name     | ManagerID |
|------------|----------|-----------|
| 1          | Alice    | NULL      |
| 2          | Bob      | 1         |
| 3          | Charlie  | 1         |

**Query:**
```sql
SELECT A.Name AS Employee, B.Name AS Manager
FROM Employees A
LEFT JOIN Employees B
ON A.ManagerID = B.EmployeeID;
```

**Output:**
| Employee | Manager |
|----------|---------|
| Alice    | NULL    |
| Bob      | Alice   |
| Charlie  | Alice   |

---

### **Key Differences Between Joins**

| **Join Type**    | **Includes Unmatched Rows** | **Matched Rows** |
|-------------------|----------------------------|------------------|
| **INNER JOIN**    | No                         | Yes              |
| **LEFT JOIN**     | Yes (left table only)      | Yes              |
| **RIGHT JOIN**    | Yes (right table only)     | Yes              |
| **FULL JOIN**     | Yes (both tables)          | Yes              |
| **CROSS JOIN**    | N/A                        | Cartesian product|

---

### **Best Practices**
1. Use **INNER JOIN** for common matches between tables.  
2. Use **LEFT JOIN** or **RIGHT JOIN** for partial matches with one-sided completeness.  
3. Avoid **CROSS JOIN** unless the Cartesian product is required.  
4. Index join columns for better performance.

---

The terms like **self join**, **equi join**, **lateral join**, etc., are specific types or variations of SQL joins that expand on the primary categories of joins. Here’s a breakdown of these types and how they relate to the main join categories:

---

### **1. Self Join**
- **Definition:** A self join occurs when a table is joined with itself.
- **Category:** It is usually an **INNER JOIN** or **LEFT JOIN** where the same table is used on both sides of the join.
- **Use Case:** Used for hierarchical or relationship-based data.

**Example:**
```sql
SELECT A.EmployeeID AS Employee, B.EmployeeID AS Manager
FROM Employees A
LEFT JOIN Employees B
ON A.ManagerID = B.EmployeeID;
```

**Output:** Compares rows within the same table.

---

### **2. Equi Join**
- **Definition:** A join where the condition is based on equality between columns in both tables (`=` operator).
- **Category:** This is a **subset of INNER JOIN** or other joins.
- **Use Case:** Most commonly used join type when matching rows based on key columns.

**Example:**
```sql
SELECT Employees.Name, Departments.DepartmentName
FROM Employees
INNER JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

**Output:** Rows where `DepartmentID` matches in both tables.

---

### **3. Non-Equi Join**
- **Definition:** A join where the condition is not based on equality (e.g., `<`, `>`, `BETWEEN`).
- **Category:** Variation of **INNER JOIN** or **OUTER JOIN**.
- **Use Case:** Useful for range comparisons.

**Example:**
```sql
SELECT E.Name, S.Grade
FROM Employees E
JOIN Salaries S
ON E.Salary BETWEEN S.MinSalary AND S.MaxSalary;
```

**Output:** Rows where salary falls within a range.

---

### **4. Lateral Join**
- **Definition:** A **lateral join** allows a subquery in the `FROM` clause to reference columns from preceding tables.
- **Category:** Typically used with `CROSS APPLY` or `OUTER APPLY`.
- **Use Case:** Extracts specific data for each row in the preceding table.

**Example:**
```sql
SELECT E.Name, S.TopSkill
FROM Employees E
CROSS APPLY (
    SELECT Skill AS TopSkill 
    FROM Skills S
    WHERE S.EmployeeID = E.EmployeeID
    ORDER BY Proficiency DESC
    LIMIT 1
) S;
```

**Output:** Each employee’s top skill.

---

### **5. Cross Join**
- **Definition:** Combines every row from one table with every row from another (Cartesian product).
- **Category:** Independent join type.
- **Use Case:** Used when no relationship exists between the tables, or for generating combinations.

**Example:**
```sql
SELECT E.Name, D.DepartmentName
FROM Employees E
CROSS JOIN Departments D;
```

**Output:** All possible combinations of employees and departments.

---

### **6. Natural Join**
- **Definition:** A join that automatically matches columns with the same names in both tables.
- **Category:** Typically an **INNER JOIN** with automatic column matching.
- **Use Case:** Simplifies join syntax if column names match.

**Example:**
```sql
SELECT * 
FROM Employees
NATURAL JOIN Departments;
```

**Output:** Rows where column names and values match.

---

### **7. Outer Joins Variations**
- These are **LEFT JOIN**, **RIGHT JOIN**, and **FULL JOIN**.
- Used to include unmatched rows from one or both tables.

---

### **Comparison of Join Types**

| **Join Type**       | **Belongs To**      | **Key Feature**                                           |
|----------------------|---------------------|----------------------------------------------------------|
| **Self Join**        | INNER/LEFT JOIN     | Joins a table to itself.                                 |
| **Equi Join**        | INNER JOIN          | Matches rows using `=` operator.                        |
| **Non-Equi Join**    | INNER/OUTER JOIN    | Matches rows with range or inequality conditions.        |
| **Lateral Join**     | Special Join        | Allows subquery referencing previous tables.             |
| **Cross Join**       | Independent         | Returns Cartesian product of two tables.                |
| **Natural Join**     | INNER JOIN          | Matches columns with the same names automatically.       |
| **Outer Joins**      | LEFT/RIGHT/FULL     | Includes unmatched rows from one or both tables.         |

---

### **Key Points**
1. **Self Join, Equi Join, and Non-Equi Join** are techniques that utilize **INNER JOIN** or other standard joins.
2. **Lateral Join and Cross Join** are independent categories with specific use cases.
3. **Natural Join** simplifies syntax but requires matching column names.







---



# Some Interview question queries

`1`

```sql
SELECT YEAR(Order_date) AS Years, MONTH(Order_date) AS Months, SUM(Sales) AS TotalSales
FROM Products
GROUP BY YEAR(Order_date), MONTH(Order_date)
ORDER BY TotalSales DESC;
```
`2`













---

## Test Question Check

`1`

`Is this correct or not`

```sql
select count(*) as count from train_details_tbl
    where train_from = (select station_name from train_stations_tbl where station_name = 'NEW DELHI')
    and
    train_to = (select station_name from train_stations_tbl where station_name = 'MUMBAI CENTRAL' OR 'BHOPAL');
```



---

$$
\text{End Of File}
$$
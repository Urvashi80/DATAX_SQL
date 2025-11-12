# DATAX_SQL
Create Database and Perform queries. 
📁 SQLite Basic Operations Example

This project provides a simple, self-contained guide and demonstration of fundamental database operations (CRUD: Create, Read, Update, Delete) using SQLite.

This is the code for an application that uses a simple two-table schema (Employee and Departments) to illustrate standard SQL queries.

🛠️ Prerequisites

To run these commands, you need a SQLite client installed on your system.

SQLite: Command Line Tool (sqlite3 or equivalent).

🚀 Setup

Follow these steps to set up the database and create the tables.

1. Start SQLite

Open your terminal or command prompt and start the SQLite command-line interface:

sqlite3 employees.db


2. Create Tables

We will create two tables: Departments and Employee. Note that we are using the column name DeptmentId as per our previous debugging session.

-- 1. Create the Departments table first
CREATE TABLE Departments (
    ID INTEGER PRIMARY KEY,
    DepartmentName TEXT NOT NULL
);

-- 2. Create the Employee table
CREATE TABLE Employee (
    EmplId INTEGER PRIMARY KEY,
    Name TEXT NOT NULL,
    Salary REAL,
    DeptmentId INTEGER,
    FOREIGN KEY (DeptmentId) REFERENCES Departments(ID)
);


3. Verify Schema

You can confirm the table structure using the PRAGMA table_info command:

PRAGMA table_info(Employee);
PRAGMA table_info(Departments);


📚 Basic SQL Queries (CRUD & More)

Here are the essential queries demonstrated using the created tables.

1. INSERT (Create)

Adding new data into the tables.

-- Insert data into Departments
INSERT INTO Departments (ID, DepartmentName) VALUES (10, 'Marketing');
INSERT INTO Departments (ID, DepartmentName) VALUES (20, 'Engineering');
INSERT INTO Departments (ID, DepartmentName) VALUES (30, 'Sales');

-- Insert data into Employee
INSERT INTO Employee (EmplId, Name, Salary, DeptmentId) VALUES (101, 'Alice Johnson', 60000.00, 10);
INSERT INTO Employee (EmplId, Name, Salary, DeptmentId) VALUES (102, 'Bob Smith', 75000.00, 20);
INSERT INTO Employee (EmplId, Name, Salary, DeptmentId) VALUES (103, 'Charlie Brown', 80000.00, 20);
INSERT INTO Employee (EmplId, Name, Salary, DeptmentId) VALUES (104, 'Diana Prince', 55000.00, 10);
INSERT INTO Employee (EmplId, Name, Salary, DeptmentId) VALUES (105, 'Eve Adams', 90000.00, NULL); -- Employee not yet assigned to a department


2. SELECT (Read)

Retrieving data from the tables.

Query Type

Description

SQL Command

All Columns

Select everything from a table.

SELECT * FROM Employee;

Specific Columns

Select only the Name and Salary.

SELECT Name, Salary FROM Employee;

Filtering (WHERE)

Select employees earning more than $70,000.

SELECT Name FROM Employee WHERE Salary > 70000;

Sorting (ORDER BY)

Select all employees, sorted by salary descending.

SELECT * FROM Employee ORDER BY Salary DESC;

3. UPDATE

Changing existing data in the tables.

-- Increase Alice Johnson's salary
UPDATE Employee
SET Salary = 65000.00
WHERE Name = 'Alice Johnson';

-- Update an employee's department
UPDATE Employee
SET DeptmentId = 30
WHERE EmplId = 105;


4. DELETE

Removing data from the tables.

-- Delete a specific employee
DELETE FROM Employee
WHERE EmplId = 104;

-- Delete an entire department (only possible if no employees reference it)
-- DELETE FROM Departments WHERE ID = 30;


5. Advanced Queries

A. Grouping and Aggregation (The fixed query!)

Count the number of employees in each department.

SELECT
    DeptmentId,
    COUNT(EmplId) AS Employee_Count
FROM
    Employee
GROUP BY
    DeptmentId;


B. Joining Tables

Combine employee names with their full department names using an INNER JOIN.

SELECT
    E.Name,
    E.Salary,
    D.DepartmentName
FROM
    Employee AS E
INNER JOIN
    Departments AS D
ON
    E.DeptmentId = D.ID;

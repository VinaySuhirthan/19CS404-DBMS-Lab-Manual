# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Attendance with the following constraints:
- AttendanceID as INTEGER should be the primary key.
- EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
- AttendanceDate as DATE.
- Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
CREATE TABLE Attendance(
AttendanceID INTEGER, 
EmployeeID INTEGER,
AttendanceDate DATE,
Status TEXT CHECK(Status IN('Present','Absent','Leave')),
FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1076" height="129" alt="image" src="https://github.com/user-attachments/assets/a2fec63b-e113-419c-a6ac-48cde04e92b3" />


**Question 2**
---
Create a table named Locations with the following columns:
- LocationID as INTEGER
- LocationName as TEXT
- Address as TEXT

```sql
CREATE TABLE Locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT
);
```

**Output:**

<img width="1833" height="327" alt="image" src="https://github.com/user-attachments/assets/407e7673-d40c-464f-98f8-19294f354c87" />


**Question 3**
---
Create a new table named contacts with the following specifications:
- contact_id as INTEGER and primary key.
- first_name as TEXT and not NULL.
- last_name as TEXT and not NULL.
- email as TEXT.
- phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```sql
CREATE TABLE contacts(
contact_id INTEGER PRIMARY KEY,
first_name TEXT NOT NULL,
last_name TEXT NOT NULL,
email TEXT,
phone TEXT NOT NULL CHECK (LENGTH(phone)>=10)
);
```

**Output:**

<img width="1759" height="205" alt="image" src="https://github.com/user-attachments/assets/7694de92-0ac4-46d5-bf6b-ad1882069f97" />


**Question 4**
---
Write a SQL Query  to Rename attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date,State as varchar(30) in the table Companies. 

```sql
ALTER TABLE Companies RENAME COLUMN name to first_name;
ALTER TABLE Companies ADD mobilenumber number;
ALTER TABLE Companies ADD DOB Date;
ALTER TABLE Companies ADD State varchar(30);
 
```

**Output:**

<img width="1887" height="412" alt="image" src="https://github.com/user-attachments/assets/7050b004-8849-49ed-abc5-0b98ab85cdc7" />


**Question 5**
---
Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

```sql
ALTER TABLE Student_details ADD MobileNumber NUMBER;
ALTER TABLE Student_details ADD Address VARCHAR(100);
```

**Output:**

<img width="1790" height="365" alt="image" src="https://github.com/user-attachments/assets/f0a853f3-8dc9-481b-8f1d-853251460b6d" />


**Question 6**
---
Create a table named Employees with the following constraints:

- EmployeeID should be the primary key.
- FirstName and LastName should be NOT NULL.
- Email should be unique.
- Salary should be greater than 0.
- DepartmentID should be a foreign key referencing the Departments table.

```sql
CREATE TABLE Employees (
EmployeeID INTEGER PRIMARY KEY,
FirstName TEXT NOT NULL,
LastName TEXT NOT NULL, 
Email TEXT UNIQUE,
Salary INTEGER CHECK (Salary>0),
DepartmentID INTEGER,
FOREIGN KEY (DepartmentID)REFERENCES Departments
);
```

**Output:**

<img width="1782" height="363" alt="image" src="https://github.com/user-attachments/assets/1e0f67d6-cbc2-403e-a4f3-abe103bbdaca" />


**Question 7**
---
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

```sql
INSERT INTO Customers(CustomerID,Name,Address,City,ZipCode) VALUES (301,'Michael Jordan','123 Maple St', 'Chicago',60616);
```

**Output:**

<img width="1884" height="231" alt="image" src="https://github.com/user-attachments/assets/c470295e-c070-4f05-8dad-4441f33802a8" />


**Question 8**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

```sql
INSERT INTO Employee (EmployeeID, Name, Department, Salary)
SELECT EmployeeID, Name, Department, Salary
FROM Former_employees;
```

**Output:**

<img width="1311" height="278" alt="image" src="https://github.com/user-attachments/assets/ded17bfb-23d3-486a-9643-c560e043d750" />


**Question 9**
---
Create a table named Customers with the following columns:

-CustomerID as INTEGER
- Name as TEXT
- Email as TEXT
- JoinDate as DATETIME
```sql
CREATE TABLE Customers(

CustomerID INTEGER,
Name  TEXT,
Email  TEXT,
JoinDate  DATETIME 
);
```

**Output:**

<img width="1656" height="280" alt="image" src="https://github.com/user-attachments/assets/660325e3-77d9-4faf-97f4-c59e815a0a54" />


**Question 10**
---
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

| ProductID | Name             | Category     | Price   | Stock |
|------------|------------------|--------------|---------|-------|
| 106        | Fitness Tracker  | Wearables    | NULL    | NULL  |
| 107        | Laptop           | Electronics  | 999.99  | 50    |
| 108        | Wireless Earbuds | Accessories  | NULL    | 100   |


```sql

INSERT INTO Products (ProductID,Name,Category) VALUES (106,'Fitness Tracker','Wearables');
INSERT INTO Products(ProductID,Name,Category,Price,Stock) VALUES (107,'Laptop','Electronic',999.99,50);
INSERT INTO Products(ProductID,Name,Category,Stock) VALUES (108,'Wireless Earbud','Accessorie',100);
 
```

**Output:**

<img width="1811" height="306" alt="image" src="https://github.com/user-attachments/assets/30860e7b-ff40-4fad-8470-35c5eb5edd28" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

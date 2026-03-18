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
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0


```sql
CREATE TABLE PRODUCTS
(
product_id INT PRIMARY KEY,
product_name VARCHAR(20),
list_price DECIMAL(10,2) NOT NULL,
discount DECIMAL(10,2) DEFAULT 0 NOT NULL,
CONSTRAINT products CHECK(list_price>=discount AND discount>=0 AND list_price>=0)
);
```

**Output:**

<img width="1333" height="202" alt="image" src="https://github.com/user-attachments/assets/70bacf1d-9101-44cd-bdca-f640d388ac1c" />


**Question 2**
---
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

```sql
insert into Customers select * from Old_customers;
```

**Output:**

<img width="1314" height="215" alt="image" src="https://github.com/user-attachments/assets/6a31887d-b679-48db-9068-271ccb2de65a" />


**Question 3**
---
Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.

```sql
insert into Employee values (001,'Sarah Parker','Manager','HR',60000);
```

**Output:**

<img width="1066" height="180" alt="image" src="https://github.com/user-attachments/assets/e1c0ae8b-3508-4a11-bce7-89f6affa93f5" />


**Question 4**
---
Write an SQL query to add two new columns, designation and net_salary, to the table Companies. The designation column should have a data type of varchar(50), and the net_salary column should have a data type of number.

```sql
alter table Companies
add column designation varchar(50); 
alter table Companies add column net_salary number;
```

**Output:**

<img width="1063" height="270" alt="image" src="https://github.com/user-attachments/assets/d803239d-aec4-4199-b667-00b4bc6acce1" />


**Question 5**
---
Create a table named Departments with the following columns:

DepartmentID as INTEGER
DepartmentName as TEXT

```sql
create table Departments 
(
DepartmentID INTEGER,
DepartmentName TEXT
);
```

**Output:**

<img width="1116" height="263" alt="image" src="https://github.com/user-attachments/assets/43201f14-5a60-4a6d-8aef-07c82f702677" />


**Question 6**
---
Write a SQL query to Add a new column Mobilenumber as number in the Student_details table.

Sample table: Student_details

 cid              name             type             notnu  dflt_value  pk
---------------  ---------------  ---------------  -----  ----------  ----------
0                RollNo           int              0                  1
1                Name             VARCHAR(100)     1                  0
2                Gender           TEXT             1                  0
3                Subject          VARCHAR(30)      0                  0
4                MARKS            INT (3)          0                  0
For example:

```sql
alter table Student_details add column Mobilenumber number;
```

**Output:**

<img width="1083" height="257" alt="image" src="https://github.com/user-attachments/assets/bd2e6cc5-efb4-4bf7-b3ed-26d2429f3374" />


**Question 7**
---
Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE

```sql
create table Events
(
EventID INTEGER,
EventName TEXT,
EventDate DATE
);
```

**Output:**

<img width="1213" height="269" alt="image" src="https://github.com/user-attachments/assets/49d2ffc7-c4c7-4cce-8421-d3bdc6918def" />


**Question 8**
---
Create a table named Products with the following columns:

ProductID as INTEGER
ProductName as TEXT
Price as REAL
Stock as INTEGER

```sql
create table Products
(
ProductID INTEGER,
ProductName TEXT,
Price REAL,
Stock INTEGER
);
```

**Output:**

<img width="1100" height="228" alt="image" src="https://github.com/user-attachments/assets/402ee1c7-9f9e-4d92-b7af-0863ed2f729d" />


**Question 9**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

```sql
insert into products (ProductID,Name,Category) values (104,'Tablet','Electronics');
```

**Output:**

<img width="1274" height="195" alt="image" src="https://github.com/user-attachments/assets/63fea215-6749-4162-9f3f-8a194326ca61" />


**Question 10**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

```sql
create table ProjectAssignments
(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY(ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

<img width="1340" height="204" alt="image" src="https://github.com/user-attachments/assets/03ac08ce-0f65-43b2-ac13-0d152d5a0d93" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

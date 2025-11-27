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
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

| RollNo | Name            | Gender | Subject      | Marks |
|--------|-----------------|--------|--------------|-------|
| 205    | Olivia Green    | F      |              |       |
| 207    | Liam Smith      | M      | Mathematics  | 85    |
| 208    | Sophia Johnson  | F      | Science      |       |

```sql
Insert into Student_details values(205, "Olivia Green", 'F', null, null);
Insert into Student_details values(207, "Liam Smith", 'M', "Mathematics", 85);
Insert into Student_details values(208, "Sophia Johnson", 'F', "Science", null);
```

**Output:**

<img width="1691" height="521" alt="image" src="https://github.com/user-attachments/assets/ffa0010c-3b6d-4b52-9b2f-886234a0eb6a" />

**Question 2**
---
Insert all students from Archived_students table into the Student_details table.

| cid | name    | type          | notnull | dflt_value | pk |
|-----|---------|---------------|---------|------------|----|
| 0   | RollNo  | INT           | 0       |            | 1  |
| 1   | Name    | VARCHAR(100)  | 0       |            | 0  |
| 2   | Gender  | VARCHAR(10)   | 0       |            | 0  |
| 3   | Subject | VARCHAR(50)   | 0       |            | 0  |
| 4   | MARKS   | INT           | 0       |            | 0  |

```sql
Insert into student_details Select * from Archived_students;
```

**Output:**

<img width="1608" height="495" alt="image" src="https://github.com/user-attachments/assets/21fd1d19-035f-4270-9c16-5b225b0f5165" />

**Question 3**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.

```sql
Create table item(
    item_id TEXT PRIMARY KEY,
    item_desc TEXT not null,
    rate INTEGER not null,
    icom_id TEXT CHECK(length(icom_id) >= 4),
    foreign key (icom_id) references company(com_id) on update cascade on delete cascade
);
```

**Output:**

<img width="1604" height="578" alt="image" src="https://github.com/user-attachments/assets/c1c6052e-2616-4eed-8624-6db1becac01d" />

**Question 4**
---
Create a table named Attendance with the following constraints:
  AttendanceID as INTEGER should be the primary key.
  EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
  AttendanceDate as DATE.
  Status as TEXT should be one of 'Present', 'Absent', 'Leave'.

```sql
create table Attendance(
    AttendanceID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    AttendanceDate  DATE,
        Status TEXT CHECK(Status IN ('Present', 'Absent', 'Leave')),
        FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1606" height="483" alt="image" src="https://github.com/user-attachments/assets/3ed04652-8967-4659-b41c-8ab6bbc0d461" />

**Question 5**
---
Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'

```sql
alter table Student_details add column email TEXT not null default 'Invalid';
```

**Output:**

<img width="1608" height="429" alt="image" src="https://github.com/user-attachments/assets/3cb8e3da-ee0b-489f-b511-44a67d4d18a1" />

**Question 6**
---
Create a table named Employees with the following constraints:
  EmployeeID should be the primary key.
  FirstName and LastName should be NOT NULL.
  Email should be unique.
  Salary should be greater than 0.
  DepartmentID should be a foreign key referencing the Departments table.

```sql
create table Employees(
    EmployeeID int PRIMARY KEY,
    FirstName TEXT not null,
    LastName TEXT not null,
    Email TEXT unique,
    Salary int check(Salary > 0),
    DepartmentID int,
    Foreign key (DepartmentID) references Departments(DepartmentID)
);
```

**Output:**

<img width="1607" height="679" alt="image" src="https://github.com/user-attachments/assets/e77af0c6-3191-4142-8df6-9ddd63466fc5" />

**Question 7**
---
Create a table named Invoices with the following constraints:
  InvoiceID as INTEGER should be the primary key.
  InvoiceDate as DATE.
  DueDate as DATE should be greater than the InvoiceDate.
  Amount as REAL should be greater than 0.

```sql
create table Invoices(
    InvoiceID  Integer PRIMARY KEY,
    InvoiceDate DATE,
    DueDate DATE CHECK(DueDate > InvoiceDate),
    Amount REAL CHECK(Amount > 0)
);
```

**Output:**

<img width="1608" height="486" alt="image" src="https://github.com/user-attachments/assets/51536a0b-d91c-46de-bddc-e8de1b913e79" />

**Question 8**
---
Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.

```sql
alter table employee add column department_id INTEGER;
alter table employee add column manager_id INTEGER default NULL;
```

**Output:**

<img width="1602" height="525" alt="image" src="https://github.com/user-attachments/assets/812cb35c-fd50-4a20-9fd4-e9049f8e4ce3" />

**Question 9**
---
Insert a book with ISBN 978-1234567890, Title Data Science Essentials, Author Jane Doe, Publisher TechBooks, and Year 2024 into the Books table.

```sql
Insert into Books values(
     "978-1234567890",
     "Data Science Essentials",
     "Jane Doe",
     "TechBooks",
     2024
);
```

**Output:**

<img width="1611" height="429" alt="image" src="https://github.com/user-attachments/assets/8eef4b6e-9ab0-4186-b82a-d7f9bad4d76a" />

**Question 10**
---
Create a table named Customers with the following columns:
  CustomerID as INTEGER
  Name as TEXT
  Email as TEXT
  JoinDate as DATETIME

```sql
create table Customers(
    CustomerID INTEGER,
    Name TEXT,
    Email TEXT,
    JoinDate DATETIME
);
```

**Output:**

<img width="1608" height="644" alt="image" src="https://github.com/user-attachments/assets/bb2084f0-d00e-4170-a003-5cc669ecbfab" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

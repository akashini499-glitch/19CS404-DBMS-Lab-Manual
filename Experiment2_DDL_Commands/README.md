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
--In the Employee table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT
 

For example:

Test	Result
SELECT * FROM Employee;
EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT


```sql
-- INSERT INTO EMPLOYEE(EmployeeID,Name,Position,Department,Salary)
VALUES(5,'George Clark','Consultant',NULL,NULL);

INSERT INTO EMPLOYEE(EmployeeID,Name,Position,Department,Salary)
VALUES(7,'Noah Davis','Manager','HR',60000);

INSERT INTO Employee(EmployeeID,Name,Position,Department,Salary)
VALUES(8,'Ava Miller','Consultant','IT',NULL);
```

**Output:**

<img width="1216" height="361" alt="image" src="https://github.com/user-attachments/assets/11493641-ac2e-46c6-8fd8-83b926d4937c" />


**Question 2**
---
-- create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.
For example:

Test	Result
INSERT INTO jobs (job_id, job_title, min_salary, max_salary) VALUES (1, 'Software Engineer', 9000, 15000);
SELECT * FROM jobs;
job_id      job_title          min_salary  max_salary
----------  -----------------  ----------  ----------
1           Software Engineer  9000        15000


```sql
-- CREATE TABLE jobs(
       job_id INT,
       job_title VARCHAR(255) DEFAULT ' ',
       min_salary DECIMAL(10,2) DEFAULT 8000,
       max_salary DECIMAL(10,2) DEFAULT NULL
       );
```

**Output:**
<img width="1222" height="396" alt="image" src="https://github.com/user-attachments/assets/dc155075-0e60-449e-84d1-911517036b41" />


**Question 3**
---
--Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
 
 
For example:

Test	Result
SELECT ISBN, Title, Author
FROM Books 


ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

```sql
-- INSERT INTO Books(ISBN,Title,Author)
VALUES('978-6655443321','Big Data Analytics','Karen Adams');
```

**Output:**
<img width="1228" height="411" alt="image" src="https://github.com/user-attachments/assets/e2d4a35d-8a8a-467b-989a-3f6096be7642" />


**Question 4**
---
-- Write an SQL command can to add a column named email of type TEXT to the customers table

 

For example:

Test	Result
pragma table_info('Customers');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           name        text        0                       0
2           email       TEXT        0                       0


```sql
-- ALTER TABLE Customers ADD COLUMN email TEXT;
```

**Output:**

<img width="1222" height="366" alt="image" src="https://github.com/user-attachments/assets/29d9a14b-41e1-4c02-9103-709979bed543" />


**Question 5**
---
--Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint failed


```sql
-- CREATE TABLE ProjectAssignments(
      AssignmentID INTEGER PRIMARY KEY,
      EmployeeID INTEGER,
      ProjectID INTEGER,
      AssignmentDate DATE NOT NULL,
      FOREIGN KEY(EmployeeID) REFERENCES Employees(EmployeeID),
      FOREIGN KEY(ProjectID) REFERENCES Projects(ProjectID)
      

)
```

**Output:**
<img width="1227" height="360" alt="image" src="https://github.com/user-attachments/assets/476dd1c7-1714-4483-9e74-625804f7f3c0" />


**Question 6**
---
--Write an SQL query to change the name of the column id to employee_id in the table employee.

 

 

 

 

For example:

Test	Result
pragma table_info('employee');
cid         name         type        notnull     dflt_value  pk
----------  -----------  ----------  ----------  ----------  ----------
0           employee_id  integer     0                       0
1           salary       number      0                       0


```sql
--ALTER TABLE employee RENAME COLUMN id TO employee_id;
```

**Output:**

<img width="1222" height="348" alt="image" src="https://github.com/user-attachments/assets/66a8dff8-fb77-42bf-ab08-1ff8ada21ed7" />


**Question 7**
---
-- Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0
For example:

Test	Result
INSERT INTO products (product_id, product_name, list_price) VALUES (2, 'Product B', 50.00);
SELECT * FROM products;
product_id  product_name  list_price  discount
----------  ------------  ----------  ----------
2           Product B     50          0


```sql
--CREATE TABLE products (
       product_id INTEGER,
       product_name TEXT NOT NULL,
       list_price DECIMAL(10,2) NOT NULL,
       discount DECIMAL(10,2) DEFAULT 0 NOT NULL,
       PRIMARY KEY(product_id),
       CHECK(list_price>=discount AND discount >=0 AND list_price >=0)
       


)
```

**Output:**

<img width="1218" height="367" alt="image" src="https://github.com/user-attachments/assets/a799539e-5849-4136-830d-84fa957965f5" />


**Question 8**
---
-- Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
For example:

Test	Result
INSERT INTO Department (DepartmentID, DepartmentName, Location) VALUES (1, 'Human Resources', 'New York');
select * from Department;
DepartmentID  DepartmentName   Location
------------  ---------------  ----------
1             Human Resources  New York

```sql
-- CREATE TABLE Department(
          DepartmentID INTEGER PRIMARY KEY,
          DepartmentName TEXT NOT NULL UNIQUE,
          Location TEXT


);
```

**Output:**

<img width="1220" height="370" alt="image" src="https://github.com/user-attachments/assets/8cd7b4dc-1c12-4d30-802c-a29c56260870" />


**Question 9**
---
-- Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

Test	Result
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
Error: UNIQUE constraint failed: Invoices.InvoiceID


```sql
-- CREATE TABLE Invoices(
       InvoiceID INTEGER PRIMARY KEY,
       InvoiceDate DATE,
       DueDate DATE,
       Amount REAL,
       CHECK(Duedate>=InvoiceDate AND Amount >=0)



);
```

**Output:**

<img width="1227" height="372" alt="image" src="https://github.com/user-attachments/assets/e829550e-af47-420d-bbeb-4adb9d4d0567" />


**Question 10**
---
-- Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

For example:

Test	Result
SELECT * FROM Customers WHERE CustomerID = 301;
CustomerID  Name            Address       City        ZipCode
----------  --------------  ------------  ----------  ----------
301         Michael Jordan  123 Maple St  Chicago     60616

```sql
-- INSERT INTO Customers(CustomerID,Name,Address,City,Zipcode)
VALUES(301,'Michael Jordan','123 Maple St','Chicago','60616');
```

**Output:**

<img width="1233" height="325" alt="image" src="https://github.com/user-attachments/assets/76f6bf70-c4a6-4aca-ae76-2e15172c591b" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

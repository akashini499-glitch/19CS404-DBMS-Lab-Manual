# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
-- Write a SQL query to Delete customers from 'customer' table where 'WORKING_AREA' is 'New York'.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
CUST_CODE   CUST_NAME   CUST_CITY   WORKING_AREA  CUST_COUNTRY  GRADE       OPENING_AMT  RECEIVE_AMT  PAYMENT_AMT  OUTSTANDING_AMT  PHONE_NO    AGENT_CODE
----------  ----------  ----------  ------------  ------------  ----------  -----------  -----------  -----------  ---------------  ----------  ----------
C00001      Micheal     New York    New York      USA           2           3000         5000         2000         6000             CCCCCCC     A008
C00020      Albert      New York    New York      USA           3           5000         7000         6000         6000             BBBBSBB     A008
C00002      Bolt        New York    New York      USA           3           5000         7000         9000         3000             DDNRDRH     A008
changes()
----------
3


```sql
--DELETE FROM customer
WHERE WORKING_AREA='New York';
```

**Output:**

<img width="1242" height="842" alt="image" src="https://github.com/user-attachments/assets/76757868-6a31-4df8-a3b1-dcb3afdeb140" />


**Question 2**
---
--Write a SQL query to delete a specific doctor from Doctors table whose ID is 1.

Sample table: Doctors

attributes: doctor_id, first_name, last_name, specialization


```sql
-- DELETE FROM Doctors
WHERE doctor_id=1;
```

**Output:**

<img width="1231" height="348" alt="image" src="https://github.com/user-attachments/assets/fd2bd23b-b244-4ca7-bb4e-617a92490345" />


**Question 3**
---
--Write a SQL query to retrieve all employee names in lower case. 

Table name: emp

name        type
----------  ----------
empno       INT
ename       VARCHAR(100)
job         VARCHAR(50)
mgr         INT
hiredate    DATE
sal         DECIMAL(10,2)
comm        DECIMAL(10,2)
deptno      INT
For example:

Result
EmpName
----------
king
jones
clark
scott
ford
miller


```sql
--SELECT LOWER(ename) AS EmpName 
FROM emp;
```

**Output:**

<img width="1217" height="367" alt="image" src="https://github.com/user-attachments/assets/dd558af2-913a-497f-b3ac-7047f8612c97" />


**Question 4**
---
-- Write a SQL query to round the decimal column to 3 decimal places from the Calculations table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
 

For example:

Result
id          rounded_value
----------  -------------
1           123.457
2           567.891
3           78.234
4           45.78


```sql
-- SELECT 
id,
ROUND(decimal,3) AS rounded_value
FROM calculations;
```

**Output:**

<img width="1233" height="617" alt="image" src="https://github.com/user-attachments/assets/13271e9f-44a0-41e4-8407-ce11ac7ae96e" />


**Question 5**
---
-- Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql
-- UPDATE Products
SET sell_price=sell_price*1.10
WHERE category='Bakery';
```

**Output:**

<img width="1227" height="418" alt="image" src="https://github.com/user-attachments/assets/233e1aef-4c80-4156-8853-d59cc15f3b78" />


**Question 6**
---
-- Write a query to fetch last 5 rows in EmployeeInfo table.

EmpID

EmpFname

EmpLname

Department

Project

Address

DOB

Gender

1

Sanjay

Mehra

HR

P1

Hyderabad(HYD)

01/12/1976

M

2

Ananya

Mishra

Admin

P2

Delhi(DEL)

02/05/1968

F

 

For example:

Result
EmpID       EmpFname    EmpLname    Department  Project     Address     DOB         Gender
----------  ----------  ----------  ----------  ----------  ----------  ----------  ----------
5           Ankit       Kapoor      Admin       P2          Delhi(DEL)  1994-07-03  M
4           Sonia       Kulkarni    HR          P1          Hyderabad(  1992-05-02  F
3           Rohan       Diwan       Account     P3          Mumbai(BOM  1980-01-01  M
2           Ananya      Mishra      Admin       P2          Delhi(DEL)  1968-05-02  F
1           Sanjay      Mehra       HR          P1          Hyderabad(  1976-12-01  M


```sql
-- SELECT *
FROM EmployeeInfo
ORDER BY EmpID DESC
LIMIT 5;
```

**Output:**

<img width="1230" height="452" alt="image" src="https://github.com/user-attachments/assets/83af46c9-f9e3-43e4-bbdf-802fcdeca107" />


**Question 7**
---
-- Write a SQL query to retrieve the year, month, and day from the hiredate column in the emp table.

For example:

Result
Year        Month       Day
----------  ----------  ----------
1981        04          02
1981        09          28
1981        05          01
1981        06          09
1982        12          09
1981        11          17
1981        09          08


```sql
-- SELECT strftime('%Y',hiredate) AS Year,
       strftime('%m',hiredate) AS Month,
       strftime('%d',hiredate) AS Day
FROM emp;
```

**Output:**

<img width="1235" height="478" alt="image" src="https://github.com/user-attachments/assets/f3b792ce-c730-49e7-80db-6944ea61cfc3" />


**Question 8**
---
-- Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

Sample table: Doctors

attributes: doctor_id, first_name, last_name, specialization

```sql
--DELETE FROM Doctors
WHERE specialization='Pediatrics' AND first_name='Michael';
```

**Output:**

<img width="1235" height="647" alt="image" src="https://github.com/user-attachments/assets/35f4baae-57c8-4ba2-ab3b-10bd36cd2d93" />


**Question 9**
---
-- Write a SQL query to Delete customers from 'customer' table where 'GRADE' is less than 2.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select distinct(grade)from customer;
GRADE
----------
2
3
1
0
GRADE
----------
2
3


```sql
-- DELETE FROM customer
WHERE GRADE<2;
```

**Output:**

<img width="1228" height="540" alt="image" src="https://github.com/user-attachments/assets/a5cfaba8-9b2a-4840-8e8f-ea19735bea51" />


**Question 10**
---
-- Write a SQL query to reduce the reorder level by 30% where cost price is more than 50 and quantity in stock is less than 100 in the products table.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lvl    INT        
quantity       INT        
supplier_id    INT               
For example:

Test	Result
--pragma table_info('products');
select changes();
changes()
----------
2


```sql
--UPDATE products
SET reorder_lvl=reorder_lvl*0.7
WHERE cost_price>50 AND QUANTITY <100;
```

**Output:**

<img width="1228" height="540" alt="image" src="https://github.com/user-attachments/assets/78e8c68e-b85b-4c0d-8788-278f74a23186" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.

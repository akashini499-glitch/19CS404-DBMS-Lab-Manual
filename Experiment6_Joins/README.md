# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
-- Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.

PATIENTS TABLE:



TEST_RESULT TABLES:



For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------
2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01      2

```sql
-- select p.*
from patients p
inner join test_results as t
on p.patient_id=t.patient_id
where t.test_date between '2024-03-01' and '2024-03-31';
```

**Output:**

<img width="1242" height="507" alt="image" src="https://github.com/user-attachments/assets/fbe9be54-de63-44f7-aa15-15afb37b5ee8" />


**Question 2**
---
-- Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'New York'.

Customer Table:



Salesmen Table:



 

For example:

Result
name
---------------
Bob Emily


```sql
-- select s.name
from salesman s
left join customer as c
on s.salesman_id=c.salesman_id
where c.city='New York';
```

**Output:**

<img width="1223" height="492" alt="image" src="https://github.com/user-attachments/assets/32226153-814a-41d5-ae33-48952c2274d4" />


**Question 3**
---
-- Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column. Include conditions to filter for patients discharged between '2024-03-01' and '2024-03-31' but not admitted during the same period.

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE

For example:

Result
first_name       surgery_id       patient_id       surgeon_id       surgery_date
---------------  ---------------  ---------------  ---------------  ------------
Bob              2                2                2                2024-02-28

```sql
-- select p.first_name,s.surgery_id,s.patient_id,s.surgeon_id,s.surgery_date
from patients p
inner join surgeries as s
on p.patient_id=s.patient_id
where p.discharge_date between '2024-03-01' and '2024-03-31';
```

**Output:**

<img width="1227" height="512" alt="image" src="https://github.com/user-attachments/assets/e784d7ad-3f35-42a7-89f5-19fbd85eb83b" />


**Question 4**
---
--Write the SQL query that accomplishes the selection of the first name and last name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:

name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

SURGERIES TABLE:

name             type
---------------  ---------------
surgery_id       INT
patient_id       INT
surgeon_id       INT
surgery_date     DATE

For example:

Result
first_name       last_name
---------------  ---------------
Alice            Williams


```sql
-- select first_name ,last_name 
from patients 
inner join surgeries 
on patients.patient_id=surgeries.patient_id
where surgery_date between '2024-01-01' and '2024-01-31';
```

**Output:**

<img width="1228" height="483" alt="image" src="https://github.com/user-attachments/assets/5c5aa371-c313-4306-aea2-6aca47ff2812" />


**Question 5**
---
-- Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

PATIENTS TABLE:



TEST_RESULT TABLES:



For example:

Result
patient_name     result_id        patient_id       test_name        result      test_date
---------------  ---------------  ---------------  ---------------  ----------  ----------
Alice            1                1                Blood Pressure   120/80      2024-01-20


```sql
-- select p.first_name as patient_name,t.*
from patients p
inner join test_results t on p.patient_id =t.patient_id
where t.test_name='Blood Pressure';
```

**Output:**

<img width="1217" height="505" alt="image" src="https://github.com/user-attachments/assets/3a8b0abb-12f1-4e33-8452-86d4453dc837" />


**Question 6**
---
--From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005
Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
For example:

Result
Customer Name    city             Salesman         commission
---------------  ---------------  ---------------  ---------------
Nick Rimando     Chennai          Bob Emily        0.15
Graham Zusi      California       Nail Knite       0.13
Brad Guzan       London           Pit Alex         0.11
Fabian Johns     Paris            Mc Lyon          0.14
Brad Davis       New York         Bob Emily        0.15
Geoff Cameron    Berlin           Lauson Hen       0.12
Julian Green     London           Nail Knite       0.13
Jozy Altidore    Moscow           Paul Adam        0.13

```sql
-- select c.cust_name as "Customer Name",c.city as "city",s.name as "Salesman",s.commission as "commission"
from customer c
join salesman s on c.salesman_id=s.salesman_id;
```

**Output:**

<img width="1300" height="487" alt="image" src="https://github.com/user-attachments/assets/413e0753-e631-49c4-8bdd-d6c6241c701c" />


**Question 7**
---
--Write the SQL query that achieves the selection of all columns from the "patients" table and the specialization from the "doctors" table (aliased as "doctor_specialization"), with an inner join on the "doctor_id" column.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)

For example:

Result
patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id   doctor_specialization
---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------  ---------------------
1                Alice            Williams         1980-05-12       2024-01-10                      1           Cardiology
2                Bob              Miller           1995-08-23       2024-02-15      2024-03-01      2           Orthopedics
3                Charlie          Davis            1972-11-30       2024-03-10                      3           Pediatrics

```sql
--select p.*,d.specialization as doctor_specialization
from patients p
inner join doctors d on p.doctor_id=d.doctor_id;
```

**Output:**

<img width="1308" height="743" alt="image" src="https://github.com/user-attachments/assets/a43db951-9147-49ed-83dc-3823027994cd" />


**Question 8**
---
--Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "commission" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column.

Customer Table:



Salesmen Table:



 

For example:

Result
cust_name        commission
---------------  ---------------
Nick Rimando     0.15
Graham Zusi      0.13
Brad Guzan       0.11
Fabian Johns     0.14
Brad Davis       0.15
Geoff Cameron    0.12
Julian Green     0.13
Jozy Altidore    0.13


```sql
-- select c.cust_name ,s.commission
from customer c
left join salesman s on c.salesman_id=s.salesman_id;
```

**Output:**

<img width="1308" height="743" alt="Screenshot 2026-09-03 153022" src="https://github.com/user-attachments/assets/e4cad53d-0444-400f-8a4c-918b42e17004" />



**Question 9**
---
-- Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount greater than 1000.

CUSTOMER TABLE:



ORDERS TABLE:



For example:

Result
cust_name        ord_no           ord_date         purch_amt
---------------  ---------------  ---------------  ---------------
Brad Davis       70005            2012-07-27       2400.6
Nick Rimando     70008            2012-09-10       5760.0
Fabian Johns     70010            2012-10-10       1983.43
Geoff Cameron    70003            2012-10-10       2480.4
Nick Rimando     70013            2012-04-25       3045.6


```sql
--select c.cust_name,o.ord_no,o.ord_date,o.purch_amt
from customer c
left join orders o
on c.customer_id=o.customer_id
where o.purch_amt>1000;
```

**Output:**





**Question 10**
---
--Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

NURSES TABLE:



DEPARTMENTS TABLE:



For example:

Result
nurse_id         first_name       last_name        department_id    department_name
---------------  ---------------  ---------------  ---------------  ---------------
1                Emma             Taylor           1                Cardiology
2                David            Moore            2                Orthopedics
3                Sophia           Clark            3                Pediatrics


```sql
-- select n.*,department_name
from nurses n
inner join departments d
on n.department_id=d.department_id;

```

**Output:**

<img width="1297" height="477" alt="image" src="https://github.com/user-attachments/assets/7b27d219-d19d-4100-a0ab-2c0f3f064fea" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.

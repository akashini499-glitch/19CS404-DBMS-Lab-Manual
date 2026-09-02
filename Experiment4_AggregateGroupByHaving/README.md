# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
--Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.

Sample table: customer



 

For example:

Result
COUNT
----------
1


```sql
--SELECT count(*) as COUNT
from customer
where city='Noida';
```

**Output:**

<img width="1232" height="392" alt="image" src="https://github.com/user-attachments/assets/a7b63612-7911-4862-bee6-584acddb84bb" />


**Question 2**
---
-- Write a SQL query to find the average length of email addresses (in characters):

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
avg_email_length
----------------
15.0


```sql
-- SELECT avg(length(email)) as avg_email_length
from customer
```

**Output:**

<img width="1221" height="391" alt="image" src="https://github.com/user-attachments/assets/223157a8-ee6a-4224-8f65-3cde72c28425" />


**Question 3**
---
-- Write a SQL query to find the maximum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MAXIMUM
----------
5760.0


```sql
-- select max(purch_amt) as MAXIMUM
FROM orders
```

**Output:**

<img width="1228" height="397" alt="image" src="https://github.com/user-attachments/assets/6f8c0efc-67a3-496e-9a14-2e6794d79295" />


**Question 4**
---
-- How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT
For example:

Result
ValidityYear  TotalPatients
------------  -------------
2024          3
2025          1
2027          4
2031          2


```sql
-- SELECT SUBSTR(ValidityPeriod,1,4) as ValidityYear,
count(PatientID) as TotalPatients
from Insurance
group by ValidityPeriod
order by ValidityYear ASC;
```

**Output:**

<img width="1207" height="468" alt="image" src="https://github.com/user-attachments/assets/71eb0fae-5914-4146-bee7-933b6804b4de" />


**Question 5**
---
-- How many appointments are scheduled in each hour of the day?

Sample table:Appointments Table

name                              type
--------------------          ----------
AppointmentID               INTEGER
PatientID                         INTEGER
DoctorID                         INTEGER
AppointmentDateTime   DATETIME
Purpose                           TEXT
Status                              TEXT     

For example:

Result
HourOfDay   TotalAppointments
----------  -----------------
09          2
10          5
11          1
14          1
16          1


```sql
-- SELECT strftime('%H',AppointmentDateTime) as HourOfDay,count(AppointmentID) as TotalAppointments
from Appointments
group by HourOfDay
order by HourOfDay;
```

**Output:**

<img width="1227" height="605" alt="image" src="https://github.com/user-attachments/assets/d9fc0fb6-3d30-45d5-899c-6eeea68e4d64" />


**Question 6**
---
-- How many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

Sample tablePrescriptions Table



For example:

Result
Frequency      TotalPrescriptions
-------------  ------------------
Every 3 weeks  1
Every 6 hours  1
Once           1
Once daily     4
Once daily at  1
Pending        1
Twice daily    1


```sql
-- SELECT Frequency,count(*) as TotalPrescriptions
from Prescriptions
group by Frequency
order by Frequency;
```

**Output:**

<img width="1232" height="602" alt="image" src="https://github.com/user-attachments/assets/3e27dbe4-3ec7-4956-8218-0d6e3f8e8bbb" />


**Question 7**
---
-- Write the SQL query that achieves the grouping of data by city, calculates the average income for each city, and includes only those cities where the average income is greater than 500,000.

Sample table: employee



For example:

Result
city        AVG(income)
----------  -----------
Arizona     1000000.0
California  2650000.0
Florida     2675000.0


```sql
-- select city,AVG(income)
from employee
group by city
having avg(income)>500000;

```

**Output:**

<img width="1228" height="525" alt="image" src="https://github.com/user-attachments/assets/06fd212f-9cea-48e9-b830-1e2abbf09896" />


**Question 8**
---
-- Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1



For example:

Result
address     SUM(salary)
----------  -----------
Bhopal      8500
Hyderabad   4500
Indore      10000
Mumbai      6500


```sql
-- select address,SUM(salary)
from customer1
group by address
having SUM(salary)>2000;
```

**Output:**

<img width="1230" height="562" alt="Screenshot 2026-09-02 214257" src="https://github.com/user-attachments/assets/1228d54e-d99c-4404-a6b9-184d8a67fae8" />



**Question 9**
---
-- Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
AVERAGE
----------
1461.765


```sql
-- SELECT AVG(purch_amt) AS AVERAGE
FROM orders
```

**Output:**

<img width="1220" height="392" alt="image" src="https://github.com/user-attachments/assets/8afc3418-a884-43e9-99ff-f0e68f13a725" />


**Question 10**
---
-- Write a SQL query to calculate total purchase amount of all orders. Return total purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

For example:

Result
TOTAL
----------
17541.18


```sql
-- SELECT SUM(purch_amt) AS TOTAL
FROM orders
```

**Output:**

<img width="1222" height="383" alt="image" src="https://github.com/user-attachments/assets/471aa5b4-896b-44bd-963f-db5456b7f01f" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

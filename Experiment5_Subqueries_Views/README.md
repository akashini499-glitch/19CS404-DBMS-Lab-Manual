# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
--Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

For example:

Result
id     name             age              city             income
-----  ---------------  ---------------  ---------------  ----------
101    Peter            32               NewYork          200000
102    Mark             32               California       300000
103    Donald           25               Arizona          1000000
105    Linklon          32               Georgia          250000

```sql
-- select *
from Employee
where age <(
select avg(age)
from Employee
where income>1000000
);
```

**Output:**

<img width="1241" height="505" alt="image" src="https://github.com/user-attachments/assets/2b30d26d-d5db-49a2-ad5e-797ee3861127" />


**Question 2**
---
-- Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
id     name             city             email            phone
-----  ---------------  ---------------  ---------------  ----------
6      Aarti Desai      Pune             aarti@gmail.com  890123456
7      Vivek Sharma     Chandigarh       vivek@gmail.com  980154021
8      Nisha Patel      Noida            nisha@gmail.com  901234567
9      Rajesh Singh     Hyderabad        rajesh@gmail.co  917654301


```sql
--select *
from customer
where city != (
 select city
 from customer
 order by id desc
 limit 1
 );
 
 
```

**Output:**

<img width="1232" height="577" alt="image" src="https://github.com/user-attachments/assets/eec7625f-8e3e-4513-ab78-062931873188" />


**Question 3**
---
--Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
name
---------------
Aarti Desai
Vivek Sharma
Nisha Patel
Rajesh Singh
Radha Iyer


```sql
-- select name 
from customer
where phone in
(
select phone
from customer
group by phone
having count(*)=1
);
```

**Output:**

<img width="1222" height="542" alt="Screenshot 2026-09-02 220910" src="https://github.com/user-attachments/assets/a892aeb0-a3c6-4b3d-8616-3c2b9737ea55" />



**Question 4**
---
-- Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
2           Khilan      25          Delhi       1500


```sql
--select *
from customers
where salary=1500;
```

**Output:**

<img width="1226" height="430" alt="image" src="https://github.com/user-attachments/assets/6981f732-c91c-4a31-97e5-56aa6d888493" />


**Question 5**
---
-- Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

For example:

Result
id     name             age              city             income
-----  ---------------  ---------------  ---------------  ----------
101    Peter            32               NewYork          200000
102    Mark             32               California       300000
103    Donald           25               Arizona          1000000
104    Obama            35               Florida          5000000
105    Linklon          32               Georgia          250000
107    Adam             35               California       5000000


```sql
-- select *
from Employee
where age<(select avg(age)
from Employee
where income>250000);
```

**Output:**

<img width="1222" height="607" alt="image" src="https://github.com/user-attachments/assets/209c70e9-828a-4aed-a7e7-d3288b0c6fe2" />


**Question 6**
---
-- From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

For example:

Result
ord_no      purch_amt   ord_date    salesman_id
----------  ----------  ----------  -----------
70002       65.26       2012-10-05  5001
70005       2400.6      2012-07-27  5001
70008       5760.0      2012-09-10  5001
70013       3045.6      2012-04-25  5001

```sql
-- select ord_no,purch_amt,ord_date,salesman_id
from orders
where salesman_id in
(
 select salesman_id
 from salesman
 where commission=(select max(commission) from salesman)
 );

```

**Output:**

<img width="1228" height="552" alt="image" src="https://github.com/user-attachments/assets/6deca1c9-43a6-415b-8fed-75f52f92a283" />


**Question 7**
---
-- Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
 

For example:

Result
customer_id  cust_name    city        grade       salesman_id
-----------  -----------  ----------  ----------  -----------
3005         Graham Zusi  California  200         5002


```sql
-- select * 
from customer
where customer_id=(
    select salesman_id
    from salesman
    where name='Mc Lyon'
)-2001;
```

**Output:**

<img width="1221" height="400" alt="image" src="https://github.com/user-attachments/assets/0761bd91-9c0e-468d-a316-ca0e9ea321d9" />


**Question 8**
---
-- From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

customer table

name         type
-----------  ----------
customer_id  int
cust_name    text
city         text
grade        int
salesman_id  int
For example:

Result
grade       COUNT(*)
----------  ----------
300         2


```sql
-- select grade,COUNT(*)
from customer
where grade>(
 select avg(grade)
 from customer 
 where city='New York')
 group by grade;
```

**Output:**

<img width="1226" height="402" alt="image" src="https://github.com/user-attachments/assets/4efe56c6-7e24-4e0c-a8a3-e6d7435d1d62" />


**Question 9**
---
--Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES



For example:

Result
student_id       student_name     subject          grade
---------------  ---------------  ---------------  ---------------
3                Charlie          Math             95
5                Emma             Science          92
7                John             Social           85


```sql
-- select *
from Grades g1
where grade=(
  select max(grade)
  from Grades g2
  where g2.subject=g1.subject
);
```

**Output:**

<img width="1222" height="532" alt="image" src="https://github.com/user-attachments/assets/dc15a2f6-5ba4-4c1e-afe1-ded96e925a0c" />


**Question 10**
---
-- Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

Sample table: CUSTOMERS

ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
4           Chaitali    25          Mumbai      6500
5           Hardik      27          Bhopal      8500
7           Muffy       24          Indore      10000

```sql
-- select *
from customers
where salary>4500;
```

**Output:**

<img width="1227" height="512" alt="image" src="https://github.com/user-attachments/assets/80791dd0-f7b6-4526-b000-c4d3804ff99c" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.

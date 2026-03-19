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
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'London'.

GIVEN Customer Table and Salesmen Table

```sql
select s.name from salesman s left join Customer c on s.salesman_id = c.salesman_id where c.city = 'London';
```

**Output:**

<img width="358" height="333" alt="image" src="https://github.com/user-attachments/assets/15cbf2af-f01e-4983-b44e-e8cdbcc1f663" />


**Question 2**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date between '2012-07-01' and '2012-07-30'.

GIVEN CUSTOMER TABLE AND ORDERS TABLE

```sql
select c.* from customer c left join orders o on c.customer_id = o.customer_id where o.ord_date between '2012-07-01' and '2012-07-30';
```

**Output:**
<img width="562" height="307" alt="image" src="https://github.com/user-attachments/assets/27fd908f-7d77-40cb-8ed9-cb953192d1c4" />


**Question 3**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

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
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001

```sql
select o.ord_no, o.purch_amt, c.cust_name, c.city from orders o join customer c on o.customer_id = c.customer_id where o.purch_amt between 500 and 2000;
```

**Output:**

<img width="569" height="355" alt="image" src="https://github.com/user-attachments/assets/65372aa4-b2ed-43ea-99ab-998097443e24" />


**Question 4**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

GIVEN PATIENTS TABLE AND TEST_RESULTS TABLE

```sql
select p.first_name as patient_name, t.* from patients p inner join test_results t on p.patient_id = t.patient_id where t.test_name = 'Blood Pressure';
```

**Output:**

<img width="1145" height="302" alt="image" src="https://github.com/user-attachments/assets/ba6f3369-2b62-4b6c-970a-cdf1bf0bcf02" />


**Question 5**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

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

```sql
select c.cust_name, c.city as city, c.grade,s.name as Salesman,s.city as city from customer c join salesman s on c.salesman_id = s.salesman_id order by c.customer_id asc; 
```

**Output:**

<img width="1085" height="603" alt="image" src="https://github.com/user-attachments/assets/dfacf753-a2bc-4d07-b96b-0831bccacdcb" />

**Question 6**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

GIVEN PATIENTS TABLE AND TEST_RESULTS TABLE:

```sql
select p.first_name as patient_name from patients p inner join test_results t on p.patient_id = t.patient_id where t.test_name = 'Blood Pressure';
```

**Output:**

<img width="555" height="295" alt="image" src="https://github.com/user-attachments/assets/5c55754d-29ec-4117-854c-34e55089540c" />


**Question 7**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the same city as the salesman.

GIVEN Customer Table and Salesmen table

```sql
select c.cust_name, s.name from customer c left join salesman s on c.salesman_id = s.salesman_id where c.city = s.city;
```

**Output:**

<img width="494" height="379" alt="image" src="https://github.com/user-attachments/assets/ec72f0c2-abbd-45f5-90e8-9a635ab350ed" />


**Question 8**
---
Write the SQL query that achieves the selection of all columns from the "patients" table, with an inner join on the "doctor_id" column, and includes a condition filtering for patients whose doctors have the first name 'John' and last name 'Smith'.

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

```sql
select p.* from patients p inner join doctors d on p.doctor_id = d.doctor_id where d.first_name = 'John' and d.last_name = 'Smith';
```

**Output:**

<img width="1324" height="291" alt="image" src="https://github.com/user-attachments/assets/5043b258-f650-4009-945f-8e4f75974d7c" />

**Question 9**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001
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
Sample table : salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

```sql
select o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id, c.cust_name, c.city,c.grade,s.name,s.commission from orders o inner join customer c on o.customer_id = c.customer_id inner join salesman s on o.salesman_id = s.salesman_id where o.ord_no in (70009,70005,70010) order by case o.ord_no when 70009 then 1 when 70005 then 2 when 70010 then 3 else 4 end;
```

**Output:**

<img width="1340" height="400" alt="image" src="https://github.com/user-attachments/assets/5bb7a3b0-9c45-4489-97e0-4750768fa3fe" />


**Question 10**
---
Write the SQL query that achieves the selection of the first name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date of '2024-01-15'.:

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

```sql
select patients.first_name from patients inner join surgeries on patients.patient_id = surgeries.patient_id where surgeries.surgery_date = '2024-01-15';
```

**Output:**

<img width="479" height="290" alt="image" src="https://github.com/user-attachments/assets/5f72c954-c82d-4b1c-b91b-8af37c0d8934" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.

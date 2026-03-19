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
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

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

```sql
select * from customer where customer_id = (select salesman_id - 2001 from salesman where name = 'Mc Lyon');
```

**Output:**

<img width="567" height="255" alt="image" src="https://github.com/user-attachments/assets/00b9ce2e-dc9c-48fd-ad12-e7db186bc0bf" />


**Question 2**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

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

```sql
select * from customers where salary > 4500;
```

**Output:**

<img width="563" height="334" alt="image" src="https://github.com/user-attachments/assets/fd7ac926-0215-4a4a-9a0b-a0811144dfa1" />


**Question 3**
---
Write a SQL query to List departments with names longer than the average length

Departments Table



```sql
select * from Departments where length(department_name) > (select avg(length(department_name))from Departments);
```

**Output:**

<img width="417" height="299" alt="image" src="https://github.com/user-attachments/assets/e00416e8-c1d6-475d-955b-737c50842cb3" />


**Question 4**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 1 million

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

```sql
select * from Employee where age < (select avg(age) from Employee where income > 1000000);
```

**Output:**

<img width="570" height="323" alt="image" src="https://github.com/user-attachments/assets/351e89f7-c77b-4e34-b272-6a4bdab5732c" />


**Question 5**
---
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE

name            type
----------     ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

```sql
select * from orders where purch_amt > (select avg(purch_amt) from orders where ord_date = '2012-10-10');
```

**Output:**

<img width="568" height="356" alt="image" src="https://github.com/user-attachments/assets/1c9d70b0-c19d-418e-b204-7abd246b71e2" />


**Question 6**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
select name, city from customer where city in (select city from customer where id in (3,7));
```

**Output:**

<img width="432" height="332" alt="image" src="https://github.com/user-attachments/assets/19e0312d-0bf4-4804-8e3c-cf552a10bb85" />


**Question 7**
---
From the following tables, write a SQL query to find those salespeople who earned the maximum commission. Return ord_no, purch_amt, ord_date, and salesman_id.

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

```sql
select ord_no, purch_amt, ord_date, salesman_id from orders where salesman_id = (select salesman_id from salesman where commission = (select max(commission) from salesman));
```

**Output:**

<img width="568" height="359" alt="image" src="https://github.com/user-attachments/assets/77ee3df1-dc42-4091-bc8a-70b64064f8f3" />


**Question 8**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

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

 

```sql
select * from customers where address = 'Delhi';
```

**Output:**

<img width="567" height="271" alt="image" src="https://github.com/user-attachments/assets/76bca023-a017-4e18-8710-69b51e72a41f" />


**Question 9**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

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

```sql
select * from customers where salary < 2500;
```

**Output:**

<img width="568" height="343" alt="image" src="https://github.com/user-attachments/assets/b27a1ce9-ccc5-402d-9f19-24f82db72c63" />


**Question 10**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES

```sql
select student_name, grade from grades g1 where grade = (select max(grade) from grades g2 where g1.subject = g2.subject);
```

**Output:**

<img width="528" height="319" alt="image" src="https://github.com/user-attachments/assets/64db267f-64e9-443b-a707-4c040b9d4e15" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.

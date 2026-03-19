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
Write a SQL statement to Increase quantity of all products by 10% to adjust for surplus stock counted

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
update Products 
set quantity=quantity*1.10;
```

**Output:**

<img width="1306" height="406" alt="image" src="https://github.com/user-attachments/assets/42e1f945-aace-4ea7-abd2-53d87220267a" />


**Question 2**
---
Write a SQL query to find all orders that meet the following conditions. Exclude combinations of order date equal to '2012-08-17' or customer ID greater than 3005 and purchase amount less than 1000.

Sample table : orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001

```sql
select * from orders where NOT(ord_date = '2012-08-17' OR (customer_id > 3005 AND purch_amt < 1000));
```

**Output:**

<img width="868" height="503" alt="image" src="https://github.com/user-attachments/assets/653e3161-42a4-45cf-a494-4eeac317f4e3" />


**Question 3**
---
Write a query to find the top 2 products with the highest discount percentage. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products

product_id | original_price | discount_percentage

-----------------------------------------------------------

"101" "50" "0.1"

"102" "150" "0.15"

"103" "200" "0.2"

"104" "300" "0.25"

```sql
select product_id,original_price,discount_percentage,(original_price-(original_price*discount_percentage)) as discounted_price from Products order by discount_percentage desc limit 2; 
```

**Output:**

<img width="1259" height="291" alt="image" src="https://github.com/user-attachments/assets/d88365e6-8138-4c3b-8eea-e4706d187495" />


**Question 4**
---
Write a SQL query to Delete customers from 'customer' table where 'WORKING_AREA' is 'New York'.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |


```sql
delete from Customer where WORKING_AREA = "New York";
```

**Output:**

<img width="1344" height="539" alt="image" src="https://github.com/user-attachments/assets/ca1830b1-453c-4576-abed-390535174055" />


**Question 5**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is less than 2.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

```sql
delete from Customer where GRADE<2;
```

**Output:**

<img width="464" height="386" alt="image" src="https://github.com/user-attachments/assets/f6a2a96c-eb83-417c-bc66-7be47d07a928" />


**Question 6**
---
Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

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
update Products 
set sell_price=sell_price*1.10 where category='Bakery';
```

**Output:**

<img width="1329" height="375" alt="image" src="https://github.com/user-attachments/assets/f53a45f8-15f2-43f3-962f-2c0aace25a7b" />


**Question 7**
---
Write a query to fetch details of employees with the address as “DELHI(DEL)” from EmployeeInfo table.

<img width="812" height="143" alt="image" src="https://github.com/user-attachments/assets/5502ebaa-cccb-41f3-a9f0-b838b6f2cb14" />


```sql
select * from EmployeeInfo where Address = "Delhi(DEL)";
```

**Output:**

<img width="1254" height="324" alt="image" src="https://github.com/user-attachments/assets/b7ea9e31-348f-4b80-97f6-37bb6003fcac" />


**Question 8**
---
Write a SQL query to find all those customers who does not have any grade. Return customer_id, cust_name, city, grade, salesman_id.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002

```sql
select * from customer where grade IS NULL;
```

**Output:**

<img width="1163" height="435" alt="image" src="https://github.com/user-attachments/assets/aedd5801-90af-4df5-916f-66ae40cd6eaa" />


**Question 9**
---
Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

```sql
delete from Customer where (GRADE = 3 OR AGENT_CODE = 'A008') AND OUTSTANDING_AMT < 5000;
```

**Output:**

<img width="1337" height="312" alt="image" src="https://github.com/user-attachments/assets/1b4959e6-2995-4cb0-97ae-d02b54a93333" />


**Question 10**
---
Write a SQL query to Concatenate the first three characters of the employee's name with the last three characters of their job title.

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

```sql
select ename,job,substr(ename,1,3)||substr(job,-3) as ConcatenatedString from emp;
```

**Output:**

<img width="601" height="432" alt="image" src="https://github.com/user-attachments/assets/db5a45e4-8ee7-4ffb-89a7-138db5595b0c" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.

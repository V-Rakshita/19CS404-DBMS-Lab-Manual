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
Write a SQL query to calculate the total number of working hours of all employees

Sample table: employee1

```sql
select sum(workhour) as "Total working hours" from employee1;
```

**Output:**

<img width="360" height="239" alt="image" src="https://github.com/user-attachments/assets/83e850a7-22f6-406f-84b0-e5167f57de03" />


**Question 2**
---
Write a SQL query to find Who has the highest income among employee living in California?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
select name, max(income) from employee where city='California';
```

**Output:**

<img width="385" height="235" alt="image" src="https://github.com/user-attachments/assets/a17df021-38b4-48bc-85bb-865ae5b1208b" />


**Question 3**
---
Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
select avg(purch_amt) as AVERAGE from orders ;
```

**Output:**

<img width="295" height="240" alt="image" src="https://github.com/user-attachments/assets/049270d9-309b-4516-876a-5a54c26ad8f4" />


**Question 4**
---
Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table

```sql
select PatientID, count(Medications) as AvgMedications from MedicalRecords group by(PatientID);
```

**Output:**

<img width="397" height="415" alt="image" src="https://github.com/user-attachments/assets/f35e631f-b03a-4020-8d27-6cc81d18bcf0" />


**Question 5**
---
What is the average dosage prescribed for each medication?

Sample tablePrescriptions Table

```sql
select Medication, avg(Dosage) as AvgDosage from Prescriptions group by(Medication);
```

**Output:**

<img width="537" height="499" alt="image" src="https://github.com/user-attachments/assets/719d9c58-6733-4973-ba5e-51d1672ec4a8" />

**Question 6**
---
What is the most common diagnosis among patients?

Sample table:MedicalRecords Table

```sql
select Diagnosis, count(Diagnosis) as DiagnosisCount from MedicalRecords group by(Diagnosis) order by(DiagnosisCount) Desc limit 1;
```

**Output:**

<img width="539" height="239" alt="image" src="https://github.com/user-attachments/assets/d2e2832d-d3a3-473c-9752-00bcf81dada2" />


**Question 7**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the total work hours for each occupation, and excludes occupations where the total work hour sum is not greater than 20.

Sample table: employee1



```sql
select occupation, SUM(workhour) from employee1 group by(occupation) having SUM(workhour) > 20;
```

**Output:**

<img width="448" height="331" alt="image" src="https://github.com/user-attachments/assets/5238d69a-c4e3-4432-bd68-898fb01f2e2d" />


**Question 8**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the minimum work hours for each occupation, and excludes occupations where the minimum work hour is not greater than 8.

Sample table: employee1

```sql
select occupation, MIN(workhour) from employee1 group by(occupation) having MIN(workhour) > 8;
```

**Output:**

<img width="429" height="346" alt="image" src="https://github.com/user-attachments/assets/a0837b11-5b7a-4b1d-975d-8abbd1c9c9e5" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the total work hours for each date, and excludes dates where the total work hour sum is not greater than 40.

Sample table: employee1

```sql
select jdate, SUM(workhour) from employee1 group by(jdate) having SUM(workhour) > 40;
```

**Output:**

<img width="475" height="283" alt="image" src="https://github.com/user-attachments/assets/d341a136-9ebb-4dff-a3a1-f4d993a5c766" />


**Question 10**
---
Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

Sample table: customer1

```sql
select address, AVG(salary) from customer1 group by(address) having AVG(salary) > 5000.0;
```

**Output:**

<img width="421" height="316" alt="image" src="https://github.com/user-attachments/assets/9613e412-07fc-40e8-808b-765f40faf7ee" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

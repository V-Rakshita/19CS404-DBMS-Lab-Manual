# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

**Program:**

```sql
--Create tables
-- Main table
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);

-- Log table
CREATE TABLE employee_log (
    log_id NUMBER GENERATED ALWAYS AS IDENTITY,
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    log_date DATE
);
```

```sql
--Create AFTER INSERT Trigger
CREATE OR REPLACE TRIGGER trg_after_insert_emp
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log (emp_id, emp_name, designation, log_date)
    VALUES (:NEW.emp_id, :NEW.emp_name, :NEW.designation, SYSDATE);
END;
/
```
```sql
--Insert Data into Employees Table
INSERT INTO employees VALUES (1, 'Arun', 'Manager');
INSERT INTO employees VALUES (2, 'Divya', 'Developer');

COMMIT;
```
```sql
--View Log Table
SELECT * FROM employee_log;
```
**Output:**

<img width="929" height="197" alt="image" src="https://github.com/user-attachments/assets/a9e7de35-11e1-485f-9565-0c3e7b35eaca" />


---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

```sql
--Create Table
CREATE TABLE sensitive_data (
    id NUMBER PRIMARY KEY,
    data VARCHAR2(100)
);
```

```sql
--Create BEFORE DELETE Trigger
CREATE OR REPLACE TRIGGER trg_prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
END;
/
```

```sql
--Test the Trigger
DELETE FROM sensitive_data WHERE id = 1;
```
**Output:**

<img width="798" height="134" alt="image" src="https://github.com/user-attachments/assets/000e7a81-16a0-46bb-a675-d2c983806617" />


---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

**Program:**

```sql
--Create Table
CREATE TABLE products (
    product_id NUMBER PRIMARY KEY,
    product_name VARCHAR2(50),
    price NUMBER,
    last_modified TIMESTAMP
);
```
```sql
--Insert Sample Data
INSERT INTO products (product_id, product_name, price)
VALUES (1, 'Laptop', 50000);

COMMIT;
```
```sql
--Create BEFORE UPDATE Trigger
CREATE OR REPLACE TRIGGER trg_update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/
```
```sql
--Test the Trigger
UPDATE products
SET price = 55000
WHERE product_id = 1;

COMMIT;
```
```sql
--View Result
SELECT product_id, product_name, price, last_modified FROM products;
```

**Output:**

<img width="959" height="239" alt="image" src="https://github.com/user-attachments/assets/5878ae67-dc2c-4ac5-8b45-a39d74fbe3d9" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

**Program:**
```sql
--Create Tables
-- Main table
CREATE TABLE customer_orders (
    order_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(50),
    amount NUMBER
);

-- Audit table
CREATE TABLE audit_log (
    update_count NUMBER
);
```
```sql
--Initialize Audit Table
INSERT INTO audit_log VALUES (0);
COMMIT;
```
```sql
--Create AFTER UPDATE Trigger
CREATE OR REPLACE TRIGGER trg_count_updates
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;
/
```
```sql
--Insert Sample Data
INSERT INTO customer_orders VALUES (1, 'Ravi', 1000);
INSERT INTO customer_orders VALUES (2, 'Anita', 2000);
COMMIT;
```
```sql
--Perform Updates
UPDATE customer_orders SET amount = 1500 WHERE order_id = 1;
UPDATE customer_orders SET amount = 2500 WHERE order_id = 2;

COMMIT;
```
```sql
--Check Audit Log
SELECT * FROM audit_log;
```

**Output:**

<img width="805" height="173" alt="image" src="https://github.com/user-attachments/assets/2b6655eb-d0df-40a1-8414-686b763821bc" />


---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

**Program:**

```sql
--Create Table
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    salary NUMBER
);
```
```sql
--Create BEFORE INSERT Trigger
CREATE OR REPLACE TRIGGER trg_check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(-20002, 'ERROR: Salary below minimum threshold.');
    END IF;
END;
/
```
```sql
--Test the Trigger
--Valid Insert
INSERT INTO employees VALUES (1, 'Arun', 5000);
--Invalid Insert
INSERT INTO employees VALUES (2, 'Divya', 2000);
```

**Output:**

<img width="633" height="137" alt="image" src="https://github.com/user-attachments/assets/e695c790-8f42-4d5d-97b8-f179cc0b864c" />




## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.

# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**Expected Output:**  
The program should display the employee details or an error message.

**Program:**
```sql
--Create Table and Insert Sample Data
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50)
);

INSERT INTO employees VALUES (1, 'Arun', 'Manager');
INSERT INTO employees VALUES (2, 'Divya', 'Developer');
INSERT INTO employees VALUES (3, 'Kiran', 'Analyst');

COMMIT;
```
```sql
--PL/SQL Program with Cursor and Exception Handling
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, designation FROM employees;

    v_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;

    no_data EXCEPTION;   -- Custom exception
    counter NUMBER := 0;
BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_name, v_designation;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || 
                             ', Designation: ' || v_designation);
        counter := counter + 1;
    END LOOP;

    CLOSE emp_cursor;

    -- Raise exception if no rows fetched
    IF counter = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
**Output:**

<img width="527" height="213" alt="image" src="https://github.com/user-attachments/assets/bc85ecb5-0362-413b-aca0-6f64a0466d10" />





---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.

**Expected Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.

**Program:**
```sql
--Modify Table and Insert Salary Data
ALTER TABLE employees ADD salary NUMBER;

UPDATE employees SET salary = 50000 WHERE emp_id = 1;
UPDATE employees SET salary = 30000 WHERE emp_id = 2;
UPDATE employees SET salary = 40000 WHERE emp_id = 3;

COMMIT;
```
```sql
--PL/SQL Program with Parameterized Cursor
DECLARE
    -- Parameterized Cursor
    CURSOR emp_cursor (min_sal NUMBER, max_sal NUMBER) IS
        SELECT emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN min_sal AND max_sal;

    v_name employees.emp_name%TYPE;
    v_designation employees.designation%TYPE;
    v_salary employees.salary%TYPE;

    no_data EXCEPTION;   -- Custom exception
    counter NUMBER := 0;

    -- Input salary range
    v_min NUMBER := 35000;
    v_max NUMBER := 60000;

BEGIN
    OPEN emp_cursor(v_min, v_max);

    LOOP
        FETCH emp_cursor INTO v_name, v_designation, v_salary;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name ||
                             ', Designation: ' || v_designation ||
                             ', Salary: ' || v_salary);
        counter := counter + 1;
    END LOOP;

    CLOSE emp_cursor;

    -- Raise exception if no rows found
    IF counter = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the given salary range.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
**Output:**

<img width="533" height="274" alt="image" src="https://github.com/user-attachments/assets/e6d160f6-6597-4bac-b050-3787d8b7b11e" />






---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.

**Expected Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.

**Program:**
```sql
--Modify Table and Insert Department Data
ALTER TABLE employees ADD dept_no NUMBER;

UPDATE employees SET dept_no = 10 WHERE emp_id = 1;
UPDATE employees SET dept_no = 20 WHERE emp_id = 2;
UPDATE employees SET dept_no = 30 WHERE emp_id = 3;

COMMIT;
```

```sql
--PL/SQL Program Using Cursor FOR Loop
DECLARE
    no_data EXCEPTION;   -- Custom exception
    counter NUMBER := 0;
BEGIN
    -- Cursor FOR loop (implicit cursor)
    FOR emp_rec IN (SELECT emp_name, dept_no FROM employees) LOOP
        DBMS_OUTPUT.PUT_LINE('Name: ' || emp_rec.emp_name ||
                             ', Dept No: ' || emp_rec.dept_no);
        counter := counter + 1;
    END LOOP;

    -- Raise exception if no rows found
    IF counter = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
**Output:**

<img width="530" height="230" alt="image" src="https://github.com/user-attachments/assets/771d65c7-05f5-4f8c-9b24-ba3d3dca9960" />


---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

**Expected Output:**  
The program should display employee records or the appropriate error message if no data is found.

**Program:**

```sql
--Ensure Table Structure and Sample Data
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    salary NUMBER
);

INSERT INTO employees VALUES (1, 'Arun', 'Manager', 50000);
INSERT INTO employees VALUES (2, 'Divya', 'Developer', 30000);
INSERT INTO employees VALUES (3, 'Kiran', 'Analyst', 40000);

COMMIT;
```

```sql
--PL/SQL Program Using %ROWTYPE
DECLARE
    CURSOR emp_cursor IS
        SELECT * FROM employees;

    emp_rec emp_cursor%ROWTYPE;  -- %ROWTYPE declaration

    no_data EXCEPTION;
    counter NUMBER := 0;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO emp_rec;
        EXIT WHEN emp_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE(
            'ID: ' || emp_rec.emp_id ||
            ', Name: ' || emp_rec.emp_name ||
            ', Designation: ' || emp_rec.designation ||
            ', Salary: ' || emp_rec.salary
        );

        counter := counter + 1;
    END LOOP;

    CLOSE emp_cursor;

    -- Raise exception if no rows found
    IF counter = 0 THEN
        RAISE no_data;
    END IF;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
/
```
**Output:**

<img width="528" height="212" alt="image" src="https://github.com/user-attachments/assets/60316c06-664f-440a-a433-06887bad38ef" />



---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.

**Expected Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

**Program:**
```sql
--Ensure Table Structure and Sample Data
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    dept_no NUMBER,
    salary NUMBER
);

-- Insert sample data
INSERT INTO employees VALUES (1, 'Arun', 'Manager', 10, 50000);
INSERT INTO employees VALUES (2, 'Divya', 'Developer', 20, 30000);
INSERT INTO employees VALUES (3, 'Kiran', 'Analyst', 10, 40000);

COMMIT;
```

```sql
--PL/SQL Program Using FOR UPDATE

DECLARE
    CURSOR emp_cursor IS
        SELECT emp_id, emp_name, salary
        FROM employees
        WHERE dept_no = 10
        FOR UPDATE;

    v_emp_id employees.emp_id%TYPE;
    v_name employees.emp_name%TYPE;
    v_salary employees.salary%TYPE;

    no_data EXCEPTION;
    counter NUMBER := 0;

BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_emp_id, v_name, v_salary;
        EXIT WHEN emp_cursor%NOTFOUND;

        -- Update salary (increase by 10%)
        UPDATE employees
        SET salary = salary + (salary * 0.10)
        WHERE CURRENT OF emp_cursor;

        DBMS_OUTPUT.PUT_LINE('Updated Salary for ' || v_name);

        counter := counter + 1;
    END LOOP;

    CLOSE emp_cursor;

    -- Raise exception if no rows updated
    IF counter = 0 THEN
        RAISE no_data;
    ELSE
        DBMS_OUTPUT.PUT_LINE('Salary updated successfully for department 10');
    END IF;

    COMMIT;

EXCEPTION
    WHEN no_data THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified department.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
        ROLLBACK;
END;
/
```

**Output:**


<img width="530" height="276" alt="image" src="https://github.com/user-attachments/assets/db551a05-9538-4229-9603-4f68f9f77574" />




---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 


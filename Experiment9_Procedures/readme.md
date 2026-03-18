# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

**Expected Output:**  
Square of 6 is 36

**Program:**

```sql
--Create the Procedure
CREATE OR REPLACE PROCEDURE find_square (num IN NUMBER) IS
    result NUMBER;
BEGIN
    result := num * num;
    DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || result);
END;
/
```

```sql
--Call the Procedure
BEGIN
    find_square(6);
END;
/
```

<img width="539" height="197" alt="image" src="https://github.com/user-attachments/assets/53875397-8383-4922-840b-e798b1c133f4" />


---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

**Expected Output:**  
Factorial of 5 is 120

**Program:**
```sql
--Create the Function
CREATE OR REPLACE FUNCTION get_factorial (n IN NUMBER)
RETURN NUMBER
IS
    fact NUMBER := 1;
BEGIN
    FOR i IN 1..n LOOP
        fact := fact * i;
    END LOOP;

    RETURN fact;
END;
/
```

```sql
--Call the Function
DECLARE
    result NUMBER;
BEGIN
    result := get_factorial(5);
    DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || result);
END;
/
```

**Output:**

<img width="533" height="201" alt="image" src="https://github.com/user-attachments/assets/6e8b3f6f-9a0b-49c7-b384-5f856bf58125" />


---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
12 is Even
**Program:**
```sql
--Create the Procedure
CREATE OR REPLACE PROCEDURE check_even_odd (num IN NUMBER) IS
BEGIN
    IF MOD(num, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(num || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(num || ' is Odd');
    END IF;
END;
/
```
```sql
--Call the Procedure
BEGIN
    check_even_odd(12);
END;
/
```

**Output:**

<img width="535" height="202" alt="image" src="https://github.com/user-attachments/assets/60de8cee-8560-4fb2-9a5d-095f08ba9867" />

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

**Expected Output:**  
Reversed number of 1234 is 4321

**Program:**
```sql
--Create the Function
CREATE OR REPLACE FUNCTION reverse_number (n IN NUMBER)
RETURN NUMBER
IS
    rev NUMBER := 0;
    temp NUMBER := n;
    rem NUMBER;
BEGIN
    WHILE temp > 0 LOOP
        rem := MOD(temp, 10);        -- Extract last digit
        rev := rev * 10 + rem;       -- Build reversed number
        temp := TRUNC(temp / 10);    -- Remove last digit
    END LOOP;

    RETURN rev;
END;
/
```
```sql
--Call the Function
DECLARE
    result NUMBER;
BEGIN
    result := reverse_number(1234);
    DBMS_OUTPUT.PUT_LINE('Reversed number of 1234 is ' || result);
END;
/
```
**Output:**

<img width="532" height="239" alt="image" src="https://github.com/user-attachments/assets/a17fad65-27b2-45e5-8c36-6cff76ea65b9" />


---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

**Program:**
```sql
--Create the Procedure
CREATE OR REPLACE PROCEDURE print_table (num IN NUMBER) IS
BEGIN
    DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || num || ':');

    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(num || ' x ' || i || ' = ' || (num * i));
    END LOOP;
END;
/
```

```sql
--Call the Procedure
BEGIN
    print_table(5);
END;
/
```

**Output:**

<img width="529" height="309" alt="image" src="https://github.com/user-attachments/assets/f00a2323-c137-4f11-a678-258999ca9fa6" />



## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.

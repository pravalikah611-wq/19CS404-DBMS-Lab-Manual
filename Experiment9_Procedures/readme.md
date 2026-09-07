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

SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE find_square(n NUMBER)
IS
    square NUMBER;
BEGIN
    square := n * n;

    DBMS_OUTPUT.PUT_LINE('Square of ' || n || ' is ' || square);
END;
/

BEGIN
    find_square(6);
END;
/

<img width="1412" height="734" alt="db exp 9 qu 1" src="https://github.com/user-attachments/assets/1b189d36-b542-4107-966c-811e2d441842" />


## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

**Expected Output:**  
Factorial of 5 is 120

SET SERVEROUTPUT ON;

CREATE OR REPLACE FUNCTION get_factorial(n NUMBER)
RETURN NUMBER
IS
    fact NUMBER := 1;
    i NUMBER := 1;
BEGIN
    WHILE i <= n LOOP
        fact := fact * i;
        i := i + 1;
    END LOOP;

    RETURN fact;
END;
/

<img width="1409" height="735" alt="db exp 9 qu 2" src="https://github.com/user-attachments/assets/644d8279-d9e8-4b70-b417-57e230d358b7" />


## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
12 is Even

SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE check_even_odd(n NUMBER)
IS
BEGIN
    IF MOD(n, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(n || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(n || ' is Odd');
    END IF;
END;
/

<img width="1394" height="793" alt="db ex 9 qu 3" src="https://github.com/user-attachments/assets/fde0a062-e835-4dc5-876d-a3a92e158df5" />


## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

**Expected Output:**  
Reversed number of 1234 is 4321

SET SERVEROUTPUT ON;

CREATE OR REPLACE FUNCTION reverse_number(n NUMBER)
RETURN NUMBER
IS
    rev NUMBER := 0;
    digit NUMBER;
    num NUMBER := n;
BEGIN
    WHILE num > 0 LOOP
        digit := MOD(num, 10);
        rev := (rev * 10) + digit;
        num := TRUNC(num / 10);
    END LOOP;

    RETURN rev;
END;
/

<img width="1396" height="741" alt="db ex 9 qu 4" src="https://github.com/user-attachments/assets/6e779131-1179-40d2-a1b7-94d954342696" />


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

SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE print_table(n NUMBER)
IS
    i NUMBER := 1;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || n || ':');

    WHILE i <= 10 LOOP
        DBMS_OUTPUT.PUT_LINE(n || ' x ' || i || ' = ' || (n * i));
        i := i + 1;
    END LOOP;
END;
/

<img width="1395" height="730" alt="db qu 5" src="https://github.com/user-attachments/assets/28be8f81-235b-4a31-b3b4-3bf8e2f44e6f" />


## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.

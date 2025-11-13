# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

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

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.
- 
**Expected Output:**  
Greater number is: 80

### PROGRAM:
```SQL
DECLARE
   num1 NUMBER := 25;  -- You can change this value
   num2 NUMBER := 80;  -- You can change this value
   greatest NUMBER;
BEGIN
   IF num1 > num2 THEN
      greatest := num1;
   ELSE
      greatest := num2;
   END IF;

   DBMS_OUTPUT.PUT_LINE('The greatest number is: ' || greatest);
END;
```
**Output:** 
<img width="947" height="273" alt="443116215-d44a35ee-fa4f-4c9b-a894-2c402b96fe40" src="https://github.com/user-attachments/assets/bcf4dec1-fdab-4d93-b121-90cd1ea3750c" />

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

## PROGRAM:
```SQL
DECLARE
   N NUMBER := 10;
   i NUMBER := 1;
   sum NUMBER := 0;
BEGIN
   WHILE i <= N LOOP
      sum := sum + i;
      i := i + 1;
   END LOOP;

   DBMS_OUTPUT.PUT_LINE('The sum of the first ' || N || ' natural numbers is: ' || sum);
END;
```
## OUTPUT:
<img width="943" height="272" alt="443117000-ba29737b-3fff-4756-8956-a7aaded595b8" src="https://github.com/user-attachments/assets/9bc84616-4546-4448-a3a9-ad431cc5290d" />

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

## PROGRAM:
```SQL
DECLARE
   N NUMBER := 10;
   first NUMBER := 0;
   second NUMBER := 1;
   next NUMBER;
   i NUMBER := 3;
BEGIN
   DBMS_OUTPUT.PUT_LINE('Fibonacci Series up to ' || N || ' terms:');
   DBMS_OUTPUT.PUT_LINE(first);
   DBMS_OUTPUT.PUT_LINE(second);

   WHILE i <= N LOOP
      next := first + second;
      DBMS_OUTPUT.PUT_LINE(next);
      first := second;
      second := next;
      i := i + 1;
   END LOOP;
END;

```
## OUTPUT:
<img width="943" height="273" alt="443117559-149063e1-c1bb-4102-b525-c307da60b972" src="https://github.com/user-attachments/assets/5b506482-2467-41f9-a809-c5230d93fa4c" />

---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351

## PROGRAM:
``` SQL
DECLARE
   num NUMBER := 12345; 
   reversed NUMBER := 0;
   digit NUMBER;
BEGIN
   DBMS_OUTPUT.PUT_LINE('Original Number: ' || num);

   WHILE num > 0 LOOP
      digit := MOD(num, 10);         
      reversed := reversed * 10 + digit;
      num := TRUNC(num / 10);         
   END LOOP;

   DBMS_OUTPUT.PUT_LINE('Reversed Number: ' || reversed);
END;

```
## OUTPUT:
<img width="944" height="154" alt="443118169-9117e268-89cb-4f11-8abb-4b63aa8b76f0" src="https://github.com/user-attachments/assets/12f9ea81-72f9-4a21-b8de-e228c36d5aff" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

## PROGRAM:
```SQL
DECLARE
   num1 NUMBER := 25;  
   num2 NUMBER := 42;   
   num3 NUMBER := 31;   
   largest NUMBER;
BEGIN
   IF num1 >= num2 AND num1 >= num3 THEN
      largest := num1;
   ELSIF num2 >= num1 AND num2 >= num3 THEN
      largest := num2;
   ELSE
      largest := num3;
   END IF;

   DBMS_OUTPUT.PUT_LINE('The largest number among ' || num1 || ', ' || num2 || ', and ' || num3 || ' is: ' || largest);
END;
```
## OUTPUT:
<img width="947" height="283" alt="443118665-b4d97a40-2a61-4a15-8dea-1e9787970902" src="https://github.com/user-attachments/assets/7c2df218-e040-49d4-b65a-861c876fac92" />


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.


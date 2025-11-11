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
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Medications Table
```sql
SELECT medication_id as medic, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MAX(dosage)
    FROM Medications
);
```

**Output:**
<img width="1476" height="970" alt="Screenshot 2025-11-11 223844" src="https://github.com/user-attachments/assets/2a80d289-c6c7-4a58-a079-333aca19813b" />

**Question 2**
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
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 1000000
);
```

**Output:**
<img width="1519" height="967" alt="Screenshot 2025-11-11 223826" src="https://github.com/user-attachments/assets/13fbf87d-b302-48e3-9d21-93a040ff1b34" />


**Question 3**
---
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Medications Table

```sql
SELECT medication_id as medic, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MIN(dosage)
    FROM Medications
);
```

**Output:**
<img width="1404" height="985" alt="Screenshot 2025-11-11 223812" src="https://github.com/user-attachments/assets/6cf3fdaf-8844-40fa-b93a-e4659b9e5140" />


**Question 4**
---
Write a query to display all the customers whose ID is the difference between the salesperson ID of Mc Lyon and 2001.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

```sql
SELECT customer_id, cust_name, city, grade, salesman_id
FROM customer
WHERE customer_id = (
    SELECT salesman_id - 2001
    FROM salesman
    WHERE name = 'Mc Lyon'
);

```

**Output:**
<img width="1476" height="938" alt="Screenshot 2025-11-11 223759" src="https://github.com/user-attachments/assets/9f3b89ae-60ea-43bc-a446-2af6c4485ff3" />


**Question 5**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

name             type

------------   ---------------

id                    INTEGER

name              TEXT

age                 INTEGER

city                 TEXT

income           INTEGER

```sql
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);

```

**Output:**
<img width="1493" height="996" alt="Screenshot 2025-11-11 223743" src="https://github.com/user-attachments/assets/5b6ded37-ac88-4618-aaef-f962297253e6" />


**Question 6**
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
SELECT *
FROM CUSTOMERS
WHERE SALARY < 2500;
```

**Output:**
<img width="1559" height="968" alt="Screenshot 2025-11-11 223722" src="https://github.com/user-attachments/assets/a4997201-0c82-4676-a3f2-e348ead80f8b" />


**Question 7**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE

name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)

```sql
SELECT ord_no, purch_amt, ord_date, customer_id, o.salesman_id
FROM Orders o
JOIN Salesman s
ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';
```

**Output:**
<img width="1522" height="990" alt="Screenshot 2025-11-11 223706" src="https://github.com/user-attachments/assets/e035bdd6-daf6-438d-b71d-17ac795c55aa" />

**Question 8**
---
From the following tables write a SQL query to find salespeople who had more than one customer. Return salesman_id and name.

salesman table

name                 type
---------------   ---------------
salesman_id       numeric(5)
name                  varchar(30)
city                     varchar(15)
commission       decimal(5,2)

customer table

name              type
-----------       ----------
customer_id   int
cust_name     text
city                text
grade            int
salesman_id  int

```sql
SELECT s.salesman_id, s.name
FROM salesman s
JOIN customer c
ON s.salesman_id = c.salesman_id
GROUP BY s.salesman_id, s.name
HAVING COUNT(c.customer_id) > 1;
```

**Output:**
<img width="1458" height="982" alt="Screenshot 2025-11-11 223650" src="https://github.com/user-attachments/assets/cccb2720-9216-4329-8ab7-e39a4f2d6c56" />

**Question 9**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(phone) = 1
);
```

**Output:**
<img width="1283" height="977" alt="Screenshot 2025-11-11 223637" src="https://github.com/user-attachments/assets/d71cbe59-f0e8-4edb-9c67-d81266250899" />


**Question 10**
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
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);

```

**Output:**
<img width="1299" height="956" alt="Screenshot 2025-11-11 223619" src="https://github.com/user-attachments/assets/fb7803b9-9d25-491c-b611-92d2c508240b" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.

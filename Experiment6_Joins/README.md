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
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with a date of birth after '1990-01-01'.

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
SELECT 
    p.first_name, 
    s.*
FROM 
    patients p
INNER JOIN 
    surgeries s
ON 
    p.patient_id = s.patient_id
WHERE 
    p.date_of_birth > '1990-01-01';
```

**Output:**
<img width="1257" height="455" alt="Screenshot 2025-11-14 104508" src="https://github.com/user-attachments/assets/184ccc35-51d7-4860-aa4c-250d7ccd357c" />


**Question 2**
--
Write the SQL query that accomplishes the selection of all columns from the "patients" table and the first name of doctors from the "doctors" table, with an inner join on the "doctor_id" column.

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
SELECT 
    p.*, 
    d.first_name AS doctor_name
FROM 
    patients p
INNER JOIN 
    doctors d
ON 
    p.doctor_id = d.doctor_id;
```

**Output:**
<img width="1325" height="952" alt="Screenshot 2025-11-14 104600" src="https://github.com/user-attachments/assets/775ab336-9667-4c3f-bec0-0dabe078ed03" />


**Question 3**
--
 From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

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
SELECT 
    c.cust_name AS "Customer Name",
    c.city,
    s.name AS "Salesman",
    s.commission
FROM 
    customer c
INNER JOIN 
    salesman s
ON 
    c.salesman_id = s.salesman_id;
```

**Output:**
<img width="1502" height="965" alt="Screenshot 2025-11-14 104620" src="https://github.com/user-attachments/assets/54578e9f-600e-4f6d-9a92-0c1dec9199e3" />



**Question 4**
--
Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

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

```sql
SELECT 
    c.cust_name ,
    c.city,
    o.ord_no ,
    o.ord_date ,
    o.purch_amt AS "Order Amount"
FROM 
    customer c
left JOIN 
    orders o
ON 
    c.customer_id = o.customer_id
ORDER BY 
    o.ord_date ASC;
```

**Output:**
<img width="1688" height="942" alt="Screenshot 2025-11-16 133121" src="https://github.com/user-attachments/assets/075f9e48-9896-4305-9ea2-313bf836cb86" />



**Question 5**
--
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

```sql
SELECT 
    s.*, 
    d.department_name
FROM 
    nurses s
INNER JOIN 
    departments d
ON 
    s.department_id = d.department_id;
```

**Output:**
<img width="1659" height="950" alt="Screenshot 2025-11-16 133136" src="https://github.com/user-attachments/assets/e1468dd0-a67c-465a-b285-ae6468312249" />


**Question 6**
--
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.

```sql
SELECT 
    s.name AS salesman_name,
    c.cust_name AS customer_name
FROM 
    salesman s
LEFT JOIN 
    customer c
ON 
    s.salesman_id = c.salesman_id;
```

**Output:**
<img width="1616" height="992" alt="Screenshot 2025-11-16 133645" src="https://github.com/user-attachments/assets/561a75f7-492f-463d-ab79-77081791c977" />



**Question 7**
--
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients admitted between '2024-01-01' and '2024-01-31'.

```sql
SELECT 
    p.first_name AS patient_name,
    t.*
FROM 
    patients p
INNER JOIN 
    test_results t
ON 
    p.patient_id = t.patient_id
WHERE 
    p.admission_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**
<img width="1585" height="938" alt="Screenshot 2025-11-16 133656" src="https://github.com/user-attachments/assets/d8150643-5223-4df0-a6c1-c26102b6aeba" />



**Question 8**
--
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
SELECT 
    p.*
FROM 
    patients p
INNER JOIN 
    doctors d
ON 
    p.doctor_id = d.doctor_id
WHERE 
    d.first_name = 'John' 
    AND d.last_name = 'Smith';
```

**Output:**
<img width="1630" height="919" alt="Screenshot 2025-11-16 133707" src="https://github.com/user-attachments/assets/11b97a1b-a53d-4026-82e0-a81340bc0c63" />



**Question 9**
--
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "commission" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column.

```sql
SELECT 
    c.cust_name,
    s.commission
FROM 
    customer c
LEFT JOIN 
    salesman s
ON 
    c.salesman_id = s.salesman_id;
```

**Output:**
<img width="1623" height="882" alt="Screenshot 2025-11-16 133718" src="https://github.com/user-attachments/assets/b48c52af-5ade-497f-8171-5f51de1be2dd" />



**Question 10**
--
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

```sql
SELECT 
    p.first_name AS patient_name,
    t.test_name
FROM 
    patients p
INNER JOIN 
    test_results t
ON 
    p.patient_id = t.patient_id;
```

**Output:**
<img width="1541" height="956" alt="Screenshot 2025-11-16 133733" src="https://github.com/user-attachments/assets/f3d24a5d-2645-4025-8ca2-db1c312a69ed" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.

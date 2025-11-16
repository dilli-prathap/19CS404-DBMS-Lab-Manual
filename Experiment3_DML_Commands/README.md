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
Write a SQL query to delete a specific doctor from Doctors table whose ID is 1.
```sql
DELETE FROM Doctors
WHERE doctor_id = 1;
```

**Output:**
<img width="1522" height="868" alt="Screenshot 2025-11-16 142111" src="https://github.com/user-attachments/assets/29881bbd-cfb5-40df-9c2e-d20a2e6507d8" />


**Question 2**
--
Write a SQL query to Delete customers from 'customer' table where 'CUST_CITY' is not 'New York' and 'OUTSTANDING_AMT' is greater than 5000.
```sql
DELETE FROM Customer
WHERE CUST_CITY <> 'New York'
  AND OUTSTANDING_AMT > 5000;
```

**Output:**
<img width="1351" height="927" alt="Screenshot 2025-11-16 142122" src="https://github.com/user-attachments/assets/a59aabd7-84e0-43e8-8801-0a0507d1d9b4" />


**Question 3**
--
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table
```sql
UPDATE Products
SET reorder_lvl = 20
WHERE quantity < 10
  AND category = 'Snacks';
```

**Output:**
<img width="1571" height="950" alt="Screenshot 2025-11-16 142133" src="https://github.com/user-attachments/assets/9e0037de-ca57-405d-85f2-b3013266b327" />



**Question 4**
--
Write a query to list all products that have a discounted price between $100 and $250. Return product_id, original_price, discount_percentage, and discounted_price from products table
```sql
SELECT 
    product_id,
    original_price,
    discount_percentage,
    (original_price - (original_price * discount_percentage)) AS discounted_price
FROM products
WHERE (original_price - (original_price * discount_percentage))
      BETWEEN 100 AND 250;
```

**Output:**
<img width="1540" height="941" alt="Screenshot 2025-11-16 142142" src="https://github.com/user-attachments/assets/6d557240-59bc-46d7-9c3d-d87025261da6" />



**Question 5**
--
Write a SQL query to find the details of those salespeople who live in cities other than Paris and Rome. Return salesman_id, name, city, commission.
```sql
SELECT 
    salesman_id,
    name,
    city,
    commission
FROM salesman
WHERE city NOT IN ('Paris', 'Rome');
```

**Output:**
<img width="1554" height="966" alt="Screenshot 2025-11-16 142155" src="https://github.com/user-attachments/assets/67d6490e-f461-4ef1-ad20-037dbed23205" />



**Question 6**
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
UPDATE Products
SET quantity = quantity * 1.10;
```

**Output:**
<img width="1556" height="917" alt="Screenshot 2025-11-16 142205" src="https://github.com/user-attachments/assets/7d967f5c-b76c-491c-8c50-50dbe0a46a95" />



**Question 7**
---
Write a query to fetch details of employees whose EmpLname ends with an alphabet ‘A’ and contains five alphabets.

```sql
SELECT 
    EmpID,
    EmpFname,
    EmpLname,
    Department,
    Project,
    Address,
    DOB,
    Gender
FROM EmployeeInfo
WHERE EmpLname LIKE '____A';
```

**Output:**
<img width="1550" height="901" alt="Screenshot 2025-11-16 142215" src="https://github.com/user-attachments/assets/f1da1625-2e26-4d10-ab07-712171dd1e67" />



**Question 8**
--
Create a report that shows the capitalized FirstName and capitalized LastName renamed as FirstName and Lastname respectively and EmployeeId from the employees table sorted by EmployeeId in descending order.

employees table

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           EmployeeID  INTEGER      0                       1
1           LastName    VARCHAR(15)  0                       0
2           FirstName   VARCHAR(15)  0                       0
3           BirthDate   DATETIME     0                       0
4           Photo       VARCHAR(25)  0                       0
5           Notes       VARCHAR(10)  0

```sql
SELECT 
    UPPER(FirstName) AS FirstName,
    UPPER(LastName) AS LastName,
    EmployeeID
FROM employees
ORDER BY EmployeeID DESC;
```

**Output:**
<img width="1713" height="969" alt="Screenshot 2025-11-16 142227" src="https://github.com/user-attachments/assets/617ad058-e556-463a-9a50-c0b74fe5da19" />



**Question 9**
---
Write a SQL query to find all employees who were hired on a weekend (Saturday or Sunday) from the emp table

emp table

cid         name        type        
----------  ----------  ---------- 
0           empno       INT         
1           ename       VARCHAR(100)
2           job         VARCHAR(50)
3           mgr         INT        
4           hiredate    DATE        
5           sal         DECIMAL(10,2)  
6           comm        DECIMAL(10,2)  
7           deptno      INT         

```sql
SELECT 
    ename,
    hiredate,
    strftime('%w', hiredate) AS day_of_week
FROM emp
WHERE strftime('%w', hiredate) IN ('0', '6');
```

**Output:**
<img width="1608" height="866" alt="Screenshot 2025-11-16 142239" src="https://github.com/user-attachments/assets/e888fd32-24f9-4fab-b7db-07fb94411ea1" />


**Question 10**
--
Write a SQL query to remove rows from the table 'customer' with the following condition -
```sql
DELETE FROM customer
WHERE cust_city LIKE 'L%';
```

**Output:**
<img width="1592" height="966" alt="Screenshot 2025-11-16 142250" src="https://github.com/user-attachments/assets/db498327-ec24-4dda-8feb-95cd91279539" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.

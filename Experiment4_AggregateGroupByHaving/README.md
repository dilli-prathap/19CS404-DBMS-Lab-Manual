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
Write a SQL query to find the total income of employees aged 40 or above.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
SELECT SUM(income) as total_income
FROM employee
WHERE age >= 40;
```

**Output:**
<img width="1018" height="912" alt="Screenshot 2025-11-11 221420" src="https://github.com/user-attachments/assets/0b9a05ce-185b-4ad4-99d4-b2d200a3fd5b" />


**Question 2**
---
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
SELECT name AS Employee_Name,age AS Age
FROM  employee
ORDER BY age ASC
LIMIT 1;
```

**Output:**
<img width="879" height="911" alt="Screenshot 2025-11-11 221432" src="https://github.com/user-attachments/assets/8087f6cb-e5d2-4d01-9e0e-585dfe5aa1a1" />


**Question 3**
---
Write a SQL query to find the difference between the maximum and minimum price of fruits?

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL

```sql
SELECT MAX(price) - MIN(price) as price_diff
FROM fruits
```

**Output:**
<img width="646" height="942" alt="Screenshot 2025-11-11 221445" src="https://github.com/user-attachments/assets/580f977d-9c1e-4f1c-ad69-00aac6a1aa25" />


**Question 4**
---
How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT
```sql
SELECT PatientID,COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY PatientID;

```

**Output:**
<img width="828" height="998" alt="Screenshot 2025-11-11 221500" src="https://github.com/user-attachments/assets/0dc8f247-1e65-4d40-ab4a-b883d796bafe" />


**Question 5**
---
What is the average dosage prescribed for each medication?

Sample tablePrescriptions Table
```sql
SELECT 
    Medication,
    AVG(Dosage) AS  AvgDosage
FROM Prescriptions
GROUP BY Medication;
```

**Output:**
<img width="716" height="942" alt="Screenshot 2025-11-11 221513" src="https://github.com/user-attachments/assets/12694d68-63ab-457d-bb3a-d7e5c94be92d" />


**Question 6**
---
What is the total number of appointments scheduled for each day?

Sample table:Appointments Table
```sql
SELECT 
    DATE(AppointmentDateTime) AS AppointmentDate,
    COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DATE(AppointmentDateTime)
ORDER BY AppointmentDate;
```

**Output:**
<img width="815" height="984" alt="Screenshot 2025-11-11 221525" src="https://github.com/user-attachments/assets/89f4e5d4-fa8b-42cb-b286-b5c3032c5a4d" />


**Question 7**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the average work hours for each occupation, and includes only those occupations where the average work hour falls between 10 and 12.
```sql
SELECT occupation, AVG(workhour)
FROM employee1
GROUP BY occupation
HAVING AVG(workhour) BETWEEN 10 AND 12;

```

**Output:**
<img width="696" height="984" alt="Screenshot 2025-11-11 221535" src="https://github.com/user-attachments/assets/80daa430-1af7-4468-93f9-26ad2bf52f50" />


**Question 8**
---
Write the SQL query that achieves the selection of product names and the maximum price for each category from the "products" table, and includes only those products where the maximum price is greater than 15.
```sql
SELECT category_id,product_name, MAX(price) AS Price
FROM products
GROUP BY category_id
HAVING MAX(price) > 15;
```

**Output:**
<img width="835" height="906" alt="Screenshot 2025-11-11 221548" src="https://github.com/user-attachments/assets/4c23ea71-fd0e-4eb3-b715-4303b6ba03ce" />


**Question 9**
---
Write the SQL query to find how many patients have more than 3 medical records?.

Sample table: MedicalRecords

name        type
----------  ----------
RecordID    INTEGER
PatientID   INTEGER
DoctorID    INTEGER
Date        DATE
Diagnosis   TEXT
Treatment   TEXT
Medication  TEXT
```sql
SELECT
    PatientID,
    COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY PatientID
HAVING COUNT(*) > 3


```

**Output:**
<img width="741" height="952" alt="Screenshot 2025-11-11 221556" src="https://github.com/user-attachments/assets/ae967d8a-c794-494a-a385-f4da33f2fb9d" />


**Question 10**
---
Write the SQL query that accomplishes the selection of number of products for each category from products table which includes only those products where the category ID is greater than 2.

Sample table: products
```sql
SELECT category_id,COUNT(*) as COUNT
FROM products
WHERE category_id > 2
GROUP BY category_id;
```

**Output:**
<img width="1204" height="918" alt="Screenshot 2025-11-11 221611" src="https://github.com/user-attachments/assets/05fed1b5-2716-4cf7-ba24-ae5e0e10e469" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

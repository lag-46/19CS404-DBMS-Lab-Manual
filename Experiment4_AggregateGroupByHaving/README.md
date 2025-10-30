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
For example:

Result
PatientID   TotalAppointments
----------  -----------------
3           3
5           2
6           1
7           1
10          3

```sql
SELECT PatientID,
       COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY PatientID;
```

**Output:**

<img width="773" height="651" alt="image" src="https://github.com/user-attachments/assets/e0d66029-354d-4424-98c5-10138ef77c34" />


**Question 2**
---
How many patients have expired insurance coverage for each insurance company?

Sample table:Insurance Table



For example:

Result
InsuranceCompany  TotalExpiredPatients
----------------  --------------------
ABC Insurance     1
DEF Insurance     1
GHI Insurance     1
JKL Insurance     1
MNO Insurance     1
PQR Insurance     1
STU Insurance     1
VWX Insurance     1
XYZ Insurance     1
YZA Insurance     1


```sql
SELECT InsuranceCompany,
       COUNT(*) AS TotalExpiredPatients
FROM Insurance
GROUP BY InsuranceCompany;
```

**Output:**

<img width="873" height="752" alt="image" src="https://github.com/user-attachments/assets/d2352ef5-3cbe-475c-9fa1-714cb2ae7853" />


**Question 3**
---
What is the total number of appointments scheduled for each day?

Table: Appointments

name                 type
-------------------  ----------
AppointmentID        INTEGER
PatientID            INTEGER
DoctorID             INTEGER
AppointmentDateTime  DATETIME
Purpose              TEXT
Status               TEXT
 

For example:

Result
AppointmentDate  TotalAppointments
---------------  -----------------
2024-02-16       4
2024-02-18       1
2024-02-20       1
2024-02-21       1
2024-02-22       1
2024-02-23       2

```sql
SELECT DATE(AppointmentDateTime) AS AppointmentDate,
       COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY DATE(AppointmentDateTime)
ORDER BY AppointmentDate;
```

**Output:**

<img width="834" height="669" alt="image" src="https://github.com/user-attachments/assets/d3bc0b11-e5f7-4ed4-abe9-cac6ee3fc1c0" />


**Question 4**
---
Write a SQL query to find the number of employees whose age is greater than 32.

Sample table: employee

id

name

age

address

salary

1

Paul

32

California

20000

4

Mark

25

Richtown

65000

5

David

27

Texas

85000

 

For example:

Result
COUNT
----------
5


```sql
SELECT COUNT(*) AS COUNT
FROM employee
WHERE age > 32;
```

**Output:**

<img width="727" height="363" alt="image" src="https://github.com/user-attachments/assets/b7fb390b-1f0b-49f8-8cb7-973d331ebe8d" />


**Question 5**
---
Write a SQL query to find  how many employees work in California?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

For example:

Result
employees_in_california
-----------------------
2


```sql
SELECT COUNT(*) AS employees_in_california
FROM employee
WHERE city = 'California';
```

**Output:**

<img width="726" height="351" alt="image" src="https://github.com/user-attachments/assets/a24a68e6-6f61-43c7-ba54-24d91fcd82e8" />


**Question 6**
---
Write a SQL query to find the average length of email addresses (in characters):

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
avg_email_length
----------------
15.0

```sql
SELECT AVG(LENGTH(email)) AS avg_email_length
FROM customer;
```

**Output:**

<img width="795" height="364" alt="image" src="https://github.com/user-attachments/assets/f7d4690c-e54a-4a5b-b98b-ddd570c36a2f" />


**Question 7**
---
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
total
----------
225


```sql
SELECT SUM(inventory) AS total
FROM fruits
WHERE unit = 'LB';
```

**Output:**

<img width="764" height="362" alt="image" src="https://github.com/user-attachments/assets/56f57bb4-192b-41cf-9e36-9bef65ced457" />


**Question 8**
---
Write the SQL query that accomplishes the selection of number of products for each category from products table which includes only those products where the category ID is greater than 2.

Sample table: products



For example:

Result
category_id  COUNT
-----------  ----------
3            3


```sql
SELECT category_id,
       COUNT(*) AS COUNT
FROM products
WHERE category_id > 2
GROUP BY category_id;
```

**Output:**

<img width="781" height="384" alt="image" src="https://github.com/user-attachments/assets/90cc8b3d-34e0-486e-87dd-0e2b09676b7e" />


**Question 9**
---
Which cities (addresses) in the "customer1" table have an average salary lesser than Rs. 15000

Sample table: customer1



For example:

Result
address     AVG(salary)
----------  -----------
Ahmedabad   2000.0
Bhopal      8500.0
Delhi       1500.0
Hyderabad   4500.0
Indore      10000.0
Kota        2000.0
Mumbai      6500.0


```sql
SELECT address,
       AVG(salary) AS "AVG(salary)"
FROM customer1
GROUP BY address
HAVING AVG(salary) < 15000;
```

**Output:**

<img width="776" height="626" alt="image" src="https://github.com/user-attachments/assets/472214ee-c636-4d24-9ae3-493faa2a1221" />


**Question 10**
---
Write the SQL query that achieves the selection of product names and the maximum price for each category from the "products" table, and includes only those products where the maximum price is greater than 15.

Sample table: products



For example:

Result
category_id  product_name  Price
-----------  ------------  ----------
1            Orange        15.5
2            Monitor       25


```sql
SELECT p.category_id,
       p.product_name,
       p.price AS Price
FROM products p
JOIN (
    SELECT category_id,
           MAX(price) AS max_price
    FROM products
    GROUP BY category_id
) mp ON p.category_id = mp.category_id AND p.price = mp.max_price
WHERE p.price > 15;
```

**Output:**

<img width="969" height="432" alt="image" src="https://github.com/user-attachments/assets/1100f7fc-a6af-4223-84ea-5942b577b5ce" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

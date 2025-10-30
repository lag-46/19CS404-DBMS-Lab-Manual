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
Write a SQL statement to Update the hire_date of employees in department 50 to 2024-01-24.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT EMPLOYEE_ID, FIRST_NAME, HIRE_DATE FROM EMPLOYEES 
WHERE DEPARTMENT_ID=50 LIMIT 3;
EMPLOYEE_ID  FIRST_NAME  HIRE_DATE
-----------  ----------  ----------
120          Matthew     2024-01-24
121          Adam        2024-01-24
122          Payam       2024-01-24



```sql
UPDATE employees
SET hire_date = '2024-01-24'
WHERE department_id = 50;
```

**Output:**

<img width="1261" height="327" alt="image" src="https://github.com/user-attachments/assets/5d71cb65-2e1e-4686-9948-477d66d365f7" />


**Question 2**
---
Write a SQL statement to Update the grade of all customers in Chennai city as  5. 

Customer table (customer_id,cust_name,city,grade,salesman_id)

```sql
UPDATE customer
SET grade = 5
WHERE city = 'Chennai';
```

**Output:**

<img width="1311" height="411" alt="image" src="https://github.com/user-attachments/assets/1f614b5e-9fba-48b6-ae4b-d08f32fa70e1" />


**Question 3**
---
Write a SQL statement to Increase the selling price per unit by 5% for product ID 15 who's sale is on '2023-01-31'.

sales(sale_id,sale_date,product_id,quantity,sell_price,total_sell_price)

For example:

Test	Result
select changes();
changes()
----------
3


```sql
UPDATE sales
SET sell_price = sell_price * 1.05
WHERE product_id = 15
  AND sale_date = '2023-01-31';
```

**Output:**

<img width="1333" height="347" alt="image" src="https://github.com/user-attachments/assets/5b4df4f6-2cb7-4e3e-8f8d-a5c5c6cd20c3" />


**Question 4**
---
Write a SQL statement to increase the salary of employees under the department 40, 90 and 110 according to the company rules.

Salary will be increased by 25% for the department 40, 15% for department 90 and 10% for the department 110 and the rest of the departments will remain same.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT EMPLOYEE_ID, FIRST_NAME, SALARY, PHONE_NUMBER, EMAIL, JOB_ID FROM EMPLOYEES LIMIT 10;
EMPLOYEE_ID  FIRST_NAME  SALARY      PHONE_NUMBER  EMAIL       JOB_ID
-----------  ----------  ----------  ------------  ----------  ----------
100          Steven      27600       515.123.4567  SKING       AD_PRES
101          Neena       19550       515.123.4568  NKOCHHAR    AD_VP
102          Lex         19550       515.123.4569  LDEHAAN     AD_VP
103          Alexander   9000        590.423.4567  AHUNOLD     IT_PROG
104          Bruce       6000        590.423.4568  BERNST      IT_PROG
105          David       4800        590.423.4569  DAUSTIN     IT_PROG
106          Valli       4800        590.423.4560  VPATABAL    IT_PROG
107          Diana       4200        590.423.5567  DLORENTZ    IT_PROG
108          Nancy       12000       515.124.4569  NGREENBE    FI_MGR
109          Daniel      9000        515.124.4169  DFAVIET     FI_ACCOUNT


```sql
UPDATE employees
SET salary = CASE
    WHEN department_id = 40  THEN ROUND(salary * 1.25)
    WHEN department_id = 90  THEN ROUND(salary * 1.15)
    WHEN department_id = 110 THEN ROUND(salary * 1.10)
    ELSE salary
END;
```

**Output:**

<img width="1376" height="271" alt="image" src="https://github.com/user-attachments/assets/7ef3fe82-d6da-4900-9768-3180567fc41a" />


**Question 5**
---
Increase the reorder level by 30% for products from 'Food' category having quantity in stock less than 50% of existing reorder level in the products table
name               type
--------------  ----------
product_id         INT
product_name       VARCHAR(10)
category           VARCHAR(50)
cost_price         DECIMAL(10)
sell_price         DECIMAL(10)
reorder_lvl        INT
quantity              INT
supplier_id           INT
For example:

Test	Result
select changes();
changes()
----------
4


```sql
UPDATE products
SET reorder_lvl = ROUND(reorder_lvl * 1.3)
WHERE category = 'Food'
  AND quantity < (reorder_lvl * 0.5);
```

**Output:**

<img width="1370" height="236" alt="image" src="https://github.com/user-attachments/assets/b62ba2ba-0004-411d-a4fd-be64fdb68081" />


**Question 6**
---
Write a SQL query to Delete All Doctors with a NULL Last Name

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin                   Cardiology
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics


```sql
DELETE FROM doctors
WHERE last_name IS NULL;
```

**Output:**

<img width="704" height="396" alt="image" src="https://github.com/user-attachments/assets/176ec21b-c2c7-473d-b03e-8bc9517c0d73" />


**Question 7**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3 or surgeon ID is 4.

Sample table: Surgeries


For example:

Test	Result
--After Deletion
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28


```sql
DELETE FROM surgeries
WHERE surgery_id = 3
   OR surgeon_id = 4;
```

**Output:**

<img width="804" height="506" alt="image" src="https://github.com/user-attachments/assets/de67ed46-4020-4f1c-84f9-22a01962d0e8" />


**Question 8**
---
Write a SQL query to Delete customers from 'customer' table where 'AGENT_CODE' is either 'A003' or 'A008'.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select distinct(agent_code)from customer;
AGENT_CODE
----------
A003
A008
A011
A006
A005
A010
A002
A004
A009
A007
A012
A001
AGENT_CODE
----------
A011
A006
A005
A010
A002
A004
A009
A007
A012
A001

```sql
DELETE FROM customer
WHERE agent_code IN ('A003', 'A008');
```

**Output:**

<img width="737" height="607" alt="image" src="https://github.com/user-attachments/assets/4997e642-073b-4bac-be9e-51ccef34be19" />


**Question 9**
---
Write a SQL query to Delete customers with 'CUST_COUNTRY' 'UK' and 'WORKING_AREA' 'London' whose 'GRADE' is less than 3

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
4


```sql
DELETE FROM customer
WHERE cust_country = 'UK'
  AND working_area = 'London'
  AND grade < 3;
```

**Output:**

<img width="1193" height="193" alt="image" src="https://github.com/user-attachments/assets/d003525d-d5f3-44ad-a390-ebe8c2044de5" />


**Question 10**
---
Write a SQL query to Delete customers with 'GRADE' 2 and 'CUST_NAME' starting with 'M', and whose 'PAYMENT_AMT' is less than 3000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
For example:

Test	Result
select changes();
changes()
----------
1


```sql
DELETE FROM customer
WHERE grade = 2
  AND cust_name LIKE 'M%'
  AND payment_amt < 3000;
```

**Output:**

<img width="1132" height="165" alt="image" src="https://github.com/user-attachments/assets/ddc1c5c3-0b81-487a-8d2b-89844cedae9b" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.

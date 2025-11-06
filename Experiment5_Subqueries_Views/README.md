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
Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)



For example:

Result
depar  department_name
-----  ---------------
5      Anesthesiologis


```sql
SELECT department_id, department_name
FROM Departments
WHERE LENGTH(department_name) > (
    SELECT AVG(LENGTH(department_name)) FROM Departments
);

```

**Output:**

<img width="1048" height="499" alt="image" src="https://github.com/user-attachments/assets/ddf2a557-5c16-4607-a077-68ac04511032" />


**Question 2**
---
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int
 

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70011       75.29       2012-08-17  3003         5007


```sql
SELECT 
    ord_no,
    purch_amt,
    ord_date,
    customer_id,
    salesman_id
FROM orders
WHERE salesman_id IN (
    SELECT salesman_id FROM salesman WHERE name = 'Paul Adam'
);

```

**Output:**

<img width="1286" height="470" alt="image" src="https://github.com/user-attachments/assets/87bee35e-a606-414d-9f45-5ea8a90a0ff3" />


**Question 3**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER
For example:

Result
id     name             city             email            phone
-----  ---------------  ---------------  ---------------  ----------
6      Aarti Desai      Pune             aarti@gmail.com  890123456
7      Vivek Sharma     Chandigarh       vivek@gmail.com  980154021
8      Nisha Patel      Noida            nisha@gmail.com  901234567
9      Rajesh Singh     Hyderabad        rajesh@gmail.co  917654301


```sql
SELECT id, name, city, email, phone
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    ORDER BY id DESC
    LIMIT 1
);

```

**Output:**

<img width="1311" height="514" alt="image" src="https://github.com/user-attachments/assets/37f96057-d6e3-47a1-b53e-61f9f039cff4" />


**Question 4**
---
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE

name            type
----------     ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70005       2400.6      2012-07-27  3007         5001
70008       5760.0      2012-09-10  3002         5001
70003       2480.4      2012-10-10  3009         5003
70013       3045.6      2012-04-25  3002         5001


```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM ORDERS
WHERE purch_amt > (
    SELECT AVG(purch_amt)
    FROM ORDERS
    WHERE ord_date = '2012-10-10'
);

```

**Output:**

<img width="1308" height="487" alt="image" src="https://github.com/user-attachments/assets/98488937-523f-4b5f-91bb-0f6f3b638a88" />


**Question 5**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

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

 
 

For example:

Result
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
2           Khilan      25          Delhi       1500


```sql
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi'
  AND AGE < 30
ORDER BY ID;

```

**Output:**

<img width="1305" height="405" alt="image" src="https://github.com/user-attachments/assets/b5a5a20c-2a94-4519-97cc-aa8789c51639" />


**Question 6**
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

For example:

Result
id     name             age              city             income
-----  ---------------  ---------------  ---------------  ----------
101    Peter            32               NewYork          200000
102    Mark             32               California       300000
103    Donald           25               Arizona          1000000
105    Linklon          32               Georgia          250000


```sql
SELECT 
    id,
    name,
    age,
    city,
    income
FROM 
    Employee
WHERE 
    age < (
        SELECT AVG(age)
        FROM Employee
        WHERE income > 1000000
    );

```

**Output:**

<img width="1297" height="450" alt="image" src="https://github.com/user-attachments/assets/a8c79035-b9d4-41dd-b1b0-81d0d89c44ce" />


**Question 7**
---
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)



For example:

Result
medic  medication_name  dosage
-----  ---------------  ---------------
2      Ibuprofen        200mg


```sql
SELECT 
    medication_id AS medic,
    medication_name,
    dosage
FROM 
    Medications
WHERE 
    dosage = (
        SELECT MIN(dosage) 
        FROM Medications
    );

```

**Output:**

<img width="967" height="440" alt="image" src="https://github.com/user-attachments/assets/d0223f7a-9059-4a0a-8896-11215136c5d7" />


**Question 8**
---
Write a SQL query to Retrieve the medications with dosages equal to the highest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)



For example:

Result
medic  medication_name  dosage
-----  ---------------  ---------------
4      Acetaminophen    600mg


```sql
SELECT 
    medication_id AS medic,
    medication_name,
    dosage
FROM 
    Medications
WHERE 
    dosage = (
        SELECT MAX(dosage) 
        FROM Medications
    );

```

**Output:**

<img width="1041" height="439" alt="image" src="https://github.com/user-attachments/assets/466ce1c9-e694-4ee4-b072-4b4d06c67084" />


**Question 9**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



For example:

Result
student_name     grade
---------------  ---------------
Bob              85
Frank            85
John             85


```sql
SELECT 
    g.student_name,
    g.grade
FROM 
    GRADES g
JOIN (
    SELECT 
        subject,
        MIN(grade) AS min_grade
    FROM 
        GRADES
    GROUP BY 
        subject
) AS min_grades
ON 
    g.subject = min_grades.subject
    AND g.grade = min_grades.min_grade;

```

**Output:**

<img width="1080" height="473" alt="image" src="https://github.com/user-attachments/assets/e7fff174-1044-455d-bee5-b609562f9408" />


**Question 10**
---
Write a SQL query to List all the details of employees those name is atleast four characters and third character must be ‘r’.

Table name: emp

name        type
----------  ----------
empno       INT
ename       VARCHAR(100)
job         VARCHAR(50)
mgr         INT
hiredate    DATE
sal         DECIMAL(10,2)
comm        DECIMAL(10,2)
deptno      INT
For example:

Result
empno       ename       job         mgr         hiredate    sal         comm        deptno
----------  ----------  ----------  ----------  ----------  ----------  ----------  ----------
7654        MARTIN      SALESMAN    7698        1981-09-28  1250        1400        30


```sql
SELECT *
FROM emp
WHERE LENGTH(ename) >= 4
  AND UPPER(SUBSTR(ename, 3, 1)) = 'R';
```

**Output:**

<img width="1332" height="285" alt="image" src="https://github.com/user-attachments/assets/21c6bf42-590d-4df8-876e-7be5c11e192a" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.

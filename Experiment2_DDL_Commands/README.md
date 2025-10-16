# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
-- In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100
 

For example:

Test	Result
SELECT * FROM Products;
ProductID   Name             Category    Price       Stock
----------  ---------------  ----------  ----------  ----------
106         Fitness Tracker  Wearables
107         Laptop           Electronic  999.99      50
108         Wireless Earbud  Accessorie              100

```sql
insert into
Products(ProductID,Name,Category,Price,Stock)
VALUES
(106,'Fitness Tracker','Wearables',NULL,NULL),
(107,'Laptop','Electronic',999.99,50),
(108,'Wireless Earbud','Accessorie',null,100);
```

**Output:**

<img width="1291" height="291" alt="image" src="https://github.com/user-attachments/assets/837acab1-ab13-4a2d-aa04-ac36675bf1c3" />


**Question 2**
---
-- Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0
For example:

Test	Result
INSERT INTO products (product_id, product_name, list_price) VALUES (2, 'Product B', 50.00);
SELECT * FROM products;
product_id  product_name  list_price  discount
----------  ------------  ----------  ----------
2           Product B     50          0

```sql
CREATE TABLE products (
    product_id   INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    list_price   DECIMAL(10,2) NOT NULL,
    discount     DECIMAL(10,2) NOT NULL DEFAULT 0,
    CHECK (
        list_price >= discount
        AND discount >= 0
        AND list_price >= 0
    )
);
```

**Output:**

<img width="1074" height="172" alt="image" src="https://github.com/user-attachments/assets/c1ca1fbb-8a5c-41ae-aa61-6c75a0a04b97" />


**Question 3**
---
Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME
For example:

Test	Result
pragma table_info('Customers');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           CustomerID  INTEGER     0                       0
1           Name        TEXT        0                       0
2           Email       TEXT        0                       0
3           JoinDate    DATETIME    0                       0

```sql
CREATE TABLE  Customers (
CustomerID INTEGER,
Name TEXT,
Email TEXT,
JoinDate DATETIME
);
```

**Output:**

<img width="1109" height="244" alt="image" src="https://github.com/user-attachments/assets/a52c5c0e-9702-4a9d-ae78-9118590cbae8" />


**Question 4**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
For example:

Test	Result
INSERT INTO Customers (CustomerID, FirstName, LastName, Email) VALUES (1, 'Alice', 'Johnson', 'alice.johnson@example.com');
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
select * from orders;
OrderID     OrderDate   CustomerID
----------  ----------  ----------
1           2024-08-01  1

```sql
CREATE TABLE Orders(
OrderID  INTEGER  primary key,
OrderDate DATE not NULL,
CustomerID INTEGER,
FOREIGN KEY(CustomerID ) REFERENCES Customers(CustomerID)
);
```

**Output:**

<img width="1023" height="183" alt="image" src="https://github.com/user-attachments/assets/5ce52a4a-379e-4c59-9c5e-90f4743fae38" />


**Question 5**
---
Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0
For example:

Test	Result
select * from student_details;
RollNo      Name           Gender      Subject     MARKS
----------  -------------  ----------  ----------  ----------
1           Alice Johnson  Female      Math        85
2           Bob Smith      Male        Science     90
3           Charlie Brown  Male        English     78

```sql
INSERT INTO Student_details (RollNo, Name, Gender, Subject, Marks)
SELECT RollNo, Name, Gender, Subject, Marks
FROM Archived_students;
```

**Output:**



**Question 6**
---
Write an SQL Query to add the attributes designation, net_salary, and dob to the Companies table with the following data types:
designation as VARCHAR(50)
net_salary as NUMBER
dob as DATE
 

 

For example:

Test	Result
pragma table_info('Companies');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          int         0                       0
1           name        varchar(50  0                       0
2           address     text        0                       0
3           email       varchar(50  0                       0
4           phone       varchar(10  0                       0
5           designatio  varchar(50  0                       0
6           net_salary  number      0                       0
7           dob         date        0                       0

```sql
ALTER TABLE Companies
ADD COLUMN designation varchar(50);

ALTER TABLE Companies
ADD COLUMN net_salary number;

ALTER TABLE Companies
ADD COLUMN dob date;
```

**Output:**

<img width="916" height="246" alt="image" src="https://github.com/user-attachments/assets/daad0bbc-44b4-409b-9143-cf9ea513c64c" />


**Question 7**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024-08-01   100.0       2024-09-01  1

```sql
CREATE TABLE Invoices (
    InvoiceID   INTEGER PRIMARY KEY,
    InvoiceDate DATE NOT NULL,
    Amount      REAL CHECK (Amount > 0),
    DueDate     DATE CHECK (DueDate > InvoiceDate),
    OrderID     INTEGER,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1343" height="175" alt="image" src="https://github.com/user-attachments/assets/385149d3-02ca-4630-9666-9116f0b95fa3" />

**Question 8**
---
Create a new table named orders with the following specifications:
ord_id as TEXT with a length of 4.
item_id as TEXT.
ord_date as DATE.
ord_qty as INTEGER.
cost as INTEGER.
The primary key is a composite key consisting of item_id and ord_date.
ord_id and item_id should not accept NULL
For example:

Test	Result
INSERT INTO orders (ord_id, item_id, ord_date, ord_qty, cost) VALUES ('O001', 'I001', '2023-08-01', 10, 100);
SELECT * FROM orders;
ord_id      item_id     ord_date    ord_qty     cost
----------  ----------  ----------  ----------  ----------
O001        I001        2023-08-01  10          100

```sql
CREATE TABLE orders (
    ord_id   TEXT NOT NULL CHECK (LENGTH(ord_id) = 4),
    item_id  TEXT NOT NULL,
    ord_date DATE NOT NULL,
    ord_qty  INTEGER,
    cost     INTEGER,
    PRIMARY KEY (item_id, ord_date)
);
```

**Output:**

<img width="1154" height="206" alt="image" src="https://github.com/user-attachments/assets/267033f0-0075-453d-b800-c61660b24a15" />


**Question 9**
---
Insert a product with ProductID 104, Name Tablet, and Category Electronics into the Products table, where Price and Stock should use default values.

For example:

Test	Result
SELECT ProductID, Name, Category, Price, Stock 
FROM Products 
WHERE ProductID = 104;
ProductID   Name        Category     Price       Stock
----------  ----------  -----------  ----------  ----------
104         Tablet      Electronics  100         50
```sql
insert into  Products(ProductID,Name,Category,Price,Stock)
values(104,'Tablet','Electronics',100,50);
```

**Output:**

<img width="1010" height="155" alt="image" src="https://github.com/user-attachments/assets/a92b4bb5-f550-4f70-b580-e7c2f49181e7" />


**Question 10**
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

<img width="1314" height="348" alt="image" src="https://github.com/user-attachments/assets/b88e1cad-7991-4856-a1b5-f9cdda2892db" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

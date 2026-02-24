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
For  Increase the selling price per unit by 3 for all products supplied by supplier ID 4 in the sales table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT

SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)
For example:

Test	Result
select changes();
changes()
----------
1

```sql
UPDATE sales SET sell_price =sell_price+3 WHERE product_id IN(SELECT product_id FROM products WHERE supplier_id=4);
```

**Output:**


<img width="1236" height="463" alt="image" src="https://github.com/user-attachments/assets/f56e36c3-292d-4bb9-b27b-2ba02b43e0d0" />


**Question 2**
---
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.

products table

---------------
product_id
product_name
category_id
availability

```sql
UPDATE products SET product_name = 'Grapefruit' WHERE product_id=4;
```

**Output:**

<img width="1219" height="314" alt="image" src="https://github.com/user-attachments/assets/9fb5853b-603b-43e1-8b9c-e49ca67f8b43" />


**Question 3**
---
Write a SQL statement to Change the supplier name to 'A1 Suppliers' where the supplier ID is 8 in the suppliers table.

Table info

suppliers(supplier_id,supplier_name,contact_person,phone_number,email,address)

For example:

Test	Result
select changes();
changes()
----------
1


```sql
UPDATE suppliers SET supplier_name = 'A1 Suppliers' WHERE  supplier_id=8;
```

**Output:**

<img width="1232" height="464" alt="image" src="https://github.com/user-attachments/assets/6ead17a4-4131-4a30-b626-a8ba7ec4f1f3" />


**Question 4**
---
Decrease the reorder level by 30 percent where the product name contains 'cream' and quantity in stock is higher than reorder level in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
 

For example:

Test	Result
select changes();
changes()
----------
3


```sql
UPDATE products SET reorder_lvl = reorder_lvl * 0.70 WHERE product_name LIKE '%cream%' AND quantity>reorder_lvl;
```

**Output:**

<img width="1217" height="565" alt="image" src="https://github.com/user-attachments/assets/42554573-6e3a-4d0a-a2b4-1328832a8242" />


**Question 5**
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

SELECT * FROM emp WHERE ename LIKE '__r_%';

```

**Output:**


<img width="1222" height="416" alt="image" src="https://github.com/user-attachments/assets/fe9ed2ce-b0c3-4b17-a264-216c431858eb" />


**Question 6**
---
Write a SQL query to locate the details of customers with grade values above 100. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

For example:

Result
customer_id   cust_name        city          grade  salesman_id
------------  ---------------  ------------  -----  -----------
3007          Brad Davis       New York      200    5001
3008          Julian Green     London        300    5002


```sql
SELECT customer_id,cust_name,city,grade,salesman_id FROM customer WHERE grade>100;
```

**Output:**


<img width="1222" height="505" alt="image" src="https://github.com/user-attachments/assets/87c2b7d4-6f53-42a0-a0eb-df7f459f7958" />


**Question 7**
---
Write a SQL query to label rows in the Calculations table as 'Even' if value1 is even, otherwise 'Odd'.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
 

For example:

Result
id          value1      parity
----------  ----------  ----------
1           -87.65      Odd
2           45.78       Odd
3           89.99       Odd
4           -0.005      Even


```sql
SELECT id,value1,CASE WHEN CAST(value1 AS INTEGER)%2 =0 THEN 'Even'ELSE 'Odd' END AS parity FROM Calculations;
```

**Output:**


<img width="917" height="512" alt="image" src="https://github.com/user-attachments/assets/c4a5d9b2-f513-43a4-ad43-ecd967ad34ce" />


**Question 8**
---
Write a SQL query to find all orders that meet the following conditions. Exclude combinations of order date equal to '2012-08-17' or customer ID greater than 3005 and purchase amount less than 1000.

Sample table : orders

ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
For example:

Result
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70009       270.65      2012-09-10  3001         5005
70008       5760.0      2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006


```sql
SELECT * FROM orders WHERE NOT ((ord_date ='2012-08-17' OR Customer_id>3005) AND purch_amt<1000);
```

**Output:**

<img width="1222" height="877" alt="image" src="https://github.com/user-attachments/assets/60e7a12e-d5ca-42e3-8289-57b9d54c4ee3" />


**Question 9**
---
Write a SQL query to find customers who are either from the city 'New York' or who have a grade greater than 200. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
For example:

Result
customer_id  cust_name     city        grade       salesman_id
-----------  ------------  ----------  ----------  -----------
3004         Fabian Johns  Paris       300         5006
3007         Brad Davis    New York    200         5001
3008         Julian Green  London      300         5002


```sql
SELECT customer_id,cust_name,city,grade,salesman_id FROM customer WHERE city='New York' OR grade>200;
```

**Output:**


<img width="1217" height="514" alt="image" src="https://github.com/user-attachments/assets/953bcd1c-4a9c-4eb5-bdd8-2cf949e18318" />


**Question 10**
---
Write a SQL query to calculate the discounted price for products where the discount percentage is greater than 0, and order the results by discounted_price in ascending order. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products

product_id | original_price | discount_percentage 

------------+----------------+--------------------- 

101 | 50.00 | 0.10 

102 | 75.00 | 0.00 

103 | 100.00 | 0.20

 

For example:

Result
product_id  original_price  discount_percentage  discounted_price
----------  --------------  -------------------  ----------------
101         50.0            0.1                  45.0
102         75.0            0.15                 63.75
103         100.0           0.2                  80.0


```sql
SELECT product_id,original_price,discount_percentage,original_price *(1- discount_percentage)AS discounted_price
FROM Products WHERE discount_percentage>0 ORDER BY discounted_price ASC;
```

**Output:**


<img width="1204" height="355" alt="image" src="https://github.com/user-attachments/assets/01be3d1a-2559-482d-9081-0fe96b2b3138" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.

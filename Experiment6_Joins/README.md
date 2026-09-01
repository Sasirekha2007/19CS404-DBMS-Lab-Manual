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
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
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

```sql
SELECT s.name AS Salesman, c.cust_name, s.city
FROM salesman s
JOIN customer c
ON s.city = c.city;
```

**Output:**


<img width="897" height="790" alt="image" src="https://github.com/user-attachments/assets/e44eb9e2-0d2a-44a3-8c53-fef80a6f8f1c" />


**Question 2**
---
Write an SQL query to select all columns from the 'customer' table (aliased as 'c') by performing a LEFT JOIN with the 'orders' table on the 'customer_id' column, including only those orders where the order date falls between '2012-08-01' and '2012-08-30'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

 

For example:

Result
customer_id      cust_name        city             grade            salesman_id
---------------  ---------------  ---------------  ---------------  -----------
3009             Geoff Cameron    Berlin           100              5003
3003             Jozy Altidore    Moscow           200              5007


```sql
SELECT c.*
FROM customer c
JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.ord_date BETWEEN '2012-08-01' AND '2012-08-30';
```

**Output:**

<img width="910" height="580" alt="image" src="https://github.com/user-attachments/assets/8c987070-68a4-42ce-9dce-245db1fd57f3" />


**Question 3**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

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
SELECT c.cust_name,
       c.city,
       c.grade,
       s.name AS Salesman,
       s.city
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;
```

**Output:**

<img width="872" height="838" alt="image" src="https://github.com/user-attachments/assets/deddac0a-9fff-4a6d-a307-120ac2a1c26d" />


**Question 4**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

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
    c.cust_name,
    c.city,
    c.grade,
    s.name AS Salesman,
    s.city
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE c.grade < 300
ORDER BY c.customer_id;
```

**Output:**


<img width="877" height="783" alt="image" src="https://github.com/user-attachments/assets/d90011f5-10b5-443e-84e4-c56c32318dd4" />


**Question 5**
---
 From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

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
    s.name AS Salesman,
    s.commission
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;
```

**Output:**

<img width="862" height="772" alt="image" src="https://github.com/user-attachments/assets/33229ae7-7260-417f-b9c5-69a439be8dca" />


**Question 6**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
TEST_RESULT TABLES:
ATTRIBUTES - result_id, patient_id, test_name, result, test_date



```sql
SELECT p.first_name AS patient_name,
       t.test_name
FROM patients p
INNER JOIN test_results t
ON p.patient_id = t.patient_id;
```

**Output:**

<img width="897" height="631" alt="image" src="https://github.com/user-attachments/assets/3acde394-8656-4f5f-b792-c37ef03ed3de" />


**Question 7**
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "commission" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

For example:

Result
cust_name        commission
---------------  ---------------
Nick Rimando     0.15
Graham Zusi      0.13
Brad Guzan       0.11
Fabian Johns     0.14
Brad Davis       0.15
Geoff Cameron    0.12
Julian Green     0.13
Jozy Altidore    0.13

```sql
SELECT c.cust_name,
       s.commission
FROM customer c
LEFT JOIN salesman s
ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="862" height="828" alt="image" src="https://github.com/user-attachments/assets/15d3767a-c276-4446-94d8-f832fe2ce43f" />


**Question 8**
---
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n"), with an inner join on the "department_id" column and a condition filtering for nurses in the 'Pediatrics' department.

NURSES TABLE:

ATTRIBUTES - nurse_id, first_name, last_name, department_id



DEPARTMENTS TABLE:

ATTRIBUTES - department_id, department_name



```sql
SELECT n.*
FROM nurses n
INNER JOIN departments d
ON n.department_id = d.department_id
WHERE d.department_name = 'Pediatrics';
```

**Output:**

<img width="907" height="507" alt="image" src="https://github.com/user-attachments/assets/7388ca09-dbf3-42fe-b875-411c177bb797" />


**Question 9**
-Write the SQL query that accomplishes the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

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
surgery_date     DATE--

```sql
SELECT p.first_name,
       s.*
FROM patients p
INNER JOIN surgeries s
ON p.patient_id = s.patient_id
WHERE p.first_name = 'Alice';
```

**Output:**


<img width="902" height="490" alt="image" src="https://github.com/user-attachments/assets/147a379c-290a-4520-837a-866fa85789f1" />


**Question 10**

From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

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
For example:

```sql
SELECT o.ord_no,
       o.ord_date,
       o.purch_amt,
       c.cust_name AS "Customer Name",
       c.grade,
       s.name AS Salesman,
       s.commission
FROM orders o
INNER JOIN customer c
ON o.customer_id = c.customer_id
INNER JOIN salesman s
ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="862" height="823" alt="image" src="https://github.com/user-attachments/assets/c9b352ca-d635-4184-ac5b-b04752ed471c" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.

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
How many patients are covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT
```sql
select InsuranceCompany, count(PatientID)
as TotalPatients from Insurance group by InsuranceCompany;
```

**Output:**
<img width="855" height="750" alt="image" src="https://github.com/user-attachments/assets/dd312383-d8a1-4086-aed3-ff1ccfc0c01b" />


**Question 2**
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
select PatientID, count(AppointmentID) as TotalAppointments from Appointments group by PatientID;
```
**Output:**

<img width="855" height="722" alt="image" src="https://github.com/user-attachments/assets/a841a750-c541-4caa-bf55-57b9c0b9907d" />


**Question 3**
---
<img width="908" height="257" alt="image" src="https://github.com/user-attachments/assets/8af1dd0d-6c0b-4f89-ab96-03b900c8069a" />


```sql
select PatientID, count(RecordID) as TotalRecords from MedicalRecords group by PatientID;
```

**Output:**

<img width="870" height="752" alt="image" src="https://github.com/user-attachments/assets/e435556a-5bbe-4876-a77e-b6d56c1c85a3" />


**Question 4**
---
<img width="891" height="501" alt="image" src="https://github.com/user-attachments/assets/37622463-f402-44b6-824a-7b96505debb4" />


```sql
select sum(workhour) as "Total working hours" from employee1;
```

**Output:**

<img width="867" height="396" alt="image" src="https://github.com/user-attachments/assets/9ed029f7-d7b6-4d3d-88bc-4093a83d2dc0" />


**Question 5**
---
Write a SQL query to  find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
select avg(income) as "Average_Salary" from employee;
```

**Output:**

<img width="877" height="385" alt="image" src="https://github.com/user-attachments/assets/3402d9a3-518d-4efc-a06c-01b09a507e2f" />


**Question 6**
---
Write a SQL query to find the total number of unique cities in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER

```sql
select count(distinct city) as unique_cities from customer;
```

**Output:**

<img width="873" height="416" alt="image" src="https://github.com/user-attachments/assets/5fda06b6-d2f5-4215-a09f-7dc91dd56ae9" />


**Question 7**
---
Write a SQL query to calculate the average purchase amount of all orders. Return average purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

```sql
select avg(purch_amt) as AVERAGE from orders;
```

**Output:**

<img width="872" height="405" alt="image" src="https://github.com/user-attachments/assets/f2bcc24a-3342-418c-b130-46d25dae683d" />


**Question 8**
---
Write the SQL query that accomplishes the selection of total cost of all products in each category from the "products" table and includes only those products where the total cost is greater than 50.

```sql
select category_id, sum(price) as Total_Cost from products group by category_id having sum(price)>50;
```

**Output:**

<img width="896" height="410" alt="image" src="https://github.com/user-attachments/assets/deec6ebb-b810-48e3-9270-3042a3fbca35" />


**Question 9**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the average work hours for each date, and excludes dates where the average work hour is not less than 10.

Sample table: employee1



```sql
select jdate, AVG(workhour) from employee1 group by jdate having AVG(workhour)<10;
```

**Output:**

<img width="871" height="420" alt="image" src="https://github.com/user-attachments/assets/2e1d6c99-6bf2-41ce-8c64-57b69a4e094d" />


**Question 10**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the total work hours for each occupation, and excludes occupations where the total work hour sum is not greater than 20.

Sample table: employee1



```sql
select occupation, SUM(workhour) from employee1 group by occupation having SUM(workhour)>20;
```

**Output:**
<img width="855" height="537" alt="image" src="https://github.com/user-attachments/assets/1ee46784-7cd1-444e-bf67-00834deb94c3" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.

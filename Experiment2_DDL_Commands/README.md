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
Write a SQL Query for inserting the below values in the table Customers

ID               NAME             AGE  ADDRESS     SALARY      
---------------  ---------------  ---  ----------  ----------  
1                Ramesh           32   Ahmedabad   2000
2                Khilan           25   Delhi       1500
3                Kaushik          23   Kota        2000
 

For example:

Test	Result
SELECT * FROM Customers;
ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------
1           Ramesh      32          Ahmedabad   2000
2           Khilan      25          Delhi       1500
3           Kaushik     23          Kota        2000


```
insert into Customers(ID,NAME,AGE,ADDRESS,SALARY)values(1,'Ramesh',32,'Ahmedabad',2000),(2,'Khilan', 25,'Delhi',1500),(3,'Kaushik',23,'Kota',2000);  
```

**Output:**
<img width="851" height="371" alt="image" src="https://github.com/user-attachments/assets/ed4ebc2b-ed45-4911-912c-6271be0d4fc4" />



**Question 2**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT
For example:

Test	Result
pragma table_info('Reviews');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           ReviewID    INTEGER     0                       0
1           ProductID   INTEGER     0                       0
2           Rating      REAL        0                       0
3           ReviewText  TEXT        0                       0

```sql
create table Reviews (ReviewID INTEGER,ProductID INTEGER,Rating REAL,ReviewText TEXT);
```

**Output:**

<img width="825" height="372" alt="image" src="https://github.com/user-attachments/assets/3e30e580-22c8-4fba-88c4-3b5619aa46f2" />


**Question 3**
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

```sql
create table Orders(OrderID INTEGER PRIMARY KEY,OrderDate DATE NOT NULL,CustomerID INTEGER, FOREIGN KEY(CustomerID) REFERENCES Customers(CustomerID));
```

**Output:**

<img width="892" height="352" alt="image" src="https://github.com/user-attachments/assets/88da55e7-bac8-47b8-9fda-7923b9fbff6c" />


**Question 4**
---
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.
 
For example:

Test	Result
SELECT CustomerID, Name, Address
FROM Customers;
CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St


```sql
insert into Customers(CustomerID,Name,Address)values(304,'Peter Parker','Spider St');
```

**Output:**

<img width="852" height="426" alt="image" src="https://github.com/user-attachments/assets/e2539474-9958-47f0-b1fc-d84cc0a79ca6" />


**Question 5**
---
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
For example:

Test	Result
INSERT INTO Attendance (AttendanceID, EmployeeID, AttendanceDate, Status) VALUES (1, 1, '2024-08-01', 'Present');
SELECT * FROM Attendance;

```sql
create table Attendance(AttendanceID INTEGER PRIMARY KEY,EmployeeID INTEGER REFERENCES Employees(EmployeeID), AttendanceDate DATE,Status TEXT CHECK (Status IN ('Present','Absent','Leave')));
```

**Output:**

<img width="853" height="391" alt="image" src="https://github.com/user-attachments/assets/d6285ed6-7902-4977-990d-56dea4371669" />


**Question 6**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

For example:

Test	Result
select * from Books;
ISBN            Title           Author              Publisher      YearPublished
--------------  --------------  ------------------  -------------  -------------
978-1234567890  The Lost World  Arthur Conan Doyle  Vintage Books  1912
978-0987654321  Gone with the   Margaret Mitchell   Macmillan      1936
978-1122334455  Moby Dick       Herman Melville     Harper & Brot  1851

```sql
INSERT INTO Books
SELECT * FROM Out_of_print_books;
```

**Output:**

<img width="857" height="360" alt="image" src="https://github.com/user-attachments/assets/8193a019-4b95-4585-99c5-cd0a766f34ee" />


**Question 7**
---
Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

For example:

Test	Result
pragma table_info('Student_details');
cid    name             type             notnu  dflt_value  pk
-----  ---------------  ---------------  -----  ----------  ----------
0      RollNo           int              0                  1
1      Name             VARCHAR(100)     1                  0
2      Gender           TEXT             1                  0
3      Subject          VARCHAR(30)      0                  0
4      MARKS            INT (3)          0                  0
5      MobileNumber     NUMBER           0                  0
6      Address          VARCHAR(100)     0                  0


```sql
alter table Student_details add MobileNumber NUMBER;

alter table Student_details add Address VARCHAR(100);
```

**Output:**

<img width="888" height="457" alt="image" src="https://github.com/user-attachments/assets/5a2fbafd-8f70-4ef3-9cc7-03f8d16543a0" />


**Question 8**
---
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName


```sql
create table Products (ProductID INTEGER PRIMARY KEY,ProductName VARCHAR(100) NOT NULL,Price REAL NOT NULL CHECK (Price > 0),Stock INTEGER NOT NULL CHECK(Stock>=0));
```

**Output:**

<img width="863" height="355" alt="image" src="https://github.com/user-attachments/assets/351bd60c-925c-4629-8c92-575898d3f205" />


**Question 9**
---
Write a SQL Query  to add attribute ISBN as varchar(30) and domain_dept as varchar(30) in the table 'books'

 

 

For example:

Test	Result
pragma table_info('books');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           book_id     INT         0                       1
1           title       VARCHAR(15  0                       0
2           author      VARCHAR(10  0                       0
3           genre       VARCHAR(50  0                       0
4           publicatio  INT         0                       0
5           ISBN        varchar(30  0                       0
6           domain_dep  varchar(30  0                       0


```sql
alter table books add ISBN varchar(30);

alter table books add domain_dept varchar(30);
```

**Output:**

<img width="855" height="467" alt="image" src="https://github.com/user-attachments/assets/df40eebb-70e7-4e3d-9244-9240e9065d45" />


**Question 10**
---
Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700     

```sql
create table item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT(4),
FOREIGN KEY(icom_id) REFERENCES company(com_id) ON UPDATE CASCADE ON DELETE CASCADE);
```

**Output:**

<img width="920" height="455" alt="image" src="https://github.com/user-attachments/assets/9a49def6-4dcf-4b2e-9155-ccc912976751" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

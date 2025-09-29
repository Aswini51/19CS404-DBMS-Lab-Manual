## Experiment 2: DDL Commands

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
```
Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0
```
<img width="703" height="194" alt="Screenshot 2025-09-29 134208" src="https://github.com/user-attachments/assets/47e5b189-d6e5-4ef2-81cc-139781755f31" />

```
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
SELECT RollNo, Name, Gender, Subject, MARKS
FROM Archived_students;
```
**Output:**
<img width="1281" height="232" alt="Screenshot 2025-09-29 134216" src="https://github.com/user-attachments/assets/4c4fd156-7cde-4af3-a7ab-8c4e60d3b627" />

**Question 2**

Insert a student with RollNo 201, Name David Lee, Gender M, Subject Physics, and MARKS 92 into the Student_details table.

<img width="821" height="159" alt="Screenshot 2025-09-29 134244" src="https://github.com/user-attachments/assets/a837d6bd-8056-4c78-a9b9-c9f1c626b3cb" />

```
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES (201, 'David Lee', 'M', 'Physics', 92);
```

**Output:**

<img width="1282" height="223" alt="Screenshot 2025-09-29 134301" src="https://github.com/user-attachments/assets/50918a7c-2705-4897-94bc-1cbda2e78c35" />

**Question 3**
```
Write a SQL Query for inserting the below values in the table Customers

ID               NAME             AGE  ADDRESS     SALARY      
---------------  ---------------  ---  ----------  ----------  
1                Ramesh           32   Ahmedabad   2000
2                Khilan           25   Delhi       1500
3                Kaushik          23   Kota        2000
```

<img width="604" height="191" alt="Screenshot 2025-09-29 134312" src="https://github.com/user-attachments/assets/0ccc9b78-a6ad-4864-8687-32790ffbddc4" />

```
INSERT INTO Customers (ID, NAME, AGE, ADDRESS, SALARY)
VALUES 
(1, 'Ramesh', 32, 'Ahmedabad', 2000),
(2, 'Khilan', 25, 'Delhi', 1500),
(3, 'Kaushik', 23, 'Kota', 2000);
```

**Output:**

<img width="1089" height="257" alt="Screenshot 2025-09-29 134324" src="https://github.com/user-attachments/assets/3a6c7aa7-db4d-47bb-b30c-58d5a4f21d27" />

**Question 4**

Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).
<img width="1116" height="147" alt="Screenshot 2025-09-29 134333" src="https://github.com/user-attachments/assets/94f2c3e9-5b50-4fad-b1e2-708d9456d120" />

```
CREATE TABLE Orders (
    OrderID     INTEGER PRIMARY KEY,
    OrderDate   DATE NOT NULL,
    CustomerID  INTEGER,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

**Output:**

<img width="1312" height="233" alt="Screenshot 2025-09-29 134346" src="https://github.com/user-attachments/assets/f0c9c485-7a06-4127-80b5-8622dccb625b" />

**Question 5**

Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.

<img width="523" height="130" alt="Screenshot 2025-09-29 134355" src="https://github.com/user-attachments/assets/a7ddc812-2a3e-43a7-acc6-8d5e2620467d" />

```
CREATE TABLE Products (
    ProductID   INTEGER PRIMARY KEY,
    ProductName VARCHAR(100) NOT NULL,
    Price       REAL CHECK (Price > 0),
    Stock       INTEGER CHECK (Stock >= 0)
);
```

**Output:**

<img width="951" height="221" alt="Screenshot 2025-09-29 134401" src="https://github.com/user-attachments/assets/58f53bc7-3889-4446-b21c-e132131b0c7a" />

**Question 6**

Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

<img width="924" height="142" alt="Screenshot 2025-09-29 134408" src="https://github.com/user-attachments/assets/6796959b-1759-4458-b647-34cab60b0e91" />

```
CREATE TABLE Department (
    DepartmentID   INTEGER PRIMARY KEY,
    DepartmentName TEXT UNIQUE NOT NULL,
    Location       TEXT
);
```

**Output:**

<img width="1209" height="177" alt="Screenshot 2025-09-29 134428" src="https://github.com/user-attachments/assets/6eca3392-73be-4de4-a6c0-3dab2991f36a" />

**Question 7**

Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

<img width="885" height="111" alt="Screenshot 2025-09-29 134442" src="https://github.com/user-attachments/assets/62724049-ccdf-4627-ae2a-c92b96b769e2" />

```
CREATE TABLE Shipments (
    ShipmentID   INTEGER PRIMARY KEY,
    ShipmentDate DATE,
    SupplierID   INTEGER,
    OrderID      INTEGER,
    FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1150" height="195" alt="Screenshot 2025-09-29 134450" src="https://github.com/user-attachments/assets/d69f9421-77e1-4b3b-999f-bc758dfbc08b" />

**Question 8**

Write a SQL query to Add a new ParentsNumber column  as number and Adhar_Number as Number in the Student_details table.

<img width="694" height="233" alt="Screenshot 2025-09-29 134458" src="https://github.com/user-attachments/assets/d6bb62e9-9973-43b6-adfc-be042d890b09" />

```
ALTER TABLE Student_details
ADD COLUMN ParentsNumber number;

ALTER TABLE Student_details
ADD COLUMN Adhar_Number number;
```
**Output:**

<img width="1204" height="301" alt="Screenshot 2025-09-29 134528" src="https://github.com/user-attachments/assets/77127944-1500-4919-bd7b-9f9675989e33" />

**Question 9**

Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

```
cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
```

<img width="684" height="222" alt="Screenshot 2025-09-29 134547" src="https://github.com/user-attachments/assets/d69843b8-3fb7-44da-aab5-f27cf43faa28" />

```
ALTER TABLE Student_details
ADD COLUMN Country TEXT;
```

**Output:**

<img width="1196" height="275" alt="Screenshot 2025-09-29 134554" src="https://github.com/user-attachments/assets/0b99039f-49a1-48cd-b2ef-5beb2ce98c49" />

**Question 10**

Create a table named Members with the following columns:

MemberID as INTEGER
MemberName as TEXT
JoinDate as DATE

<img width="669" height="182" alt="Screenshot 2025-09-29 134559" src="https://github.com/user-attachments/assets/f9e3d520-de08-44c4-af68-8b7c402eee27" />

```
CREATE TABLE Members (
    MemberID   INTEGER,
    MemberName TEXT,
    JoinDate   DATE
);
```
**Output:**

<img width="1304" height="287" alt="Screenshot 2025-09-29 134614" src="https://github.com/user-attachments/assets/a4d712af-fd62-4eb5-bcad-dd7d5c1a9356" />

## RESULT:

Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.

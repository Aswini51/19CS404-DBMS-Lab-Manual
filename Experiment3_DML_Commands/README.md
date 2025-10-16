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

Write a SQL statement to Increase the selling price by 15% in the products table where quantity in stock is less than 50 and supplier ID is 10.

<img width="825" height="197" alt="image" src="https://github.com/user-attachments/assets/463ee1bd-343e-4d73-bb2b-550983c60d4f" />

```
UPDATE Products
SET sell_price = sell_price * 1.15
WHERE quantity < 50 AND supplier_id = 10;
```

**Output:**

<img width="1376" height="284" alt="image" src="https://github.com/user-attachments/assets/413b434f-ea77-4ec3-9ee0-37f291ac2323" />

**Question 2**

Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'

<img width="688" height="126" alt="image" src="https://github.com/user-attachments/assets/5735faf5-c63e-4171-896c-edb76b066e0f" />

```
UPDATE Employees
SET salary = salary * 2
WHERE department_id = 20
  AND job_id LIKE '%MAN';
```

**Output:**

<img width="942" height="211" alt="image" src="https://github.com/user-attachments/assets/99f9dad5-782e-42e8-8e02-55c01e76b131" />

**Question 3**

Write a SQL statement to Update the product_name to 'Premium Bread' whose product ID is 5 in the products table.

<img width="227" height="155" alt="image" src="https://github.com/user-attachments/assets/89643968-9a43-4399-9332-12abeef338c6" />

```
UPDATE Products
SET product_name = 'Premium Bread'
WHERE product_id = 5;
```

**Output:**

<img width="1191" height="233" alt="image" src="https://github.com/user-attachments/assets/2561cd6d-207e-469a-a370-e1ecd0353046" />

**Question 4**

Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

<img width="221" height="161" alt="image" src="https://github.com/user-attachments/assets/946f5b3e-39d1-4919-8e29-47e1d0035c7d" />

```
UPDATE Products
SET sell_price = sell_price * 1.10
WHERE category = 'Bakery';
```

**Output:**

<img width="1246" height="295" alt="image" src="https://github.com/user-attachments/assets/bc02c270-d0f5-4471-b57b-10fdb89231e1" />

**Question 5**

Write a SQL statement to change the EMAIL and COMMISSION_PCT column of the following EMPLOYEES table with 'not available' and 0.55 for those employees whose DEPARTMENT_ID is 110.

<img width="575" height="108" alt="image" src="https://github.com/user-attachments/assets/663dcec6-9b08-48e0-a7ed-f6a8cc2ccd90" />

```
UPDATE Employees
SET email = 'not available',
    commission_pct = 0.55
WHERE department_id = 110;
```

**Output:**

<img width="888" height="215" alt="image" src="https://github.com/user-attachments/assets/b35921e7-449d-4d6a-bfb5-bc8437472158" />

**Question 6**

Write a SQL query to Delete customers from 'customer' table where 'GRADE' is not equal to 3.

<img width="771" height="283" alt="Screenshot 2025-10-15 103925" src="https://github.com/user-attachments/assets/05277acb-3930-4875-9a4a-a2e848a4d46a" />

```
DELETE FROM Customer
WHERE GRADE <> 3;
```

**Output:**

<img width="400" height="303" alt="image" src="https://github.com/user-attachments/assets/52be0020-bfbf-4c34-99a8-07e8ab5e7aca" />

**Question 7**

Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.

<img width="761" height="215" alt="image" src="https://github.com/user-attachments/assets/cabcb69f-16f0-486b-b904-17312d43304c" />

```
DELETE FROM Customer
WHERE GRADE % 2 = 1;
```

**Output:**

<img width="1058" height="165" alt="image" src="https://github.com/user-attachments/assets/0307c63c-a6bd-446f-a029-6230f1c85931" />

**Question 8**

Write a SQL query to delete a specific doctor from Doctors table whose ID is 1.

<img width="338" height="72" alt="image" src="https://github.com/user-attachments/assets/2a78717d-28a3-45c1-8534-423c45fdf35b" />

```
DELETE FROM Doctors
WHERE doctor_id = 1;
```

**Output:**

<img width="649" height="158" alt="image" src="https://github.com/user-attachments/assets/440a5e9c-d8fb-4c2c-97dd-6d9a35511975" />

**Question 9**

Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

<img width="389" height="246" alt="image" src="https://github.com/user-attachments/assets/c14e66f0-2cd3-49ae-8fd4-38a5218563b9" />

```
DELETE FROM Doctors
WHERE doctor_id BETWEEN 2 AND 4;
```

**Output:**

<img width="665" height="461" alt="image" src="https://github.com/user-attachments/assets/e6aa0fc3-a64a-4401-8011-233f60234f5d" />

**Question 10**

Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

<img width="310" height="69" alt="image" src="https://github.com/user-attachments/assets/fe1e3995-4baa-4f46-bc64-f17703a93606" />

```
DELETE FROM Doctors
WHERE specialization = 'Pediatrics'
  AND first_name = 'Michael';
```

**Output:**

<img width="649" height="217" alt="image" src="https://github.com/user-attachments/assets/7249c0c5-5fa4-48ac-8146-471dc982d649" />

## RESULT

Thus, the SQL queries to implement DML commands have been executed successfully.

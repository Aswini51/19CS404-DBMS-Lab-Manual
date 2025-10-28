# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM:
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY:

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

How many male and female doctors are there in each medical specialty?

Sample table:Doctors Table

<img width="991" height="533" alt="image" src="https://github.com/user-attachments/assets/cbcf78bf-7c92-45bd-9201-3f5d316dc15d" />

```
SELECT 
    Specialty, 
    Gender, 
    COUNT(*) AS TotalDoctors
FROM Doctors
GROUP BY Specialty, Gender;
```

**Output:**

<img width="934" height="720" alt="image" src="https://github.com/user-attachments/assets/9e5ce402-0980-4c7e-bdd9-7bc6c5c7cab4" />

**Question 2**

How many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

Sample tablePrescriptions Table

<img width="979" height="548" alt="Screenshot 2025-10-28 180949" src="https://github.com/user-attachments/assets/3ae9074d-3c2e-4802-b066-fe2c9ac448f8" />

```
SELECT 
    Frequency, 
    COUNT(*) AS TotalPrescriptions
FROM Prescriptions
GROUP BY Frequency;
```

**Output:**

<img width="761" height="612" alt="image" src="https://github.com/user-attachments/assets/9141bceb-39b3-4106-9673-2a763a33a203" />

**Question 3**

What is the most common diagnosis among patients?

Sample table:MedicalRecords Table

<img width="978" height="415" alt="image" src="https://github.com/user-attachments/assets/bf4396e2-86ad-4235-86bd-c419e261fe63" />

```
SELECT 
    Diagnosis, 
    COUNT(*) AS DiagnosisCount
FROM MedicalRecords
GROUP BY Diagnosis
ORDER BY DiagnosisCount DESC
LIMIT 1;
```

**Output:**

<img width="824" height="382" alt="image" src="https://github.com/user-attachments/assets/2454e096-a7f6-4bf0-8300-21ee983e7373" />

**Question 4**

Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

Note: Inventory attribute contains amount of fruits

<img width="279" height="520" alt="image" src="https://github.com/user-attachments/assets/27f0d7db-d4a0-4967-8b19-676ef98ea1c7" />

```
SELECT 
    SUM(inventory) AS total
FROM fruits
WHERE unit = 'LB';
```

**Output:**

<img width="330" height="379" alt="image" src="https://github.com/user-attachments/assets/f024cf78-e4d7-4aad-83ab-2f8ca5df8711" />

**Question 5**

Write a SQL query to find the customer with longest name?

Table: customer

<img width="280" height="440" alt="image" src="https://github.com/user-attachments/assets/bbcb153b-1655-42ec-b74d-8110ca9d062c" />

```
SELECT 
    name, 
    LENGTH(name) AS length
FROM customer
ORDER BY length DESC
LIMIT 1;
```

**Output:**

<img width="652" height="377" alt="image" src="https://github.com/user-attachments/assets/4ff03e20-5c8a-4fdc-9839-54203723115e" />

**Question 6**

Write a SQL query to find the difference between the maximum and minimum price of fruits?

Table: fruits

<img width="284" height="472" alt="image" src="https://github.com/user-attachments/assets/93f17c9c-926b-48c4-9293-90bd75c2ad54" />

```
SELECT 
    (MAX(price) - MIN(price)) AS price_diff
FROM fruits;
```

**Output:**

<img width="343" height="376" alt="image" src="https://github.com/user-attachments/assets/34dd2d45-f656-40e2-b51f-723226a2562e" />

**Question 7**

Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

<img width="757" height="440" alt="image" src="https://github.com/user-attachments/assets/4624bc42-9f9d-4586-ad33-761fe32c33b7" />

```
SELECT 
    COUNT(DISTINCT age) AS COUNT
FROM employee;
```

**Output:**

<img width="339" height="380" alt="image" src="https://github.com/user-attachments/assets/03b97369-6883-4781-b85b-587234a76a1d" />

**Question 8**

Write the SQL query that accomplishes the grouping of data by age, calculates the total income for each age group, and includes only those age groups where the total income sum is greater than 1,000,000.

Sample table: employee

<img width="795" height="452" alt="image" src="https://github.com/user-attachments/assets/ceccf7b4-d263-45cf-a51f-392e0f1ae344" />

```
SELECT 
    age, 
    SUM(income) AS "SUM(income)"
FROM employee
GROUP BY age
HAVING SUM(income) > 1000000;
```

**Output:**

<img width="569" height="485" alt="image" src="https://github.com/user-attachments/assets/7f5ce442-46a9-4b3d-927c-561446ac384e" />

**Question 9**

Write the SQL query that achieves the grouping of data by occupation, calculates the total work hours for each occupation, and excludes occupations where the total work hour sum is not greater than 20.

Sample table: employee1

<img width="804" height="489" alt="image" src="https://github.com/user-attachments/assets/fef65a90-3846-4173-86b9-bb783ae91790" />

```
SELECT 
    occupation, 
    SUM(workhour) AS "SUM(workhour)"
FROM employee1
GROUP BY occupation
HAVING SUM(workhour) > 20;
```

**Output:**

<img width="612" height="523" alt="image" src="https://github.com/user-attachments/assets/37e96b67-5f2a-4561-bb09-6ce321d77d25" />

**Question 10**

Write the SQL query that achieves the selection of category and calculates the sum of the product of price and category ID as Revenue for each category from the "products" table, and includes only those products where the total revenue is greater than 25.

Sample table: products

<img width="796" height="478" alt="image" src="https://github.com/user-attachments/assets/0d333a01-d63a-4c7d-a586-2e94b0fdeae6" />

```
SELECT 
    category_id, 
    SUM(price * category_id) AS Revenue
FROM products
GROUP BY category_id
HAVING SUM(price * category_id) > 25;
```

**Output:**

<img width="566" height="498" alt="image" src="https://github.com/user-attachments/assets/672c1e2d-61f1-42a8-8c2c-a75814310bd1" />

## RESULT:

Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.

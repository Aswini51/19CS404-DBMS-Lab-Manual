# Experiment 6: Joins

## AIM:
To study and implement different types of joins.

## THEORY:

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

Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for test results with a test date between '2024-03-01' and '2024-03-31'.

<img width="934" height="608" alt="image" src="https://github.com/user-attachments/assets/8fe6ba59-c196-48ec-a80c-e10787863eac" />

```
SELECT 
    p.*
FROM 
    patients p
INNER JOIN 
    test_results t
ON 
    p.patient_id = t.patient_id
WHERE 
    t.test_date BETWEEN '2024-03-01' AND '2024-03-31';
```

**Output:**

<img width="1069" height="238" alt="image" src="https://github.com/user-attachments/assets/6541e3e9-52dc-425e-b887-efca66830266" />

**Question 2**

Write the SQL query that achieves the selection of all columns from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers with the name 'Fabian Johns'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

<img width="636" height="246" alt="image" src="https://github.com/user-attachments/assets/56f3ab67-f98b-4d1f-bbe9-d6381a349d0d" />

```
SELECT 
    s.*
FROM 
    salesman s
LEFT JOIN 
    customer c
ON 
    s.salesman_id = c.salesman_id
WHERE 
    c.cust_name = 'Fabian Johns';
```

**Output:**

<img width="1213" height="414" alt="image" src="https://github.com/user-attachments/assets/2621093a-0593-4b73-aae2-0f5480b046eb" />

**Question 3**

Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for customers with a grade less than or equal to 100.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

<img width="684" height="267" alt="image" src="https://github.com/user-attachments/assets/d4dc7906-a167-4332-880f-60ce5f576da0" />

```
SELECT 
    s.name, 
    c.cust_name, 
    c.city, 
    c.grade, 
    c.salesman_id
FROM 
    salesman s
LEFT JOIN 
    customer c
ON 
    s.salesman_id = c.salesman_id
WHERE 
    c.grade <= 100;
```

**Output:**

<img width="1273" height="494" alt="image" src="https://github.com/user-attachments/assets/85f16889-805c-4ebd-9d97-f20a1f771b33" />

**Question 4**

From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

Sample table: orders

<img width="659" height="963" alt="image" src="https://github.com/user-attachments/assets/e803c9d4-b14b-4945-9e5f-b9a274b47aa1" />

```
SELECT 
    o.ord_no,
    o.ord_date,
    o.purch_amt,
    c.cust_name AS "Customer Name",
    c.grade,
    s.name AS "Salesman",
    s.commission
FROM 
    orders o
INNER JOIN 
    customer c ON o.customer_id = c.customer_id
INNER JOIN 
    salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1345" height="857" alt="image" src="https://github.com/user-attachments/assets/6b1c54c4-53f4-4041-98ee-59e3b90e4f2e" />

**Question 5**

Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a null discharge date.

<img width="589" height="473" alt="image" src="https://github.com/user-attachments/assets/dabf2968-9942-493f-bc68-2930e8c68cc0" />

```
SELECT 
    p.first_name AS patient_name,
    d.first_name AS doctor_name
FROM 
    patients p
INNER JOIN 
    doctors d ON p.doctor_id = d.doctor_id
WHERE 
    p.discharge_date IS NULL;
```

**Output:**

<img width="504" height="360" alt="image" src="https://github.com/user-attachments/assets/64f8e6c8-f3f8-4e7e-b273-ad61a5613c2b" />

**Question 6**

Write a SQL statement to make a report with customer name, city, order number, order date, and order amount in ascending order according to the order date to determine whether any of the existing customers have placed an order or not.

<img width="544" height="798" alt="image" src="https://github.com/user-attachments/assets/25705a6b-4574-4d41-aa74-bd54bc8ef34d" />

```
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount"
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
ORDER BY 
    o.ord_date ASC;
```

**Output:**

<img width="1086" height="855" alt="image" src="https://github.com/user-attachments/assets/25c20330-0cc6-4249-9f4a-6326761f415d" />

**Question 7**

From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

Sample table: customer

<img width="446" height="601" alt="image" src="https://github.com/user-attachments/assets/31f8cc70-4e5f-4b7f-9a15-c05f03033dda" />

```
SELECT 
    c.cust_name AS "Customer Name",
    c.city,
    s.name AS "Salesman",
    s.commission
FROM 
    customer c
INNER JOIN 
    salesman s ON c.salesman_id = s.salesman_id
WHERE 
    s.commission > 0.12;
```

**Output:**

<img width="899" height="563" alt="image" src="https://github.com/user-attachments/assets/dbf7d5f8-7b57-4161-8515-1f9b8c0e5cd2" />

**Question 8**

SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

<img width="662" height="985" alt="image" src="https://github.com/user-attachments/assets/118b4675-a570-4566-95e9-f3b10031166f" />

```
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name,
    s.commission
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
LEFT JOIN 
    salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1327" height="865" alt="image" src="https://github.com/user-attachments/assets/6cbc4da3-dc96-456b-bd39-5cc6689f9026" />

**Question 9**

From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

<img width="505" height="618" alt="image" src="https://github.com/user-attachments/assets/d4d302f0-e5ed-44d4-b5de-631eb0209d80" />

```
SELECT 
    c.cust_name,
    c.city,
    c.grade,
    s.name AS Salesman,
    s.city AS city
FROM 
    customer c
JOIN 
    salesman s 
ON 
    c.salesman_id = s.salesman_id
WHERE 
    c.grade < 300
ORDER BY 
    c.customer_id ASC;
```

**Output:**

<img width="1051" height="557" alt="image" src="https://github.com/user-attachments/assets/205c2617-e224-4a17-84e6-f968b5a904c3" />

**Question 10**

Write the SQL query that accomplishes the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a non-null discharge date.

<img width="228" height="502" alt="image" src="https://github.com/user-attachments/assets/8de42b47-0c6b-4835-8d26-c8e812d294da" />

```
SELECT 
    p.first_name AS patient_name,
    d.first_name AS doctor_name
FROM 
    patients p
INNER JOIN 
    doctors d 
ON 
    p.doctor_id = d.doctor_id
WHERE 
    p.discharge_date IS NOT NULL;
```

**Output:**

<img width="492" height="317" alt="image" src="https://github.com/user-attachments/assets/c397578a-bae0-4893-aa02-cf0570d4b927" />

## RESULT:

Thus, the SQL queries to implement different types of joins have been executed successfully.

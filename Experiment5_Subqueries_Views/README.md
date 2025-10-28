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

Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

<img width="784" height="608" alt="image" src="https://github.com/user-attachments/assets/a40a6cfd-f246-4bba-b3fb-7fa3c130ddcc" />

```
SELECT 
    g.student_name,
    g.grade
FROM 
    GRADES g
WHERE 
    g.grade = (
        SELECT MAX(g2.grade)
        FROM GRADES g2
        WHERE g2.subject = g.subject
    );
```

**Output:**

<img width="735" height="496" alt="image" src="https://github.com/user-attachments/assets/cc5be1ab-9ecb-426b-8adf-9590c7379005" />

**Question 2**

Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

Sample table: CUSTOMERS

<img width="567" height="594" alt="image" src="https://github.com/user-attachments/assets/4a6c9f73-e7d2-4670-9cf2-c40f1367dfed" />

```
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi'
  AND AGE < 30
ORDER BY ID;
```

**Output:**

<img width="1193" height="429" alt="image" src="https://github.com/user-attachments/assets/53f0cac0-059f-467f-8937-4d987c52888c" />

**Question 3**

Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer

<img width="279" height="514" alt="image" src="https://github.com/user-attachments/assets/abd8e3f4-8f2d-4116-be44-aa9d7aba4361" />

```
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);
```

**Output:**

<img width="547" height="527" alt="image" src="https://github.com/user-attachments/assets/11f11487-0ccd-4277-b387-ac476a22829e" />

**Question 4**

Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)

<img width="846" height="434" alt="image" src="https://github.com/user-attachments/assets/83d11c70-954e-4269-be6e-5fc6a4541d26" />

```
SELECT 
    department_id AS depar,
    department_name
FROM 
    Departments
WHERE 
    LENGTH(department_name) > (
        SELECT AVG(LENGTH(department_name))
        FROM Departments
    );
```

**Output:**

<img width="548" height="470" alt="image" src="https://github.com/user-attachments/assets/e0626ebd-f323-4ac2-a86e-c6899636722a" />

**Question 5**

From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

<img width="275" height="470" alt="image" src="https://github.com/user-attachments/assets/528a4ae3-e000-4fef-a0f5-47ec4c6155f4" />

```
select grade, COUNT(*) from customer
where grade > (select grade from customer where city='New York') group by grade;
```

**Output:**

<img width="551" height="404" alt="image" src="https://github.com/user-attachments/assets/a867585b-fc8e-4351-9098-19283554d6b9" />

**Question 6**

Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

<img width="657" height="634" alt="image" src="https://github.com/user-attachments/assets/007322ed-a960-49ea-b29f-8f34b3617ed5" />

```
SELECT *
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);
```

**Output:**

<img width="1240" height="519" alt="image" src="https://github.com/user-attachments/assets/438148e8-7306-4ccd-932c-211c20cc562e" />

**Question 7**

Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID

SAMPLE TABLE: customer

<img width="586" height="494" alt="image" src="https://github.com/user-attachments/assets/eaae4c80-3ba0-4854-9474-c189dd7aaaa7" />

```
SELECT *
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);
```

**Output:**

<img width="1243" height="487" alt="image" src="https://github.com/user-attachments/assets/1cddbed2-eca9-447b-8458-bb29d3d212f2" />

**Question 8**

Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

Sample table: CUSTOMERS

<img width="503" height="578" alt="image" src="https://github.com/user-attachments/assets/1de78540-7faf-4b62-ab6f-7e464a759956" />

```
SELECT *
FROM CUSTOMERS
WHERE SALARY > 4500;
```

**Output:**

<img width="1080" height="449" alt="image" src="https://github.com/user-attachments/assets/0727e49c-bc23-4569-909e-9b4bd7b61a43" />

**Question 9**

From the following tables write a SQL query to find all orders generated by New York-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

<img width="526" height="720" alt="image" src="https://github.com/user-attachments/assets/48260263-b87c-4372-978c-1f9ab4ea1780" />

```
SELECT *
FROM orders
WHERE salesman_id IN (
    SELECT salesman_id
    FROM salesman
    WHERE city = 'New York'
);
```

**Output:**

<img width="1116" height="477" alt="image" src="https://github.com/user-attachments/assets/93252373-c6d0-4c53-8b6a-96665b8390fa" />

**Question 10**

Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

Sample table: CUSTOMERS

<img width="509" height="536" alt="image" src="https://github.com/user-attachments/assets/3c9725c8-6fd3-438c-8dca-1499c8891f93" />

```
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi';

```

**Output:**

<img width="1090" height="361" alt="image" src="https://github.com/user-attachments/assets/a6240398-df19-4e53-8e3b-bf7018568b00" />

## RESULT:

Thus, the SQL queries to implement subqueries and views have been executed successfully.

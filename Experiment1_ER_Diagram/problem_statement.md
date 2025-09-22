# ER Diagram Workshop – Submission Template

# OBJECTIVE:
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

# PURPOSE:
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.


# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

# ER DIAGRAM:

<<img width="710" height="568" alt="image" src="https://github.com/user-attachments/assets/a51ae26e-6c35-4a75-9387-04c4a115c4f0" />

# ENTITIES AND ATTRIBUTES:

| Entity       | Attributes (PK, FK)                                                                               | Notes                                                                                                  |
| ------------ | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| Customer     | customer\_id (PK), name, phone, email                                                             | Customers can make reservations or walk in.                                                            |
| Table        | table\_id (PK), table\_number, capacity, location                                                 | Represents physical tables in the restaurant.                                                          |
| Reservation  | reservation\_id (PK), date, time, num\_guests, customer\_id (FK), table\_id (FK), waiter\_id (FK) | Links customers, tables, and waiters. Walk-ins can also be stored as reservations with immediate time. |
| Waiter       | waiter\_id (PK), name, phone                                                                      | Each waiter serves multiple reservations.                                                              |
| DishCategory | category\_id (PK), category\_name                                                                 | Categories like Starter, Main, Dessert.                                                                |
| Dish         | dish\_id (PK), name, price, category\_id (FK)                                                     | Menu items belong to categories.                                                                       |
| Order        | order\_id (PK), reservation\_id (FK), order\_time                                                 | Orders are linked to reservations.                                                                     |
| OrderItem    | order\_id (FK, PK), dish\_id (FK, PK), quantity                                                   | Junction table for many-to-many between Orders and Dishes.                                             |
| Bill         | bill\_id (PK), reservation\_id (FK), food\_total, service\_charge, grand\_total, payment\_status  | One bill per reservation.                                                                              |

# RELATIONSHIPS AND CONSTRAINTS:

| Relationship                 | Cardinality             | Participation                                   | Notes                                                                            |
| ---------------------------- | ----------------------- | ----------------------------------------------- | -------------------------------------------------------------------------------- |
| Customer – Reservation       | 1 : N                   | Total (for reservation), Partial (for customer) | A customer can make many reservations, each reservation belongs to one customer. |
| Reservation – Table          | 1 : 1 (per reservation) | Total                                           | Each reservation is linked to exactly one table at a time.                       |
| Waiter – Reservation         | 1 : N                   | Partial (waiter), Total (reservation)           | A waiter can serve many reservations; each reservation has exactly one waiter.   |
| Reservation – Order          | 1 : N                   | Total                                           | Each reservation can have multiple orders.                                       |
| Order – Dish (via OrderItem) | M : N                   | Total                                           | Each order can include multiple dishes; each dish can appear in many orders.     |
| DishCategory – Dish          | 1 : N                   | Total                                           | Each dish belongs to one category.                                               |
| Reservation – Bill           | 1 : 1                   | Total                                           | Each reservation generates exactly one bill.                                     |


# ASSUMPTIONS :

1. Walk-in customers are also recorded as reservations with immediate date/time.
2. A reservation is always tied to a single table (no table sharing in this model).
3. Bills include both food cost (sum of ordered dishes) and service charges.
4. A waiter must be assigned to every reservation.
5. Orders cannot exist without a reservation.
6. Payment status is tracked in the Bill entity (e.g., Paid / Pending).

# Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**

# Design Choices:

In this restaurant reservation and ordering system, separate entities are created for Customer, Table, Reservation, Waiter, DishCategory, Dish, Order, OrderItem, and Bill to clearly define responsibilities, with OrderItem serving as a junction table to manage the many-to-many relationship between Orders and Dishes. The design is reservation-centric, meaning all business flows such as orders, billing, and waiter assignments are linked to a Reservation, while walk-in customers are also treated as reservations with the same-day date and time. A waiter is assigned at the reservation level, as service is tied to the entire table rather than individual dishes. Billing is generated per reservation instead of per order to simplify accounting, and totals such as food cost, service charge, and grand total are stored for performance. Dishes are categorized under DishCategory for easier menu organization and filtering. Each reservation is tied to one table, but for larger groups, the design can be extended with a junction table to allow multiple tables per reservation. Data integrity is ensured through foreign key constraints, and cascade deletes are avoided to preserve historical data. The model supports scalability by separating Orders and OrderItems, which allows handling complex orders and enables billing extensions like discounts or taxes. Finally, payment status is tracked in the Bill entity with simple states (e.g., Paid, Pending, Cancelled), though the design can be extended with a separate Payment entity for more advanced payment handling.

# RESULT:
Hence, the concepts of ER modeling is understood and applied by creating an ER diagram for a real-world application.

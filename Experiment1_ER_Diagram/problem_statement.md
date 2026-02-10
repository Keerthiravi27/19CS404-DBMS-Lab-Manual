# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
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

### ER Diagram:
<img width="1536" height="1024" alt="er diagram exp1" src="https://github.com/user-attachments/assets/aae94918-d55d-404b-850c-68f822b445d1" />


### Entities and Attributes

| Entity          | Attributes (PK, FK)                                                                                                                          | Notes                                                          |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| **Customer**    | customer_id (PK), name, phone                                                                                                                | A customer can make multiple reservations                      |
| **Reservation** | reservation_id (PK), reservation_date, reservation_time, number_of_guests, reservation_type, customer_id (FK), table_id (FK), waiter_id (FK) | Reservation type = Walk-in / Advance                           |
| **Table**       | table_id (PK), capacity, status                                                                                                              | One table can be used for many reservations at different times |
| **Waiter**      | waiter_id (PK), name, shift                                                                                                                  | One waiter serves many reservations                            |
| **Order**       | order_id (PK), order_time, reservation_id (FK)                                                                                               | Orders are linked to reservations                              |
| **Order_Item**  | order_item_id (PK), quantity, order_id (FK), dish_id (FK)                                                                                    | Resolves many-to-many between Order and Dish                   |
| **Dish**        | dish_id (PK), dish_name, price, category_id (FK)                                                                                             | Each dish belongs to one category                              |
| **Category**    | category_id (PK), category_name                                                                                                              | Starter, Main Course, Dessert                                  |
| **Bill**        | bill_id (PK), food_amount, service_charge, total_amount, payment_status, reservation_id (FK)                                                 | One bill per reservation                                       |


### Relationships and Constraints

| Relationship           | Cardinality | Participation        | Notes                                        |
| ---------------------- | ----------- | -------------------- | -------------------------------------------- |
| Customer — Reservation | 1 : M       | Total on Reservation | A customer can make multiple reservations    |
| Reservation — Table    | M : 1       | Total on Reservation | Each reservation must have a table           |
| Waiter — Reservation   | 1 : M       | Partial on Waiter    | A waiter may serve many reservations         |
| Reservation — Order    | 1 : M       | Total on Order       | Orders cannot exist without reservation      |
| Order — Dish           | M : N       | Total on Order_Item  | Implemented using Order_Item                 |
| Category — Dish        | 1 : M       | Total on Dish        | Each dish belongs to one category            |
| Reservation — Bill     | 1 : 1       | Total                | Every reservation generates exactly one bill |


### Assumptions
```
Each customer can make multiple reservations, but each reservation is made by only one customer.

A reservation is mandatory for placing an order.
(Walk-in customers are treated as reservations with type = Walk-in.)

Each reservation is assigned exactly one table based on availability and seating capacity.

A table can serve multiple reservations on different dates or times, but only one reservation at a given time.

Each reservation is served by one waiter, while a waiter can serve many reservations during a shift.

A reservation can have multiple orders, but each order belongs to only one reservation.

An order can include multiple dishes, and a dish can appear in multiple orders
(handled using the Order_Item entity).

Each dish belongs to exactly one category (Starter, Main Course, Dessert, etc.).

Every reservation generates exactly one bill, and a bill is associated with only one reservation.

The bill amount includes:

Total food cost

Service charge

Final payable amount

Payment status is recorded for every bill (e.g., Paid, Unpaid).

The system assumes no table sharing between different reservations at the same time.
```

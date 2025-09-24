
# Task 1 - Database Setup and Schema Design (E-commerce Domain)

## Objective
Create a well-structured database schema for a simple e-commerce system, demonstrating:
- DDL: CREATE TABLE with proper data types
- Keys: Primary keys, Foreign keys, Composite keys
- Constraints: NOT NULL, UNIQUE, DEFAULT, CHECK
- Normalization: Reduce redundancy via table decomposition
- ER diagram representing entities and relationships

## Files
- `task1_schema.sql` : SQL script to create the schema (MySQL-compatible).
- `er_diagram_task1.png` : Visual ER diagram (top-level relationships).
- `README.md` : This file.

## Schema Overview (entities)
- `users` : stores customer accounts (surrogate key `user_id`)
- `addresses` : multiple addresses per user (FK -> users)
- `categories` : product categories
- `products` : items for sale (FK -> categories)
- `orders` : purchases by users (FK -> users, addresses)
- `order_items` : items inside each order (composite PK (order_id, product_id))
- `payments` : payment record tied to an order
- `reviews` : user reviews for products (user_id + product_id unique)

## Normalization & Design Choices
- The design follows 3NF: data is split into logical entities to avoid repetition.
- Surrogate keys (`AUTO_INCREMENT`) used for simplicity and performance.
- Composite primary key in `order_items` models the many-to-many relationship without an extra surrogate key.
- Referential actions (ON DELETE CASCADE/SET NULL/RESTRICT) chosen to preserve integrity:
  - Delete a user -> delete their addresses and orders.
  - Delete an order -> delete related order_items/payments.
  - Delete a category -> set product.category_id to NULL (keeps products discoverable).

## Next steps (Task 2 mapping)
For Task 2 (DML / Null handling), you can perform:
- Insert sample users, products, categories (some fields NULL or using DEFAULT).
- Update stock_qty after an order is placed.
- Delete a canceled order and demonstrate `ROLLBACK` in a transaction.
- Insert partial rows (e.g., address without address_line2) to show NULL handling.
- Show `INSERT INTO ... SELECT ...` by copying product rows for testing.



---

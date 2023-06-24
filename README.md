# SQL
# Dtabase Quries
```
CREATE DATABASE sales; - Create New DB
SHOW DATABASES;
DROP DATABASE sales; 
ALTER DATABASE sales MODIFY NAME = new_sales;

USE sales; - Use Created DB
SELECT * FROM SYS.DATABASES - Get System Databases List 
SELECT * FROM sales; - Get all details from particular DB
```

# Create Tables
- Create customers table
```
CREATE TABLE sales.customers (
  customer_id INT PRIMARY KEY,
  customer_name VARCHAR(100),
  email VARCHAR(100),
  phone VARCHAR(20),
  address VARCHAR(200)
);
```
- Create products table
```
CREATE TABLE sales.products (
  product_id INT PRIMARY KEY,
  product_name VARCHAR(100),
  price DECIMAL(10,2),
  description VARCHAR(200),
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES sales.customers(customer_id)
);
```

# Insert Data
- Inserting data into the "customers" table
```
INSERT INTO sales.customers (customer_id, customer_name, email, phone, address)
VALUES
  (1, 'John Smith', 'john.smith@example.com', '123-456-7890', '123 Main St'),
  (2, 'Jane Doe', 'jane.doe@example.com', '987-654-3210', '456 Elm St'),
  (3, 'Michael Johnson', 'michael.johnson@example.com', '555-123-4567', '789 Oak Ave'),
  (4, 'Emily Wilson', 'emily.wilson@example.com', '111-222-3333', '987 Pine St'),
  (5, 'David Thompson', 'david.thompson@example.com', '444-555-6666', '321 Cedar Rd'),
  (6, 'Sarah Brown', 'sarah.brown@example.com', '777-888-9999', '555 Maple Ave'),
  (7, 'Daniel Davis', 'daniel.davis@example.com', '333-444-5555', '222 Elm St'),
  (8, 'Olivia Anderson', 'olivia.anderson@example.com', '666-777-8888', '444 Oak Ave'),
  (9, 'Jacob Martin', 'jacob.martin@example.com', '999-000-1111', '789 Pine St'),
  (10, 'Sophia Taylor', 'sophia.taylor@example.com', '222-333-4444', '123 Cedar Rd');
```

- Inserting data into the "products" table
``` 
INSERT INTO sales.products (product_id, product_name, price, description)
VALUES
  (1, 'Widget A', 9.99, 'A high-quality widget'),
  (2, 'Gizmo B', 14.99, 'A versatile gizmo'),
  (3, 'Thingamajig C', 19.99, 'The latest thingamajig'),
  (4, 'Doodad X', 7.99, 'An innovative doodad'),
  (5, 'Whatchamacallit Y', 12.99, 'The classic whatchamacallit'),
  (6, 'Doohickey Z', 8.49, 'A reliable doohickey'),
  (7, 'Gadget P', 24.99, 'A feature-packed gadget'),
  (8, 'Contraption Q', 16.79, 'A cutting-edge contraption'),
  (9, 'Apparatus R', 11.49, 'An efficient apparatus'),
  (10, 'Gizmometer S', 18.99, 'A handy gizmometer');
```

# Show Table Details
```
SELECT * FROM customers;
SELECT * FROM sales.customers;
```
# Alter Table
- Rename
```
ALTER TABLE sales.customers RENAME TO new_customers;
```
- Add more cloumn
```
ALTER TABLE sales.products
ADD deliver BOOLEAN;
```
- Drop Column
```
ALTER TABLE sales.products
DROP COLUMN deliver;
```

# Where
```
SELECT *
FROM sales.customers
WHERE customer_name = 'John Smith';
```
```
SELECT *
FROM sales.customers
WHERE customer_name = 'John Smith' AND email = 'john.smith@example.com';
```
SELECT product_name,price FROM products WHERE product_name = 'Widget A' AND price > '8.00';
SELECT product_id, price FROM products;

SELECT product_id,product_name, AVG(price) as avg_price FROM products GROUP BY product_name;
```


# AS
- The "AS" syntax in SQL is used for aliasing, which provides a way to assign temporary names or labels to tables or columns in a query. There are several reasons why you might use the "AS" syntax:
```
SELECT c.customer_id, c.customer_name, p.product_name
FROM customers AS c
JOIN products AS p ON c.customer_id = p.customer_id;
```

# String Operations
- The "%" wildcard represents any number of characters
```
SELECT customer_name
FROM customers
WHERE customer_name LIKE '%dar%';
```
- escape - The backslash \ is used as an escape character to treat the percentage sign % as a literal character instead of a wildcard. The escape character allows you to search for strings that contain the exact pattern "100 % escape ".

```
SELECT customer_name
FROM customers
WHERE customer_name LIKE '100 \% escape \';
```



# Order By
- ASC
```
SELECT product_id, product_name, price
FROM products
ORDER BY price ASC;
```
- DESC
```
SELECT product_id, product_name, price
FROM products
ORDER BY price DESC;
```

# Between
```
SELECT product_name
FROM products
WHERE price BETWEEN 90000 AND 100000;
```
# Tuple comparison
```
SELECT product_name, price
FROM products
WHERE (product_name, price) = ('Widget A', 10.99);

```
# Delete From
- The "DELETE FROM" syntax in SQL is used to delete records from a table
```
DELETE FROM customers
WHERE customer_id = 1;
```

```
SELECT product_id,product_name, AVG(price) as avg_price FROM products GROUP BY product_name;
SELECT product_id,product_name, MIN(price) as avg_price FROM products GROUP BY product_name;
SELECT product_id,product_name, MAX(price) as avg_price FROM products GROUP BY product_name;
SELECT product_id,product_name, SUM(price) as avg_price FROM products GROUP BY product_name;
SELECT product_id,product_name, COUNT(price) as avg_price FROM products GROUP BY product_name;
```

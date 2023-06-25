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

```
SELECT product_name,price FROM products WHERE product_name = 'Widget A' AND price > '8.00';
```

```
SELECT product_id, price FROM products;
```

```
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






# Foreign Key
```
-- Create the customers table
CREATE TABLE sales.customers (
  customer_id INT PRIMARY KEY,
  customer_name VARCHAR(100),
  email VARCHAR(100),
  phone VARCHAR(20),
  address VARCHAR(200)
);

-- Create the products table with a foreign key reference to customers
CREATE TABLE sales.products (
  product_id INT PRIMARY KEY,
  product_name VARCHAR(100),
  price DECIMAL(10,2),
  description VARCHAR(200),
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES sales.customers(customer_id)
);

-- Insert data into the customers table
INSERT INTO sales.customers (customer_id, customer_name, email, phone, address)
VALUES
  (1, 'John Doe', 'john@example.com', '1234567890', '123 Main St'),
  (2, 'Mary Johnson', 'mary@example.com', '5555555555', '789 Oak St'),
  (3, 'Robert Smith', 'robert@example.com', '9999999999', '321 Pine St'),
  (4, 'Emily Davis', 'emily@example.com', '1111111111', '987 Maple Ave');
  (5, 'Jane Smith', 'jane@example.com', '9876543210', '456 Elm St');

-- Insert data into the products table
INSERT INTO sales.products (product_id, product_name, price, description, customer_id)
VALUES
  (1, 'Widget A', 10.99, 'Description for Widget A', 1),
  (2, 'Widget C', 19.99, 'Description for Widget C', 3),
  (3, 'Widget D', 24.99, 'Description for Widget D', 4),
  (4, 'Widget E', 29.99, 'Description for Widget E', 5);
  (5, 'Widget B', 15.99, 'Description for Widget B', 2);
```

## Remove duplicates and give unique details
```
select distinct product_name from products;
```

## Having
```
select product_name, avg (price) as avg_price from products group by product_name having avg (price) > 10;
```

## IN and NOT IN
```
SELECT product_name FROM products WHERE product_name IN ('Electronics', 'Clothing', 'Books');
SELECT product_name FROM products WHERE product_name NOT IN ('Electronics', 'Clothing', 'Books');
```
## EXISTS & NOT EXISTS
- The result will include products that have at least one associated order.
```
SELECT product_name FROM products WHERE EXISTS ( SELECT 1 FROM customers WHERE customers.product_id = products.product_id );
SELECT product_name FROM products WHERE NOT EXISTS ( SELECT 1 FROM customers WHERE customers.product_id = products.product_id );
```

## sub query
```
SELECT product_name, price
FROM products
WHERE price BETWEEN (SELECT MIN(price) FROM products) AND (SELECT MAX(price) FROM products);
```

## WITH
- the "WITH" clause defines a temporary result set named "average_price" that calculates the average price from the "products" table. The main query then retrieves the product_name and price from the "products" table where the price is greater than the average price obtained from the CTE.
```
WITH average_price AS ( SELECT AVG(price) AS avg_price FROM products ) SELECT product_name, price FROM products WHERE price > (SELECT avg_price FROM average_price);
```

## UPDATE
```
UPDATE products SET price = price * 5 WHERE product_id = 1;
```

- The UNION operator is used to combine the result sets of two or more SELECT statements, eliminating duplicates. 
```
SELECT product_name, price FROM products WHERE price > 100 UNION SELECT product_name, price FROM products WHERE price < 50;
```

- The INTERSECT operator is used to retrieve the common rows between the result sets of two or more SELECT statements
```
SELECT product_name, price FROM products WHERE price > 100 INTERSECT SELECT product_name, price FROM products WHERE price < 200;
```

- The EXCEPT operator is used to retrieve the rows from the first SELECT statement that do not exist in the result set of the second SELECT statement.
```
SELECT product_name, price FROM products WHERE price > 100 EXCEPT SELECT product_name, price FROM products WHERE price < 200;
```

# NULL
```
select customer_id from products where customer_id is null;
```

# SOME
- The "SOME" keyword in SQL is used to compare a value with a set of values returned by a subquery. It checks if the value satisfies the condition for at least one row in the subquery result. 
```
SELECT product_name, price FROM products WHERE price > SOME (SELECT price FROM products WHERE product_name = 'Electronics');
```

# ALL
```
SELECT product_name, price FROM products WHERE price > ALL (SELECT price FROM products WHERE product_name = 'Electronics');
```





















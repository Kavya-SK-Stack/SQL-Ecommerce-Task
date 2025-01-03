### Create database
    CREATE DATABASE ecommerce;

### Use database
    USE ecommerce;
 
 ### Create Customers Table

    create table customers (id int auto_increment primary key, name varchar(30), email varchar(30), address varchar(30));
    
![alt text](/Screenshot%202025-01-03%20110718.png)

### Create Orders Table

    create table orders (id int auto_increment primary key, customer_id int, order_date date,total_amount decimal (10, 2), foreign key (customer_id) references customers(id));
   
![alt text](/Screenshot%202025-01-03%20112404.png) 

### Create Products Table
    create table products (id int auto_increment primary key, name varchar(30), price decimal (10, 2), description text);
   
![alt text](/Screenshot%202025-01-03%20112432.png) 

### Insert Cutomers Table data
insert into customers (name, email, address) values 

    - ('Heman Babu', 'hemanbabu548@gmail.com', 'Pandiyan Nagar Tiruppur'),                      
    - ('Anushree', 'anuanu4554@gmail.com', 'Pooluvapatti Tiruppur'),
    - ('Anbarasu', 'anbarasukl546@gmail.com', 'Kunnathur Tiruppur'),    
    - ('Kannan', 'kannankannan67@gmail.com', 'Perumanallur Tiruppur'), 
    - ('Shree', 'shreeselvaraj009@gmail.com', 'Anna Nagar Tiruppur'),               
    - ('Kumar', 'kumar65564@gmail.com', 'Ayyampalayam Tiruppur');    

![alt text](/Screenshot%202025-01-03%20113128.png)


### Insert Products Table data
insert into products (name, price, description) values

    -  ('Product A', 25.00, 'Description for Product A'),
    - ('Product B', 35.00, 'Description for Product B'),                            
    - ('Product C', 50.00, 'Description for Product C'), 
    - ('Product D', 100.00, 'Description for Product D'); 

![alt text](/Screenshot%202025-01-03%20113149.png)


### Insert Orders Table data

insert into orders (customer_id, order_date, total_amount) values 

    - (1,'2024-12-01', 50.00),
    - (2,'2024-12-05', 35.00),                                                      
    - (3,'2024-12-15', 75.00), 
    - (4,'2024-12-18', 100.00),
    - (5,'2024-12-20', 150.00), 
    - (6,'2024-12-25', 250.00); 

![alt text](/Screenshot%202025-01-03%20113209.png)

### QUERIES

### 1. Retrieve customers who placed orders in the last 30 days:

    SELECT DISTINCT c.* FROM customers c JOIN orders o ON c.id= o.customer_id WHERE o.order_date >= CURDATE() - INTERVAL 30 DAY;

 ![alt text](/Screenshot%202025-01-03%20013340.png)

### 2. Get the total amount of all orders placed by each customer
    SELECT c.name, SUM(o.total_amount) AS total_spent FROM customers c JOIN orders o ON c.id = o.customer_id GROUP BY c.id;

![alt text](/Screenshot%202025-01-03%20013341.png)

### 3. Update the price of Product C to 45.00

     UPDATE products SET price = 45.00 WHERE name = 'Product C';

![alt text](/Screenshot%202025-01-03%20115258.png)

### 4. Add a new column discount to the products table
    ALTER TABLE products ADD COLUMN discount DECIMAL(5, 2) DEFAULT 0.00;
    
    
![alt text](/Screenshot%202025-01-03%20013359.png)

### 5. Retrieve the top 3 products with the highest price
    SELECT * FROM products ORDER BY price DESC LIMIT 3;

![alt text](/Screenshot%202025-01-03%20115856.png)

### 6. Get the names of customers who have ordered Product A

    SELECT DISTINCT c.name FROM customers c JOIN orders o ON c.id = o.customer_id JOIN order_items oi ON o.id = oi.order_id JOIN products p ON oi.product_id = p.id WHERE p.name = 'Product A';

    
        ---------
        | name |
        ---------
        Anbarasu

### 7. Join orders and customers tables to retrieve the customer's name and order date for each order

    SELECT c.name, o.order_date FROM orders o JOIN customers c ON o.customer_id = c.id;
    
![alt text](/Screenshot%202025-01-03%20013412.png)


### 8. Retrieve the orders with a total amount greater than 150.00
    SELECT * FROM orders WHERE total_amount > 150.00;

![alt text](/Screenshot%202025-01-03%20013413.png)

### 9. Normalize database by creating an order_items table
    CREATE TABLE order_items (id INT AUTO_INCREMENT PRIMARY KEY order_id INT NOT NULL, product_id INT,quantity INT);

    -- ALTER table orders drop column total_amount;
    
    
![alt text](/Screenshot%202025-01-03%20013430.png)

### 10. Retrieve the average total of all orders

    SELECT AVG(total_amount) AS average_order_total FROM orders;
 
 ![alt text](/Screenshot%202025-01-03%20124054.png)
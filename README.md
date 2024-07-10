/*1. Create the following tables inside the database ‘global_store_db’.(Score :2)
‘products’ with columns: 
product_id (INT, auto_increment, primary key), 
name (VARCHAR(100)), 
price (DECIMAL(10,2)), 
quantity (INT).
‘orders’ with columns: 
order_id (INT, auto_increment, primary key), 
product_id (INT, foreign key referencing product_id in the inventory table),
quantity_ordered (INT)
 order_date (DATE)..*/
 
 Query
 
 CREATE DATABASE global_store_db;
 
USE global_store_db;

CREATE TABLE products (product_id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100),
  price DECIMAL(10,2),
  quantity INT);

CREATE TABLE orders (order_id INT AUTO_INCREMENT PRIMARY KEY,
  product_id INT,
  quantity_ordered INT,
  order_date DATE,
  FOREIGN KEY (product_id) REFERENCES products(product_id));

-- 2.Alter the products table to add a new column named category (VARCHAR(50)) after the price column. (score : 0.5)

alter table products add column category varchar(30) ;

-- 3. Rename the products table to inventory.  (score : 0.5)

rename table products to inventory;

-- 4. Insert at least 10 records into the inventory table and 5 records into orders table and display the tables. (score : 1)

INSERT INTO inventory (name, price, quantity, category) VALUES
  ('iphone', 10.99, 5, 'Electronics'),
  ('earbud', 20.99, 10, 'Electronics');
  insert into inventory (name,price,quantity,category) values
  ('jacket',2.49,8,'cloth'),
  ('sofa',6.99,9,'furniture'),
  ('laptop',14.49,7,'electronics'),
('fridge',9.99,5,'home applicance'),
('jeans',3.25,12,'cloth'),
('chain',10.99,13,'jewel'),
('bangles',9.99,16,'jewel'),
('filter',8.99,7,'home applicance');
insert into orders (order_id,quantity_ordered,order_date) values(101,2,curdate());
update orders set product_id=1 where order_id = 101;
insert into orders (product_id,quantity_ordered,order_date) values(2,2,'2024-5-4');
insert into orders (product_id,quantity_ordered,order_date) values(3,4,'2024-7-4');
insert into orders (product_id,quantity_ordered,order_date) values(7,11,'2024-7-4');
insert into orders (product_id,quantity_ordered,order_date) values(5,3,'2024-7-4');
insert into orders (product_id,quantity_ordered,order_date) values(9,11,'2024-7-4');

select * from inventory;
select * from orders;
-- 5. Write queries for the following : (Score :3)
-- a) Write a query to display distinct categories from the inventory table.

select distinct(category) from inventory;

-- b) Select the top 5 products by their prices in descending order from the inventory table.

select name ,price from inventory order by price desc limit 5;

-- c) Display the names of products with a quantity greater than 10 from the inventory table.

select name, quantity from inventory where quantity > 10;

-- d) Use the SUM() function to calculate the total price of all products in the inventory table.

select sum(price) 'tot price' from inventory;

-- e )Group products by their categories and display the count of products in each category.

select category,count(name) 'type of products in this category' from inventory group by category ;

-- f) Write a query to identify products that are currently out of stock (i.e., quantity is zero). Display the product details including the product name and price.

update inventory set quantity = 0 where product_id =1 ;
update inventory set quantity = 0 where product_id =6 ;
select name,price from inventory where quantity = 0;

-- 6. Create a view named expensive_products that displays the details of products with a price above the average price of all products. (score : 1)

create view expensive_products
as
select * from inventory where price > (select avg(price) from inventory);

select * from expensive_products;


-- 7. Write a join query to display the names of products along with the corresponding order quantities from the inventory and orders tables. (score : 

select i.name,o.quantity_ordered from inventory i right join orders o on i.product_id = o.product_id;



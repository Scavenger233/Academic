# Lab Exercise: The SELECT Statement (1)
The goal of this exercise is to practice single-table queries in SQL.

Review the slides of Lecture 4.
Login to MySQL and make sure you have the tables products, pcs, laptops, printers, customers and sales in your database.
Click on the SQL tab in phpMyAdmin. Here you can write and execute SQL statements.
Write SQL SELECT statements for performing the following queries:
- List the model numbers of all products made by maker B.
```
SELECT model FROM products where maker LIKE 'B';
```
- List the model numbers of all products not made by maker B.
```
SELECT model FROM products where maker NOT LIKE 'B';
```
- List the model numbers of all PCs with speed >= 3.00.
```
SELECT model FROM pcs WHERE speed >=3.00;
```
- List the model numbers of all color laser printers.
```
SELECT model FROM printers WHERE color = 'TRUE' AND type = 'laser';
```
- List the customer IDs of all customers who paid for a product with a Visa card (debit or credit).
```
SELECT customer_id FROM sales WHERE type_of_payment NOT LIKE 'cash';
```
- List the first names, the last names, the city and the street address of all customers who have the letter 'e' either in their first name or in their last name.
```
SELECT firstname, lastname, city, address FROM customers WHERE firstname LIKE '%e%' OR lastname LIKE '%e%';
```
- List all attributes of the transactions (from table sales) made between the 18th and the 20th of December 2013 (including the 18th and the 20th).
```
SELECT * FROM sales WHERE day BETWEEN '2013-12-18' AND '2013-12-20';
```
- List all attributes of the transactions (from table sales) made either before the 18th or after the 20th of December 2013.
```
SELECT * FROM sales WHERE day NOT BETWEEN '2013-12-18' AND '2013-12-20';
```
- Assume all prices in table Laptops are in Euro. List the model numbers of all laptops with ram at least 1024. 
```
SELECT model FROM laptops WHERE ram >= 1024;
```
- For each model, list also its price in USD. Assume that 1 USD = 0.93 EURO.
```
SELECT model, price * 0.93 AS USD FROM laptops;
```

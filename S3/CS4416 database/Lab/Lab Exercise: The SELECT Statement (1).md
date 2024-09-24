# Lab Exercise: The SELECT Statement (1)
The goal of this exercise is to practice single-table queries in SQL.

Review the slides of Lecture 4.
Login to MySQL and make sure you have the tables products, pcs, laptops, printers, customers and sales in your database.
Click on the SQL tab in phpMyAdmin. Here you can write and execute SQL statements.
Write SQL SELECT statements for performing the following queries:
- List the model numbers of all products made by maker B.
```
  SELECT * FROM products where maker LIKE 'B';
```
- List the model numbers of all products not made by maker B.
```



- List the model numbers of all PCs with speed >= 3.00.
- List the model numbers of all color laser printers.
- List the customer IDs of all customers who paid for a product with a Visa card (debit or credit).
- List the first names, the last names, the city and the street address of all customers who have the letter 'e' either in their first name or in their last name.
- List all attributes of the transactions (from table sales) made between the 18th and the 20th of December 2013 (including the 18th and the 20th).
- List all attributes of the transactions (from table sales) made either before the 18th or after the 20th of December 2013.
Assume all prices in table Laptops are in Euro. List the model numbers of all laptops with ram at least 1024. For each model, list also its price in USD. Assume that 1 USD = 0.93 EURO.

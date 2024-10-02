## Task

The goal of this exercise is to practice joins and subqueries in the SQL SELECT statement.

1. Review the slides of Lecture 5.

2. Login to MySQL and make sure you have the tables products, pcs, laptops, printers, customers and sales in your database.

3. Click on the SQL tab in phpMyAdmin. Here you can write and execute SQL statements.

4. Write SQL SELECT statements for performing the following queries. Use either a join or a subquery. If a question is asking to include attributes from one table only in the SELECT clause of the SELECT statement, try to find two solutions, one with a join, and another with a subquery.

- a. List all PC models that have been sold at least once.

- b. List the makers of laptops with speed of at least 2.00.

- c. List all pairs of PC models that have both the same speed and ram. A pair should be listed only once; e.g., list (i, j) but not (j, i).

- d. List the makers that make at least two different models of PC.

- e. List the maker(s) of the laptop(s) with the highest available speed.

- f. List the cities with customers who bought a printer.

- g. List the makers of PCs that don't make any laptop (but may make printers)

- h. List the makers of PCs that don't make any laptop or printer

- i. List the model numbers and prices of laptops which are cheaper than at least one PC

5. Write SQL SELECT statements which use outer joins for performing the following queries.

- a. List all makers, all model numbers they make, and the corresponding product types (i.e. the entire maker, model and type columns from table Products). For the PC models only list their speed and price as well in two additional columns. These two extra columns should contain NULL markers for laptop and printer models.

- b. List all laptop model numbers and only for those made by makers A and B list also their price. The prices of laptops not made by either A or B should be NULL.

 - Hint: List the laptop model numbers made by A and B and their prices. Use the result of this query as a subquery in the FROM clause of the main query.

- c. List the names (first name and last name) of customers who haven't bought any product. Use an outer join. Can you solve it with a subquery instead?

 - Hint: In the solution that uses an outer join, use 'IS NULL' in the WHERE clause.

Note: There are no such customers in the example database. Insert a new customer into table customers to test your solution.

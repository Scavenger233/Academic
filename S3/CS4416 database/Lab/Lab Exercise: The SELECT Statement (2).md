## Task

The goal of this exercise is to practice joins and subqueries in the SQL SELECT statement.
<img width="857" alt="image" src="https://github.com/user-attachments/assets/f8849896-5674-44ec-8933-7a1a4bdc6238">

1. Review the slides of Lecture 5.

2. Login to MySQL and make sure you have the tables products, pcs, laptops, printers, customers and sales in your database.

3. Click on the SQL tab in phpMyAdmin. Here you can write and execute SQL statements.

4. Write SQL SELECT statements for performing the following queries. Use either a join or a subquery. If a question is asking to include attributes from one table only in the SELECT clause of the SELECT statement, try to find two solutions, one with a join, and another with a subquery.

- a. List all PC models that have been sold at least once.
```sql
SELECT DISTINCT pcs.model
FROM pcs
JOIN sales ON sales.model = pcs.model;
```
- b. List the makers of laptops with speed of at least 2.00.
```sql
SELECT DISTINCT products.maker FROM products
JOIN laptops ON laptops.model = products.model
WHERE laptops.speed >= 2 AND products.type = 'laptop';
```

- c. List all pairs of PC models that have both the same speed and ram. A pair should be listed only once; e.g., list (i, j) but not (j, i).
```sql
SELECT p1.model, p2.model
FROM pcs p1
JOIN pcs p2 ON p1.speed = p2.speed AND p1.ram = p2.ram
WHERE p1.model < p2.model;
```

- d. List the makers that make at least two different models of PC.
```sql
SELECT maker
FROM products p1
WHERE p1.type = 'pc'
AND EXISTS (
    SELECT 1
    FROM products p2
    WHERE p2.maker = p1.maker
    AND p2.model <> p1.model
    AND p2.type = 'pc'
);

```
- e. List the maker(s) of the laptop(s) with the highest available speed.
```sql
SELECT DISTINCT products.maker
FROM products
JOIN laptops ON products.model = laptops.model
WHERE laptops.speed = (
    SELECT MAX(speed)
    FROM laptops
);
```
- f. List the cities with customers who bought a printer.
```sql
SELECT DISTINCT c.city
FROM customers c
JOIN sales s ON c.customer_id = s.customer_id
WHERE s.model IN (
    SELECT model
    FROM products
    WHERE type = 'printer'
);
```
- g. List the makers of PCs that don't make any laptop (but may make printers)
```sql
SELECT DISTINCT p.maker
FROM products p
WHERE p.type = 'pc'
AND p.maker NOT IN (
    SELECT DISTINCT p2.maker
    FROM products p2
    WHERE p2.type = 'laptop'
);
```
- h. List the makers of PCs that don't make any laptop or printer
```sql
SELECT DISTINCT p.maker
FROM products p
WHERE p.type = 'pc'
AND p.maker NOT IN (
    SELECT DISTINCT p2.maker
    FROM products p2
    WHERE p2.type IN ('laptop', 'printer')
);
```

- i. List the model numbers and prices of laptops which are cheaper than at least one PC
```sql

```

5. Write SQL SELECT statements which use outer joins for performing the following queries.

- a. List all makers, all model numbers they make, and the corresponding product types (i.e. the entire maker, model and type columns from table Products). For the PC models only list their speed and price as well in two additional columns. These two extra columns should contain NULL markers for laptop and printer models.

- b. List all laptop model numbers and only for those made by makers A and B list also their price. The prices of laptops not made by either A or B should be NULL.

 - Hint: List the laptop model numbers made by A and B and their prices. Use the result of this query as a subquery in the FROM clause of the main query.

- c. List the names (first name and last name) of customers who haven't bought any product. Use an outer join. Can you solve it with a subquery instead?

 - Hint: In the solution that uses an outer join, use 'IS NULL' in the WHERE clause.

Note: There are no such customers in the example database. Insert a new customer into table customers to test your solution.

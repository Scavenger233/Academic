# DATABASE
## Week 1
### Database
<img width="1213" alt="image" src="https://github.com/user-attachments/assets/9d8b2a0e-cee4-4163-9130-d84e26b13846">

- DBMS: database management system
- query optimization

### SQL

#### Definition
- primarily a query language
- also a data definition component

#### Constraints
- names/identifiers:
  - no longer than 128 characters
  - must start with a letter
  - contain no spaces
  
#### SQL data types
  - Boolean: BOOLEAN
  - Character: 
     - CHAR(n ) = **fixed-length** string of n  characters.
     - VARCHAR(n ) = **variable-length** string of up to n  characters.
  - Numeric: NUMERIC, DECIMAL, INTEGER, SMALLINT, FLOAT, REAL, DOUBLE PRECISION
  - Datetime: DATE, TIME, TIMESTAMP

#### Values
- Integers and reals (i.e. floating point numbers) are represented as you would expect
- Strings are too, except they require single quotes
- Any value can be **NULL**

### Schemas

- A database schema is structure that represents the logical storage of the data in a database.

### Primary Key/Unique

- There can be only one PRIMARY KEY for a relation, but several UNIQUE attributes.
- No attribute of a PRIMARY KEY can ever be NULL in any tuple.  But attributes declared UNIQUE may have NULL values, and there may be several tuples with NULL.

 <img width="859" alt="image" src="https://github.com/user-attachments/assets/44579857-c124-4a73-8d47-6b190b3a88eb">

# Week 2

## SQL statements

### SELECT

```sql
SELECT * FROM Customers	WHERE city = 'Limerick';
```

- Result of query
  - <img width="782" alt="image" src="https://github.com/user-attachments/assets/2335b724-5516-4166-8d8a-b59aa1790965">

- Meaning of Single-Relation Query
  - Begin with the relation in the FROM clause.
  - Apply the selection indicated by the WHERE clause.
  - Apply the projection indicated by the SELECT clause.
 
```sql
    SELECT model, price*1.4 AS priceUSD
    FROM PCs;
```


#### Pattern

- A condition can compare a string to a pattern by:
  -  Attribute LIKE pattern or 
  -  Attribute NOT LIKE pattern
    
```sql
   SELECT * FROM Employees WHERE name LIKE 'A%';
```
#### NULL values

- Missing value : e.g., we know a customer has some address, but we don’t know what it is.
- Inapplicable : e.g., the value of attribute name of spouse for an unmarried person.

#### Comparing NULLs to values

- The logic of conditions in SQL is really 3-valued logic: TRUE, FALSE, UNKNOWN.
- Comparing any value (including NULL itself) with NULL yields UNKNOWN.
- A tuple is in a query answer if and only if the WHERE clause is TRUE (not FALSE or UNKNOWN).

#### Three-Valued Logic

<img width="785" alt="image" src="https://github.com/user-attachments/assets/e9c61e3a-8220-4b4f-8c42-6f718e5f80f7">

- 2-Valued Laws != 3-Valued Laws
- See details in [here](logic.md)

#### Multiiteration Queries

- Distinguish attributes of the same name by **relation.attribute**

```sql
SELECT Employees.name, Departments.name
FROM Employees, Departments;
```

## Week 3
### SELECT

- 去重
```sql
SELECT DISTINCT name FROM WHERE Customers.customer_is = Sales.customer_id AND city = 'Limerick" AND day = '2015-12-20';
```

- JOIN
<img width="599" alt="image" src="https://github.com/user-attachments/assets/2af34cc2-9ed5-4720-811b-1709fb926a90">

```sql
table1 JOIN table2 ON condition
/* combine date from 2 tables */

table1 LEFT JOIN table2 ON condition
/* Similar to JOIN but if a row in table1 has no match in table2 then it is matched with a row containing NULL values */

table1 RIGHT JOIN table2 ON condition /* is equal to */ table2 RIGHT JOIN table1 ON condition

table1 FULL JOIN table2 ON condition
/* 左右表都保留，返回左表和右表的所有记录，匹配的行会成对，不匹配的行会与NULL值进行匹配。*/

table1 JOIN table2 USING (a1, a2,...,an)
/*To check both tables contains a1, a2,...
  only one copy is present in the value*/

table1 NATURAL JOIN table2
/* same as above but find the same a1, a2 automatically*/

	SELECT c1.customer_id, c2.customer_id
	FROM Customers c1, Customers c2
	WHERE c1.city = c2.city AND
		  c1.customer_id < c2.customer_id;
/* Produce pairs in ascending (or alphabetic) order */

```
### Subqueries

A parenthesized SELECT-FROM-WHERE statement(***subquery***) can be used as a value in a number of places, including **FROM** and **WHERE** clause.

- **Must** use a tuple-variable to name tuples of the result.

#### Subqueries in WHERE

```sql
  SELECT model
		FROM Products JOIN PCs USING(model)
		WHERE maker = 'A' AND speed >= 2.0;

/* Equals to */

  SELECT model
  FROM Products JOIN
       (SELECT model FROM PCs WHERE speed >= 2.0) atleast2
       USING(model)
  WHERE maker = 'A';
```

#### Subqueries in FROM

- The tuple must has one component.
- A run-time error occurs if there is no tuple or more than one tuple.
  
Using Customers, find the names of all customers from Limerick who have the same lastname as the customer with ID 1111111111.
Two queries would surely work:
1. Find the lastname of customer 1111111111 (say it is Ryan)
2. Find the names of those customers from Limerick who have the same lastname (i.e. Ryan).
```sql
  SELECT firstname, lastname
	FROM customers
	WHERE city = 'Limerick' AND
		       lastname = (SELECT lastname
			     	           FROM customers
			             	   WHERE customer_id='1111111111');
```

#### The IN Operator

- <tuple> IN (<subquery>) is true if and only if the tuple is a member of the relation produced by the subquery.
  - Opposite: <tuple> NOT IN (<subquery>).
- IN-expressions can appear in **WHERE** clauses.

```sql
SELECT model
	   FROM Products
	   WHERE maker = 'B' AND
		          model IN (SELECT model
			          	     FROM PCs
			                 WHERE speed >= 2.0 AND
                                                       speed <= 2.8);
```

#### The Exists Operator

- EXISTS(<subquery>) is true if and only if the subquery result is **not empty**.
- Example: From Customers, find the IDs of those customers whose first names are unique, i.e. no other customer has the same first name.
```sql
	SELECT customer_id
	FROM Customers c1
	WHERE NOT EXISTS (
		SELECT *
		FROM Customers
		WHERE firstname = c1.firstname AND
			    customer_id <> c1.customer_id);
```

#### The Operators ANY and ALL

- x = ANY(<subquery>) is a Boolean condition that is true if and only if x equals at least one tuple in the subquery result.
  - = could be any comparison operator.
- x <> ALL(<subquery>) is true if and only if x is different from all tuples in the subquery result.
  - <> can be any comparison operator.
 
- From PCs find the fastest PC model(s) with hd less than or equal to 250.
```sql
SELECT model
	FROM PCs
	WHERE hd <= 250 AND
                   speed >= ALL(SELECT speed
			                      FROM PCs
                                            WHERE hd <= 250);
```




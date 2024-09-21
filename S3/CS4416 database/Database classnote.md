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
<img width="792" alt="image" src="https://github.com/user-attachments/assets/6d6eb3ef-254c-4398-8649-19557b6470f9">

- Result of query
  - <img width="782" alt="image" src="https://github.com/user-attachments/assets/2335b724-5516-4166-8d8a-b59aa1790965">

- Meaning of Single-Relation Query
  - Begin with the relation in the FROM clause.
  - Apply the selection indicated by the WHERE clause.
  - Apply the projection indicated by the SELECT clause.

#### Pattern

- A condition can compare a string to a pattern by:
    - <Attribute> LIKE <pattern> or 
    - <Attribute> NOT LIKE <pattern>
    
```sql
   SELECT * FROM Employees WHERE name LIKE 'A%';
```


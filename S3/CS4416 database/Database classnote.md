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

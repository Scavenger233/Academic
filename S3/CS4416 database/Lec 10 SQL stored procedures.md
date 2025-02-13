# Lec 10 SQL stored procedures
## PSM persistent stored modules
- Procedure(no return value)
  - ```sql
    CREATE PROCEDURE name(parameter list);
    ```
- Function( with a return value)
  - ```sql
    CREATE FUNCTION name(parameter list)
    RETURN type;
    ```
### Parameters in PSM
- mode-name-type triples
- mode can be:
  - IN : uses value, no value change
  - OUT : no use, procedure changes
  - INOUT: both
 
# Involing procedure
```sql
CALL someProcedure;
```

### Statements in PSM
```sql
--DECLARATION
  DECLARE name type;

  DECLARE total INT;

--BEGIN & END
CREATE FUNCTION CalculateTotal (price DECIMAL, qty INT) RETURNS DECIMAL
  BEGIN
      DECLARE total DECIMAL;
      SET total = price * qty; -- Multiply price and quantity
      RETURN total; -- Set the return value (but function continues)
  END;
--ASSIGNMENT STATEMENT
  SET x = 'Limerick';

--LABEL USE
  BEGIN
    DECLARE x INT DEFAULT 0;

    loop_label: WHILE x < 5 DO
        SET x = x + 1;
        IF x = 3 THEN
            LEAVE loop_label; -- Exit the loop when x = 3
        END IF;
    END WHILE;

  END;

--IF STATEMENT
IF x > 10 THEN
    SET y = 20; -- Executes if x > 10
ELSEIF x = 10 THEN
    SET y = 15; -- Executes if x = 10
ELSE
    SET y = 5; -- Executes if x < 10
END IF;
```

### Explanation of Queries in PSM

In **Persistent Stored Modules (PSM)**, general `SELECT-FROM-WHERE` queries cannot be used as standalone statements. Instead, you have three ways to use them:

---

### 1. **Queries Producing One Value (Assignment):**
   - Use a query that produces a single value in an **assignment statement**.
   - Example:
     ```sql
     SET total_sales = (SELECT SUM(quantity) FROM Sales WHERE model = 'L123');
     ```
     **Explanation:**
     - The query calculates the total sales for a specific model (`'L123'`).
     - The result is assigned to the variable `total_sales`.

---

### 2. **Single-Row SELECT INTO:**
   - Use `SELECT ... INTO` to assign values directly to variables when the query returns **one row**.
   - Example:
     ```sql
     SELECT price INTO laptop_price FROM Laptops WHERE model = 'L123';
     ```
     **Explanation:**
     - The query fetches the `price` of the model `'L123'`.
     - The result is stored in the variable `laptop_price`.

---

### 3. **Cursors:**
   - Use **cursors** for queries that return multiple rows. Cursors allow you to process rows one at a time.
   - Example:
     ```sql
     DECLARE cursor_name CURSOR FOR SELECT model, price FROM Laptops;
     OPEN cursor_name;
     FETCH cursor_name INTO model_var, price_var;
     CLOSE cursor_name;
     ```
     **Explanation:**
     - A cursor is declared for a query that retrieves multiple rows.
     - The cursor is opened, rows are fetched into variables (`model_var`, `price_var`), and then the cursor is closed.

---

### Summary:
- Use **assignments** for queries returning a single value.
- Use **SELECT INTO** for queries returning one row.
- Use **cursors** for queries returning multiple rows.

# Here’s an explanation and a breakdown of the **RateLaptop** function with comments:

### Function Purpose:
The `RateLaptop` function rates a laptop model (`m`) as 'unpopular', 'average', or 'popular' based on its total sales quantity between two dates (`d1` and `d2`). If the inputs are invalid, it returns 'incorrect'.

---

### Code with Comments:
```sql
CREATE FUNCTION RateLaptop (m CHAR(4), d1 DATE, d2 DATE) 
    RETURNS VARCHAR(10) -- The function returns a string ('unpopular', 'average', 'popular', or 'incorrect')
READS SQL DATA -- Indicates the function reads data from the database
BEGIN
    DECLARE total_quantity INT; -- Declare a variable to store the total sales quantity

    -- Step 1: Check if the laptop model exists in the Laptops table
    IF m NOT IN (SELECT model FROM Laptops) THEN 
        RETURN 'incorrect'; -- Return 'incorrect' if the model is not found
    -- Step 2: Check if the date range is valid
    ELSEIF d2 < d1 THEN 
        RETURN 'incorrect'; -- Return 'incorrect' if the end date is earlier than the start date
    ELSE
        -- Step 3: Calculate the total quantity sold between the given dates
        SELECT SUM(quantity) INTO total_quantity 
        FROM Sales
        WHERE model = m AND (day BETWEEN d1 AND d2);

        -- Step 4: Rate the laptop based on the total quantity
        IF (total_quantity IS NULL) OR (total_quantity < 10) THEN 
            RETURN 'unpopular'; -- Less than 10 units sold
        ELSEIF total_quantity < 100 THEN 
            RETURN 'average'; -- 10–99 units sold
        ELSE 
            RETURN 'popular'; -- 100 or more units sold
        END IF;
    END IF;
END;
```

---

### How It Works:
1. **Input Validation:**
   - If the model does not exist in the `Laptops` table → Return `'incorrect'`.
   - If the date range (`d2` before `d1`) is invalid → Return `'incorrect'`.

2. **Total Sales Calculation:**
   - Fetch the total sales quantity for the given model and date range from the `Sales` table.

3. **Rating Logic:**
   - **Total quantity < 10** → `'unpopular'`.
   - **Total quantity between 10 and 99** → `'average'`.
   - **Total quantity >= 100** → `'popular'`.

---

### Example Call:
```sql
SELECT RateLaptop('L123', '2024-01-01', '2024-12-31');
```

### Possible Results:
- `'unpopular'`, `'average'`, `'popular'`, or `'incorrect'` based on the inputs and sales data.

# Here’s a breakdown of the **LaptopPriceAdjustment** procedure with comments for clarity:

### **Code with Comments:**

```sql
CREATE PROCEDURE LaptopPriceAdjustment(IN X CHAR(1)) -- Takes maker X as input
BEGIN
    DECLARE done INT DEFAULT FALSE; -- Flag to check when cursor finishes
    DECLARE m CHAR(4); -- Variable to hold the model name
    DECLARE rating VARCHAR(10); -- Variable to hold the rating ('popular', 'unpopular', etc.)
    
    -- Declare a cursor to fetch model and its rating
    DECLARE c CURSOR FOR 
        SELECT model, RateLaptop(model, CURDATE() - INTERVAL 1 MONTH, CURDATE())
        FROM Laptops 
        WHERE model IN (
            SELECT model FROM Products WHERE maker = X -- Get models by maker X
        );

    -- Handler to set 'done' flag to TRUE when no more rows are available
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;

    OPEN c; -- Open the cursor
    
    -- Start the loop to process each laptop model
    menuLoop: LOOP
        FETCH c INTO m, rating; -- Fetch the next model and its rating
        IF done THEN 
            LEAVE menuLoop; -- Exit loop if no more rows
        END IF;

        -- Check the rating and adjust the price accordingly
        IF rating = 'unpopular' THEN 
            UPDATE Laptops SET price = price - 10 WHERE model = m; -- Lower price by 10 euros
        ELSEIF rating = 'popular' THEN 
            UPDATE Laptops SET price = price + 10 WHERE model = m; -- Raise price by 10 euros
        END IF;
    END LOOP;

    CLOSE c; -- Close the cursor after processing
END;
```

---
---

### **What the Procedure Does:**
1. **Input:** 
   - Takes a maker (`X`) as input to filter laptop models belonging to that maker.
2. **Cursor:**
   - Loops through all laptop models by maker `X`.
   - Uses the `RateLaptop` function to determine if each model is `popular` or `unpopular`.
3. **Adjust Prices:**
   - **Raise price** by 10 euros for `popular` laptops.
   - **Lower price** by 10 euros for `unpopular` laptops.
4. **Exits Loop:** 
   - Ends the loop when no more rows are available.

---



### **How It Works:**

1. **Input Maker (X):**
   - The procedure takes the maker as input and finds all laptop models by that maker.

2. **Cursor and Loop:**
   - The cursor iterates over each model and retrieves:
     - The **model name (`m`)**.
     - The **rating** (using `RateLaptop` function for the last month).

3. **Price Adjustment:**
   - For each model:
     - If rated `unpopular`: Decrease the price by 10 euros.
     - If rated `popular`: Increase the price by 10 euros.

4. **Termination:**
   - When all rows are processed, the `done` flag ensures the loop exits, and the cursor is closed.

---

### **Example Call:**
```sql
CALL LaptopPriceAdjustment('D'); -- Adjusts prices for maker 'D'
```

### **Explanation of Results:**
- If a laptop by maker `'D'` is **popular**, its price is increased by 10 euros.
- If it’s **unpopular**, its price is decreased by 10 euros.
- The prices for other laptops remain unchanged.

This demonstrates how to combine **cursors**, **functions**, and **conditional logic** effectively in stored procedures.

### **Explanation of Cursor Loops with SQLSTATE Handling**

In PSM (Persistent Stored Modules), when using a **cursor** inside a loop, you need to handle the case where the cursor has no more rows to fetch. This is typically done using SQLSTATE or by declaring a **condition** to check specific SQLSTATE values.

---

### **Key Concepts:**

1. **SQLSTATE:**
   - A 5-character string updated after each SQL operation.
   - **`02000`** means "No more rows found."

2. **Condition Declaration:**
   - You can declare a **condition** to represent a specific SQLSTATE value.
   - Example:
     ```sql
     DECLARE NotFound CONDITION FOR SQLSTATE '02000';
     ```

3. **Cursor Loop Structure:**
   - Use `FETCH` to get the next tuple.
   - Use `NotFound` or SQLSTATE to exit the loop when there are no more rows.


---

### **Key Benefits:**
- **SQLSTATE or Conditions:** Ensure graceful handling of the cursor’s end.
- **Flexible Processing:** Allows you to process each tuple independently.
- **Scalable:** Useful for large datasets where row-by-row processing is needed.

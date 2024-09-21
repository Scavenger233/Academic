这段话讨论了**三值逻辑**（`TRUE`, `FALSE`, `UNKNOWN`）中常见的逻辑定律，以及哪些定律在这种逻辑下成立，哪些不成立。让我们逐步解释这段话。

### 1. **"Some common laws hold in 3-valued logic."**
   - 在传统的两值逻辑中，常见的逻辑定律依然在三值逻辑中成立。两值逻辑指的是所有命题的真值只能是 `TRUE` 或 `FALSE`。三值逻辑引入了 `UNKNOWN`，但某些逻辑定律仍然适用于三值逻辑。

### 2. **"Example: commutativity of AND, i.e. p AND q is the same as q AND p."**
   - **交换律（Commutativity of AND）**是指，对于两个条件 `p` 和 `q`，无论它们的顺序如何，`AND` 运算的结果是相同的。
   - **`p AND q` 和 `q AND p` 是等价的**，不论 `p` 和 `q` 的值是 `TRUE`、`FALSE` 或 `UNKNOWN`。
   - 这在三值逻辑中也是成立的。
     - 例如：
       - 如果 `p = TRUE`，`q = UNKNOWN`，那么 `p AND q = UNKNOWN`，而 `q AND p` 也是 `UNKNOWN`。
       - 如果 `p = FALSE`，`q = UNKNOWN`，那么 `p AND q = FALSE`，而 `q AND p` 也是 `FALSE`。

   这个例子说明了三值逻辑下**`AND` 运算的交换律**依然成立。

### 3. **"But not others, e.g. the law of the excluded middle: p OR NOT p = TRUE."**
   - **排中律（Law of the Excluded Middle）**在传统两值逻辑中成立，它的意思是**对任何命题 `p`，`p` 和 `NOT p` 之间必定有一个为真**。
   - 用逻辑表示就是：
     ```sql
     p OR NOT p = TRUE
     ```
     这意味着无论 `p` 是 `TRUE` 还是 `FALSE`，这个表达式总是 `TRUE`。
   - 但是，在三值逻辑中，这个定律不再成立，因为三值逻辑中还有一个额外的值：`UNKNOWN`。

### 4. **"When p = UNKNOWN, the left side is UNKNOWN!"**
   - 当 `p = UNKNOWN` 时，`p OR NOT p` 的值并不一定是 `TRUE`，而是 `UNKNOWN`。这破坏了传统逻辑中的排中律。
   - 具体分析：
     - 当 `p = UNKNOWN` 时，`NOT p` 也会是 `UNKNOWN`。
     - 因此，`p OR NOT p` = `UNKNOWN OR UNKNOWN`，根据三值逻辑的运算规则，`UNKNOWN OR UNKNOWN` 结果依然是 `UNKNOWN`。
     - 这与传统的两值逻辑不同，因为在传统逻辑中，`p OR NOT p` 总是 `TRUE`，而在三值逻辑中，结果可能是 `UNKNOWN`。

### 示例：三值逻辑中的排中律失效
假设在 SQL 中有以下表达式：
```sql
SELECT * FROM Employees WHERE salary IS NULL OR salary IS NOT NULL;
```
- 根据两值逻辑，`salary` 要么是 `NULL`，要么不是 `NULL`，因此 `salary IS NULL OR salary IS NOT NULL` 应该是 `TRUE`。
- 但在三值逻辑中，如果 `salary = NULL`，则：
  - `salary IS NULL` 的结果是 `TRUE`。
  - `salary IS NOT NULL` 的结果是 `FALSE`。
  - 所以 `TRUE OR FALSE = TRUE`，这是排中律在这部分逻辑中的体现。
  
  然而，如果我们尝试如下情况：
  
```sql
SELECT * FROM Employees WHERE salary = 5000 OR salary != 5000;
```
当 `salary` 为 `NULL` 时：
- `salary = 5000` 结果是 `UNKNOWN`。
- `salary != 5000` 结果也是 `UNKNOWN`。
- 于是 `UNKNOWN OR UNKNOWN = UNKNOWN`。

这里违反了排中律，因为传统逻辑中我们期望 `p OR NOT p` 总是为 `TRUE`，但三值逻辑中的 `UNKNOWN` 打破了这一点。

### 总结
- 在 SQL 的三值逻辑中，某些常见的逻辑定律（如 `AND` 的交换律）依然成立，因为它们不依赖于真假值的具体类型。
- 但其他逻辑定律（如排中律）在三值逻辑中可能失效，特别是在 `UNKNOWN` 存在的情况下，`p OR NOT p` 并不总是 `TRUE`，而可能是 `UNKNOWN`。三值逻辑的引入使得对 `NULL` 值的处理变得更复杂。

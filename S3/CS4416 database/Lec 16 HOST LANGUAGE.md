

### **1. Three-Tier Architecture**

  1. **First tier**（Cilent, user-interface）
  2. **Second tier**（application）
  3. **Third tier**（database server）


---

### **2. Java中使用JDBC连接数据库**
- **JDBC (Java Database Connectivity)**：

  - [官方教程](http://docs.oracle.com/javase/tutorial/jdbc/basics/) 提供了完整文档。

#### **步骤1：建立连接**
- sample code：
  ```java
  import java.sql.*;
  Class.forName("com.mysql.jdbc.Driver");
  Connection myCon = DriverManager.getConnection("数据库URL", "用户名", "密码");
  ```
  - `Class.forName`：加载数据库驱动。
  - `DriverManager.getConnection`：获取数据库连接。

#### **步骤2：创建SQL语句**
- **三种语句类型**：
  1. **Statement**：简单SQL语句，无参数。
  2. **PreparedStatement**：预编译语句，支持参数化查询（更高效、安全）。
  3. **CallableStatement**：用于调用存储过程。

- 示例：
  ```java
  Statement stat1 = myCon.createStatement();
  PreparedStatement stat2 = myCon.prepareStatement(
      "SELECT model, SUM(quantity) FROM pcshop.Sales GROUP BY model"
  );
  ```

#### **步骤3：执行SQL语句**
- **查询**：使用 `executeQuery()` 返回结果集（`ResultSet`）。
- **更新/修改**：使用 `executeUpdate()` 执行插入、删除、更新操作。

- 示例：
  - 插入：
    ```java
    stat1.executeUpdate("INSERT INTO pcshop.Products VALUES('A', '5001', 'pc')");
    ```
  - 查询：
    ```java
    ResultSet totalsales = stat2.executeQuery();
    ```

#### **步骤4：处理结果集**
- **ResultSet** 是类似于游标的数据结构，用于遍历查询结果。
- 常用方法：
  - `next()`：移动到下一行，返回 `true` 或 `false`。
  - `getX(i)`：获取当前行第 `i` 列的数据，`X` 是列的数据类型。

- 示例：
  ```java
  while (totalsales.next()) {
      String model = totalsales.getString(1);
      int totalQuantity = totalsales.getInt(2);
  }
  ```

#### **步骤5：关闭连接**
- 释放资源：
  ```java
  myCon.close();
  ```

---

### **3. PHP中使用MySQL连接数据库**
#### **步骤1：连接数据库**
- 示例代码：
  ```php
  $connection = mysqli_connect("服务器", "用户名", "密码") or die("Unable to connect!");
  mysqli_select_db($connection, "数据库名") or die("Unable to select database!");
  ```

#### **步骤2：创建和执行查询**
- 创建查询语句：
  ```php
  $query = "SELECT model, maker FROM Products WHERE type = 'pc'";
  ```
- 执行查询：
  ```php
  $result = mysqli_query($connection, $query) or die("Error in query.");
  ```

#### **步骤3：处理查询结果**
- 检查是否有结果：
  ```php
  if (mysqli_num_rows($result) > 0) {
      while ($row = mysqli_fetch_row($result)) {
          echo "<tr><td>$row[0]</td><td>$row[1]</td></tr>";
      }
  } else {
      echo "No rows found!";
  }
  ```

#### **步骤4：关闭连接**
- 释放资源并关闭连接：
  ```php
  mysqli_free_result($result);
  mysqli_close($connection);
  ```

---

### **4. 实践中的建议**
1. 使用 **PreparedStatement** 替代 **Statement**，防止SQL注入，提高查询效率。
2. 在 PHP 中，尽量使用 `mysqli` 或 `PDO`，避免使用过时的 `mysql` 扩展。
3. 数据库操作后及时释放资源（如关闭 `ResultSet` 和连接）。
4. 遵循三层架构设计，保持代码的模块化和可维护性。


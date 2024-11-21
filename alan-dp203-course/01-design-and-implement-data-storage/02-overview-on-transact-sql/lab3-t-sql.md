### **T-SQL (Transact-SQL)**

#### **Connecting to Azure SQL Database in Azure Data Studio**

1. Go to the **Azure Portal** and navigate to **All Resources**.  
   You will see two resources:
   - **Azure SQL Database**
   - **Azure SQL DB Server**

2. Open **Azure Data Studio** and create a new connection:
   - Enter the **Server Name** from the Azure portal.
   - Change **Authentication Type** to **SQL Login**.
   - Provide the **Username** and **Password**.
   - Leave **Encryption** as optional.
   - Click **Connect**.

3. Once connected, you can create a query window to execute SQL statements.

---

### **Sample Table: SalesLT.SalesOrderDetail**

For demonstration, let’s assume the following data in the **SalesLT.SalesOrderDetail** table:

| **SalesOrderID** | **ProductID** | **OrderQty** | **UnitPrice** |
|-------------------|---------------|---------------|---------------|
| 71774            | 836           | 15            | 45.00         |
| 71775            | 837           | 20            | 55.00         |
| 71776            | 836           | 8             | 40.00         |
| 71777            | 838           | 12            | 60.00         |

---

### **SQL Queries and Examples with Output**

#### **1. SELECT Clause**
- Fetch all columns from the table:
  ```sql
  SELECT * FROM SalesLT.SalesOrderDetail;
  ```
  **Output:**
  | **SalesOrderID** | **ProductID** | **OrderQty** | **UnitPrice** |
  |-------------------|---------------|---------------|---------------|
  | 71774            | 836           | 15            | 45.00         |
  | 71775            | 837           | 20            | 55.00         |
  | 71776            | 836           | 8             | 40.00         |
  | 71777            | 838           | 12            | 60.00         |

- Fetch specific columns with aliasing:
  ```sql
  SELECT SalesOrderID, ProductID, OrderQty AS 'Order Quantity' FROM SalesLT.SalesOrderDetail;
  ```
  **Output:**
  | **SalesOrderID** | **ProductID** | **Order Quantity** |
  |-------------------|---------------|---------------------|
  | 71774            | 836           | 15                  |
  | 71775            | 837           | 20                  |
  | 71776            | 836           | 8                   |
  | 71777            | 838           | 12                  |

---

#### **2. WHERE Clause**
- Filter rows using specific conditions:
  ```sql
  SELECT * FROM SalesLT.SalesOrderDetail
  WHERE ProductID = 836 AND OrderQty > 10;
  ```
  **Output:**
  | **SalesOrderID** | **ProductID** | **OrderQty** | **UnitPrice** |
  |-------------------|---------------|---------------|---------------|
  | 71774            | 836           | 15            | 45.00         |

- Search for a specific value in another table:
  ```sql
  SELECT * FROM SalesLT.Customer
  WHERE LastName = 'Harris';
  ```
  *(This query depends on the **SalesLT.Customer** table contents.)*

---

#### **3. ORDER BY Clause**
- Sort rows based on a column:
  ```sql
  SELECT * FROM SalesLT.SalesOrderDetail
  WHERE OrderQty > 10
  ORDER BY UnitPrice DESC;
  ```
  **Output:**
  | **SalesOrderID** | **ProductID** | **OrderQty** | **UnitPrice** |
  |-------------------|---------------|---------------|---------------|
  | 71777            | 838           | 12            | 60.00         |
  | 71775            | 837           | 20            | 55.00         |
  | 71774            | 836           | 15            | 45.00         |

---

#### **4. Aggregate Functions**
- Count rows that meet a condition:
  ```sql
  SELECT COUNT(*) AS 'Count of Rows' 
  FROM SalesLT.SalesOrderDetail 
  WHERE OrderQty > 10;
  ```
  **Output:**
  | **Count of Rows** |
  |--------------------|
  | 3                  |

- Find the maximum value:
  ```sql
  SELECT MAX(OrderQty) AS 'Max value of Order Quantity' 
  FROM SalesLT.SalesOrderDetail;
  ```
  **Output:**
  | **Max value of Order Quantity** |
  |----------------------------------|
  | 20                               |

---

#### **5. GROUP BY Clause**
- Aggregate data based on a column:
  ```sql
  SELECT ProductID, SUM(OrderQty) AS 'Total Order Quantity' 
  FROM SalesLT.SalesOrderDetail 
  GROUP BY ProductID;
  ```
  **Output:**
  | **ProductID** | **Total Order Quantity** |
  |---------------|---------------------------|
  | 836           | 23                        |
  | 837           | 20                        |
  | 838           | 12                        |

---

#### **6. PARTITION BY Clause**
- Aggregate within partitions:
  ```sql
  SELECT ProductID, OrderQty, 
         SUM(OrderQty) OVER (PARTITION BY ProductID) AS 'Total Order Quantity'
  FROM SalesLT.SalesOrderDetail;
  ```
  **Output:**
  | **ProductID** | **OrderQty** | **Total Order Quantity** |
  |---------------|--------------|---------------------------|
  | 836           | 15           | 23                        |
  | 836           | 8            | 23                        |
  | 837           | 20           | 20                        |
  | 838           | 12           | 12                        |

---

#### **7. LEAD and LAG Functions**
- Fetch the next row’s value:
  ```sql
  SELECT ProductID, OrderQty, 
         LEAD(OrderQty) OVER (ORDER BY ProductID) AS 'Next Order Quantity'
  FROM SalesLT.SalesOrderDetail;
  ```
  **Output:**
  | **ProductID** | **OrderQty** | **Next Order Quantity** |
  |---------------|--------------|--------------------------|
  | 836           | 15           | 8                       |
  | 836           | 8            | 20                      |
  | 837           | 20           | 12                      |
  | 838           | 12           | NULL                    |

- Fetch the previous row’s value:
  ```sql
  SELECT ProductID, OrderQty, 
         LAG(OrderQty) OVER (ORDER BY ProductID) AS 'Previous Order Quantity'
  FROM SalesLT.SalesOrderDetail;
  ```
  **Output:**
  | **ProductID** | **OrderQty** | **Previous Order Quantity** |
  |---------------|--------------|-----------------------------|
  | 836           | 15           | NULL                       |
  | 836           | 8            | 15                         |
  | 837           | 20           | 8                          |
  | 838           | 12           | 20                         |

---

#### **8. WITH Clause**
- Assign a result set to a common table expression (CTE):
  ```sql
  WITH CTE_Products AS
  (
      SELECT ProductID, OrderQty
      FROM SalesLT.SalesOrderDetail
  )
  SELECT * FROM CTE_Products;
  ```
  **Output (same as SELECT query):**
  | **ProductID** | **OrderQty** |
  |---------------|--------------|
  | 836           | 15           |
  | 836           | 8            |
  | 837           | 20           |
  | 838           | 12           |

---

### **Table Creation, Insert, Foreign Key, and Drop Example with Outputs**

Let's create tables, insert data into them, define foreign key relationships, and handle drop operations. The example will simulate a simple **Student**, **Course**, and **Orders** database.

---

### **1. CREATE TABLE**

Create three tables: **Student**, **Course**, and **Orders**.

```sql
CREATE TABLE Student (
    StudentID VARCHAR(100) NOT NULL,
    StudentName VARCHAR(1000),
    PRIMARY KEY(StudentID) -- Ensures each StudentID is unique
);
```

**Output:**
Table **Student** is successfully created.

---

```sql
CREATE TABLE Course (
    CourseID VARCHAR(100) NOT NULL,
    CourseName VARCHAR(1000),
    Price REAL,
    PRIMARY KEY (CourseID)
);
```

**Output:**
Table **Course** is successfully created.

---

```sql
CREATE TABLE Orders (
    OrderID VARCHAR(100) NOT NULL,
    CourseID VARCHAR(100),
    CustomerID VARCHAR(100),
    DiscountPercent INT,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (CustomerID) REFERENCES Student(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Course(CourseID)
);
```

**Output:**
Table **Orders** is successfully created with foreign key constraints linking:
- `CustomerID` to `Student.StudentID`
- `CourseID` to `Course.CourseID`.

---

### **2. INSERT Data into Tables**

Insert sample data into the **Student** table:

```sql
INSERT INTO Student (StudentID, StudentName) VALUES ('S01', 'Alice');
INSERT INTO Student (StudentID, StudentName) VALUES ('S02', 'Bob');
INSERT INTO Student (StudentID, StudentName) VALUES ('S03', 'Charlie');
```

**Output (after `SELECT * FROM Student;`):**
| **StudentID** | **StudentName** |
|---------------|------------------|
| S01           | Alice            |
| S02           | Bob              |
| S03           | Charlie          |

---

Insert sample data into the **Course** table:

```sql
INSERT INTO Course (CourseID, CourseName, Price) VALUES ('C01', 'Data Science', 100.00);
INSERT INTO Course (CourseID, CourseName, Price) VALUES ('C02', 'AI Basics', 150.00);
INSERT INTO Course (CourseID, CourseName, Price) VALUES ('C03', 'Cloud Computing', 200.00);
```

**Output (after `SELECT * FROM Course;`):**
| **CourseID** | **CourseName**      | **Price** |
|--------------|---------------------|-----------|
| C01          | Data Science        | 100.00    |
| C02          | AI Basics           | 150.00    |
| C03          | Cloud Computing     | 200.00    |

---

Insert sample data into the **Orders** table:

```sql
INSERT INTO Orders (OrderID, CourseID, CustomerID, DiscountPercent) VALUES ('O01', 'C01', 'S01', 10);
INSERT INTO Orders (OrderID, CourseID, CustomerID, DiscountPercent) VALUES ('O02', 'C02', 'S02', 15);
INSERT INTO Orders (OrderID, CourseID, CustomerID, DiscountPercent) VALUES ('O03', 'C03', 'S03', 5);
```

**Output (after `SELECT * FROM Orders;`):**
| **OrderID** | **CourseID** | **CustomerID** | **DiscountPercent** |
|-------------|--------------|----------------|----------------------|
| O01         | C01          | S01            | 10                   |
| O02         | C02          | S02            | 15                   |
| O03         | C03          | S03            | 5                    |

---

### **3. FOREIGN KEY Constraints**

Foreign key constraints ensure referential integrity. For example:
- **CustomerID** in the **Orders** table references **StudentID** in the **Student** table.
- **CourseID** in the **Orders** table references **CourseID** in the **Course** table.

If you try to insert a row in the **Orders** table with a `CustomerID` or `CourseID` that doesn’t exist in the corresponding parent tables, it will result in an error.

**Example Error:**
```sql
INSERT INTO Orders (OrderID, CourseID, CustomerID, DiscountPercent) VALUES ('O04', 'C04', 'S04', 20);
```
**Error Message:**  
`Foreign key constraint failed because CourseID 'C04' or CustomerID 'S04' does not exist.`

---

### **4. DROP Statement**

The **DROP** statement deletes tables from the database. However, if a table is referenced by a foreign key constraint, it cannot be dropped directly.

#### Example: Dropping the **Student** Table
```sql
DROP TABLE Student;
```
**Error Message:**  
`Cannot drop the table 'Student' because it is referenced by a FOREIGN KEY in the 'Orders' table.`

---

#### Correct Way to Drop Tables:
1. **Delete the dependent table first**:
   ```sql
   DROP TABLE Orders;
   ```
   **Output:** Table **Orders** is successfully deleted.

2. Then drop the parent tables:
   ```sql
   DROP TABLE Student;
   DROP TABLE Course;
   ```
   **Output:** Tables **Student** and **Course** are successfully deleted.

---

### **Summary of Tables and Their Data Before Deletion**

- **Student Table**:
  | **StudentID** | **StudentName** |
  |---------------|------------------|
  | S01           | Alice            |
  | S02           | Bob              |
  | S03           | Charlie          |

- **Course Table**:
  | **CourseID** | **CourseName**      | **Price** |
  |--------------|---------------------|-----------|
  | C01          | Data Science        | 100.00    |
  | C02          | AI Basics           | 150.00    |
  | C03          | Cloud Computing     | 200.00    |

- **Orders Table**:
  | **OrderID** | **CourseID** | **CustomerID** | **DiscountPercent** |
  |-------------|--------------|----------------|----------------------|
  | O01         | C01          | S01            | 10                   |
  | O02         | C02          | S02            | 15                   |
  | O03         | C03          | S03            | 5                    |

---
### **Notes on Data Warehouse: Understanding the Concept**

#### **Key Concepts:**
1. **Data Lake:**  
   - A data lake serves as a repository for incoming data, which is often raw and unstructured.  

![Image 1](./assets/intro-imgs/img1.png)

![Image 2](./assets/intro-imgs/img2.png)

---

#### **What is a Data Warehouse?**
- A **Data Warehouse** is a structured repository designed to store and manage **structured data**.  
- It enables users to execute **SQL queries** to interact with and analyze the stored data effectively.

---

#### **Why Do We Need a SQL Data Warehouse?**

- Consider an **online application** such as an **online course platform**:
  - **Transactional Data Examples**:
    - **Orders** table: Stores purchases made by students.
    - **Students** table: Contains student details.
    - **Courses** table: Holds course information.

- These transactional data tables are typically part of an **OLTP system (Online Transactional Processing)**:
  - Designed to handle continuous transactions (e.g., purchases happening every second).
  - Optimized for real-time processing of transactional data.

---

#### **Challenges with Transactional Systems (OLTP):**
- Business users or senior management often require insights from the data, such as:
  - Trends in course popularity.
  - Forecasted sales for the next quarter.
  - Avenues for improving user experience.
- Analyzing this data directly on the transactional system could:
  - Put a strain on the OLTP system.
  - Impact the performance of the application (e.g., delayed purchases or data loss).

---

#### **Solution: SQL Data Warehouse**
- **Why a Separate System?**
  - A **SQL Data Warehouse** is designed to handle large volumes of data for analysis without affecting the operational systems.
  - It supports both:
    - **Current transactional data.**
    - **Historical data** for long-term trend analysis.

- **Core Functionality**:
  - Extracts data from the transactional system (and potentially other sources).
  - Stores it in a structure optimized for analytical queries.
  - Enables **OLAP (Online Analytical Processing)**, which is different from OLTP:
    - OLAP systems are designed to process and analyze large datasets efficiently.

---

#### **Key Differences Between OLTP and OLAP**:
| **Feature**                | **OLTP** (SQL Database)                  | **OLAP** (SQL Data Warehouse)        |
|----------------------------|------------------------------------------|---------------------------------------|
| **Purpose**                | Handles real-time transactions.          | Performs large-scale analytical queries. |
| **System Type**            | Online Transactional Processing (OLTP).  | Online Analytical Processing (OLAP). |
| **Data Focus**             | Current transactional data.              | Current + Historical data.           |
| **Optimization**           | Optimized for INSERT, UPDATE, DELETE.    | Optimized for SELECT queries.        |
| **Performance Impact**     | Impacted by heavy reporting.             | Separate system ensures no impact.   |

---

#### **Benefits of Using a Data Warehouse**:
1. **Separation of Concerns**:
   - OLTP and OLAP systems operate independently, ensuring no performance issues.
2. **Historical Data Analysis**:
   - Facilitates insights using both current and historical data.
3. **Efficient Querying**:
   - Optimized for running complex analytical queries over large datasets.

---

#### **Design of a SQL Data Warehouse**:
- The underlying engine is tailored for analytical purposes:
  - Handles **large volumes of data** efficiently.
  - Supports **complex aggregations and computations**.
- Example: **Azure Synapse Analytics**:
  - Offers advanced design options for SQL data warehouses, making it distinct from SQL databases.
  - Can host both transactional and historical data for detailed trend analysis.

---

#### **Summary**:
- A **data warehouse** is essential for businesses needing in-depth insights without impacting their transactional systems.
- The separation between OLTP and OLAP systems ensures smooth application performance while enabling robust analytics.  
- Tools like **Azure Synapse Analytics** provide powerful data warehousing capabilities to meet modern analytical needs. 


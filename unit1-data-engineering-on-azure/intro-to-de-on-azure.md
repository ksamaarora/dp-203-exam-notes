| **Data Type**       | **Description**                                                                                   | **Examples**                          | **Diagram**                        |
|---------------------|---------------------------------------------------------------------------------------------------|---------------------------------------|------------------------------------|
| **Structured Data** | Organized in tables with consistent rows and columns, making it easily searchable and analyzable. | Relational databases, CSV files       | Table with rows and columns        |
| **Semi-structured** | Partially organized in hierarchical formats; may require flattening to fit table structures.      | JSON, XML files                       | JSON tree format                   |
| **Unstructured**    | Lacks predefined structure; stored as files or blobs without a specific schema.                   | PDFs, images, Word documents          | Files or blobs without structure    |

### Data Operations
1. **Data Integration**: 
   - Establishes links between different services (operational/analytical) to enable secure, reliable access to data across multiple sources.
   - Example: Integrating data from CRM, ERP, and other business systems.

2. **Data Transformation**: 
   - Converts raw data to a structured format for analysis, typically through ETL (Extract, Transform, Load) or ELT (Extract, Load, Transform) processes.
   - Example: Cleaning and organizing data before storing it in a data warehouse.

3. **Data Consolidation**: 
   - Combines data from multiple sources into a consistent format, often stored in a data lake or data warehouse for reporting and analytics.
   - Example: Merging datasets from various sources for unified analytics.

Data engineers commonly use **SQL** for **managing and querying** data in tables with commands like SELECT, INSERT, UPDATE, and DELETE. **Python** is also essential, especially in data analysis and machine learning, and is widely used in notebooks for data manipulation and visualization. Additionally, languages like **R, Java, Scala,** and **.NET** may be used depending on project needs, with notebooks allowing flexible, collaborative work across languages.

> ### DATA ENGINEERING CONCEPTS

Here's a concise overview of essential data engineering concepts:

1. **Operational vs. Analytical Data**: 
   - ![Operational vs. Analytical Data](./unit1-data-engineering-on-azure/assets/Operational%20and%20analytical%20data.png)
   - **Operational data** is transactional, stored in databases, and used by applications.
   - **Analytical data** is optimized for reporting, often in a data warehouse.
   - Data engineers design ETL solutions to integrate and prepare this data for analysis.

2. **Streaming Data**:
   - Real-time data from sources like IoT devices and social media.
   - Requires solutions to capture and combine real-time and batch data.

3. **Data Pipelines**:
   - Automate data transfers and transformations in ETL workflows, triggered on schedules or events.

4. **Data Lakes**:
   - Large repositories storing raw, untransformed data from multiple sources (structured, semi-structured, unstructured).
   - Suitable for big data storage and future processing.

5. **Data Warehouses**:
   - Centralized storage for integrated data from different sources, organized for optimized analytical queries.
   - Data engineers design and manage these for efficient data querying.

6. **Apache Spark**:
   - Framework for distributed, in-memory data processing.
   - Often used to process data in data lakes, supporting large-scale data analysis and preparation.

# Social-media-pipeline


##  Project Overview

This project aims to create an **end-to-end data pipeline** to transform batch raw social media data into meaningful insights to support **business intelligence**, **reporting**, and **advanced analytics**.

The pipeline facilitates the **ingestion**, **processing**, **storage**, and **analysis** of data from multiple sources — ensuring **data integrity**, **scalability**, and **accessibility**.



##  Objectives

1. Develop a robust data ingestion pipeline that can handle batch data from sources.
2. Implement data processing workflows to transform raw data into structured formats, making it suitable for analysis and reporting.
3. Establish a data warehouse using PostgreSQL to serve as a centralized repository for business intelligence and reporting.
4. Provide actionable insights and reports to business teams.

---

##  Tools and Technologies

- **Apache Spark**: Data processing, transformation, and analysis  
- **PostgreSQL**: Data warehousing and SQL-based querying  
- **dbt**: Creating data marts and models by applying transformations and aggregations  
- **Power BI**: Creating a dashboard to serve business needs  
- **Docker**: Containerization for consistent and isolated environments  

---

## Architecture and Design :
![Pipeline Diagram](Social-media-pipeline/sociel media pipeline.png)

This pipeline consists of **5 main phases**:

---

###  1 – Ingesting from Data Source

- The data comes in a **JSON format** (semi-structured), with nested JSON objects:
  - Each main object represents a **user**
  - Inside each user: a list of **posts**
  - Inside each post: a list of **comments**
- **PySpark** was used to:
  - Ingest the raw JSON
  - Flatten and structure the nested data into an initial DataFrame

---

### 2 – Data Validation and Cleansing

- Extracted a DataFrame for each entity from the initial structured data
- Applied validations on:
  - **User emails** to ensure data integrity
  - **Null values** filled based on field data type and business logic
- Extracted fields:
  - **Individual reaction types** from nested lists
  - **Total reactions** by summing all reaction types
- Extracted **dates** from timestamp fields for easier analytics

---

###  3 – Data Warehouse Design (PostgreSQL)

- Used **Star Schema** design:
  - **1 fact table**: `interaction_fact`
  - **3 dimension tables**: `users_dimension`, `posts_dimension`, `comments_dimension`
- Fact table logic:
  - One record for each **comment on a post**
  - If a post has no comments, it's still represented once in the fact table

---

###  4 – Data Marts for Analytics (via dbt)

Created **6 dbt models** to support key analytics:

1. Top users getting **reactions** on posts  
2. Top users getting **comments** on posts  
3. Top **tags** by total reactions  
4. Top **tags** by love reactions  
5. Top **tags** by angry reactions  
6. Top **locations** by total post count  

---

###  5 – Dashboard (Final Layer)

- Built using **Power BI**
- Connected to **PostgreSQL**
- Provides clear, actionable **insights** to the business team based on data marts





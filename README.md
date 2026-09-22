# SQL Server Data Warehouse & Analytics

A modern **SQL Server data warehouse** built to integrate, clean, transform, and analyze data from **CRM and ERP source systems**. The project follows the **Medallion Architecture**, using Bronze, Silver, and Gold layers to progressively transform raw data into business-ready analytical data.

## 📌 Project Overview

The objective of this project is to build a centralized data warehouse that combines data from multiple source systems and makes it easier to perform reliable business analysis.

The project covers the complete data warehousing workflow:

**Source Data → Bronze Layer → Silver Layer → Gold Layer → Analytics**

The warehouse transforms raw transactional data into a structured **star schema** containing fact and dimension tables that can be efficiently queried for reporting and analysis.

---

## 🏗️ Architecture

The project follows a three-layer Medallion Architecture:

```text
                    Source Systems
                 ┌──────────────────┐
                 │   CRM Data       │
                 │   ERP Data       │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │  Bronze Layer    │
                 │                  │
                 │ Raw Data         │
                 │ Minimal Changes  │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │  Silver Layer    │
                 │                  │
                 │ Cleaning         │
                 │ Transformation   │
                 │ Standardization  │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │   Gold Layer     │
                 │                  │
                 │ Fact Tables      │
                 │ Dimension Tables │
                 │ Business Views   │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │    Analytics     │
                 │                  │
                 │ Sales Analysis   │
                 │ Customer Analysis│
                 │ Product Analysis │
                 └──────────────────┘
```

---

## 🥉 Bronze Layer

The Bronze layer stores data as close as possible to its original source format.

### Responsibilities

* Load raw CRM and ERP data.
* Preserve the original source information.
* Maintain a simple structure for traceability.
* Provide the foundation for downstream transformations.

No major business transformations are performed at this stage.

---

## 🥈 Silver Layer

The Silver layer is responsible for preparing the raw data for analytical use.

### Data transformations include

* Removing duplicate records.
* Handling missing and invalid values.
* Standardizing text fields.
* Converting data types.
* Cleaning inconsistent values.
* Handling invalid dates.
* Applying business rules.
* Creating consistent keys and relationships.

The goal is to produce clean and reliable data that can be used to build the Gold layer.

---

## 🥇 Gold Layer

The Gold layer contains business-ready data designed for reporting and analytics.

The data is organized using a **star schema**.

### Dimension Tables

Examples include:

* `dim_customers`
* `dim_products`
* `dim_dates`

### Fact Tables

Examples include:

* `fact_sales`

The fact tables contain measurable business events, while dimension tables provide descriptive information about those events.

---

## ⭐ Star Schema

The analytical model follows a star-schema design:

```text
                    ┌─────────────────┐
                    │  dim_customers  │
                    └────────┬────────┘
                             │
                             │
┌─────────────────┐          ▼          ┌─────────────────┐
│   dim_products  │──────► fact_sales ◄─│    dim_dates    │
└─────────────────┘                     └─────────────────┘
```

This structure simplifies analytical queries and improves readability and performance for reporting workloads.

---

## 🔍 Data Quality Checks

Several validation checks are performed during the transformation process.

Examples include:

* Duplicate record detection.
* NULL value detection.
* Invalid date detection.
* Invalid customer/product references.
* Negative or inconsistent sales values.
* Uniqueness checks for keys.
* Referential integrity validation.

Example:

```sql
SELECT
    customer_id,
    COUNT(*) AS duplicate_count
FROM silver.crm_cust_info
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

This query identifies customers that appear multiple times in the Silver layer.

---

## 📊 Analytics

The Gold layer is used to answer business-oriented questions such as:

### Customer Analysis

* Who are the highest-value customers?
* How much revenue does each customer generate?
* How many orders has each customer placed?
* How does customer performance change over time?

### Product Analysis

* Which products generate the most revenue?
* Which products have the highest sales volume?
* How are products performing across different periods?

### Sales Analysis

* What is the total revenue?
* What are the monthly sales trends?
* Which periods generate the highest sales?
* How many orders are placed over time?

---

## 🛠️ Technologies Used

* **SQL Server**
* **T-SQL**
* **SQL Server Management Studio (SSMS)**
* **Git**
* **GitHub**
* **ETL**
* **Data Warehousing**
* **Dimensional Modeling**
* **Star Schema**
* **Medallion Architecture**

---

## 📁 Project Structure

```text
sql-server-data-warehouse/
│
├── datasets/
│   ├── crm/
│   └── erp/
│
├── docs/
│   ├── architecture/
│   ├── data_model/
│   └── documentation/
│
├── scripts/
│   ├── bronze/
│   ├── silver/
│   └── gold/
│
├── analytics/
│   ├── customer_analysis.sql
│   ├── product_analysis.sql
│   └── sales_analysis.sql
│
├── tests/
│   └── data_quality_tests.sql
│
├── README.md
└── .gitignore
```

---

## 🚀 ETL Workflow

The complete ETL process follows these steps:

### 1. Extract

Raw data is collected from CRM and ERP source files.

### 2. Load

The raw data is loaded into the Bronze layer.

### 3. Transform

The Silver layer performs cleaning, standardization, validation, and transformation.

### 4. Model

Cleaned data is transformed into fact and dimension tables in the Gold layer.

### 5. Analyze

SQL queries and views are used to generate business insights from the Gold layer.

---

## 🎯 Project Objectives

The main objectives of this project are to:

* Understand the architecture of modern data warehouses.
* Practice SQL Server and advanced T-SQL.
* Build ETL pipelines using SQL.
* Work with real-world data quality issues.
* Apply dimensional modeling concepts.
* Design a star schema.
* Create analytical SQL queries.
* Develop a structured and maintainable data warehouse.

---

## 📈 Skills Demonstrated

This project demonstrates practical experience with:

* SQL development
* Advanced T-SQL
* Data cleaning
* Data transformation
* ETL pipeline development
* Data quality validation
* Dimensional modeling
* Fact and dimension tables
* Star-schema design
* Analytical SQL
* Database design
* Git and GitHub

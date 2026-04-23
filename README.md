# 🏠 End-to-End Data Engineering Project using AWS, Snowflake & dbt

## 📌 Overview

This project demonstrates a complete **end-to-end data engineering pipeline** built using modern cloud and data transformation tools. It covers data ingestion, transformation, modeling, and analytics using a structured approach (Medallion Architecture). The goal is to transform raw CSV data into clean, reliable, and analytics-ready datasets.

---

## 🏗️ Architecture

### 🔄 Data Flow

```
Source Data (CSV) → AWS S3 → Snowflake (Staging) → Bronze Layer → Silver Layer → Gold Layer
                                                        ↓              ↓             ↓
                                                    Raw Tables     Cleaned Data    Analytics
```

### 🧱 Layers Explained

* **Bronze Layer** → Raw ingested data (minimal transformation)
* **Silver Layer** → Cleaned, standardized data
* **Gold Layer** → Business-ready data for analytics

---

## 🛠️ Technology Stack

* **Cloud Storage**: AWS S3
* **Data Warehouse**: Snowflake
* **Transformation Tool**: dbt (Data Build Tool)
* **Programming**: Python
* **Version Control**: Git & GitHub

---

## 📊 Data Model

### 🟡 Medallion Architecture

🥉 Bronze Layer (Raw Data)

Raw data ingested from staging with minimal transformations:

* Edit **bronze_bookings** - Raw booking transactions
* Edit **bronze_hosts** - Raw host information
* Edit **bronze_listings** - Raw property listings
  
🥈 Silver Layer (Cleaned Data)

Cleaned and standardized data:

* **silver_bookings** - Validated booking records
* **silver_hosts** - Enhanced host profiles with quality metrics
* **silver_listings** - Standardized listing information with price categorization
  
🥇 Gold Layer (Analytics-Ready)

Business-ready datasets optimized for analytics:

* **obt** (One Big Table) - Denormalized fact table joining bookings, listings, and hosts
* **fact** - Fact table for dimensional modeling
* Ephemeral models for intermediate transformations

### 🔁 Snapshots (SCD Type 2)

Slowly Changing Dimensions to track historical changes:

* **dim_bookings** - Historical booking changes
* **dim_hosts** - Historical host profile changes
* **dim_listings** - Historical listing changes

---

## 📂 Project Structure

```
AWS_DBT_Snowflake/
├── README.md
├── pyproject.toml
├── main.py
│
├── SourceData/
│   ├── bookings.csv
│   ├── hosts.csv
│   └── listings.csv
│
├── DDL/
│   ├── ddl.sql
│   └── resources.sql
│
└── aws_dbt_snowflake_project/
    ├── dbt_project.yml
    ├── ExampleProfiles.yml
    │
    ├── models/
    │   ├── sources/
    │   ├── bronze/
    │   ├── silver/
    │   └── gold/
    │       └── ephemeral/
    │
    ├── macros/
    ├── analyses/
    ├── snapshots/
    ├── tests/
    └── seeds/
```

---

## 🚀 Getting Started

### 📋 Prerequisites

* Python (3.8+)
* AWS Account (S3 setup)
* Snowflake Account
* dbt installed

---

### ⚙️ Installation

#### 1. Clone the Repository

```
git clone <your-repo-url>
cd AWS_DBT_Snowflake
```

#### 2. Create Virtual Environment

```
python -m venv venv
venv\Scripts\activate
```

#### 3. Install Dependencies

```
pip install -r requirements.txt
```

#### Core Dependencies:

* dbt-core
* dbt-snowflake
* snowflake-connector-python
* boto3

---

### 🔌 Configure Snowflake Connection

Edit `profiles.yml`:

```
aws_dbt_snowflake_project:
  outputs:
    dev:
      type: snowflake
      account: "your_account"
      user: "your_user"
      password: "your_password"
      role: "ACCOUNTADMIN"
      database: "AIRBNB"
      warehouse: "COMPUTE_WH"
      schema: "DBT_SCHEMA"
  target: dev
```

---

### 🏗️ Set Up Snowflake Database

* Run `DDL/ddl.sql`
* Create required tables and schema

---

### 📥 Load Source Data

* Upload CSV files to AWS S3
* Load into Snowflake staging tables

---

## ▶️ Usage

### 🔹 Run dbt Project

```
cd aws_dbt_snowflake_project
dbt run
```

### 🔹 Run Full Pipeline

```
dbt build
```

### 🔹 Run Snapshots

```
dbt snapshot
```

### 🔹 Run Specific Layer

```
dbt run --select bronze
dbt run --select silver
dbt run --select gold
```

---

## ⭐ Key Features

* ✅ Incremental Loading (efficient processing)
* ✅ Custom Macros for reusable logic
* ✅ Dynamic SQL Generation using dbt
* ✅ Slowly Changing Dimensions (SCD Type 2)
* ✅ Clean schema organization (Bronze → Silver → Gold)

---

## 🧪 Data Quality

* Source tests implemented
* Validation checks for:

  * Null values
  * Data consistency
* dbt testing framework used

---

## 🛠️ Troubleshooting

| Issue                | Solution                   |
| -------------------- | -------------------------- |
| dbt connection error | Check `profiles.yml`       |
| SQL syntax errors    | Validate Jinja + SQL       |
| Snapshot errors      | Verify config & unique_key |
| Git push blocked     | Remove secrets from repo   |

---

## 🔮 Future Enhancements

* Add orchestration using Airflow
* Implement CI/CD pipeline
* Add real-time data ingestion
* Build dashboards (Power BI / Tableau)
* Improve test coverage

---

## 📌 Conclusion

This project showcases a **real-world data engineering workflow**, demonstrating strong skills in:

* Cloud data pipelines
* Data modeling
* dbt transformations
* Data warehousing (Snowflake)

---

💡 *Designed to demonstrate industry-level data engineering practices in a simple and scalable way.*

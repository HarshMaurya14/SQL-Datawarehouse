<div align="center">

<!-- Banner -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,50:16213e,100:0f3460&height=200&section=header&text=SQL%20Data%20Warehouse&fontSize=48&fontColor=e94560&fontAlignY=38&desc=End-to-End%20Modern%20Data%20Warehouse%20%7C%20Medallion%20Architecture%20%7C%20T-SQL&descAlignY=58&descColor=a8b2d8" width="100%"/>

<!-- Badges -->
<p>
  <img src="https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white"/>
  <img src="https://img.shields.io/badge/T--SQL-005C84?style=for-the-badge&logo=databricks&logoColor=white"/>
  <img src="https://img.shields.io/badge/Architecture-Medallion-gold?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge"/>
</p>

<br/>

> **A production-grade, end-to-end Data Warehouse** built with SQL Server — featuring Bronze → Silver → Gold Medallion Architecture, ETL pipelines, dimensional data modeling (star schema), and business-ready analytical reporting.

</div>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Architecture](#️-architecture)
- [Tech Stack](#️-tech-stack)
- [Project Structure](#-project-structure)
- [Data Flow](#-data-flow)
- [Layers in Detail](#-layers-in-detail)
- [Data Modeling](#️-data-modeling)
- [Analytics & Reporting](#-analytics--reporting)
- [Getting Started](#-getting-started)
- [License](#-license)

---

## 🌐 Overview

This project implements a **complete Modern Data Warehouse** using SQL Server and the **Medallion Architecture** pattern. It ingests raw ERP and CRM data, transforms it through layered pipelines, and delivers analytics-ready dimensional models for business intelligence and reporting.

### 🎯 What this project covers:

| Domain | What's Built |
|---|---|
| 🏗️ **Data Architecture** | Medallion Architecture (Bronze → Silver → Gold) |
| 🔄 **ETL Pipelines** | T-SQL stored procedures for each layer |
| 🗃️ **Data Modeling** | Star Schema with fact & dimension tables |
| 🧹 **Data Quality** | Cleansing, deduplication, standardization |
| 📊 **Reporting** | Business-ready SQL analytical queries |
| 🧪 **Testing** | Data quality validation scripts |

---

## 🏛️ Architecture

The warehouse is built on the **Medallion Architecture** — an industry-standard approach that structures data into three progressive quality layers:

```
┌─────────────────────────────────────────────────────────────────┐
│                       DATA SOURCES                              │
│              📂 ERP Data          📂 CRM Data                   │
│              (CSV Files)          (CSV Files)                   │
└─────────────────────────┬───────────────────────────────────────┘
                          │  INGEST
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│  🥉 BRONZE LAYER  ─  Raw Ingestion Zone                         │
│  ► Full-load (Truncate & Insert)  ► No transformations          │
│  ► Preserves source data as-is    ► Audit trail & traceability  │
└─────────────────────────┬───────────────────────────────────────┘
                          │  CLEANSE
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│  🥈 SILVER LAYER  ─  Cleansed & Standardized Zone              │
│  ► Deduplication & null handling  ► Data type normalization     │
│  ► Standardization & enrichment   ► Derived columns added       │
└─────────────────────────┬───────────────────────────────────────┘
                          │  MODEL
                          ▼
┌─────────────────────────────────────────────────────────────────┐
│  🥇 GOLD LAYER  ─  Business-Ready Analytics Zone               │
│  ► Star Schema (Facts + Dimensions)  ► Optimized for BI tools  │
│  ► KPI-ready views & reports         ► Final reporting layer    │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

<div align="center">

| Tool | Purpose |
|---|---|
| **Microsoft SQL Server** | Core database engine |
| **T-SQL** | ETL scripting, stored procedures, views |
| **SSMS** | SQL Server Management Studio — development environment |
| **Draw.io** | Architecture and data flow diagrams |
| **CSV Files** | Source data from ERP & CRM systems |

</div>

---

## 📁 Project Structure

```
SQL-Datawarehouse/
│
├── 📂 datasets/               # Raw source data (ERP & CRM CSV files)
│   ├── crm/                   # CRM source files
│   └── erp/                   # ERP source files
│
├── 📂 docs/                   # Project documentation & diagrams
│   ├── data_architecture.png  # Architecture overview diagram
│   ├── data_flow.png          # ETL data flow diagram
│   ├── data_models.png        # Star schema data model
│   ├── data_catalog.md        # Field descriptions & metadata
│   └── naming-conventions.md  # Naming guidelines
│
├── 📂 scripts/                # All T-SQL ETL scripts
│   ├── bronze/                # Raw data ingestion scripts
│   │   ├── ddl_bronze.sql     # Table creation for Bronze layer
│   │   └── proc_load_bronze.sql  # Stored procedure — Bronze load
│   ├── silver/                # Cleansing & transformation scripts
│   │   ├── ddl_silver.sql     # Table creation for Silver layer
│   │   └── proc_load_silver.sql  # Stored procedure — Silver load
│   └── gold/                  # Analytical model scripts
│       ├── ddl_gold.sql       # Fact & Dimension table creation
│       └── proc_load_gold.sql # Stored procedure — Gold load
│
├── 📂 test/                   # Data quality validation scripts
│   ├── quality_checks_silver.sql
│   └── quality_checks_gold.sql
│
├── 📄 README.md
└── 📄 LICENSE
```

---

## 🔄 Data Flow

```
CSV Source Files
      │
      ▼
┌─────────────┐    proc_load_bronze.sql
│   BRONZE    │◄──────────────────────── Full Load (Truncate & Insert)
│  (Raw Data) │
└──────┬──────┘
       │
       ▼
┌─────────────┐    proc_load_silver.sql
│   SILVER    │◄──────────────────────── Cleanse → Standardize → Enrich
│ (Clean Data)│
└──────┬──────┘
       │
       ▼
┌─────────────┐    proc_load_gold.sql
│    GOLD     │◄──────────────────────── Model → Fact & Dimension Tables
│ (BI Ready)  │
└─────────────┘
       │
       ▼
  📊 Analytics & Reporting
```

---

## 🔍 Layers in Detail

### 🥉 Bronze Layer — Raw Ingestion

- Ingests CSV files **as-is** into SQL Server staging tables
- **No transformations** — data is preserved in its original form
- Enables **full traceability** back to the source
- Load strategy: **Full Load** (Truncate → Insert on each run)
- Audience: Data Engineers

### 🥈 Silver Layer — Cleanse & Standardize

Transformations applied include:

- ✅ **Deduplication** using `ROW_NUMBER()` window functions
- ✅ **Null handling** — replacing invalid or missing values
- ✅ **Whitespace cleanup** using `TRIM()`
- ✅ **Data type casting** — e.g., integer dates → `DATE` format
- ✅ **Standardization** — consistent gender codes, status values, etc.
- ✅ **Derived columns** — e.g., age, full name, category ID
- ✅ **Metadata columns** — `dw_create_date` added to all tables
- ✅ **Error handling** — `BEGIN TRY...END CATCH` in all procedures

### 🥇 Gold Layer — Business-Ready Models

- Implements a **Star Schema** for analytical workloads
- Contains **Fact Tables** and **Dimension Tables**
- Exposes clean **views** optimized for BI tools
- Applies business rules and final aggregation logic
- Audience: Data Analysts, BI Developers, Data Scientists

---

## 🗂️ Data Modeling

The Gold Layer is modeled as a **Star Schema**:

```
                     ┌─────────────────┐
                     │   dim_customer  │
                     │─────────────────│
                     │ customer_key    │
                     │ customer_name   │
                     │ country         │
                     │ gender          │
                     └────────┬────────┘
                              │
┌──────────────┐     ┌────────▼────────┐     ┌──────────────┐
│  dim_product │     │   fact_sales    │     │   dim_date   │
│──────────────│     │─────────────────│     │──────────────│
│ product_key  ├────►│ order_number    │◄────┤ date_key     │
│ product_name │     │ customer_key    │     │ year         │
│ category     │     │ product_key     │     │ quarter      │
│ cost         │     │ date_key        │     │ month        │
└──────────────┘     │ sales_amount    │     └──────────────┘
                     │ quantity        │
                     │ profit          │
                     └─────────────────┘
```

---

## 📊 Analytics & Reporting

The Gold Layer enables a wide range of business queries:

```sql
-- 📈 Revenue by Product Category
SELECT p.category, SUM(f.sales_amount) AS total_revenue
FROM fact_sales f
JOIN dim_product p ON f.product_key = p.product_key
GROUP BY p.category
ORDER BY total_revenue DESC;

-- 👥 Customer Segmentation by Region
SELECT c.country, COUNT(DISTINCT f.customer_key) AS customers,
       SUM(f.sales_amount) AS revenue
FROM fact_sales f
JOIN dim_customer c ON f.customer_key = c.customer_key
GROUP BY c.country;

-- 📅 Sales Trend Over Time
SELECT d.year, d.month, SUM(f.sales_amount) AS monthly_sales
FROM fact_sales f
JOIN dim_date d ON f.date_key = d.date_key
GROUP BY d.year, d.month
ORDER BY d.year, d.month;
```

---

## 🚀 Getting Started

### Prerequisites

- Microsoft SQL Server 2016 or later
- SQL Server Management Studio (SSMS)

### Setup Steps

```sql
-- Step 1: Create the Database
CREATE DATABASE DataWarehouse;
USE DataWarehouse;

-- Step 2: Create schemas for each layer
CREATE SCHEMA bronze;
CREATE SCHEMA silver;
CREATE SCHEMA gold;
```

### Running the ETL Pipeline

```bash
# Execute scripts in the following order:
```

| Step | Script | Description |
|------|--------|-------------|
| 1️⃣ | `scripts/bronze/ddl_bronze.sql` | Create Bronze layer tables |
| 2️⃣ | `scripts/bronze/proc_load_bronze.sql` | Load raw CSV data into Bronze |
| 3️⃣ | `scripts/silver/ddl_silver.sql` | Create Silver layer tables |
| 4️⃣ | `scripts/silver/proc_load_silver.sql` | Cleanse & transform to Silver |
| 5️⃣ | `scripts/gold/ddl_gold.sql` | Create Fact & Dimension tables |
| 6️⃣ | `scripts/gold/proc_load_gold.sql` | Build Gold analytical models |

```sql
-- Then execute each stored procedure:
EXEC bronze.load_bronze;
EXEC silver.load_silver;
EXEC gold.load_gold;
```

### Running Data Quality Checks

```sql
-- Validate Silver layer
:r test/quality_checks_silver.sql

-- Validate Gold layer
:r test/quality_checks_gold.sql
```

---

## 🎓 Skills Demonstrated

This project showcases expertise in:

- ✅ **Data Engineering** — ETL pipeline design and implementation
- ✅ **Data Architecture** — Medallion / Lakehouse architecture patterns
- ✅ **Advanced T-SQL** — CTEs, window functions, stored procedures
- ✅ **Data Modeling** — Dimensional modeling, star schema design
- ✅ **Data Quality** — Profiling, validation, and cleansing
- ✅ **Business Intelligence** — Analytical SQL for KPIs and reporting

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**⭐ Star this repo if you found it useful!**

Made with ❤️ by [Harsh Maurya](https://github.com/HarshMaurya14)

## 🙏 Credits
Inspired by [DataWithBaraa](https://github.com/DataWithBaraa).

All implementation done independently by me.

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,50:16213e,100:0f3460&height=100&section=footer" width="100%"/>

</div>

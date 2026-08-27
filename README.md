# 🛒 E-Commerce End-to-End Data Pipeline & Analytics
> **Data Engineering Project** | Built with Databricks, PySpark, Delta Lake & Medallion Architecture

---

## 💼 Business Impact: How We Value-Add to the Enterprise

The company operates an e-commerce platform that streams transactional sales and user activity data in real time via an API. Previously, data was fragmented, unformatted, and prone to inconsistencies—preventing operational teams and executive stakeholders from extracting timely insights.

**Engineering Solutions & Value Delivered:**
* **Centralized Data Lakehouse:** Ingested and unified transactions, product logs, and customer profiles into a single source of truth using Delta Lake.
* **Data Quality & Lineage:** Implemented strict schema enforcement, deduplication logic, and data type casting to eliminate corrupt downstream metrics.
* **Analytics-Ready Modeling:** Modeled cleaned data into a Kimball Star Schema to answer key business KPIs:
  * Top-performing products and profit margins per category.
  * Customer segmentation, acquisition, and Customer Lifetime Value (CLV).
  * Time-series trends (daily/monthly revenue seasonality).
* **Automation & Idempotency:** Designed fault-tolerant workflows that can be safely re-executed without duplicating records or corrupting reporting layers.

---

## 🏗️ Data Pipeline Architecture (Medallion Pattern)

The project leverages the **Medallion Architecture** pattern on Databricks to govern data progression through distinct layers:


[ E-Commerce API / Data Sources ]

      │ 00_setup_SRC      │  ──> Environment Setup, Schemas & Unity Catalog Governance
      └───────────────────┘
                │
                ▼
      ┌───────────────────┐
      │ 01_Bronze Layer   │  ──> Raw Ingestion: Raw API payloads preserved in append-only Delta format
      └───────────────────┘
                │
                ▼
      ┌───────────────────┐
      │ 02_Silver Layer   │  ──> Clean & Enriched: Deduplication, Type Casting, Hashing & Null Checks
      └───────────────────┘
                │
                ▼
      ┌───────────────────┐
      │ 03_Gold Layer     │  ──> Business Layer: Kimball Dimensional Modeling (Fact & Dimension Tables)
      └───────────────────┘
                │
                ▼
      [ Databricks Dashboards / BI Analytics ]

🛠️ Stack & Core Competencies

Platform & Compute: Databricks Lakehouse Environment

Data Processing: PySpark & Spark SQL

Storage & Format: Delta Lake (ACID Transactions, Time Travel, Idempotent Processing)

Data Governance: Unity Catalog

Data Modeling: Kimball Methodology (Star Schema, Fact Tables, Dimension Tables, SCD Type 2)

Version Control: Git & GitHub

📂 Repository Structure
Plaintext

00_setup_SRC/01_config_and_schemas.sql       # Catalog creation, schema definitions, and environment variables

01_bronze/01_ingest_raw_sales.sql          # Raw ingestion pipelines preserving source data integrity

02_silver/
01_transform_silver.py           # Cleaning, schema normalization, deduplication, and surrogate key hashing (MD5)

03_gold/
01_dim_customers.sql             # Customer dimension (SCD Type 2 implementation)
02_dim_products.sql              # Product dimension
03_fact_sales.sql                # Transactional fact table with business metrics

04_utils/
helper_functions.py              # Reusable utility functions and parameter handlers

README.md                            # Main project documentation

⚙️ Key Technical Highlights
Guaranteed Idempotency: Leveraged Delta MERGE (UPSERT) operations to prevent duplicate records during job retries.

Performance Optimization: Applied OPTIMIZE and Z-ORDER clustering techniques in Delta Lake to minimize data scanning and accelerate SQL analytical queries.

Data Integrity: Used MD5 deterministic surrogate hashing to build unique identifiers across dimensional entities.

👤 Author
Martín Flores — Data Engineer

Email: martinnfloress53@gmail.com

LinkedIn: www.linkedin.com/in/victor-martin-flores-8866522b2



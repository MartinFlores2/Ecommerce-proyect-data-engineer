# 🛒 E-Commerce End-to-End Data Pipeline & Analytics

Data Engineering Project | Built with Databricks, Spark SQL, Delta Lake & Medallion Architecture

---

## 💼 Business Impact: How We Value-Add to the Enterprise

The company operates an e-commerce platform that streams transactional sales and user activity data. Previously, data was fragmented, stored entirely as unformatted text (`STRING`), and prone to schema inconsistencies—preventing operational teams and executive stakeholders from extracting timely insights.

### Engineering Solutions & Value Delivered:
* **Centralized Data Lakehouse:** Ingested and unified transactions, product logs, and customer profiles into a single source of truth using Delta Lake.
* **Production-Grade Data Governance & Quality:** Implemented strict schema enforcement, automated database-level `CHECK` constraints (fail-fast architecture), and explicit type casting (`DECIMAL`, `INT`, `DATE`) to eliminate corrupt downstream metrics.
* **Analytics-Ready Kimball Modeling:** Modeled cleaned data into a modular Star Schema (`fact_sales`, `dim_customers`, `dim_products`, `dim_date`) optimized for BI analytics.
* **Idempotent & Modular Automation:** Designed fault-tolerant workflows using incremental `MERGE INTO` patterns and separated DDL/ETL scripts by layer to prevent record duplication and guarantee maintainability.

---

## 📊 Analytical Dashboard & Business Intelligence

The Gold layer and business views (`ecommerce_views`) power an interactive executive dashboard designed to monitor sales performance and drive data-driven decisions:

### **Key Performance Indicators (KPIs):**
* **Total Revenue & Growth:** Real-time tracking of financial performance across product categories and regions.
* **Top-Performing Categories:** Identification of highest-grossing product lines (e.g., Electronics, Home, Apparel).
* **Regional & Customer Insights:** Breakdown of purchasing behaviors and customer ratings by geographical region.

### **Core Visualizations:**
* **Monthly Sales Trends:** Time-series analysis tracking seasonal revenue patterns and sales velocity.
* **Category Performance Breakdown:** Comparative view of sales volume, discounts, and margins per product category.
* **Regional Distribution Map:** Executive breakdown of revenue contribution and customer acquisition metrics segmented by region.

---

## 🏗️ Data Pipeline Architecture (Medallion Pattern)

The project leverages the Medallion Architecture pattern on Databricks to govern data progression through distinct modular layers:

* **01_Bronze Layer (`ecommerce_bronze`)**: Raw Ingestion preserving transactional payloads in an append-only Delta format via idempotent `COPY INTO`.
* **02_Silver Layer (`ecommerce_silver`)**: Cleaned & Enriched data featuring permanent data casting, string trimming, MD5 hashing, and inline data quality validations.
* **03_Gold Layer (`ecommerce_gold`)**: Business Layer featuring a modularized Star Schema (`ddl/` and `etl/` subfolders for dimensions and facts) protected by automated table constraints.
* **04_Views Layer (`ecommerce_views`)**: Analytics Serving providing business views for rapid SQL / BI consumption (Sales by Category, Region, and Monthly Trends).

---

## 📂 Repository Structure

ecommerce-project-data-engineer/
├── 00_setup_SRC/
│   └── ecommerce_sales_analytics_5000.csv    # Source raw transactional dataset
├── 01_DDL/
│   └── 01_config_and_schemas.sql           # Catalog creation, schema definitions, and setup
├── 01_EDA/
│   ├── 01_eda_bronze_quality_checks.sql      # Profiling and initial checks on raw data
│   ├── 02_eda_silver_quality_checks.sql      # Data quality, type casting, and null checks
│   └── 03_eda_gold_quality_checks.sql        # Volumetric and revenue reconciliation checks
├── ETL/
│   ├── 01_bronze/
│   │   └── 01_ingest_raw_sales.sql           # Idempotent raw ingestion (COPY INTO)
│   ├── 02_silver/
│   │   └── 02_ecommerce_transform_silver.sql # Cleaning, explicit casting, and transformations
│   └── 03_gold/
│       ├── ddl/
│       │   ├── ddl_dim_customers.sql         # Customer dimension DDL with constraints
│       │   ├── ddl_dim_products.sql          # Product dimension DDL with constraints
│       │   └── ddl_fact_sales.sql            # Fact sales DDL with foreign key constraints
│       └── etl/
│           ├── etl_dim_customers.sql         # Incremental MERGE for customer dimension
│           ├── etl_dim_products.sql          # Incremental MERGE for product dimension
│           └── etl_fact_sales.sql            # Incremental MERGE for fact sales
├── VIEWS/
│   └── 01_create_business_views.sql          # Business views for BI reporting & analytics
└── README.md

🧪 Data Quality & Governance Framework
To guarantee enterprise-grade data integrity before serving business metrics, the pipeline executes automated quality validations:

Volumetric & Revenue Reconciliation: Confirmed 100% data preservation between Silver (cleansed_sales) and Gold (fact_sales) with 0 record loss (5,000/5,000 records) and exact revenue match ($5,109,775.74).

Fail-Fast Database Constraints: Enforced CHECK constraints directly on Delta tables to halt pipelines immediately upon data quality violations.

Referential & Uniqueness Integrity: Verified primary key uniqueness and eliminated orphan facts across dimensional entities.

🛠️ Stack & Core Competencies
Platform & Compute: Databricks Lakehouse Environment

Data Processing: Spark SQL & PySpark

Storage & Format: Delta Lake (ACID Transactions, Time Travel, Idempotent Processing)

Data Governance: Unity Catalog / Schema Separation (ecommerce_bronze, ecommerce_silver, ecommerce_gold, ecommerce_views)

Data Modeling: Kimball Methodology (Star Schema)

Version Control: Git & GitHub

👤 Author
Martín Flores — Data Engineer

📧 Email: martinnfloress53@gmail.com

🔗 LinkedIn: linkedin.com/in/victor-martin-flores-8866522b2

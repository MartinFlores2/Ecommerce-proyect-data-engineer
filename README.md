# 🛒 E-Commerce End-to-End Data Pipeline & Analytics

**Data Engineering Project** | Built with Databricks, Spark SQL, Delta Lake & Medallion Architecture

---

## 💼 Business Impact: How We Value-Add to the Enterprise

The company operates an e-commerce platform that streams transactional sales and user activity data. Previously, data was fragmented, stored entirely as unformatted text (`STRING`), and prone to schema inconsistencies—preventing operational teams and executive stakeholders from extracting timely insights.

### **Engineering Solutions & Value Delivered:**
* **Centralized Data Lakehouse:** Ingested and unified transactions, product logs, and customer profiles into a single source of truth using Delta Lake.
* **Data Quality & Lineage:** Implemented strict schema enforcement, deduplication logic, and explicit type casting (`DECIMAL`, `INT`, `DATE`) to eliminate corrupt downstream metrics.
* **Analytics-Ready Modeling:** Modeled cleaned data into a Kimball Star Schema to answer key business KPIs:
  * Top-performing products and revenue metrics per category.
  * Customer purchase tracking and regional behavior.
  * Time-series trends and sales seasonality.
* **Automation & Idempotency:** Designed fault-tolerant workflows (`CREATE OR REPLACE TABLE ... USING DELTA`) that can be safely re-executed without duplicating records or corrupting reporting layers.

---

## 🏗️ Data Pipeline Architecture (Medallion Pattern)

The project leverages the Medallion Architecture pattern on Databricks to govern data progression through distinct layers:

```text
[ E-Commerce Raw CSV / Data Sources ]
                │
                ▼
  ┌──────────────────────────┐
  │ 01_Bronze Layer          │  ──> Raw Ingestion: Raw transactional payloads preserved 
  │ (ecommerce_bronze)       │      in append-only Delta format (String-typed).
  └──────────────────────────┘
                │
                ▼
  ┌──────────────────────────┐
  │ 02_Silver Layer          │  ──> Clean & Enriched: Permanent Data Casting (INT, DATE, DECIMAL),
  │ (ecommerce_silver)       │      String Trimming, Hashing (MD5) & Data Quality Checks.
  └──────────────────────────┘
                │
                ▼
  ┌──────────────────────────┐
  │ 03_Gold Layer            │  ──> Business Layer: Kimball Dimensional Modeling (Fact & 
  │ (ecommerce_gold)         │      Dimension Tables) optimized for Power BI / BI Analytics.
  └──────────────────────────┘
                │
                ▼
  [ Databricks Dashboards / BI Analytics ]

🧪 Data Quality & Governance Framework

To guarantee enterprise-grade data integrity before serving business metrics, the pipeline executes automated quality validation checks in the Gold Layer:

Volumetric & Revenue Reconciliation: Confirmed 100% data preservation between Silver (cleansed_sales) and Gold (fact_sales) with 0 record loss (5,000/5,000 records) and exact revenue match ($5,109,775.74).

Primary Key Uniqueness: Verified 0 duplicate surrogate keys across all dimension tables (dim_customers, dim_products, dim_date).

Referential Integrity: Enforced foreign key checks via LEFT JOIN validations to ensure 0 orphan facts exist in fact_sales.

Null Key Checks: Verified 0 NULL values across dimensional foreign keys.

🛠️ Stack & Core Competencies
Platform & Compute: Databricks Lakehouse Environment

Data Processing: Spark SQL & PySpark

Storage & Format: Delta Lake (ACID Transactions, Time Travel, Idempotent Processing)

Data Governance: Unity Catalog / Schema Separation (ecommerce_bronze, ecommerce_silver, ecommerce_gold)

Data Modeling: Kimball Methodology (Star Schema, fact_sales, dim_customers, dim_products, dim_date)

Version Control: Git & GitHub

📂 Repository Structure
Plaintext
├── 00_setup_SRC/
│   └── 01_config_and_schemas.sql       # Catalog creation, schema definitions, and setup
├── 01_bronze/
│   └── 01_ingest_raw_sales.sql         # Raw ingestion preserving source data integrity
├── 02_silver/
│   └── 01_transform_silver.sql         # Cleaning, explicit casting, trimming, and surrogate hashing (MD5)
├── 03_gold/
│   ├── 01_build_gold_layer.sql         # Star Schema creation (dim_customers, dim_products, dim_date, fact_sales)
│   └── 02_gold_quality_checks.sql      # Automated Data Quality validation scripts
└── README.md                           # Main project documentation

⚙️ Key Technical Highlights
Guaranteed Idempotency: Leveraged Delta Lake table overwrites and transactional guarantees to ensure pipeline reruns produce consistent states without duplication.

Precision Financial Casting: Enforced DECIMAL(10,2) casting across all financial metrics (unit_price, revenue) to eliminate floating-point arithmetic errors.

Data Integrity: Used MD5 deterministic surrogate hashing to build unique identifiers across dimensional entities.

Dynamic Time Dimension: Automated the generation of dim_date spanning the full date range of transactions, enriched with calendar attributes (year, month_name, quarter, day_of_week).

👤 Author
Martín Flores — Data Engineer

📧 Email: martinnfloress53@gmail.com

🔗 LinkedIn: linkedin.com/in/victor-martin-flores-8866522b2


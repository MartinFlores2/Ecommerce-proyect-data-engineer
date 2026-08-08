E-Commerce Sales & Logistics Analytics Data Pipeline
This repository contains an end-to-end Data Engineering pipeline. The project transforms raw retail transactional records into a structured, analytical **Star Schema** following the **Medallion Architecture (Bronze, Silver and Gold)

The pipeline processes multi-channel e-commerce records tracking customer demographics, financial sales performance, discount percentages, and supply chain logistics latency.

Dataset & Business Context
The source dataset (`ecommerce_sales_analytics_5000.csv`) simulates 5,000 retail transactions covering the full lifecycle of online marketplace orders:
- Demographics: Customer age, gender, and geographical location.
- Financial Metrics: Unit prices, order quantities, discount percentages, and net revenues.
- Logistics & Supply Chain:Order dates, shipping timestamps, and fulfillment delay distributions (1-to-7 day fulfillment lag).

Medallion Architecture

Raw CSV Source File (Volume / DBFS)

BRONZE SCHEMA                 
Table: raw_sales_analytics                 
- Preserves 100% source fidelity           
- Ingests raw types & metadata attributes   

Cleansed, Standardized & Split via CTEs & Window Functions

SILVER SCHEMA                  
Dimensions & Fact Tables (Star Schema):  
- dim_customers (Demographics & Location)  
- dim_products  (Catalog & Categories)      
- fact_sales    (Transactions & Logistics)  


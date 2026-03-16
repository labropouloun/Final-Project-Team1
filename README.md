Multi Sales: End-to-End Bike Retail Data Pipeline

Historically, Multi Sales struggled with fragmented data sources and inconsistent naming conventions, making accurate sales forecasting and inventory management a challenge. This project implements a robust Medallion Architecture to transform raw, messy data into high-integrity, "Gold-ready" schemas, optimized for direct ingestion into Microsoft Fabric and Power BI.

🛠 Architecture Overview
The pipeline follows the industry-standard Medallion Architecture to ensure data quality at every stage with the use of Databricks.

Bronze (Raw): Ingestion of raw  CSVs. No transformations—just a faithful record of the source.

Silver (Cleansed): Data is standardized. We handled the "inconsistencies" by deduplicating records, casting types (e.g., ensuring currency is numeric), and unifying bike category naming etc.

Gold (Curated): Business-level aggregates. Data is modeled into a Galaxy Schema (Fact and Dimension tables) ready for analytics.

🏗 Data Modeling (gold_schema)

The gold layer is designed as a Galaxy Schema to enable high-performance queries and clear reporting.

📊 Fact Tables

fact_sales: Granular transaction data for bikes and accessories (quantity, revenue, cost).

fact_targets: High-level sales targets defined by region and salesperson to track KPIs.

🧩 Dimension Tables

dim_product: Product metadata including category (Bike vs. Accessory), color, and model.

dim_reseller: Details on B2B partners and external bike shops.

dim_sales_person: Employee details for the Multi Sales team.

dim_region: Geographic hierarchy (country, state, city).

dim_sales_person_region

🏗 Fabric & Power BI Ingestion

This stage transitions the data from refined Parquet files into actionable business intelligence using Microsoft Fabric.

Lakehouse Ingestion (Delta/Parquet)
The gold_layer tables are saved as Delta Tables (backed by Parquet) within the Fabric Lakehouse.

This ensures ACID compliance and performance optimization.

After that they are transfered to powerBI for extensive data analysis, exploring trends, losses, best selling products etc. 

# Olist E-commerce Data Analysis (Python + SQL Server)

## Project Overview

This project focuses on a comprehensive **Data Analysis, Cleaning, and Modeling** of a real-world Brazilian E-commerce public dataset from **Olist**. The primary goal was to transform inconsistent, multi-source raw data into a clean, unified **Star Schema** data model to enable crucial business analytics, such as **Market Basket Analysis (MBA)** and **Geographic Sales Pattern Analysis**.

The entire workflow, from data extraction via **SQL Server** and cleaning with **Pandas/PyODBC** to the final **Data Modeling**, simulates a typical **enterprise-level Data Science project**, prioritizing data integrity and efficient reporting.

***

## Key Outcomes & Business Objectives

This project aimed to solve real-world data issues to drive better business decisions for Olist:

1.  **Data Unification & Standardization:** Merged 8 separate raw tables into a single, clean source of truth, standardizing language (Portuguese to English) and validating chronological order data.
2.  **Market Basket Analysis (MBA) Readiness:** Created a dataset suitable for discovering **cross-selling opportunities** (items frequently bought together) to improve the website's recommendation engine.
3.  **Geographic Sales Pattern Analysis:** Standardized all city names using `unidecode` and `str.title()` to enable accurate city-wise sales and demand analysis.
4.  **Enterprise Data Modeling:** Designed and structured the data into a **Star Schema** for optimal performance in BI tools (like Power BI), ensuring fast and reliable reporting.

***

## Technical Stack & Libraries

| Category | Tools/Technologies | Purpose |
| :--- | :--- | :--- |
| **Data Extraction** | **SQL Server, pyodbc** | Securely connecting to the RDBMS and pulling large datasets (mimicking enterprise environment). |
| **Data Processing** | **Python (Pandas, NumPy)** | Advanced data cleaning, merging, aggregation, and time validation. |
| **Text Cleaning** | **`unidecode`, RegEx** | Robustly handling non-ASCII characters (Portuguese accents) and encoding errors. |
| **Modeling** | **Star Schema** | Designing an efficient, fast structure for BI reporting and OLAP. |
| **Analysis** | **Market Basket Analysis (MBA)** | Discovering high-Lift association rules for product cross-selling. |

***

## Data Cleaning & Transformation Workflow

The raw data had significant issues (Dirty Data) that required robust cleaning:

| Data Issue | Cleaning Step Taken | Technical Rationale |
| :--- | :--- | :--- |
| **Inconsistent City Names** | Applied `unidecode` followed by `str.title()` on geographic columns. | `unidecode` handles accents (e.g., São Paulo $\rightarrow$ Sao Paulo); `str.title()` ensures case uniformity (e.g., sao paulo $\rightarrow$ Sao Paulo). |
| **Multi-Row Payments** | Used `groupby('order_id').sum()` on `payment_value` after cleaning. | Consolidated multiple payment rows (vouchers, multi-cards) into a single, total value per order. |
| **Chronological Errors** | Applied **Logical Time Checks** using `Timedelta` subtraction. | Ensured the sequence: `purchase $\leq$ approved $\leq$ carrier handoff` for data integrity. |
| **Missing/Irrelevant Features** | Used **Dimensionality Reduction** by dropping columns like `product_weight_g` and `payment_sequential`. | Made the DataFrame lightweight and focused on core sales metrics, improving analysis speed. |

***

## Key Insights & Analytics Generated

### 1. Market Basket Analysis (MBA) Rules
-   The clean dataset is ready to discover strong **"If-Then" Association Rules** for cross-selling.
-   **Focus Metric: Lift** ($>1$ indicates a strong, non-random relationship).
-   *Business Impact:* Directly informs **product bundling** strategies and website **recommendation engines**.

### 2. Product Visual Impact Analysis
-   Analyzed the relationship between `product_photos_qty` and the `Average of Quantity` sold.
-   **Insight:** A non-linear relationship was observed, highlighting a "Sweet Spot" at **17 photos**, which corresponded to the maximum average sales quantity (Approx. $1.25$ units per order).
-   *Business Impact:* Provides a clear target for marketing/seller onboarding teams on the **optimal number of product images**.

### 3. Star Schema for BI

-   The final model is organized into a **Star Schema** ($\mathbf{\text{Fact Table}}$ surrounded by $\mathbf{\text{Dimension Tables}}$). 
-   This structure is highly optimized for analytical tools, allowing analysts to drill down (high granularity) or aggregate (low granularity) data quickly and accurately.

***

## What I Learned

-   **Enterprise Data Access:** Successfully utilizing **`pyodbc`** to connect to SQL Server, simulating a professional data workflow and emphasizing **security** (Trusted Connection).
-   **Scalable Data Cleaning:** Using **`unidecode`** as a robust, industry-standard solution for handling international character sets, which is more reliable than manual string replacements.
-   **Data Integrity:** Implementing stringent **logical filtering** on time data to ensure the reliability of transactional records.
-   **Dimensional Modeling:** The strategic decision-making process between using a **Star Schema** (prioritizing speed and reporting) versus a **Snowflake Schema** (prioritizing normalization).

***

## Conclusion

This project successfully demonstrates an **end-to-end workflow** of an E-commerce data pipeline, from raw, inconsistent data to a high-integrity, analytically-ready **Star Schema** model. By tackling real-world challenges like encoding errors and chronological inconsistencies, I created a **reliable single source of truth** that provides the foundation for critical business functions like inventory management, targeted marketing, and sales forecasting.

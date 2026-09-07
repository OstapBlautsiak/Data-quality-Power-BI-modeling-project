# Enterprise Data Model Remodeling and Re-engineering in Power BI

## Project Overview
This project focuses on the comprehensive architectural overhaul and data modeling optimization of an enterprise-level Power BI dataset. The initial state consisted of raw, unformatted, and disconnected flat tables extracted from an ERP system (SAP). 

The primary objective was to eliminate data silos, establish robust relational integrity, and transition to a highly scalable, high-performance Star Schema that complies with strict corporate data governance and development standards.

---

## Technical Stack and Methodology
* Power BI Desktop — Data modeling, relationship management, and visual analytics.
* Power Query (M Language) — Advanced ETL processes: data cleansing, text standardization, custom indexing, and structural transformation.
* DAX (Data Analysis Expressions) — Business logic definition, Time Intelligence calculations, and KPI tracking.

---

## Architectural Transformation (Before vs. After)

The project successfully addressed critical data engineering challenges by shifting from a chaotic raw structure to an optimized star schema.

### Initial State Challenges (Before)
* Data Silos and Disconnected Tables: Key operational tables, including Inventory, exchange rates, and CAMPAIGN_LOG, were completely isolated with no active relationships to transactional data.
* Vertical Cleavage of Entities: Transactional data was split horizontally across multiple tables by year (e.g., ORDERS 2025, ORDERS 2026), which unnecessarily complicated cross-year analytical calculations.
* Non-Standardized Naming Conventions: The model contained a mix of UPPER_CASE, camelCase, and names with spaces (e.g., CUST_MASTER, invoice_lines, ORDERS 2025), reducing readability and maintainability.
* Absence of Reliable Keys: The raw source lacked clean primary keys, risking unstable many-to-many relationships and data ambiguity.

### Target State Solutions (After)
* Implementation of a Strict Star Schema: Designed a clean separation between Fact Tables (fact_sales, fact_inventory, fact_order_process, fact_campaign_spend, fact_promotion_coverage) and Dimension Tables (dim_customers, dim_products, dim_dates, dim_geo, dim_campaign).
* Enforcement of Project Development Standards:
  * Snake Case Convention: All table and column names were systematically converted to lowercase with underscores (e.g., customer_id, order_date_key).
  * Data Normalization: Inside tables, text attributes were programmatically converted to UPPERCASE to eliminate duplicate rows caused by mixed-case inputs.
  * Custom Surrogate Keys (_key): Generated robust unique identifier columns manually in Power Query (e.g., _customer_key, _product_key) instead of relying on unstable legacy IDs from SAP.
* Structural Segmentation: Isolated technical elements, security configurations (security), and measures into distinct system tables (e.g., _measures) for efficient maintenance.

---

## Analytics and Core Deliverables
Beyond the backend remodeling, a clean and powerful data layer was built using DAX:
* Sales Dynamics Analytics: Tailored dashboard components displaying key metrics segmented across continuous dates using a robust calendar dimension (dim_dates).
* Active Customer Base Tracking: Implemented distinct customer calculations to extract exact active buyer counts across dynamic time frames.
* Centralized Measure Repository: Grouped all KPI logic into a clean, dedicated measure folder to avoid calculation clutter.

---

## Repository Structure
* Data_Model_Remodeling.pbix — The primary Power BI file containing the remodeled star schema (saved with randomized/masked data for confidentiality).
* README.md — Project documentation and architecture logs.

---

## Key Achievements and Business Value
* Performance Optimization: Reduced file size and significantly accelerated model refresh times by eliminating redundant raw columns and merging split tables.
* Scalability: The new model allows stakeholders to drag and drop fields to build reports on the fly without risking structural relationship breaks.
* Maintainability: Standardized naming conventions and structural clarity ensure seamless onboarding for any incoming BI Engineer.

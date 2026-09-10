# Commercial Performance Dashboard (Excel BI Project)

## 📌 Project Overview
An interactive Business Intelligence (BI) dashboard developed entirely in **Microsoft Excel** to analyze and monitor commercial performance. The project integrates multi-source business data, transforming raw datasets into actionable visual insights to support strategic marketing and operational decision-making.

---

## 📐 Data Modeling & Architecture (Star Schema)
The project's backbone is a fully optimized **Star Schema Data Model** built within **Power Pivot**. 

* **Fact Table:** The `Orders` table serves as the central hub connecting all datasets, containing the transactional data and quantitative metrics.
* **Dimension Tables:** `Customers`, `Products`, and the dedicated `Date` table act as the points of the star schema.
* **Relationships:** Established robust relationships using **Primary Keys (PK)** from the dimension tables linked to **Foreign Keys (FK)** inside the central `Orders` table. This 1-to-Many architecture ensures optimal performance and seamless cross-filtering without heavy formulas.

---

## ⚙️ Data Pipeline & Methodology (Step-by-Step)

### 1. Data Ingestion & ETL Process (Power Query)
Imported the core datasets into **Power Query** to run extensive cleaning pipelines. The transformation steps were executed via M-Code as follows:

#### 📊 Orders (Central Fact) Dataset Transformation:
* **Folder Ingestion & Consolidation:** Connected directly to an external folder source to dynamically combine and expand multiple transactional text/CSV files, filtering out hidden system files.
* **Metadata Extraction:** Extracted specific string text between delimiters from the file source names to isolate and generate a dynamic `Month` reference.
* **Data Integrity & Null Handling:** Enforced row-level integrity by stripping out duplicate `OrderID` rows and filtering out null/blank entries across `OrderID`, `ProductID`, and `Quantity` columns.
* **Advanced Date Standardization Logic:** 
  * Replaced irregular text delimiters (`/` to `-`) and split the complex `OrderDate` strings into component parts.
  * Applied complex **Conditional Logic** to accurately identify and parse variations in Date formats (handling flipped Day/Month/Year components dynamically) to isolate true `Year` and `Day` integers.
  * Re-merged the standardized components into a unified, clean text string and safely cast it into a strict `Date` data type (`New Date`).
* **Surrogate Key Generation:** Created a sequential `Index` column to establish a clean, continuous primary identity row key (`Order ID`), removing redundant structural columns to optimize model memory.

#### 📦 Products Dataset Transformation:
* **Schema Definition & Integrity:** Promoted raw headers, set baseline data types, removed duplicate entries based on `ProductID`, and filtered out null IDs.
* **Text Standardization:** Applied `Trim` and `Capitalize Each Word (Proper Case)` to both `ProductName` and `Category`.
* **Value Cleansing:** Replaced textual anomalies (e.g., converting `"Two Hundred"` to `"200"`) and stripped currency symbols (`$`).
* **Optimization:** Converted `Price` to `Currency.Type` and applied a `RoundUp` function.

#### 👥 Customers Dataset Transformation:
* **Schema & Integrity:** Promoted headers, removed duplicate entries based on `CustomerID`, and filtered out null/blank IDs.
* **Advanced Text Splitting:** Trimmed spaces from `CustomerName` and utilized a space delimiter split to separate full names into distinct `Firstname` and `Lastname` columns.
* **Name Normalization:** Applied `Text.Proper` to both name fields to ensure correct capitalization formatting.
* **Geographical Cleansing:** Removed hidden spaces within the `Region` column using `ReplaceValue` and standardized the text to `Proper Case` for flawless regional aggregation.

### 2. DAX Measures & Key Metrics (KPIs)
Calculated the core business metrics within the Data Model using explicit calculations:
* 💰 **Total Sales:** Total revenue generated from all orders.
* 📦 **Total Quantity:** Total number of product units sold.
* 🛒 **Total Number of Orders:** Total transaction count.

### 3. Advanced Analysis (Power Pivot Tables)
Created multiple **Power Pivot Tables** to break down the calculated metrics across different business dimensions:
* **Table 1 (Product vs. Quantity):** Analyzes volume of units sold per product.
* **Table 2 (Total Sales per Product):** Identifies top-performing products by revenue.
* **Table 3 (Monthly Sales Trend):** Analyzes sales performance over time, leveraging the **Date Hierarchy** (Year > Quarter > Month > Day).
* **Table 4 (Total Sales by Region):** Breaks down revenue performance across geographical areas.
* **Table 5 (Total Orders by Region):** Monitors order volume distribution by region.
* **Table 6 (Regional Sales Percentage):** Calculates the percentage contribution of each region to the total sales.
* **Table 7 (Total Sales per Product):** Aggregates overall financial performance per product.
* **Table 8 (Top 5 Customers):** Isolates the highest-value customers based on their total spending.

### 4. Interactive Visualization (Dashboard Design)
Developed the final user interface with dynamic visual elements tied directly to the Power Pivot tables:
* 📊 **Bar Chart:** Visualizes **Total Sales per Product** for easy product performance ranking.
* 📊 **Column Chart:** Highlights the **Top 5 Customers** by revenue contribution.
* 🍕 **Pie Chart:** Displays the **Regional Sales Percentage** to show market share distribution.
* 📈 **Line Chart:** Tracks the **Total Sales per Month** trend over time.
* 🎛️ **Interactive Slicer:** Implemented a **Product Name Slicer** to allow stakeholders to filter the entire dashboard by specific products with a single click.
*

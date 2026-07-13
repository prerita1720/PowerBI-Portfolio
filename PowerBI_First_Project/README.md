# ⚡ Data Leverager — Power BI Power Query Project

A comprehensive Power BI project demonstrating end-to-end data ingestion, transformation, and modelling using Power Query — combining customer, product, and transaction data into a clean, analysis-ready data model.

---

## 📌 Project Overview

| Property | Details |
| **Tool** | Microsoft Power BI Desktop |
| **File** | `Data_Leverager.pbix` |
| **Total Tables** | 3 source tables (Customer, Product, Transaction) |
| **Data Sources** | Customer Data, Product Data, Transaction Data (Kaggle — Business Revenue Analysis dataset) |
| **Key Operations** | Merge Queries, Data Cleaning, Text Transformations, Conditional Columns, Grouping & Aggregation, Pivot/Unpivot, Parameters |

---

## 📂 Data Sources

| Source | Format | Description |
|---|---|---|
| Customer Data | CSV | Customer demographics — ID, signup date, country, age, gender, loyalty tier, acquisition channel |
| Product Data | CSV | Product catalog — ID, category, brand, base price, launch date, premium flag |
| Transaction Data | CSV | Sales transactions — ID, timestamp, customer ID, product ID, quantity, discount, gross revenue, campaign ID, refund flag |

> All three datasets were originally sourced from Kaggle. Since the raw files contained a very large number of rows, Python was used to slice and reduce each dataset to the first **2,000 rows**, producing lighter, manageable CSV files for smooth processing in Power BI.

---

## 🧹 Data Preparation & Cleaning

- Imported all three CSV files into Power BI Desktop using **Get Data → Text/CSV**
- Removed empty or null rows from each dataset
- Promoted the first row to headers
- Updated column data types (text, whole number, decimal, date, percentage) for accurate calculations
- Renamed columns to clear, readable names
- Renamed queries to meaningful names: `Customer_Data`, `Product_Data`, `Transaction_Data`

---

## ✍️ Text Transformations

| Query | Column | Transformation |
|---|---|---|
| Customer_Data | Country_Name | `UPPER()` — converted to uppercase |
| Customer_Data | Gender | `LOWER()` — converted to lowercase |
| Customer_Data | Loyalty_Tier | Capitalize Each Word |
| Customer_Data | (multiple) | Clean Text — removed hidden characters/symbols |
| Product_Data | (required columns) | Trim — removed leading/trailing spaces |
| Product_Data | Brand | Replace Values — `_` replaced with `-` (e.g. `brand_1` → `brand-1`) |
| Product_Data | Base_Price | Rounded to 2 decimal places |

---

## 🧮 Calculated Columns & Custom Logic

**Net Revenue** (Transaction_Data):
```
Net_Revenue = Gross_Revenue – (Gross_Revenue × Discount_Applied)
```

**Revenue Status** (Transaction_Data) — conditional column based on `Net_Revenue`:

| Condition | Status |
|---|---|
| Net_Revenue ≥ 200 | High |
| Net_Revenue ≥ 100 | Medium |
| Else | Low |

---

## 📅 Date Transformations

| Query | Source Column | Extracted Fields |
|---|---|---|
| Customer_Data | SignUp_Date | Year |
| Product_Data | Launch_Date | Month, Quarter, Day of Week |
| Transaction_Data | Timestamp | Month |

---

## 🔗 Combining & Shaping Data

- **Merge Queries** — Joined `Transaction_Data` and `Customer_Data` on `Customer_Id` to link customer info with transaction records
- **Append Queries** — Not used, as the tables did not share common columns
- **Group By** — Grouped `Product_Data` by `Product_Category` with aggregation to summarize category-level metrics
- **Aggregation** — Calculated total revenue per `Product_Id` using `SUM(Gross_Revenue)` on `Transaction_Data`
- **Pivot / Unpivot** — Applied on `Customer_Data` to practice reshaping data between wide and long formats

---

## ✅ Data Quality & Governance

- Used **Data Profiling tools** (Column Profile, Column Distribution, Column Quality) to check for missing values and assess data consistency
- Configured **Parameters** for a dynamic folder path
- Reviewed **Data Source Settings** and credentials for each connection

---

## 🛠️ Tools & Skills Demonstrated

`Power Query` · `Power BI Desktop` · `Data Cleaning` · `Text Transformations` · `Conditional Columns` · `Merge & Append Queries` · `Grouping & Aggregation` · `Pivot/Unpivot` · `Parameters` · `Data Profiling`

---

## 📁 Repository Contents

| File | Description |
|---|---|
| `Data_Leverager.pbix` | Power BI project file with full data model and transformations |
| `customers_sample.csv` | Sample customer dataset |
| `products_sample.csv` | Sample product dataset |
| `transactions_sample.csv` | Sample transaction dataset |
| `Summary_Of_Data_Sources_And_Transformation.pdf` | Detailed write-up of data sources and transformation steps |

---
# 💡 What I Learned

- How to plan and structure an end-to-end ETL workflow inside Power Query, from raw CSV import to a clean, analysis-ready model
- Practical use of text transformation tools (UPPER, LOWER, Capitalize Each Word, Trim, Clean Text, Replace Values) to standardize messy real-world data
- How to build calculated columns and conditional logic (e.g. Net Revenue, Revenue Status) to derive business-ready metrics
- The importance of choosing the right combine strategy — understanding when to use **Merge** vs **Append** based on table schema
- How to extract meaningful date parts (Year, Month, Quarter, Day of Week) to enable time-based analysis
- Using **Group By** and aggregation to summarize data at category and product level
- How **Pivot/Unpivot** reshapes data between wide and long formats, and when each is useful
- The value of **Data Profiling tools** in catching quality issues early, before they affect downstream analysis
- How to use **Parameters** and manage **Data Source Settings** to make a project more dynamic and portable


## 👤 Author

**PRERITA MORASHIYA**



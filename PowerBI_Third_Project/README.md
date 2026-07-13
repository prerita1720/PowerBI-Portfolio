# 📊 DAX Depo — Power BI Data Modeling & Advanced DAX Project

A Power BI project focused entirely on **data modelling and advanced DAX calculations** — no dashboards or charts, with all results surfaced strictly through DAX measures on Matrix visuals.

---

## 📌 Project Overview

| Property | Details |
|---|---|
| **Tool** | Microsoft Power BI Desktop |
| **File** | `Project-3_Dex_Depo.pbix` |
| **Scope** | Data modelling + advanced DAX only — no dashboards/charts |
| **Total Tables** | 7 (4 dimension + 2 fact + 1 dedicated Measure table) |
| **Schema Type** | Star Schema |
| **Key Operations** | Relationship Building, Calculated Columns, DAX Measures, Time Intelligence, Matrix Validation |

---

## 📂 Data Sources

| Table | Type | Key Columns |
|---|---|---|
| Customer_Dimension | Dimension | CustomerID (PK), FirstName, LastName, Segment |
| Product_Dimension | Dimension | ProductID (PK), ProductName, Category, Cost |
| Region_Dimension | Dimension | RegionID (PK), RegionName |
| Date_Dimension | Dimension | DateKey (PK), Date, Year, Month, MonthName, Quarter, Day, Weekday |
| Sales_Fact_Table | Fact | SalesID (PK), DateKey (FK), ProductID (FK), CustomerID (FK), RegionID (FK), Quantity, SalesAmount, Cost |
| Returns_Fact_Table | Fact | ReturnID (PK), SalesID (FK), DateKey (FK), ProductID (FK), CustomerID (FK), RegionID (FK), Quantity |

---

## 🧹 Data Preparation

- Imported all datasets into Power BI using **Get Data**
- Opened **Model View** to identify fact and dimension tables:
  - **Fact tables:** Sales_Fact_Table, Returns_Fact_Table
  - **Dimension tables:** Customer_Dimension, Product_Dimension, Date_Dimension, Region_Dimension
- Reviewed columns in each table to identify primary keys and foreign keys required for relationships
- Cleaned column names and corrected data types where needed to support accurate relationship creation

---

## 🔑 Keys & Relationships

| From (Fact) | To (Dimension) | Key Used | Cardinality | Direction |
|---|---|---|---|---|
| Sales_Fact_Table | Customer_Dimension | CustomerID | One-to-Many | Single |
| Sales_Fact_Table | Product_Dimension | ProductID | One-to-Many | Single |
| Sales_Fact_Table | Date_Dimension | DateKey | One-to-Many | Single |
| Sales_Fact_Table | Region_Dimension | RegionID | One-to-Many | Single |
| Returns_Fact_Table | Sales_Fact_Table | SalesID | One-to-Many | Single |

- All relationships were kept **single-directional**, maintaining a clean **star schema** with `Sales_Fact_Table` at the center

---

## 🧮 Calculated Columns

| Column | Table | Description |
|---|---|---|
| Profit | Sales_Fact_Table | Derived from SalesAmount minus Cost |
| ReturnFlag | Sales_Fact_Table | Flags transactions that have a matching return record |
| Customer Full Name | Customer_Dimension | Combines FirstName and LastName |

---

## 📐 DAX Measures

A dedicated **Measure table** was created to keep all DAX measures organized and separate from the data tables.

| Measure | Purpose |
|---|---|
| Total Sales | Sum of SalesAmount across transactions |
| Total Cost | Sum of Cost across transactions |
| Total Profit | Total Sales minus Total Cost |
| Return Rate | Proportion of returned transactions to total sales |
| Average Sales | Average SalesAmount per transaction |
| YTD Sales | Year-to-date sales using `TOTALYTD` |
| YoY Sales | Year-over-year comparison using `SAMEPERIODLASTYEAR` |
| Running Total | Cumulative sales total over time |

**Key DAX functions used:**

| Category | Functions |
|---|---|
| Iterators | `SUMX`, `AVERAGEX` |
| Conditional Logic | `IF`, `SWITCH` |
| Filter Context | `ALL`, `FILTER`, `CALCULATE` |
| Time Intelligence | `TOTALYTD`, `SAMEPERIODLASTYEAR`, `DATESBETWEEN` |

---

## ✅ Model Validation

As per project instructions, only the **Matrix visual** was used to display results — no charts or dashboards. Matrices were built to validate measures across multiple dimensions:

| Matrix Grouping | Purpose |
|---|---|
| By Region | Verified Sales_Fact_Table → Region_Dimension relationship and regional measure accuracy |
| By Month | Validated time intelligence measures (YTD, YoY, Running Total) against Date_Dimension |
| By Product Category | Confirmed Product_Dimension link and category-level profit/sales figures |
| By Customer Details | Verified Customer_Dimension link and customer-level measure accuracy |

---

## 🚧 Challenges & Solutions

| Challenge | Solution |
|---|---|
| Keeping the project strictly to modelling and DAX (no dashboards) | Displayed all results only through Matrix visuals, as required by instructions |
| Ensuring correct relationship keys across multiple fact/dimension tables | Reviewed each table's columns to correctly identify PK/FK pairs before building relationships |
| Linking returns back to original sales | Connected Returns_Fact_Table to Sales_Fact_Table using SalesID |
| Keeping DAX measures organized as the model grew | Created a dedicated Measure table to house all DAX measures separately from data tables |
| Calculating profit and flags without altering source data | Used calculated columns (Profit, ReturnFlag, Customer Full Name) instead of modifying raw fields |
| Building accurate time-based measures | Leveraged Date_Dimension with TOTALYTD, SAMEPERIODLASTYEAR, and DATESBETWEEN for YTD, YoY, and running totals |
| Avoiding row context/filter context confusion in complex measures | Used SUMX/AVERAGEX for iteration and CALCULATE/FILTER/ALL to control filter context precisely |

---

## 💡 What I Learned

- How to build a clean **star schema** with single-directional relationships between multiple fact and dimension tables
- The difference between **calculated columns** and **DAX measures**, and when to use each
- How to structure a model using a **dedicated Measure table** for better organization and maintainability
- Practical use of **iterator functions** (`SUMX`, `AVERAGEX`) versus simple aggregations
- How to control **filter context** using `CALCULATE`, `FILTER`, and `ALL`
- Writing **time intelligence** measures (`TOTALYTD`, `SAMEPERIODLASTYEAR`, `DATESBETWEEN`) for YTD, YoY, and running total calculations
- Using conditional logic (`IF`, `SWITCH`) inside DAX to derive flags and categorized results
- How to validate an entire DAX-driven model using only **Matrix visuals** — without relying on charts or dashboards
- The importance of staying disciplined to project scope, focusing on modelling and DAX depth rather than visual design

---

## 📁 Repository Contents

```
powerbi-dax-depo/
│
├── Project-3_Dex_Depo.pbix           # Main Power BI file
├── SUMMARY_OF_Project-3.pdf           # Project summary report
├── DAX_Depo_Sample_Datasets.xlsx      # Source dataset (all dimension & fact tables)
└── README.md                          # Project documentation
```

---

## 👤 Author

**Prerita Morashiya**

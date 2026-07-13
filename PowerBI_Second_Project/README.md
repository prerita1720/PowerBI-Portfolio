# 🧩 Data Modeler — Power BI Star Schema Project

A focused Power BI project demonstrating **pure data modelling** — building relationships, a star schema, and hierarchies across fact and dimension tables, with no data analysis or DAX measures involved.

---

## 📌 Project Overview

| Property | Details |
|---|---|
| **Tool** | Microsoft Power BI Desktop |
| **File** | `Project-2_Data_Modeler.pbix` |
| **Scope** | Data modelling only — no analysis, no DAX measures |
| **Total Tables** | 6 (4 dimension + 2 fact) |
| **Schema Type** | Star Schema |
| **Key Operations** | Data Cleaning, Relationship Building, Star Schema Design, Hierarchies, Matrix Validation |

---

## 📂 Data Sources

| Table | Type | Key Columns |
|---|---|---|
| Customer_Dimension | Dimension | CustomerID (PK), FullName, Age, Gender, Segment |
| Product_Dimension | Dimension | ProductID (PK), ProductName, Category, Subcategory, Brand |
| Region_Dimension | Dimension | RegionID (PK), Country, State, City |
| Date_Dimension | Dimension | DateKey (PK), Date, Month, Quarter, Year, Fiscal Year |
| Sales_Fact | Fact | SalesID (PK), CustomerID (FK), ProductID (FK), RegionID (FK), DateKey (FK), Quantity, Revenue, Discount |
| Returns_Fact | Fact | ReturnID (PK), SalesID (FK), ReturnDateKey (FK), Reason |

---

## 🧹 Data Preparation & Cleaning

- Imported all six Excel files into Power BI using **Get Data**
- Opened Power Query Editor to clean and prepare data before modelling
- Set correct data types across all tables — whole numbers for IDs, currency for revenue, date type for date columns
- Removed empty/null rows carefully, ensuring no important fact table records were filtered out
- Identified table roles by naming convention: tables with **Dim** = dimension tables (descriptive), tables with **Fact** = fact tables (transactional)
- Renamed tables for clarity: `Customer_Dimension`, `Product_Dimension`, `Region_Dimension`, `Date_Dimension`, `Sales_Fact`, `Returns_Fact`

---

## 🔑 Keys & Relationships

- Identified **Primary Keys (PK)** in each dimension table and **Foreign Keys (FK)** in fact tables
- Placed `Sales_Fact` at the center of the model as the main transactional table

| From (Fact) | To (Dimension) | Key Used | Cardinality | Status |
|---|---|---|---|---|
| Sales_Fact | Customer_Dimension | CustomerID | Many-to-One | Active |
| Sales_Fact | Product_Dimension | ProductID | Many-to-One | Active |
| Sales_Fact | Region_Dimension | RegionID | Many-to-One | Active |
| Sales_Fact | Date_Dimension | DateKey | Many-to-One | Active |
| Returns_Fact | Sales_Fact | SalesID | Many-to-One | Active |
| Returns_Fact | Date_Dimension | ReturnDateKey | Many-to-One | **Inactive** (per project instructions) |

- All relationships were built manually using PK–FK logic
- Verified cardinality and cross-filtering direction on every relationship

---

## ⭐ Star Schema Design

`Sales_Fact` sits at the center of the model, directly connected to `Customer_Dimension`, `Product_Dimension`, `Region_Dimension`, and `Date_Dimension`. `Returns_Fact` branches off `Sales_Fact` via `SalesID`, with a separate **inactive** link to `Date_Dimension` through `ReturnDateKey` for tracking return dates without affecting the primary date filtering path.

No extra tables or relationships were created beyond what the project instructions required.

---

## 🪜 Hierarchies

| Dimension | Hierarchy Levels |
|---|---|
| Date_Dimension | Year → Quarter → Month → Date |
| Product_Dimension | Category → Subcategory → ProductName |
| Region_Dimension | Country → State → City |

---

## ✅ Model Validation

Since the project scope was modelling-only, the **Matrix visual** was the only visual used to verify relationships:

| Matrix Built | Purpose |
|---|---|
| Revenue by Product Category and Region | Verified Product_Dimension and Region_Dimension links to Sales_Fact |
| Returns by Fiscal Year | Verified the inactive Returns_Fact → Date_Dimension relationship |
| Revenue by Customer Segment | Verified the Sales_Fact → Customer_Dimension link |

Hierarchy levels were used within these matrices where relevant, and values changed correctly when dimensions were drilled or swapped — confirming the model was wired correctly.

---

## 🚧 Challenges & Solutions

| Challenge | Solution |
|---|---|
| Distinguishing dimension vs. fact tables at a glance | Used naming convention (Dim/Fact) to classify and rename tables clearly |
| Connecting Returns_Fact to Date_Dimension without disrupting Sales_Fact's date filtering | Set the Returns_Fact → Date_Dimension relationship to **inactive** |
| Ensuring correct relationship direction and cardinality | Manually reviewed each relationship's cross-filter direction and set Many-to-One explicitly |
| Avoiding scope creep with extra tables/measures | Stuck strictly to the modelling-only instructions — no DAX, no analysis visuals |
| Verifying the model without using standard chart visuals | Relied solely on the Matrix visual with hierarchies to confirm relationships worked |
| Cleaning fact tables without losing transactional data | Removed only truly empty/null rows, double-checking fact tables were not over-filtered |

---

## 💡 What I Learned

- How to distinguish between **fact tables** and **dimension tables** and structure a model around that distinction
- How to identify and use **primary keys** and **foreign keys** to build correct relationships
- Practical experience designing a **star schema**, with a central fact table connected to surrounding dimensions
- The difference between **active** and **inactive** relationships, and when to use `USERELATIONSHIP`-style inactive links (e.g. Returns_Fact to Date_Dimension)
- How **cardinality** (Many-to-One) and **cross-filter direction** affect how data flows through a model
- How to build **hierarchies** (Date, Product, Region) to support drill-down analysis
- Using the **Matrix visual** as a lightweight way to validate relationships without building full analytical reports
- The importance of staying within project scope — focusing purely on modelling instead of jumping ahead to analysis

---

## 📁 Repository Contents

```
powerbi-data-modeler/
│
├── Project-2_Data_Modeler.pbix        # Main Power BI file
├── Summary_of_Data_Modeler.pdf         # Data modelling summary report
├── Customer_Dim.xlsx                   # Customer dimension table
├── Product_Dim.xlsx                    # Product dimension table
├── Region_Dim.xlsx                     # Region dimension table
├── Date_Dim.xlsx                       # Date dimension table
├── Sales_Fact.xlsx                     # Sales fact table
├── Returns_Fact.xlsx                   # Returns fact table
└── README.md                           # Project documentation
```

---

## 👤 Author

**PRERITA MORASHIYA**

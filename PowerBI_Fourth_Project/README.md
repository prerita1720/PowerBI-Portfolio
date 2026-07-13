# 👥 Workforce Analytics — HR Power BI Project

An end-to-end Power BI project covering data modelling, advanced DAX, and report design — analysing employee lifecycle data across headcount, attrition, performance, engagement, recruitment, and training.

---

## 📌 Project Overview

| Property | Details |
|---|---|
| **Tool** | Microsoft Power BI Desktop |
| **File** | `pr_4.pbix` |
| **Scope** | Full workflow — data modelling, DAX measures, and report building |
| **Total Tables** | 6 (5 source + 1 custom Date table) + 1 Measure table |
| **Report Pages** | Workforce Overview, Attrition Analysis |
| **Key Operations** | Data Cleaning, Custom Date Table, Relationship Modelling, Calculated Columns, DAX Measures, Time Intelligence, Report Design |

---

## 📂 Data Sources

| Query Name | Source File | Description |
|---|---|---|
| EmployeeMaster | `employee_data.csv` | Core employee records — ID, salary, dates, title, department, status, rating |
| Training | `training_and_development_data.csv` | Training programs attended, outcomes, duration, and cost per employee |
| EngagementSurvey | `employee_engagement_survey_data.csv` | Engagement, satisfaction, and work-life balance survey scores |
| Performance | `performance_data.csv` | Quarterly/yearly performance ratings per employee |
| Recruitment | `recruitment_data.csv` | Applicant records — not linked to employee data (no Employee ID) |

---

## 🧹 Data Preparation & Cleaning

- Imported all five CSV files into Power BI using **Get Data → Text/CSV**
- Renamed each query to a meaningful name: `EmployeeMaster`, `Training`, `EngagementSurvey`, `Performance`, `Recruitment`
- Updated data types in `EmployeeMaster`:
  - `DateOfJoining` and `DateOfTermination` → Date
  - `Salary` → Decimal Number
  - `Current Employee Rating` → Whole Number
- Found hidden trailing spaces in `DepartmentType` (causing gaps in slicers/labels) and applied **Trim** to fix it

---

## 📅 Custom Date Table (DimDate)

- Built a new `DimDate` table using a **Blank Query and M code**, generating a continuous calendar with `Year`, `Quarter`, `Month_Num`, `Month_Name`, `Weekday`, and `Year_Quarter` columns
- Marked `DimDate` as a **Date Table** in Model view so Power BI would recognize it correctly for Time Intelligence
- Extended the date range further into the future (originally only built through 2024) since Time Intelligence functions relying on `TODAY()` needed current dates available to calculate against

---

## 🔑 Relationships

| From | To | Key Used | Status |
|---|---|---|---|
| EmployeeMaster | Training | Employee ID | Active |
| EmployeeMaster | Performance | Employee ID | Active |
| EmployeeMaster | EngagementSurvey | Employee ID | Active |
| DimDate | EmployeeMaster | DateOfJoining | Active |
| DimDate | EmployeeMaster | DateOfTermination | **Inactive** |
| Recruitment | — | — | Standalone (no Employee ID; applicants aren't yet employees) |

> ⚠️ **Debugging note:** While testing the `Attrition_Rate_YTD` measure, it returned blank. Investigation showed Power BI had **auto-detected incorrect relationships** directly between fact tables (`Training` ↔ `Performance`, `Training` ↔ `EngagementSurvey`) instead of routing everything through `EmployeeMaster`. These incorrect relationships were deleted, and the correct `EmployeeMaster` → `Performance` and `EngagementSurvey` → `EmployeeMaster` relationships were activated — restoring a clean star-schema-style model and fixing the blank measure.

---

## 🧮 Calculated Columns (EmployeeMaster)

| Column | Purpose |
|---|---|
| Tenure_Years | Employee tenure in years, based on `EmployeeStatus` (not blank `DateOfTermination`, since many Active employees carried an old termination date) |
| Career_Level_Band | Categorized career level grouping |
| Full_Name | Combined first and last name |
| Salary_Band | Salary grouped into bands |
| Is_Active | Active/Inactive flag, based on `EmployeeStatus` |
| Performance_Label | Readable label for performance rating |
| Salary_Formatted | Formatted salary display |
| Days_Since_Hire | Days elapsed since date of joining |
| Hire_Year_Month | Year-month combination of hire date |
| Above_Avg_Salary_Flag | Flags employees earning above average salary |

---

## 📐 DAX Measures

A dedicated **`_Measures`** table (created via Enter Data) holds all DAX measures, keeping them organized and separate from data tables.

**Core Measures**

| Measure | Description |
|---|---|
| Total_Headcount | Total number of employees |
| Active_Headcount | Count of currently active employees |
| Terminated_Count | Count of terminated employees |
| Avg_Salary | Average salary across employees |
| Total_Salary_Cost | Sum of all salaries |
| Avg_Tenure | Average tenure in years |
| Distinct_Departments | Count of unique departments |
| Avg_Performance_Rating | Average performance rating |

**Ratio Measures** (using `DIVIDE` to avoid divide-by-zero errors)

| Measure | Description |
|---|---|
| Attrition_Rate_% | Percentage of employees terminated |
| Gender_Diversity_Ratio | Gender balance ratio |
| Bench_Utilisation_% | Utilisation ratio metric |

**Iterator Measures**

| Measure | Function Used |
|---|---|
| Avg_Training_Cost | `AVERAGEX` |
| Total_Training_Cost | `SUMX` |

**Filter Context Measures**

| Measure | Functions Used |
|---|---|
| Total_HC_All_Depts | `CALCULATE` + `ALL` |
| Headcount_%_of_Total | `CALCULATE` + `ALL` |
| Dept_Avg_Salary_AEXCEPT | `CALCULATE` + `ALLEXCEPT` |
| Senior_Headcount | `FILTER` + `CALCULATE` |
| High_Performers_Count / High_Performer_% | Conditional filtering on active employees with high ratings |
| Salary_Rank_Dept / Training_Cost_Rank | `RANKX` |

**Time Intelligence Measures**

| Measure | Function Used |
|---|---|
| YTD_New_Hires | `TOTALYTD` |
| New_Hires_SPLY | `SAMEPERIODLASTYEAR` |
| New_Hires_YoY_% | Comparison of current vs. prior period |
| Hires_Prior_3M | `DATEADD` |
| **Attrition_Rate_YTD** (capstone measure) | `DATESYTD` + `USERELATIONSHIP` — temporarily activates the inactive `DateOfTermination` relationship for this calculation only |

- Formatted all percentage measures as **Percentage (1 decimal place)** and all salary-related measures as **Currency**
- Added a short description to every measure via the Properties panel

---

## 📊 Report Design

**Workforce Overview page**
- 8 KPI cards arranged across two rows
- Bar chart — Active Headcount by Department
- Bar chart — Average Salary by Department (with reference line)
- Donut chart — Career Level Band distribution
- Matrix — Performance Distribution by Department
- Table — Departments ranked by salary

**Attrition Analysis page**
- Dedicated KPI cards for attrition metrics
- Column chart — Annual Hiring vs. Same Period Last Year
- Line chart — YTD Hires by Month

**Interactivity**
- Slicers for **Year**, **Department**, and **Career Level Band**
- Filter context tested by clicking through departments and observing which measures recalculated vs. stayed fixed

**Formatting pass**
- Consistent title styling, data labels, bar colors, and alignment
- Fixed KPI card padding/background spacing issues
- Adjusted matrix and donut chart background/font colors for legibility

---

## ✅ Validation

- Confirmed **Active_Headcount + Terminated_Count = Total_Headcount** for every department
- Took a final screenshot of Model view showing all tables and relationships in their corrected state

---

## 🚧 Challenges & Solutions

| Challenge | Solution |
|---|---|
| `DepartmentType` showing gaps in slicers/labels | Identified hidden trailing spaces and applied Trim |
| Time Intelligence measures needed a proper calendar | Built a custom `DimDate` table via M code and marked it as a Date Table |
| `Is_Active`/`Tenure_Years` logic breaking due to stale termination dates | Based logic on `EmployeeStatus` instead of whether `DateOfTermination` was blank |
| Ratio measures breaking on division by zero | Used `DIVIDE` instead of the `/` operator |
| `Attrition_Rate_YTD` returning blank | Diagnosed and removed incorrect auto-detected relationships between fact tables; rebuilt relationships correctly through `EmployeeMaster` |
| Needed to switch to an inactive relationship for one specific measure | Used `USERELATIONSHIP` inside `Attrition_Rate_YTD` to temporarily activate the `DateOfTermination` relationship |
| Time Intelligence functions using `TODAY()` returning blanks | Extended `DimDate`'s date range further into the future |
| Matrix/donut chart text hard to read against background | Adjusted background and font colors for legibility |
| KPI cards had inconsistent spacing | Adjusted padding and background settings |

---

## 💡 What I Learned

- How to build and mark a **custom Date table** using M code for reliable Time Intelligence
- The importance of routing all fact-to-fact relationships **through a central dimension table** rather than letting Power BI auto-detect direct links
- How to safely use **inactive relationships** and activate them selectively with `USERELATIONSHIP`
- Writing robust ratio measures using `DIVIDE` to avoid runtime errors
- Practical use of iterator functions (`SUMX`, `AVERAGEX`) for row-by-row calculations before aggregation
- Controlling filter context precisely using `CALCULATE`, `ALL`, `ALLEXCEPT`, and `FILTER`
- Building **time intelligence** measures (`TOTALYTD`, `SAMEPERIODLASTYEAR`, `DATEADD`, `DATESYTD`) for YTD, YoY, and rolling comparisons
- How to organize a growing DAX model using a **dedicated Measure table**
- Debugging a broken model by tracing relationships back through **Manage Relationships**, not just the measure formula itself
- The value of a validation pass (e.g. Active + Terminated = Total) to catch modelling errors before presenting results
- Designing multi-page reports with purpose-built KPI cards, visuals, and slicers tailored to each page's analytical focus

---

## 📁 Repository Contents

```
hr-workforce-analytics/
│
├── pr_4.pbix                                  # Main Power BI file
├── employee_data.csv                          # Employee master data
├── training_and_development_data.csv          # Training records
├── employee_engagement_survey_data.csv        # Engagement survey responses
├── performance_data.csv                       # Performance ratings
├── recruitment_data.csv                       # Recruitment applications
└── README.md                                  # Project documentation
```

---

## 👤 Author

**Prerita Morashiya**

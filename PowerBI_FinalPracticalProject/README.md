# 🎓 Student Performance Dashboard — Power BI Project

An end-to-end Power BI project analysing academic performance, attendance, and behavior — combining data modelling, DAX calculations, and interactive reporting to support data-driven academic analysis.

---

## 📌 Project Overview

| Property | Details |
|---|---|
| **Tool** | Microsoft Power BI Desktop |
| **File** | `Practical_Exam_-_Student_Performance_Dashboard.pbix` |
| **Scope** | Data modelling, DAX measures, and interactive report design |
| **Total Tables** | 4 (1 dimension + 3 fact) |
| **Schema Type** | Star Schema |
| **Key Operations** | Data Cleaning, Relationship Modelling, DAX Measures, Report Design, Drillthrough & Tooltips |

---

## 📂 Data Sources

| Table | Type | Key Fields |
|---|---|---|
| Students Dimension | Dimension | StudentID (PK), Name, Gender, Class, Section |
| Scores Fact | Fact | StudentID (FK), Subject, ExamType, Score, MaxScore, Term |
| Attendance Fact | Fact | StudentID (FK), Date, Status, Reason |
| Behavior Fact | Fact | StudentID (FK), Date, BehaviorType, Notes |

---

## 🧹 Data Preparation & Cleaning

- Imported Students, Scores, Attendance, and Behavior datasets into Power BI Desktop
- In Power Query:
  - Verified and corrected data types across all tables
  - Removed unnecessary columns
  - Renamed columns for better clarity
- Moved to **Model View** to organize and structure the tables properly

---

## 🔑 Data Model & Relationships

- Designed the model using **fact and dimension tables** for an efficient, structured layout:
  - **Fact tables:** Scores Fact (exam scores & performance), Attendance Fact (present/absent records), Behavior Fact (student behavior records)
  - **Dimension table:** Students Dimension (student details — name, class, gender, section)

| From (Dimension) | To (Fact) | Key Used | Cardinality | Direction |
|---|---|---|---|---|
| Students Dimension | Scores Fact | StudentID | One-to-Many | Single |
| Students Dimension | Attendance Fact | StudentID | One-to-Many | Single |
| Students Dimension | Behavior Fact | StudentID | One-to-Many | Single |

- All relationships were kept **single-directional** to maintain a clean and logical model

---

## 📐 DAX Measures

| Measure | Description | Key Functions Used |
|---|---|---|
| Total Students | Count of distinct students | `COUNT` |
| Average Score | Average raw exam score | `AVERAGE` |
| Average % Score | Average score as a percentage of max score | `DIVIDE`, `AVERAGE` |
| Attendance Percentage | Proportion of "Present" records over total attendance records | `DIVIDE`, `CALCULATE` |
| Behavior Count by Type | Count of behavior records grouped by behavior type | `CALCULATE`, `COUNT` |
| Performance Category | Categorizes students into High / Medium / Low based on score thresholds | `SWITCH` |

- Additional DAX functions used across measures: `SUM`, `AVERAGE`, `CALCULATE`, `COUNT`, `DIVIDE`, `SWITCH`

---

## 📊 Report Design

**Visuals used:**
- KPI cards for headline metrics (e.g. Total Students, Average % Score, Attendance %)
- Bar charts, line charts, and donut charts for performance and attendance trends
- Tables with **conditional formatting** to highlight performance levels

**Interactivity:**
- Slicers for **Class**, **Section**, **Subject**, and **Term** to enable dynamic filtering
- **Drillthrough pages** for detailed, student-level or category-level insights
- **Custom tooltips** to provide contextual information on hover without leaving the current page

---

## 🚧 Challenges & Solutions

| Challenge | Solution |
|---|---|
| Keeping the model efficient with multiple data domains (scores, attendance, behavior) | Structured the model as a star schema — one Students dimension connected to three separate fact tables |
| Avoiding ambiguous filter propagation across fact tables | Kept all relationships single-directional, filtering only from Students Dimension outward |
| Calculating percentage-based metrics without errors | Used `DIVIDE` instead of the `/` operator for Average % Score and Attendance Percentage |
| Categorizing students into performance bands | Built a `SWITCH`-based Performance Category measure using score thresholds |
| Summarizing behavior records by type | Used `CALCULATE` combined with `COUNT` to break down Behavior Count by Type |
| Providing detail without cluttering summary visuals | Implemented Drillthrough pages and custom Tooltips for deeper, contextual insights |

---

## 💡 What I Learned

- How to design a **star schema** with one central dimension table connected to multiple fact tables covering different data domains
- The importance of single-directional relationships to keep filter context clean and predictable
- Practical use of `SWITCH` to build categorical measures like Performance Category
- Writing safe ratio-based measures with `DIVIDE` to avoid division-by-zero errors
- Using `CALCULATE` with `COUNT` to summarize categorical data such as behavior types
- How to design an interactive report using KPI cards, bar/line/donut charts, and conditionally formatted tables
- Implementing **Drillthrough pages** and **custom Tooltips** to add depth to a report without overwhelming the main views
- How combining academic, attendance, and behavioral data in one model supports a more complete, data-driven view of student performance

---

## 📁 Repository Contents

```
student-performance-dashboard/
│
├── Practical_Exam_-_Student_Performance_Dashboard.pbix   # Main Power BI file
├── SUMMARY.pdf                                            # Project summary report
├── Students.xlsx                                          # Student dimension data
├── Scores.xlsx                                            # Exam scores fact data
├── Attendance.xlsx                                        # Attendance fact data
├── Behavior.xlsx                                          # Behavior fact data
└── README.md                                              # Project documentation
```

---

## 👤 Author

**Prerita Morashiya**

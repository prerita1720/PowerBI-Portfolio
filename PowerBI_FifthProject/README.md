# ✈️ Airline Performance Dashboard — Power BI Report

An interactive Power BI dashboard analysing flight performance, delays, and cancellations — covering airline-level trends, route/airport geography, and time-based patterns across a multi-page report.

> ℹ️ **Note:** This project was submitted as a `.pbix` file only, without an accompanying data-source or transformation summary. The details below were reconstructed by inspecting the report's data model and visuals directly. Feel free to edit any section to better match your actual build process.

---

## 📌 Project Overview

| Property | Details |
|---|---|
| **Tool** | Microsoft Power BI Desktop |
| **File** | `pr_5.pbix` |
| **Scope** | Report building & data visualization — flight delay/cancellation analytics |
| **Core Table** | `FlightData` |
| **Measure Table** | `Measures (2)` |
| **Report Pages** | 7 — Home, Overview, Airline Performance, Route & Airport Map, Drillthrough Page, Trends & Forecast, Tooltip |

---

## 📂 Data Model

| Table | Type | Key Fields |
|---|---|---|
| FlightData | Data Table | AIRLINE, AIRLINE_CODE, ORIGIN, DEST, ARR_DELAY, DEP_DELAY, CANCELLATION_CODE, delay_status, state, Flight_Month, Flight_Year |
| Measures (2) | Dedicated Measure Table | Total_Flights, Total_Cancelled, Cancellation_Rate% |

- All DAX measures were kept in a separate **Measures (2)** table, keeping the model clean and the measures organized away from the raw data fields
- Fields cover both **flight-level detail** (airline, route, delay minutes, cancellation reason) and **time attributes** (Flight_Month, Flight_Year) to support trend analysis

---

## 📐 Key Measures

| Measure | Purpose |
|---|---|
| Total_Flights | Total count of flights in the dataset |
| Total_Cancelled | Total count of cancelled flights |
| Cancellation_Rate% | Proportion of flights cancelled out of total flights |

---

## 📊 Report Pages

| Page | Purpose |
|---|---|
| **Home** | Landing/cover page with navigation buttons and branding imagery |
| **Overview** | High-level KPI summary — Total Flights, Total Cancelled, and Cancellation Rate% cards, alongside donut chart breakdowns and Year/Airline slicers |
| **Airline Performance** | Airline-level analysis — bar chart of *Total Cancelled by Airline Code*, a pivot table, a detail table, and a column chart, with slicer-driven filtering |
| **Route & Airport Map** | Geographic view of flight routes and airport activity using **Map** and **Filled Map** visuals |
| **Drillthrough Page** | Detail page for drilling into a specific selection — KPI cards, a bar chart, a donut chart, a line chart (*Count of Cancellation Code by Flight Year*), and a supporting table |
| **Trends & Forecast** | Time-based analysis with dual line charts and slicers to explore flight and cancellation trends over time |
| **Tooltip** | Custom tooltip page showing KPI cards and a bar chart (*Total Flights by Delay Status*) displayed on hover over visuals from other pages |

---

## 🖱️ Interactivity

- **Slicers** for Year, Airline, and related dimensions across multiple pages to filter the report dynamically
- **Action buttons** used for page navigation between Home, Overview, Airline Performance, and other pages
- **Drillthrough** configured to jump from summary visuals into a dedicated detail page for deeper analysis
- **Custom tooltip page** configured to appear on hover, providing additional context (Total Flights by Delay Status) without leaving the current page

---

## 🎨 Design & Formatting

- Consistent color palette applied across cards, charts, and slicers for a cohesive look
- Custom titles applied to key visuals (e.g. *Total Cancelled by Airline Code*, *Total Flights by Delay Status*) for clarity
- Background images, shapes, and icons used on the Home and Overview pages to strengthen visual branding

---

## 🚧 Challenges & Solutions

| Challenge | Solution |
|---|---|
| Displaying detail without cluttering summary pages | Built a dedicated Drillthrough page for deeper, filtered analysis |
| Giving quick context without extra clicks | Configured a custom Tooltip page to surface Delay Status detail on hover |
| Visualizing route and airport-level performance | Used Map and Filled Map visuals on a dedicated Route & Airport page |
| Keeping DAX organized as the report grew | Maintained all measures in a separate Measures (2) table |
| Making the report easy to navigate | Added action buttons on the Home and other pages for direct page-to-page navigation |

---

## 💡 What I Learned

- How to structure a multi-page Power BI report with a clear navigation flow using **action buttons**
- Practical use of **Drillthrough pages** to let users move from a summary view into focused detail
- Building a **custom tooltip page** to enrich visuals with contextual information on hover
- Using **Map** and **Filled Map** visuals to represent route and location-based data geographically
- The value of keeping **measures in a dedicated table**, separate from raw data fields, for a cleaner model
- Designing consistent visual branding (colors, titles, icons) across multiple report pages for a polished, professional dashboard

---

## 📁 Repository Contents

```
airline-performance-dashboard/
│
├── pr_5.pbix          # Main Power BI file
└── README.md          # Project documentation
```

---

## 👤 Author

**Prerita Morashiya**

Summary Of Data Sources And Transformation

 I downloaded all files  as given in project, which included five separate files covering Employee details, Training records, Engagement survey responses, Performance ratings, and Recruitment applications.

 I imported all five CSV files into Power BI Desktop using the Get Data - Text/CSV option.

 Inside Power Query, I renamed each query to meaningful names - EmployeeMaster, Training, EngagementSurvey, Performance, and Recruitment - so the data model would stay organized.

 I updated the data types for several columns in EmployeeMaster, converting DateOfJoining and DateOfTermination to Date type, Salary to Decimal Number, and Current Employee Rating to Whole Number, so all fields had the correct type for calculations.

 I noticed the DepartmentType column was loading with hidden trailing spaces, so I applied the Trim text tool to clean it up and stop it from displaying with a gap in slicers and chart labels.

 I created a new custom table called DimDate using a Blank Query and M code, generating a continuous calendar of dates along with Year, Quarter, Month_Num, Month_Name, Weekday, and Year_Quarter columns to support time-based analysis.

 I marked DimDate as a Date Table in Model view so Power BI would recognize it correctly for Time Intelligence calculations.

 I went into Model view and created relationships connecting EmployeeMaster to the Training, Performance, and EngagementSurvey tables using Employee ID, and connected DimDate to EmployeeMaster using DateOfJoining as an active relationship and DateOfTermination as an inactive relationship.

 I left the Recruitment table standalone with no relationship, since it does not contain an Employee ID column - applicants in that table are not yet employees.

 I created a separate placeholder table called _Measures using Enter Data, and used this as a dedicated home for all my DAX measures going forward, keeping them organized away from the data tables.

 In the EmployeeMaster table, I created several new calculated columns, including Tenure_Years, Career_Level_Band, Full_Name, Salary_Band, and Is_Active, all evaluated row by row using row context.

 I made sure Tenure_Years and Is_Active were based on the EmployeeStatus column rather than on whether DateOfTermination was blank, since I found that many Active employees in this dataset still carried an old termination date.

 I added more calculated columns afterward -Performance_Label, Salary_Formatted, Days_Since_Hire, Hire_Year_Month, and Above_Avg_Salary_Flag -to support labeling, formatting, and comparison logic.

 In the _Measures table, I created basic explicit measures such as Total_Headcount, Active_Headcount, Terminated_Count, Avg_Salary, Total_Salary_Cost, Avg_Tenure, Distinct_Departments, and Avg_Performance_Rating.

 I then created ratio measures including Attrition_Rate_%, Gender_Diversity_Ratio, and Bench_Utilisation_%, using the DIVIDE function so they would not break with a division-by-zero error.

 I built two iterator measures, Avg_Training_Cost and Total_Training_Cost, using AVERAGEX and SUMX to calculate row-by-row values from the Training table before aggregating them.

 I used CALCULATE combined with ALL and ALLEXCEPT to build Total_HC_All_Depts, Headcount_%_of_Total, and Dept_Avg_Salary_AEXCEPT, which let me remove or restrict filters depending on what each measure needed to show.

 I created High_Performers_Count and High_Performer_% to measure how many active employees were rated highly.

 I used FILTER combined with CALCULATE to build Senior_Headcount, and used RANKX to build Salary_Rank_Dept and Training_Cost_Rank, which ranked departments from highest to lowest.

 I built a set of Time Intelligence measures - YTD_New_Hires using TOTALYTD, New_Hires_SPLY using SAMEPERIODLASTYEAR, New_Hires_YoY_% to compare them, and Hires_Prior_3M using DATEADD.

 I created a final capstone measure called Attrition_Rate_YTD, which combined DATESYTD with USERELATIONSHIP so it could temporarily switch onto the inactive DateOfTermination relationship just for that one calculation.

 While testing Attrition_Rate_YTD, I found it was returning a blank result, so I checked my Manage Relationships list and discovered Power BI had auto-detected incorrect relationships directly between my fact tables (Training and Performance, and Training and EngagementSurvey) instead of routing everything through EmployeeMaster.

 I deleted those incorrect relationships and activated the correct ones - EmployeeMaster to Performance, and EngagementSurvey to EmployeeMaster -  which restored a clean data model and fixed the blank measure.

 I also extended my DimDate table's date range further into the future, since it was originally only built through 2024 and Time Intelligence functions relying on TODAY() needed current dates available to calculate against.

 I formatted all my percentage measures to show as Percentage with one decimal place, and all my salary-related measures to show as Currency.

 I built eight KPI cards and arranged them across two rows for my Workforce Overview page, and additional KPI cards for my Attrition Analysis page.

 I built several core visuals, including a bar chart of Active Headcount by Department, a bar chart of Average Salary by Department with a reference line, a column chart comparing Annual Hiring against the Same Period Last Year, a line chart of YTD Hires by Month, a donut chart of Career Level Band distribution, a matrix showing Performance Distribution by Department, and a table ranking departments by salary.

 I added slicers for Year, Department, and Career Level Band, and used them to test filter context by clicking through different departments and observing which measures recalculated and which stayed fixed.

 I organized everything into two separate report pages - Workforce Overview and Attrition Analysis placing the relevant KPI cards, visuals, and slicers on each page based on what each page was meant to analyse.

 I went through a formatting pass on all the visuals, applying consistent title styling, data labels, bar colors, and alignment, and fixed some KPI cards that had extra white space around them by adjusting their padding and background settings.

 I also adjusted the background color settings on my matrix and donut chart, since some of the text was hard to read against the page background, and changed the font colors to keep everything legible.

 Finally, I added a short description to every measure through the Properties panel, ran a validation check confirming that Active_Headcount plus Terminated_Count equals Total_Headcount for every department, and took a screenshot of my Model view showing all the tables and relationships in their final, corrected state.

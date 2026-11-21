**HR Workforce & Attrition Dashboard (Power BI)**

An executive-level Power BI report that shows where, when and why employees leave, so HR leaders can decide where to act first. Built for managers and above, with every visual driven by DAX and responsive to slicers.

Screenshots: add images/dashboard-overview.png here once the report is published.

**Business Problem**

Leadership knew turnover was high but could not see where it was concentrated, how quickly people left, or which drivers the business could actually influence. The goal was a one-page view that answers four questions:

Where are we losing people (departments, managers, hiring channels)?
When did exits happen, and how quickly after hire?
Why do people leave?
What should HR do about it?
Dataset
Tab-delimited HR extract: 3,310 employee records, 36 columns
Covers employment status, department, manager, position, pay rate, recruitment source, performance score, engagement and satisfaction scores, hire and termination dates, and termination reason
Hire dates span 2006–2017; terminations span 2010–2018
Tools and apps
Area	Tool
Report and modelling	Power BI Desktop
Data preparation	Power Query (M)
Calculations	DAX (measures and calculated columns)
Custom visuals	HTML Content (AppSource) for styled, data-driven cards and bar charts
Native visuals	Column charts, cards, slicers
Prototyping	Claude (AI-assisted) for the dashboard mockup and design iteration
Version control	Git / GitHub
Skills demonstrated
Data modelling and cleaning: trimming text fields, converting dd-mm-yy dates with the right locale, handling blanks, and building calculated columns for tenure bands
Advanced DAX: CALCULATE, ADDCOLUMNS, TOPN, EXCEPT, UNION, CONCATENATEX, PERCENTILEX.INC, MEDIANX, REMOVEFILTERS, and variable-based patterns
Dynamic HTML in DAX: measures that return styled HTML, so bars, colours, legends and narrative text update with slicers
Dynamic narrative: insight sentences generated from the selected data
Data quality judgement: finding and working around an unreliable flag (see below)
Executive storytelling: leading with insights, then evidence, then actions
Dashboard design: visual hierarchy, colour with meaning (orange = needs attention), consistent card styling, accessible contrast
Stakeholder communication: translating analysis into recommendations HR can act on
Report layout
Insight strip: three headline findings that update with filters
KPI cards: employee records, current workforce, attrition rate, voluntary attrition rate, average engagement, average satisfaction
Where are we losing people? Attrition rate by department
When did exits happen? Terminations by year, with the peak highlighted and partial years flagged
Why do people leave? Share of voluntary exits by reason, with addressable reasons highlighted
Manager hotspots: highest and lowest attrition among managers with 100+ employees
Engagement by department and hiring channel retention
How fast do people leave? Tenure at exit: 25th percentile, median, 75th percentile, plus a tenure band chart
Key metrics
Metric	Definition	Value
Employee records	All rows in the file	3,310
Current workforce	Active + Leave of Absence	2,171
Exits	Voluntarily Terminated + Terminated for Cause	959
Attrition rate	Exits ÷ employee records	29.0%
Voluntary attrition rate	Voluntary exits ÷ employee records	24.1%
Average engagement	Mean survey score (1–5)	3.38
Average satisfaction	Mean rating (1–5)	3.89
Key findings
Attrition is concentrated. Production (36.0%) and Software Engineering (33.0%) run well above the 29% company rate. Production alone accounts for over 80% of all exits. IT/IS is 16.0%, Sales 8.7% and Admin 5.0%.
Exits peaked in 2015 at 276, more than double most other years. 2017 and 2018 look like partial years.
Over 40% of voluntary exits are addressable. Unhappiness (18.9%), more money (13.0%) and hours (8.9%) together make up 40.9%. Taking "another position" (20.1%) is the single largest reason, but the data does not say why.
People leave early. A quarter of leavers go within about 7 months, the median is 1.6 years, and three quarters leave within 2.9 years.
Manager results vary widely. Among managers with 100+ employees, three lose over half their teams (51–85%), while three stay under 4%.
Engagement is lowest where attrition is highest. Software Engineering scores 2.89 out of 5, the lowest of any department.
Hiring channel matters. Attrition ranges from under 6% for website banner and Google pay-per-click hires to over 40% for search engine, billboard and newspaper hires. Employee referrals sit at 22%.
Recommendations for HR
Launch a targeted retention plan for Production and Software Engineering. Run stay interviews, benchmark pay (Production has the lowest average hourly rate), and review scheduling and hours. These two groups drive most of the problem.
Review the highest-attrition manager teams. Offer leadership support and compare practices with the managers who retain well. Interpret with care: manager rates partly reflect department mix.
Fix the first year. With a quarter of leavers gone in about seven months, introduce a structured 30/60/90-day onboarding, buddy system and early check-ins.
Act on the addressable drivers. Pay competitiveness, flexible hours and day-to-day experience account for roughly 41% of voluntary exits and are the quickest wins.
Shift recruitment spend toward channels that retain. Test referrals, banner and pay-per-click channels against the high-attrition ones, and track quality of hire by source. Check whether channel results are driven by the roles each channel hires for.
Investigate low engagement in Software Engineering. Pair the survey score with exit-interview themes to find root causes.
Improve data capture. Standardise how exits are flagged, and record the reason behind "another position" (pay, career growth or leadership) so the largest driver becomes actionable.
Data quality notes
The Termd flag disagrees with EmploymentStatus for 397 active employees, so attrition is defined from EmploymentStatus throughout.
The Executive Office has only 24 records, so its figures are low-confidence.
Manager and recruitment-channel views show association, not causation.
Attrition is calculated on all records, including 180 future starts. A stricter version could exclude them from the denominator.
DAX highlights
DAX
Attrition Rate =
DIVIDE (
    CALCULATE (
        COUNTROWS ( HRDATA ),
        HRDATA[EmploymentStatus] IN { "Voluntarily Terminated", "Terminated for Cause" }
    ),
    COUNTROWS ( HRDATA )
)
DAX
Median Tenure at Exit (Yrs) =
MEDIANX (
    FILTER (
        HRDATA,
        HRDATA[EmploymentStatus] IN { "Voluntarily Terminated", "Terminated for Cause" }
    ),
    DATEDIFF ( HRDATA[DateofHireMain], HRDATA[Termination], DAY ) / 365.25
)

The HTML Content visuals use measures that build styled <div> bars and text with CONCATENATEX, so colours, rankings and sentences respond to slicers.

Limitations and next steps
Add cost-of-attrition estimates using pay rate and replacement cost assumptions
Add a pay equity and performance-versus-attrition page
Add drill-through from each visual to employee-level detail
Add a predictive layer for flight risk using engagement, tenure and manager signals
Suggested repo structure
├── README.md
├── data/            (sample or synthetic data only)
├── report/          (.pbix or .pbip files)
├── dax/             (measures and calculated columns)
├── images/          (screenshots)
└── docs/            (mockup, data dictionary)
About the author

Lola, data analyst working with Power BI, DAX and the Microsoft Fabric and Power Platform ecosystem.

LinkedIn: https://www.linkedin.com/in/lolaolumoyin
Email: funmilola.olumoyin@gmail.com

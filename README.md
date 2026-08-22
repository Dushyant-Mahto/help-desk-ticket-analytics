# IT Incident & Ticket Analytics Dashboard

An end-to-end data analytics project analyzing **66,691 IT tickets** to understand ticket workload, resolution performance, ownership, priority, workflow complexity, and operational bottlenecks.

The project uses **Python/Pandas for data cleaning and exploratory analysis** and **Tableau for interactive dashboard development**.

---

## 📌 Project Overview

IT support teams generate large volumes of tickets that vary significantly in priority, complexity, ownership, issue type, and resolution time.

The objective of this project is to analyze historical ticket data and answer key operational questions such as:

- How many tickets are being generated?
- What proportion of tickets are resolved?
- Which issue types generate the most workload?
- Are assigned tickets resolved faster than unassigned tickets?
- How does ticket priority affect resolution time?
- Does workflow complexity correspond to longer resolution times?
- Are tickets with more communication/comments taking longer to resolve?
- Which projects generate the highest ticket volume?
- Where are potential operational bottlenecks?

The analysis transforms raw ticket data into operational KPIs and actionable insights through Python and Tableau.

---

# 🎯 Business Objectives

The main objectives of the project are:

1. Measure overall ticket workload.
2. Analyze ticket resolution performance.
3. Identify unresolved and unassigned ticket populations.
4. Understand the relationship between priority and resolution time.
5. Analyze workflow complexity and its impact on resolution.
6. Investigate the relationship between comment activity and resolution time.
7. Identify high-volume issue types and projects.
8. Identify potential operational bottlenecks.
9. Provide data-driven recommendations for improving ticket management.

---

# 📊 Dataset Overview

The dataset contains **66,691 IT issue/ticket records**.

The original dataset contained workflow-related fields as well as ticket metadata.

For the analysis, only the fields necessary for workload, resolution, ownership, priority, and workflow analysis were retained.

### Selected Columns

| Column | Description |
|---|---|
| `id` | Unique ticket identifier |
| `issue_num` | Issue number |
| `issue_proj` | Project associated with the ticket |
| `issue_reporter` | Ticket reporter |
| `issue_assignee` | Person/team assigned to the ticket |
| `issue_contr_count` | Number of contributors |
| `issue_type` | Type of issue |
| `issue_priority` | Ticket priority |
| `issue_created` | Ticket creation timestamp |
| `issue_resolution_date` | Ticket resolution timestamp |
| `issue_resolution` | Resolution outcome |
| `issue_status` | Current ticket status |
| `issue_comments_count` | Number of comments |
| `last_change_date` | Last modification timestamp |
| `wf_total_time` | Total workflow time |
| `processing_steps` | Number of processing steps |

---

# 🛠️ Tools & Technologies

### Programming & Data Analysis

- Python
- Pandas
- NumPy
- Jupyter Notebook

### Data Visualization

- Tableau

### Version Control

- Git
- GitHub

---

# 🔄 Project Workflow

```text
Raw Dataset
     │
     ▼
Data Exploration
     │
     ▼
Column Selection
     │
     ▼
Data Cleaning
     │
     ▼
Missing Value Analysis
     │
     ▼
Feature Engineering
     │
     ▼
Resolution & Workflow Analysis
     │
     ▼
Exploratory Data Analysis
     │
     ▼
Tableau Dashboard
     │
     ▼
Operational Insights
     │
     ▼
Recommendations
```

---

# 🧹 Data Preparation

The raw dataset was first inspected to understand its structure, data types, missing values, categorical distributions, and numerical distributions.

The dataset contained:

- **66,691 records**
- **16 selected analytical columns**

### Missing Values

The major missing-value patterns were:

| Column | Missing Values |
|---|---:|
| `issue_assignee` | 31,047 |
| `issue_resolution_date` | 853 |
| `issue_resolution` | 853 |
| `last_change_date` | 1 |

The missing values were analyzed based on their business meaning rather than blindly removed.

For example, missing `issue_assignee` values were retained because they represent **unassigned tickets**, which is itself an important operational metric.

Similarly, missing resolution timestamps indicate tickets without a valid resolution timestamp and were not treated as resolved tickets.

---

# 🧮 Feature Engineering

Several analytical fields were created during the analysis.

## Resolution Status

Tickets were classified into resolved and unresolved categories based on the availability of a valid resolution timestamp.

The resulting distribution was:

| Resolution Status | Tickets |
|---|---:|
| Resolved | 29,231 |
| Unresolved | 37,460 |
| **Total** | **66,691** |

Therefore:

**Resolution Rate = 29,231 / 66,691 ≈ 43.8%**

---

## Resolution Time

Resolution time was calculated using the difference between:

```text
Issue Resolution Date - Issue Created Date
```

The result was converted into hours.

Only tickets with a valid resolution timestamp were included in resolution-time analysis.

Because resolution time contains significant outliers, **median resolution time** was used as the primary performance metric rather than average resolution time.

---

## Assignment Status

Tickets were categorized as:

- Assigned
- Unassigned

Missing values in `issue_assignee` were treated as unassigned tickets.

This allowed the analysis to investigate whether ticket ownership is associated with resolution performance.

---

## Workflow Complexity

Workflow complexity was derived from the number of processing steps.

Tickets were grouped into:

- Low
- Medium
- High
- Very High

This feature was used to investigate whether more complex workflows require longer resolution times.

---

# 📈 Key Dataset Statistics

## Ticket Resolution

| Metric | Value |
|---|---:|
| Total Tickets | 66,691 |
| Resolved Tickets | 29,231 |
| Unresolved Tickets | 37,460 |
| Resolution Rate | ~43.8% |

---

## Resolution Time

For tickets with a valid resolution timestamp:

| Metric | Value |
|---|---:|
| Tickets with resolution time | 28,496 |
| Mean | ~1,903 hours |
| Median | ~266 hours |
| 75th Percentile | ~1,167 hours |
| Maximum | ~91,967 hours |

The substantial difference between the mean and median demonstrates that the resolution-time distribution is highly right-skewed.

Therefore, median resolution time is used as the primary performance metric.

---

# 📊 Tableau Dashboard

The final Tableau dashboard provides an interactive overview of IT ticket operations.

The dashboard focuses on workload, resolution performance, ticket ownership, priority, workflow complexity, and project-level workload.

---

# 🎯 Dashboard KPIs

The dashboard contains four primary KPIs.

## 1. Total Tickets

### 66,691

Represents the total number of tickets in the dataset.

---

## 2. Resolution Rate

### ~43.8%

Represents the proportion of tickets with a valid resolution.

```text
29,231 / 66,691 × 100 ≈ 43.8%
```

---

## 3. Median Resolution Time

### ~244 hours in Tableau

The Tableau dashboard currently displays approximately **244 hours**.

The Python analysis produced a median of approximately **266 hours** for the 28,496 records included in that calculation.

Because the two values may be based on slightly different Tableau/Python filtering or calculation logic, the dashboard value should be interpreted as the **Tableau dashboard KPI**, while the Python result is retained as the analytical reference.

Median resolution time is preferred over average resolution time because the dataset contains significant long-running tickets and extreme outliers.

---

## 4. Unassigned Tickets

### 31,047

Represents tickets where no assignee was recorded.

This is a significant operational metric because ticket ownership is strongly associated with resolution performance in the analyzed population.

---

# 📊 Dashboard Visualizations

## 1. Ticket Volume Over Time

A line chart showing ticket creation volume over time.

This visualization helps identify periods of increased or decreased operational workload.

### Business Question

> How has ticket workload changed over time?

### Key Observation

Ticket volume varies significantly across the available historical period, indicating changing workload levels over time.

---

# 2. Median Resolution Time by Comment Activity

This visualization compares ticket comment activity with median resolution time.

Higher comment activity can indicate:

- Additional troubleshooting
- User clarification
- Cross-team communication
- Multiple investigation cycles
- Escalation
- Additional coordination

### Business Question

> Are tickets requiring more communication also taking longer to resolve?

Comment activity can potentially act as an indicator of tickets requiring additional attention.

---

# 3. Median Resolution Time by Workflow Complexity

This visualization compares resolution time across:

- Low
- Medium
- High
- Very High

### Business Question

> Does workflow complexity correspond to longer resolution times?

The analysis produced the following results:

| Workflow Complexity | Ticket Count | Median Resolution |
|---|---:|---:|
| Low | 11,667 | ~379 hrs |
| Medium | 13,257 | ~167 hrs |
| High | 3,197 | ~507 hrs |
| Very High | 375 | ~1,342 hrs |

Very High complexity tickets have the longest median resolution time.

High-complexity tickets also require substantially more time to resolve than Medium-complexity tickets.

---

# 4. Median Resolution Time by Priority

This bar chart compares median resolution time across ticket priorities.

| Priority | Ticket Count | Median Resolution |
|---|---:|---:|
| Highest | 1,845 | ~77 hrs |
| Blocker | 618 | ~91 hrs |
| High | 3,973 | ~116 hrs |
| Lowest | 45 | ~167 hrs |
| Low | 406 | ~188 hrs |
| Medium | 11,623 | ~222 hrs |
| Unknown | 9,986 | ~728 hrs |

### Business Question

> How does ticket priority relate to resolution performance?

### Key Observation

Higher-priority tickets generally show lower median resolution times than Medium and Unknown-priority tickets.

This may indicate that high-severity tickets receive faster escalation or more immediate attention.

The significantly higher resolution time for tickets with **Unknown priority** also highlights the importance of maintaining complete priority information.

---

# 5. Ticket Volume by Issue Type

This visualization shows the distribution of tickets across issue types.

The major issue types include:

| Issue Type | Ticket Count |
|---|---:|
| Ticket | 45,275 |
| Service | 5,300 |
| Subtask | 5,290 |
| Story | 4,538 |
| HD Service | 1,686 |
| Task | 1,540 |
| Vacation | 856 |
| Project | 842 |
| Epic | 403 |
| Deployment | 350 |
| Retrospective | 241 |
| Sprint Summary | 208 |
| Assistance | 109 |
| Bug | 53 |

### Business Question

> Which types of issues generate the largest operational workload?

### Key Observation

The `Ticket` category represents the majority of the dataset and therefore contributes the largest share of operational workload.

---

# 6. Resolution Rate by Priority

This visualization compares resolution rates across ticket priorities.

### Business Question

> Are higher-priority tickets being resolved at different rates than lower-priority tickets?

This analysis helps determine whether priority classification corresponds with different resolution outcomes.

It also highlights the potential impact of tickets with unknown or incomplete priority information.

---

# 7. Median Resolution Time by Assignment

This visualization compares resolution time between:

- Assigned tickets
- Unassigned tickets

The Python analysis showed:

| Assignment Status | Ticket Count | Median Resolution |
|---|---:|---:|
| Assigned | 19,414 | ~188 hrs |
| Unassigned | 9,082 | ~837 hrs |

### Business Question

> Does ticket ownership correspond with faster resolution?

### Key Observation

Unassigned tickets have a substantially higher median resolution time than assigned tickets.

This makes ticket ownership one of the most important operational findings from the analysis.

> **Important:** This analysis identifies an association between assignment status and resolution time. It does not prove that assignment itself directly causes faster resolution.

---

# 8. Median Resolution Time Distribution

This visualization shows the distribution of ticket resolution times.

The resolution-time distribution is strongly right-skewed.

| Metric | Value |
|---|---:|
| Count | 28,496 |
| Mean | ~1,903 hrs |
| Median | ~266 hrs |
| 75th Percentile | ~1,167 hrs |
| Maximum | ~91,967 hrs |

The mean is significantly higher than the median because of a relatively small number of extremely long-running tickets.

### Business Question

> How widely does ticket resolution time vary?

---

# 9. Top 10 Projects by Ticket Volume

This visualization identifies the ten projects generating the largest number of tickets.

Examples of high-volume projects include:

| Project | Ticket Count |
|---|---:|
| t.n2 | 2,213 |
| C06hg2xcu | 1,994 |
| C13ggb_0 | 1,522 |
| dx8a | 1,474 |
| C06ggzcz0 | 1,289 |
| C06ggn039 | 1,251 |
| C01ggx0z2 | 979 |
| C01ggz-3 | 942 |
| db6 | 932 |
| C13gg20 | 864 |

### Business Question

> Which projects generate the highest support workload?

High-volume projects may represent systems or applications requiring additional monitoring, support capacity, or root-cause investigation.

---

# 🔍 Key Findings

## 1. Large Unresolved Ticket Population

The dataset contains:

- **66,691 total tickets**
- **29,231 resolved tickets**
- **37,460 unresolved tickets**

This produces an overall resolution rate of approximately:

### 43.8%

More than half of the tickets do not have a valid resolution timestamp.

This indicates that backlog and ticket lifecycle management are important areas for operational improvement.

---

# 2. Ticket Workload Is Highly Concentrated

The largest issue categories are:

| Issue Type | Tickets |
|---|---:|
| Ticket | 45,275 |
| Service | 5,300 |
| Subtask | 5,290 |
| Story | 4,538 |
| HD Service | 1,686 |
| Task | 1,540 |

The `Ticket` category represents the majority of the dataset.

This suggests that general ticket-based support represents the largest component of operational workload.

---

# 3. Assignment Is Strongly Associated With Resolution Time

The analysis showed a substantial difference between assigned and unassigned tickets.

| Assignment Status | Tickets | Median Resolution |
|---|---:|---:|
| Assigned | 19,414 | ~188 hrs |
| Unassigned | 9,082 | ~837 hrs |

Unassigned tickets have a median resolution time more than four times higher than assigned tickets.

### Operational Recommendation

Introduce an ownership SLA for newly created tickets.

For example:

```text
Ticket Created
      ↓
Assignment Required
      ↓
No Assignment Within SLA
      ↓
Automatic Escalation
      ↓
Team Lead / Support Queue
```

This could reduce the time tickets remain without an owner.

---

# 4. Higher-Priority Tickets Generally Have Faster Resolution

Higher-priority tickets generally have lower median resolution times.

The observed medians were approximately:

- Highest: **77 hours**
- Blocker: **91 hours**
- High: **116 hours**
- Medium: **222 hours**
- Unknown: **728 hours**

This may indicate that high-severity tickets receive faster escalation or greater operational attention.

However, priority alone should not be interpreted as a causal factor.

---

# 5. Unknown Priority Is an Important Data Quality Issue

Approximately:

**33,965 tickets**

have an `unknown` priority in the overall dataset.

This represents a substantial portion of the dataset.

Tickets with unknown priority also show a much higher median resolution time in the analyzed resolved population.

### Operational Recommendation

Improve priority classification at ticket creation.

Possible approaches include:

- Mandatory priority selection
- Priority assignment rules
- Automated priority classification
- Validation rules
- Periodic data-quality audits

Improved priority completeness would make SLA and workload analysis more reliable.

---

# 6. Workflow Complexity Is Associated With Resolution Time

The workflow analysis produced:

| Complexity | Tickets | Median Resolution |
|---|---:|---:|
| Low | 11,667 | ~379 hrs |
| Medium | 13,257 | ~167 hrs |
| High | 3,197 | ~507 hrs |
| Very High | 375 | ~1,342 hrs |

Very High complexity tickets have the longest median resolution time.

This suggests that highly complex tickets may involve additional:

- Processing stages
- Approvals
- Dependencies
- Validation
- Monitoring
- Cross-team coordination

### Operational Recommendation

High and Very High complexity tickets should be monitored separately and considered for early escalation.

---

# 7. Resolution Time Is Highly Skewed

The resolution-time statistics demonstrate a significant difference between mean and median:

| Metric | Hours |
|---|---:|
| Mean | ~1,903 |
| Median | ~266 |
| 75th Percentile | ~1,167 |
| Maximum | ~91,967 |

The mean is substantially higher than the median.

This indicates that a relatively small number of extremely long-running tickets significantly influence the average.

Therefore, median resolution time is more representative of typical ticket performance.

---

# 8. Ticket Volume Changes Significantly Over Time

Annual ticket volumes include:

| Year | Ticket Count |
|---|---:|
| 2007 | 457 |
| 2008 | 1,103 |
| 2009 | 2,157 |
| 2010 | 3,133 |
| 2011 | 2,966 |
| 2012 | 3,071 |
| 2013 | 2,442 |
| 2014 | 2,845 |
| 2015 | 5,543 |
| 2016 | 7,053 |
| 2017 | 5,524 |
| 2018 | 1,212 |
| 2019 | 2 |
| 2020 | 7 |
| 2021 | 4,284 |
| 2022 | 6,542 |
| 2023 | 1,755 |

Ticket volume varies considerably across the historical period.

Extremely large year-over-year growth percentages in years with very small ticket volumes should be interpreted cautiously.

For example, the increase from 2019 to 2020 appears very large in percentage terms, but the underlying counts were only 2 and 7 tickets.

---

# 9. Comment Activity Can Indicate Ticket Complexity

The dashboard investigates the relationship between comment activity and resolution time.

Higher comment activity can potentially indicate:

- Multiple troubleshooting iterations
- User clarification
- Escalation
- Cross-team collaboration
- Complex investigation
- Additional coordination

Therefore, unusually high comment activity may be useful as an early warning signal for tickets requiring additional attention.

---

# 10. Support Workload Is Concentrated Across Projects

The Top 10 Projects visualization demonstrates that ticket volume is not evenly distributed across projects.

High-volume projects may represent:

- High-demand applications
- Critical systems
- Recurring issue sources
- Systems requiring additional support
- Opportunities for automation

### Operational Recommendation

Projects consistently appearing among the highest-volume projects should be reviewed for recurring incidents and potential root-cause improvements.

---

# 💡 Operational Recommendations

## 1. Reduce Unassigned Ticket Backlog

Introduce an ownership SLA for newly created tickets.

A simple process could be:

```text
Ticket Created
      ↓
Assignment Required
      ↓
Assignment SLA
      ↓
Not Assigned
      ↓
Automatic Escalation
```

This can help reduce the amount of time tickets remain without an owner.

---

## 2. Monitor High-Complexity Tickets

Create a dedicated monitoring process for High and Very High complexity tickets.

Review these tickets for:

- Excessive processing steps
- Approval bottlenecks
- Cross-team dependencies
- Long waiting periods
- Repeated validation
- Monitoring delays

---

## 3. Improve Priority Classification

The large number of tickets with unknown priority indicates a data-quality opportunity.

Improving priority classification can help:

- Improve SLA monitoring
- Improve workload prioritization
- Improve escalation decisions
- Improve dashboard accuracy
- Improve operational reporting

---

## 4. Monitor Long-Running Tickets

Because resolution time is highly skewed, operational teams should not rely exclusively on average resolution time.

Recommended metrics include:

- Median resolution time
- 75th percentile resolution time
- 90th percentile resolution time
- Number of tickets exceeding SLA
- Number of aging unresolved tickets

---

## 5. Focus on High-Volume Projects

Projects consistently appearing in the Top 10 by ticket volume should be investigated for:

- Recurring incidents
- System reliability problems
- Process inefficiencies
- Automation opportunities
- Additional staffing requirements

---

## 6. Use Comment Activity as an Early Warning Signal

Tickets accumulating unusually high numbers of comments can be flagged for review.

These tickets may require:

- Escalation
- Additional technical expertise
- Cross-team coordination
- User clarification
- Root-cause investigation

---

# 🧠 Business Questions Answered

## Workload

### Which issue types generate the most tickets?

General `Ticket` issues represent the majority of the dataset and therefore contribute the largest share of operational workload.

---

## Resolution

### How quickly are tickets being resolved?

Resolution time is highly variable.

The Python analysis produced a median resolution time of approximately **266 hours** for tickets with valid resolution timestamps.

The Tableau dashboard currently displays approximately **244 hours**, depending on the dashboard calculation/filtering.

---

## Ownership

### Does assignment correspond with resolution performance?

Yes.

Assigned tickets show a substantially lower median resolution time than unassigned tickets:

- Assigned: ~188 hours
- Unassigned: ~837 hours

This represents a strong association between ticket ownership and resolution performance.

---

## Priority

### Do higher-priority tickets receive faster resolution?

Higher-priority tickets generally show lower median resolution times than Medium and Unknown-priority tickets.

---

## Workflow

### Does workflow complexity correspond with longer resolution times?

Very High complexity tickets have the longest median resolution time at approximately **1,342 hours**.

---

## Communication

### Is comment activity associated with resolution time?

The Tableau dashboard investigates whether increasing comment activity corresponds with longer resolution cycles.

Higher comment activity can potentially indicate increased troubleshooting and coordination requirements.

---

## Trend

### How does ticket volume change over time?

Ticket volume varies significantly across the historical dataset, with particularly high volumes in 2015–2017 and 2021–2022.

---

## Projects

### Which projects generate the highest workload?

The Top 10 Projects analysis identifies a relatively small group of projects contributing a significant amount of ticket volume.

---

# 📈 KPI Definitions

| KPI | Definition |
|---|---|
| Total Tickets | Total number of ticket records |
| Resolution Rate | Resolved tickets divided by total tickets |
| Median Resolution Time | Median time between ticket creation and resolution |
| Unassigned Tickets | Tickets without an assigned owner |
| Ticket Volume | Number of tickets created within a selected period |
| Workflow Complexity | Category based on ticket processing steps |

---

# ⚠️ Analytical Considerations

## Resolution-Time Population

Resolution-time metrics are calculated only for tickets with valid resolution timestamps.

Therefore, resolution-time metrics should not be interpreted as representing all 66,691 tickets.

---

## Mean vs Median

The resolution-time distribution contains significant outliers.

For this reason, median resolution time is used as the primary performance metric.

---

## Assignment Analysis

The relationship between assignment status and resolution time represents an **association**, not proof of causation.

Other factors such as ticket priority, complexity, issue type, and project may also influence resolution time.

---

## Priority Data Quality

A significant number of tickets have unknown priority.

Therefore, priority-based analysis should be interpreted with awareness of incomplete priority classification.

---

## Historical Data Variation

Ticket volume changes considerably across years.

Years with extremely small ticket counts can produce misleading percentage growth rates.

Absolute ticket counts should therefore be considered alongside percentage changes.

---

# 📁 Suggested Repository Structure

```text
IT-Incident-Ticket-Analytics/
│
├── data/
│   └── issues_clean.csv
│
├── notebooks/
│   └── incident_ticket_analysis.ipynb
│
├── dashboard/
│   └── IT_Incident_Dashboard.twbx
│
├── images/
│   └── dashboard.png
│
└── README.md
```

---

# 📌 Key Skills Demonstrated

## Data Analysis

- Exploratory Data Analysis
- Data Cleaning
- Missing Value Analysis
- Outlier Analysis
- Descriptive Statistics
- Aggregation
- Trend Analysis
- KPI Development
- Feature Engineering

## Python

- Pandas
- NumPy
- Datetime manipulation
- GroupBy operations
- Aggregations
- Data transformation
- Missing-value handling

## Tableau

- Interactive dashboards
- KPI cards
- Time-series visualization
- Bar charts
- Performance analysis
- Filtering
- Dashboard design
- Business-focused storytelling

## Business & Operational Analytics

- IT incident analytics
- Helpdesk analytics
- Ticket lifecycle analysis
- Resolution performance
- Workload analysis
- Bottleneck identification
- Operational KPI analysis
- Data-driven recommendations

---

# 🚀 Future Improvements

Potential future enhancements include:

- SLA compliance analysis
- Ticket aging analysis
- Resolution-time percentiles
- Automated anomaly detection
- Root-cause analysis of recurring issues
- Predictive ticket resolution modeling
- Ticket volume forecasting
- Automated BI reporting
- Machine learning for resolution-time prediction

---

# 🏁 Conclusion

This project demonstrates how large-scale IT ticket data can be transformed into actionable operational insights using Python and Tableau.

The analysis highlights important relationships between:

- Ticket ownership
- Priority
- Workflow complexity
- Comment activity
- Ticket volume
- Resolution performance
- Project workload

One of the strongest findings is the substantial difference in resolution time between assigned and unassigned tickets.

The analysis also shows that Very High workflow complexity is associated with significantly longer resolution times, while higher-priority tickets generally demonstrate faster resolution.

The final Tableau dashboard provides an interactive operational view that can help support teams identify:

- Workload concentration
- Resolution bottlenecks
- Unassigned ticket backlog
- High-complexity tickets
- Priority-related performance differences
- High-volume projects
- Potential opportunities for process improvement

Overall, the project demonstrates an end-to-end analytics workflow from **raw IT ticket data → data cleaning → feature engineering → exploratory analysis → Tableau dashboard → business insights → operational recommendations**.

---

# 👨‍💻 Skills

**Python | Pandas | NumPy | Tableau | Data Cleaning | EDA | Data Visualization | KPI Development | Business Analytics | IT Operations Analytics**

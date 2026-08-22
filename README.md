# IT Incident & Ticket Analytics Dashboard

An end-to-end data analytics project analyzing **13,460 IT tickets** to understand ticket workload, resolution performance, ownership, priority, workflow complexity, and operational bottlenecks.

The project uses **Python/Pandas for data cleaning and exploratory analysis** and **Tableau for interactive dashboard development**.

🔗 **[View Live Dashboard on Tableau Public](https://public.tableau.com/views/HelpdeskTicketOperationsDashboard/HelpdeskTicketOperationsDashboard?:language=en-US&:display_count=n&:origin=viz_share_link)**

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

The dataset contains **13,460 IT issue/ticket records** after cleaning and correction.

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

**Programming & Data Analysis:** Python, Pandas, NumPy, Jupyter Notebook
**Data Visualization:** Tableau
**Version Control:** Git, GitHub

---

# 🔄 Project Workflow

\`\`\`text
Raw Dataset → Data Exploration → Column Selection → Data Cleaning
→ Missing Value Analysis → Feature Engineering → Resolution & Workflow Analysis
→ Exploratory Data Analysis → Tableau Dashboard → Operational Insights → Recommendations
\`\`\`

---

# 🧹 Data Preparation

Missing values were treated based on business meaning rather than removed outright. For example, missing `issue_assignee` values were retained because they represent **unassigned tickets** — an operational metric in its own right. Missing resolution timestamps indicate tickets that were not resolved and were treated accordingly.

---

# 🧮 Feature Engineering

- **Resolution Status** — tickets classified as resolved/unresolved based on a valid resolution timestamp.
- **Resolution Time** — `issue_resolution_date − issue_created`, converted to hours. Because this distribution is heavily right-skewed, **median** is used as the primary metric rather than mean.
- **Assignment Status** — Assigned vs. Unassigned, with missing `issue_assignee` treated as Unassigned.
- **Workflow Complexity** — derived from `processing_steps`, grouped into Low / Medium / High / Very High.

---

# 📈 Key Dataset Statistics

## Ticket Resolution

| Metric | Value |
|---|---:|
| Total Tickets | 13,460 |
| Resolution Rate | 40.02% |
| Unassigned Tickets | 6,344 |

## Resolution Time

| Metric | Value |
|---|---:|
| Median Resolution Time | ~237.6 hours |

The resolution-time distribution remains right-skewed, consistent with earlier analysis — median is used as the representative metric rather than mean.

---

# 📊 Tableau Dashboard

The final Tableau dashboard provides an interactive overview of IT ticket operations, covering workload, resolution performance, ticket ownership, priority, workflow complexity, and project-level workload.

---

# 🎯 Dashboard KPIs

## 1. Total Tickets
### 13,460

## 2. Resolution Rate
### 40.02%
Approximately 5,388 resolved / 8,072 unresolved tickets.

## 3. Median Resolution Time
### ~237.6 hours
Median is used over mean because the dataset contains significant long-running tickets and extreme outliers.

## 4. Unassigned Tickets
### 6,344
Represents tickets with no recorded assignee — a key operational metric, since ownership is strongly associated with resolution speed (see below).

---

# 📊 Dashboard Visualizations

## 1. Ticket Volume Over Time
A line chart showing ticket creation volume by month.

**Business Question:** How has ticket workload changed over time?
**Key Observation:** Volume dips noticeably in the May–June period before climbing steadily from September through December.

---

## 2. Median Resolution Time by Priority

| Priority | Relative Median Resolution |
|---|---|
| unknown | Highest (~630 hrs, approx.) |
| Low | ~310 hrs (approx.) |
| Medium | ~290 hrs (approx.) |
| Highest | ~130 hrs (approx.) |
| Blocker | ~30 hrs (approx.) |
| Lowest | ~20 hrs (approx.) |
| High | Lowest (~65 hrs, approx.) |

*(Values read from chart proportions — pull exact figures via Tableau's "View Data" to replace these approximations.)*

**Key Observation:** Tickets with `unknown` priority again show a much higher resolution time than any classified priority, reinforcing that incomplete priority data is a genuine operational blind spot — not just a labeling issue.

---

## 3. Resolution Rate by Priority

Ordered highest to lowest: **Blocker > High > Low > Highest > Lowest > Medium > unknown** (approximate, read from chart — exact percentages not labeled).

**Key Observation:** Blocker-priority tickets are resolved at a substantially higher rate than any other category, while `unknown`-priority tickets have the lowest resolution rate — priority completeness affects not just speed but whether tickets get resolved at all.

---

## 4. Median Resolution Time by Issue Type

Epic, Bug, and Subtask issue types show dramatically higher median resolution times (Epic highest, in the 15,000+ hour range) compared to all other issue types, which cluster near zero on the same scale.

**Key Observation:** This is a large gap — Epics and Bugs likely represent longer-running, multi-stage work rather than single-touch tickets, and should probably be reported on a separate scale from routine tickets rather than blended into overall averages.

---

## 5. Ticket Volume by Issue Type

| Issue Type | Ticket Count |
|---|---:|
| Ticket | 7,721 |
| Task | 1,462 |
| Subtask | 1,271 |
| Story | 923 |
| Service | 742 |
| Project | 535 |
| Vacation | 328 |
| HD Service | 269 |
| Deployment | 71 |

**Key Observation:** The `Ticket` category still represents the majority of workload, consistent with the earlier analysis.

---

## 6. Median Resolution Time by Assignment

| Assignment Status | Relative Median Resolution |
|---|---|
| Assigned | ~165 hrs (approx.) |
| Unassigned | ~695 hrs (approx.) |

*(Exact values not labeled on chart — confirm via Tableau data export.)*

**Key Observation:** Unassigned tickets still take roughly 4x longer to resolve than assigned ones — this remains one of the strongest and most consistent findings across both dataset versions.

> This is an association, not proof of causation — other factors (priority, complexity, issue type) may also drive the difference.

---

## 7. Median Resolution Time by Workflow Complexity

| Workflow Complexity | Median Resolution (hrs) |
|---|---:|
| Low | 476 |
| Medium | 115 |
| High | 527 |
| Very High | 1,246 |

**Key Observation:** Very High complexity tickets remain the slowest to resolve by a wide margin. Interestingly, Medium complexity resolves *faster* than Low complexity in this corrected dataset — worth a closer look at what distinguishes those two buckets before writing a firm recommendation here.

---

## 8. Median Resolution Time by Comment Activity

Resolution time stays relatively flat and low from "No Comments" through "Medium" activity, then rises sharply at "High" comment activity (approx. 3-4x the baseline).

**Business Question:** Are tickets requiring more communication also taking longer to resolve?
**Key Observation:** High comment activity is associated with markedly longer resolution times — a plausible early-warning signal for tickets needing escalation.

---

## 9. Top 10 Projects by Ticket Volume

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

This breakdown is unchanged from the original analysis — the top 10 projects and their exact counts hold consistent across both dataset versions.

---

# 🔍 Key Findings

## 1. Resolution Rate Is Low
Only **40.02%** of tickets have a valid resolution — a meaningful backlog/lifecycle management concern.

## 2. Ticket Workload Is Concentrated
The `Ticket` issue type accounts for the majority of volume (7,721 of 13,460), consistent with prior analysis.

## 3. Assignment Is Strongly Associated With Resolution Time
Unassigned tickets take roughly 4x longer to resolve than assigned ones (~695 hrs vs. ~165 hrs, approx.).

**Recommendation:** Introduce an ownership SLA — tickets unassigned past a defined window should auto-escalate to a team lead or support queue.

## 4. Priority Data Quality Remains an Issue
Tickets with `unknown` priority show both the highest resolution time and the lowest resolution rate among all priority levels.

**Recommendation:** Make priority selection mandatory at ticket creation, with validation rules to prevent `unknown` from being the default.

## 5. Workflow Complexity Drives Resolution Time — With a Twist
Very High complexity tickets remain the slowest (1,246 hrs median), but Medium complexity now resolves faster than Low complexity (115 hrs vs. 476 hrs) — a pattern worth investigating before finalizing a complexity-based SLA policy, since it wasn't present in the earlier dataset version.

## 6. Comment Activity Signals Risk
Tickets with high comment counts take noticeably longer to resolve — a candidate early-warning flag for support teams.

## 7. Support Workload Is Concentrated Across a Few Projects
The same 10 projects continue to dominate ticket volume — `t.n2` and `C06hg2xcu` alone account for over 4,200 tickets combined.

---

# 💡 Operational Recommendations

1. **Reduce unassigned ticket backlog** with an ownership SLA and automatic escalation.
2. **Investigate the Low vs. Medium complexity reversal** before building complexity-based routing rules.
3. **Improve priority classification** at ticket creation — mandatory fields, validation rules, periodic audits.
4. **Report on Epic/Bug resolution time separately** from routine tickets, given the scale difference.
5. **Use high comment activity as an early-warning flag** for tickets needing escalation or additional expertise.
6. **Focus process-improvement efforts on the top 10 projects**, which account for a disproportionate share of volume.

---

# ⚠️ Analytical Considerations

- **Recalculated dataset:** This version reflects a corrected ticket count (13,460) and recalculated KPIs, superseding an earlier draft based on 66,691 records.
- **Chart values without labels:** Priority resolution times, resolution rate by priority, assignment resolution time, issue-type resolution hours, and comment-activity resolution time were read from chart proportions, not data labels. Confirm exact figures via Tableau's "View Data" export before finalizing any published version of this README.
- **Mean vs. median:** Resolution time remains right-skewed; median is the primary metric throughout.
- **Assignment analysis:** Represents an association between ownership and resolution speed, not causation.

---

# 🏁 Conclusion

This project demonstrates how large-scale IT ticket data can be transformed into actionable operational insights using Python and Tableau. The strongest, most consistent finding across both dataset versions is the substantial resolution-time gap between assigned and unassigned tickets. Priority-data completeness and workflow complexity continue to be meaningful drivers of resolution performance, while the corrected dataset surfaces a new pattern — the Low/Medium complexity reversal — worth investigating further.

The final Tableau dashboard gives support teams an interactive view into workload concentration, resolution bottlenecks, unassigned backlog, high-complexity tickets, priority-driven performance gaps, and high-volume projects.

---

# 👨‍💻 Skills

**Python | Pandas | NumPy | Tableau | Data Cleaning | EDA | Data Visualization | KPI Development | Business Analytics | IT Operations Analytics**

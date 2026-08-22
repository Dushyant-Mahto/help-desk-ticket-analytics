# IT Incident & Helpdesk Ticket Analytics

## 📌 Project Overview

This project analyzes a large-scale IT helpdesk and issue-tracking dataset containing **66,691 tickets** to understand ticket volume, resolution performance, workflow complexity, assignment effectiveness, and operational workload.

The project was designed from an **IT operations / incident management perspective**, with the goal of answering practical questions such as:

- How does ticket volume change over time?
- What percentage of tickets are resolved?
- How long does it take to resolve tickets?
- Does ticket priority affect resolution time?
- Does assigning a ticket to an owner improve resolution speed?
- Does workflow complexity increase resolution time?
- Does comment activity correlate with resolution time?
- Which issue types generate the most workload?
- Which projects generate the highest ticket volume?

The analysis combines **Python/Pandas for data cleaning and exploratory analysis** with **Tableau for interactive dashboarding and business insights**.

---

## 🎯 Business Objective

The primary objective is to identify operational bottlenecks and factors associated with slower ticket resolution.

The analysis focuses on five major areas:

1. **Ticket Volume**
2. **Resolution Performance**
3. **Priority & Severity**
4. **Assignment & Ownership**
5. **Workflow Complexity**

These insights can help IT support teams identify areas where workload, ownership, prioritization, or workflow processes may be affecting service performance.

---

## 📊 Dataset

The dataset contains approximately **66,691 issue records** and includes information about:

- Issue/project identifiers
- Reporter and assignee
- Issue type
- Priority
- Creation and resolution timestamps
- Resolution status
- Number of comments
- Workflow processing time
- Number of workflow processing steps

### Key Fields

| Column | Description |
|---|---|
| `id` | Unique issue identifier |
| `issue_num` | Issue number |
| `issue_proj` | Project identifier |
| `issue_reporter` | Issue reporter |
| `issue_assignee` | Assigned user |
| `issue_type` | Type of issue |
| `issue_priority` | Issue priority |
| `issue_created` | Ticket creation timestamp |
| `issue_resolution_date` | Resolution timestamp |
| `issue_resolution` | Resolution outcome |
| `issue_status` | Current issue status |
| `issue_comments_count` | Number of comments |
| `wf_total_time` | Total workflow processing time |
| `processing_steps` | Number of workflow processing steps |

---

# 🔧 Data Preparation

The raw dataset was cleaned and transformed using Python and Pandas.

### Main preprocessing steps

- Converted timestamp columns to datetime format
- Examined missing values
- Identified unresolved tickets
- Created resolution status indicators
- Calculated ticket resolution time
- Categorized assignment status
- Categorized priority availability
- Categorized workflow complexity
- Created time-based features for trend analysis
- Validated resolution and status relationships
- Removed/handled invalid records where required for resolution-time analysis

### Resolution Time

Resolution time was calculated as:

```text
Resolution Time = Issue Resolution Date - Issue Created Date

# IT Incident Management Analytics & SLA Breach Prediction

## Overview

This project demonstrates an end-to-end IT Incident Management Analytics solution built using Python, MySQL, SQL, Power BI, and Machine Learning.

The objective was to transform raw IT incident event logs into actionable business insights through data engineering, dimensional modeling, business intelligence dashboards, and predictive analytics.

The project follows a complete analytics workflow:

Raw Event Logs → ETL → Star Schema → SQL Analysis → Power BI Dashboards → SLA Breach Prediction

---

## Business Problem

IT service organizations handle thousands of incidents every month. Managing these incidents efficiently is critical for maintaining service quality and meeting Service Level Agreements (SLAs).

This project answers key operational questions such as:

- What is the current SLA compliance rate?
- Which support teams handle the highest workload?
- Which categories generate the most incidents?
- Which teams and categories contribute most to SLA breaches?
- How does incident complexity impact resolution time?
- Can we predict SLA breaches before they occur?

---

## Technology Stack

### Data Engineering

- Python
- Pandas
- NumPy

### Database

- MySQL
- SQLAlchemy

### Analytics

- SQL
- MySQL Workbench

### Visualization

- Power BI

### Machine Learning

- Scikit-Learn
- Logistic Regression

### Version Control

- Git
- GitHub

---

# Dataset

The dataset consists of IT Incident Event Logs.

Each incident contains multiple lifecycle events such as:

- New
- Active
- Awaiting User Information
- Resolved
- Closed

The event-level dataset was transformed into a single-row-per-incident fact table for reporting and analytics.

---

# Project Workflow

```text
Raw Incident Event Log
            │
            ▼
      Python ETL
            │
            ▼
     Data Cleaning
            │
            ▼
 Fact Table Creation
            │
            ▼
   Star Schema Model
            │
            ▼
      MySQL Database
            │
            ▼
      SQL Analysis
            │
            ▼
   Power BI Dashboard
            │
            ▼
 SLA Breach Prediction
```

---

# Data Engineering & ETL

## Data Cleaning

Performed the following preprocessing steps:

- Converted date fields to datetime format
- Handled missing values
- Removed duplicates
- Standardized categorical fields
- Validated incident lifecycle records

---

## Fact Table Creation

The event log was transformed into a fact table where each row represents a unique incident.

### Fact Table

`fact_incidents`

### Key Metrics

- Incident Open Date
- Incident Resolution Date
- Incident Close Date
- MTTR (Mean Time to Resolution)
- SLA Status
- Reassignment Count
- Reopen Count
- System Modification Count
- Complexity Score

---

# Dimensional Modeling

A star schema was created to support reporting and analytical workloads.

## Fact Table

- fact_incidents

## Dimension Tables

- dim_date
- dim_priority
- dim_category
- dim_support_team

### Star Schema

```text
                  dim_date
                      │
                      │
dim_priority ── fact_incidents ── dim_support_team
                      │
                      │
                dim_category
```

---

# Business KPIs

## Executive KPIs

- Total Incidents
- SLA Compliance %
- SLA Breach %
- Average MTTR
- Median MTTR
- Critical Incident Count

## Operational KPIs

- Reassignment Rate
- Reopen Rate
- Average Updates per Incident
- Team SLA Performance
- Team MTTR

## Complexity KPIs

- Average Complexity Score
- Average Reassignments
- Average Reopens
- Average Update Count

---

# SQL Analysis

Business-focused SQL analysis was performed to answer operational questions.

## Executive Analysis

- Incident Volume Trend
- SLA Trend
- MTTR Trend

## Priority Analysis

- Priority Distribution
- Priority vs SLA
- Priority vs MTTR

## Team Analysis

- Team Workload
- Team SLA Performance
- Team MTTR

## Category Analysis

- Category Volume
- Category SLA
- Category MTTR

## Time Analysis

- Incidents by Month
- Incidents by Day of Week
- Weekend vs Weekday SLA
- Peak Incident Hours
- Peak Resolution Hours

## Complexity Analysis

- Complexity vs MTTR
- Complexity vs SLA
- Complexity by Team
- Complexity by Category

---

# Complexity Score Engineering

A custom complexity metric was developed to quantify incident handling effort.

## Formula

```text
Complexity Score =
sys_mod_count + (2 × reassignment_count)
```

## Why Complexity Score?

The score captures:

- Incident handling effort
- Routing inefficiencies
- Escalation frequency
- Operational complexity

Complexity was found to have a strong relationship with MTTR and SLA performance.

---

# Power BI Dashboards

## Dashboard 1 — Executive Overview

### KPIs

- Total Incidents
- SLA Compliance %
- SLA Breach %
- Average MTTR
- Median MTTR
- Critical Incident Count

### Visuals

- Incident Trend
- SLA Trend
- Priority Distribution
- Category Distribution

### Objective

Provide leadership with a high-level view of operational health and service quality.

---

## Dashboard 2 — Operations Dashboard

### KPIs

- Reassignment Rate
- Reopen Rate
- Average Updates

### Visuals

- Team Workload
- Team SLA Performance
- Team MTTR
- Category SLA
- Category Volume

### Objective

Identify overloaded teams, operational bottlenecks, and service issues.

---

## Dashboard 3 — Complexity Dashboard

### KPIs

- Average Complexity Score
- Average Updates
- Average Reassignments
- Average Reopens

### Visuals

- Complexity vs MTTR
- Complexity vs SLA
- Complexity by Team
- Complexity by Category
- Top 10 Complex Incidents

### Objective

Understand how operational complexity impacts performance and SLA outcomes.

---

## Drill-Through Pages

### Team Performance

Detailed team-level investigation including:

- Incident Volume
- SLA Performance
- MTTR
- Category Distribution

### Category Analysis

Detailed category-level root cause analysis including:

- Incident Trends
- SLA Performance
- Team Distribution

### SLA Investigation

Focused investigation of SLA-breached incidents including:

- Breach Drivers
- Team Performance
- Category Performance
- Incident Details

---

# Key Findings

### Finding 1

Incident complexity shows a strong positive relationship with MTTR.

Higher complexity incidents require significantly longer resolution times.

### Finding 2

Support teams with higher reassignment activity experience lower SLA performance.

### Finding 3

A small number of categories account for a disproportionate share of incident volume.

### Finding 4

Reassignments and update counts are strong indicators of operational complexity.

---

# SLA Breach Prediction

## Objective

Predict whether an incident will breach SLA using operational characteristics.

## Features Used

- Priority
- Category
- Assignment Group
- Complexity Score
- Reassignment Count
- Reopen Count
- System Modification Count

## Target Variable

```text
0 = SLA Met
1 = SLA Breached
```

## Model

- Logistic Regression

## Evaluation Metrics

- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix

## Feature Importance

The model identifies the strongest drivers of SLA breaches and highlights operational factors that increase risk.

---

# Business Recommendations

### Recommendation 1

Reduce ticket reassignments through automated routing and ownership assignment.

### Recommendation 2

Develop knowledge articles and self-service solutions for recurring incident categories.

### Recommendation 3

Introduce escalation workflows for high-complexity incidents.

### Recommendation 4

Monitor teams with consistently high SLA breach rates.

### Recommendation 5

Use SLA breach prediction as an early-warning mechanism for proactive intervention.

---

# Repository Structure

```text
IT-Incident-Management-Analytics/
│
├── data/
│   └── incident_event_log.csv
│
├── notebooks/
│   ├── data_loading_reorganized.ipynb
│   └── sla_breach_prediction.ipynb
│
├── dashboard/
│   └── IT_Incident_Analytics.pbix
│
├── screenshots/
│   ├── executive_dashboard.png
│   ├── operations_dashboard.png
│   ├── complexity_dashboard.png
│   ├── findings_recommendations.png
│   └── sla_investigation.png
│
├── README.md
│
└── requirements.txt
```

---

# Skills Demonstrated

## Data Engineering

- ETL Development
- Data Cleaning
- Data Transformation
- Dimensional Modeling

## SQL

- Business Analytics
- KPI Reporting
- Aggregations
- Performance Analysis

## Business Intelligence

- Dashboard Design
- KPI Development
- Interactive Reporting
- Drill-Through Analytics

## Machine Learning

- Feature Engineering
- Predictive Modeling
- Logistic Regression
- Model Evaluation

## Business Analysis

- Root Cause Analysis
- SLA Monitoring
- Operational Analytics
- Recommendation Development

---

## Author

**Aditya Gupta**

Data Analytics | Business Intelligence | SQL | Python | Power BI | Machine Learning

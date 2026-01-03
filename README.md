# Motor Claims Analytics Dashboard (Power BI + PostgreSQL)

A portfolio project that simulates a **Head of Claims / Claims Ops** dashboard for motor insurance: monitoring claim volume & cost trends, triaging incident drivers, and profiling fraud risk signals.

**Tech stack:** Power BI (semantic model + DAX), PostgreSQL (staging + star-schema warehouse)  
**Live dashboard:** [Click to view](https://app.powerbi.com/view?r=eyJrIjoiMDAzYjAzMTItN2E5YS00OWEyLWE5NjYtMjVhMzRiMTI1YWRjIiwidCI6ImRmNDZiODE3LTJkMWYtNGNiZS04ZDQzLTgxNWU3Y2MwOWUxYyIsImMiOjEwfQ%3D%3D)
**Data source:** Kaggle — Auto Insurance Claims Data (CSV)  
https://www.kaggle.com/datasets/buntyshah/auto-insurance-claims-data

---

## What this project demonstrates

- Designing a **claims operations dashboard** from raw claims data
- Building a **star schema** in PostgreSQL (facts + dimensions)
- Creating reusable DAX patterns for:
  - **MTD / PMTD** comparisons (anchored to last complete month)
  - **MoM %** and **percentage-point deltas**
- Delivering “business-ready” pages:
  - **Key Trends** (exec overview)
  - **Incident Triage** (drivers + drill)
  - **Fraud Profile** (risk segmentation + candidate queue)

---

## Report pages (screenshots)

### 1) Key Trends (MTD + MoM view)
<img width="2212" height="1240" alt="Key Trends" src="https://github.com/user-attachments/assets/0c9b7245-602a-401d-a766-8061dc74d267" />


### 2) Incident Triage (drivers of paid / cost + exploratory analysis)
<img width="2264" height="1270" alt="Incident Triage" src="https://github.com/user-attachments/assets/50d76b7d-4847-4ba7-94bb-d0d21ff8882c" />


### 3) Fraud Profile (risk signals + segmentation + high-value cases)
<img width="2252" height="1266" alt="Fraud Profile" src="https://github.com/user-attachments/assets/b9b45c7e-c0dc-407e-a691-164d20942cb3" />


---

## Business questions covered

### Key Trends
- What is **MTD total paid** and how does it compare to **PMTD**?
- Are we seeing changes in:
  - claim count, average cost per claim, fraud rate?
- Which **incident types / collision types / geographies** dominate MTD?

### Incident Triage
- Which segments drive **total paid** the most (severity, incident type, vehicle age)?
- Which factors correlate with **higher average cost per claim** (Key Influencers)?
- When do claims spike by **hour of day** and severity mix?

### Fraud Profile
- Which segments show **higher fraud lift** vs baseline (quadrant bubble charts)?
- What are the strongest “signals” associated with fraud flags (Key Influencers)?
- Which high-paid cases should be reviewed first (triage table)?

---

## Data model (Star schema)

The semantic model in Power BI is backed by a PostgreSQL warehouse with this structure:

**Fact**
- `fact_claims` — one row per claim/policy record (depending on dataset granularity)

**Dimensions**
- `dim_date` — date attributes (Year, Month, WeekdayName, etc.)
- `dim_vehicle` — make/model/year + derived vehicle age bands
- `dim_insured` — demographic/insured attributes
- `dim_policy` — policy attributes (premium, deductible, limits)
- `dim_incidentdetails` — incident attributes (state, city, severity, collision type, etc.)

---

## Repository structure (suggested)


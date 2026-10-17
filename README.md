# Telco Customer Churn Analysis & Retention Strategy

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power_Query-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-00585E?style=for-the-badge&logo=microsoft&logoColor=white)
![Data Analytics](https://img.shields.io/badge/Data_Analytics-4682B4?style=for-the-badge&logo=data&logoColor=white)

An end-to-end data analytics project focused on evaluating customer attrition (churn) within a telecommunications enterprise. By processing and analyzing demographic, operational, service-level, and financial data across **7,048 customer accounts**, this project identifies key drivers of churn and delivers actionable retention strategies to maximize Customer Lifetime Value (CLV).

---

## 📋 Executive Summary

Acquiring new customers in the telecom industry costs up to **5x more** than retaining existing ones. This project analyzes churn behavior to pinpoint vulnerable customer cohorts, quantify service-level risk factors, and establish an automated Power Query data transformation pipeline to power an interactive executive report.

### Key Metrics
* **Total Customers:** 7,048
* **Overall Churn Rate:** 26.52%
* **Total Churned Accounts:** 1,869
* **Identified High-Risk Active Segment:** 633 accounts

---

## 📁 Repository Structure

```
├── telco_churn_unclean.csv               # Raw transactional dataset
├── Telco Customer Churn Analysis.pbip    # Power BI Project File / Dashboard
├── Telco Customer Churn Report.pdf       # Executive Summary PDF Report
└── README.md                             # Project Documentation
```

---

## 🧹 Data Cleaning & Transformation (Power Query ETL)

Before visual modeling in Power BI, raw data (`telco_churn_unclean.csv`) underwent structured data transformation in Power Query to ensure analytical validity:

1. **TotalCharges Blank & Error Handling:**
   * Handled empty/non-numeric strings corresponding to new accounts with `tenure < 1 month`.
   * Cast column to `Decimal Number` and handled errors by imputing `0` for new accounts.
2. **MonthlyCharges Normalization:**
   * Stripped currency symbols (`$`, ` `) from text fields.
   * Converted values to `Decimal Number`.
3. **Contract Column Standardization:**
   * Standardized text casing and formatting (e.g., unified `"month to month"` and `"Month-to-month"` into `"Month-to-month"`).
4. **Whitespace Elimination:**
   * Applied `Transform -> Format -> Trim` across all categorical text attributes (`Payment Method`, `Internet Service`, `Gender`, `Churn`) to remove leading/trailing spaces.
5. **Logical Consistency & Conditional Mapping:**
   * Enforced strict domain business logic:
     * If `PhoneService = 'No'`, set `MultipleLines = 'No'`.
     * If `InternetService = 'No'`, set all add-on services (`OnlineSecurity`, `DeviceProtection`, `TechSupport`, `StreamingTV`, etc.) to `'No'`.

---

## 📊 Core Findings & Risk Profiles

### 1. Contract Type Vulnerability
* **Month-to-Month:** Accounts for **88%+** of total customer churn.
* **1-Year & 2-Year Contracts:** Show high stability with **<3%** churn on 2-year commitments.

### 2. Onboarding & Tenure Band Impact
Churn is heavily front-loaded during initial customer onboarding:
* **0–6 Months Tenure:** **53% Churn Rate** *(Highest Risk Cohort)*
* **6–12 Months Tenure:** **36% Churn Rate**
* **12+ Months Tenure:** **17% Churn Rate**

### 3. Internet Service Breakdown
| Internet Service Type | Total Base | Churned Volume | Risk Category & Impact |
| :--- | :--- | :--- | :--- |
| **Fiber Optic** | 3,096 | 1,297 | **High Risk** (Represents 69.4% of all churn) |
| **DSL** | 2,421 | 459 | **Moderate Risk** |
| **No Internet Service** | 1,531 | 113 | **Low Risk / Stable Base** |

---

## 💡 Strategic Business Recommendations

1. **90-Day Early Onboarding Interventions:**
   * Deploy dedicated onboarding guides and proactive check-ins for new subscribers during their first 6 months to curb the **53% early-stage churn**.
2. **Contract Conversion Campaigns:**
   * Offer promotional discounts, free add-on services, or speed upgrades to incentive Month-to-Month customers to transition to 1-Year or 2-Year agreements.
3. **Fiber Optic Service & Pricing Audit:**
   * Investigate network reliability, service delivery, and relative price competitiveness for Fiber Optic lines, given that Fiber Optic accounts represent nearly **70% of total churned volume**.
4. **Proactive Outreach for High-Risk Retained Accounts:**
   * Target the **633 active high-risk accounts** identified in the Power BI dashboard with automated loyalty perks and proactive tech support before cancellation occurs.

---

## 🛠️ Tools & Technologies Used
* **Power BI Desktop:** Interactive dashboard design & visual analytics.
* **Power Query (M):** ETL pipeline, data cleaning, and conditional formatting.
* **DAX (Data Analysis Expressions):** Key measures, churn rates, and cohort segmentation logic.
* **PDF / Markdown:** Executive report publishing and documentation.

---

## 🚀 How to Run the Project

1. Clone or download this repository.
2. Ensure Power BI Desktop is installed on your machine.
3. Open the `Telco Customer Churn Analysis` file (or connect `telco_churn_unclean.csv` to Power BI).
4. Review the Power Query transformations in **Transform Data** to inspect the M-code steps.
5. Interact with the dashboard visuals, slicers, and tenure drill-downs.

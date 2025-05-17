# 🚀 Loan Default & Risk Analysis Power BI Showcase 📊
Dashboard: https://app.powerbi.com/view?r=eyJrIjoiMWZhMzYxODctOTg0ZC00ZWRkLTgzMWEtMTlkYzllZDliMTg0IiwidCI6IjVlN2I1ODA0LTEyZmYtNDM0OC1hODFlLWQ5MDAwNjM0MGM5NiJ9

## 🌟 Project Overview

This repository showcases a comprehensive **3-in-1 Power BI project** analyzing a loan default dataset of approximately **260,000 applicants**. The project demonstrates end-to-end Business Intelligence capabilities, from **data sourcing and transformation** to **advanced DAX calculations** and **insightful visualizations**, all geared toward providing actionable insights for financial risk assessment and decision-making.

The core of this project lies in its ability to dissect complex loan data, identify patterns in defaults, understand applicant demographics, and calculate key financial risk metrics. It leverages **Power BI Dataflows** for efficient data management, connecting directly to a **Microsoft SQL Server** source, and incorporates **incremental refresh** for optimal performance with large datasets.

---

## 🎯 Project Modules

This project is structured into three interconnected analytical dashboards:

### 1️⃣ 🏦 Loan Default Overview & Trends
![Image](https://github.com/user-attachments/assets/3565bfef-0436-43ae-b8dc-0d5f28befd0b)
Figure 1: Loan Default Overview & Trends
- Identifies patterns and key drivers of loan defaults.
- Visualizes default rates across dimensions like employment type and loan purpose.
- Tracks trends over time, including Year-over-Year (YoY) changes.

### 2️⃣ 👥 Applicant Demographics & Financial Profile
![Image](https://github.com/user-attachments/assets/f6530143-0c90-476d-9074-fe1e0ac24042)
Figure 2: Applicant Demographics & Financial Profile
- Deep dive into applicant characteristics.
- Analyzes links between demographics (age, education, marital status) and financial behavior (income, credit score, DTI).
- Segments applicants to understand financial capacity and diversity.

### 3️⃣ 📈 Financial Risk Metrics & Advanced Analysis
![Image](https://github.com/user-attachments/assets/c8937adb-2a4b-400a-8f50-f80f730f3ec9)
Figure 3: Financial Risk Metrics & Advanced Analysis
- Provides key financial indicators for risk assessment.
- Calculates metrics like average and median loan amounts, YoY, and YTD trends.
- Uses advanced DAX logic for segmentation (e.g., by mortgage, dependents, credit score).

---

## 🛠️ Skills & Technologies Demonstrated

### 🔧 Power BI (Advanced)
- **Data Modeling:** Star schema, relationships, hierarchies.
- **DAX Expertise:** 
  - `CALCULATE`, `FILTER`, `DIVIDE`, `AVERAGEX`, `ALLEXCEPT`, `MEDIANX`, `SWITCH`, etc.
  - Time intelligence: `SAMEPERIODLASTYEAR`, `TOTALYTD`.
- **Power Query Editor:** Data profiling, transformation, cleaning.
- **Visualization:** Donut, clustered column, line charts, decomposition trees.
- **Validation:** KPI integrity and result accuracy.

### 🌐 Dataflows & ETL
- Power BI Service Dataflows for cloud-based ETL.
- SQL Server integration via Standard Gateway Mode.
- Incremental refresh setup for large datasets.

### 📊 Business Analytics
- Financial & demographic segmentation.
- KPI creation for risk assessment.
- Data storytelling via structured dashboards.

---

## ⚙️ Project Workflow & Key Steps

1. **Data Source Setup**
   - Installed Microsoft SQL Server.
   - Imported ~260,000-row dataset into SQL Server.

2. **Dataflow Creation & Management**
   - Created Dataflow to connect to SQL Server.
   - Enabled scheduled refresh and incremental refresh in Power BI Service.

3. **Power BI Desktop Development**
   - Imported data from Dataflow.
   - Performed transformations and profiling in Power Query Editor.
   - Developed calculated columns and DAX measures:
     - `Loan Amount by Purpose`: `SUMX`, `FILTER`, `ISBLANK`
     - `Average Income by Employment Type`: `CALCULATE`, `AVERAGE`, `ALLEXCEPT`
     - `Default Rate by Employment`: `COUNTROWS`, `DIVIDE`, `ALLEXCEPT`
     - `Average Loan by Age Group`: `AVERAGEX`, `VALUES`
     - `Default Rate by Year`: `CALCULATE`, `FILTER`, `DIVIDE`
     - `YOY & YTD Measures`, `MEDIANX`, `SWITCH`, etc.
   - Designed dashboards using interactive visuals.
   - Validated all key calculations across pages.

4. **Publishing & Sharing**
   - Published report to Power BI Service.
   - Set up scheduled refresh.
   - Enabled report sharing and access control.

---

## 📊 Dataset Overview

The dataset includes these key attributes:

| Column Name        | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| `LoanID`           | Unique loan identifier.                                                     |
| `Age`              | Applicant's age.                                                            |
| `Income`           | Annual income.                                                              |
| `LoanAmount`       | Total approved/requested loan amount.                                       |
| `CreditScore`      | Credit score (300–850 range).                                               |
| `MonthsEmployed`   | Total months employed.                                                      |
| `NumCreditLines`   | Number of active credit lines.                                              |
| `InterestRate`     | Annual interest rate (APR).                                                 |
| `LoanTerm`         | Duration of the loan in months.                                             |
| `DTIRatio`         | Debt-to-Income ratio.                                                       |
| `Education`        | Highest education level.                                                    |
| `EmploymentType`   | Full-Time, Part-Time, Self-Employed, etc.                                   |
| `MaritalStatus`    | Single, Married, Divorced, etc.                                             |
| `HasMortgage`      | Indicates existing mortgage (Yes/No).                                       |
| `HasDependents`    | Indicates dependents (Yes/No).                                              |
| `LoanPurpose`      | Purpose of loan (e.g., Education, Debt Consolidation).                      |
| `HasCoSigner`      | Indicates if a co-signer exists (Yes/No).                                   |
| `Default`          | Whether the loan was defaulted (Yes/No).                                    |
| `Loan Date`        | Date the loan was issued (DD/MM/YYYY).                                      |
| `Credit Categories`| Custom categorization of credit score ranges.                              |

> ⚠️ Additional columns and measures were created in Power BI for deeper analysis.

---

## 💡 Highlighted DAX Measures & Use Cases

```DAX
-- Default Rate by Employment Type
DefaultRate = 
DIVIDE(
    CALCULATE(COUNTROWS(Data), Data[Default] = "Yes"),
    CALCULATE(COUNTROWS(Data))
)

-- YOY Loan Amount Change
YOY Loan Amount = 
CALCULATE(
    SUM(Data[LoanAmount]),
    SAMEPERIODLASTYEAR(Data[Loan Date])
)

-- Median Loan by Credit Category
MedianLoanByCreditCategory =
MEDIANX(
    VALUES(Data[Credit Categories]),
    CALCULATE(AVERAGE(Data[LoanAmount]))
)

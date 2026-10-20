# Meridian Retail Group — Solstice Launch Performance Analysis (SOL-VASE-14)

![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=flat&logo=microsoft-excel&logoColor=white)
![Data Cleaning](https://img.shields.io/badge/Data_Cleaning-Data_Wrangling-blue)
![Business Insights](https://img.shields.io/badge/Analytics-Executive_Decision_Support-orange)

## 📌 Project Overview
Meridian Retail Group (MRG) conducted a regional product launch across three Nigerian hubs (Abuja, Lagos, and Port-Harcourt) for its flagship decorative line, featuring the **Solstice Ceramic Vase (`SOL-VASE-14`)**. 

As part of the post-launch review for **Elena Cross (VP, Product Launch)**, this project audits raw operational logs, resolves inventory record discrepancies, evaluates regional sell-through velocity, and provides data-backed recommendations on whether to repeat the launch approach next quarter.

---

## 🎯 Business Problem & Objectives
1. **Audit & Data Cleansing:** Identify and remediate data hygiene issues, clerical errors, and fragmented schemas within raw operational records.
2. **Stock Verification:** Resolve an upstream warehouse count anomaly affecting Port-Harcourt's inventory ledger.
3. **Regional & Launch Performance Analysis:** Evaluate sell-through dynamics, Day 1 vs. Day 2 sales distribution, and customer adoption across regional markets.
4. **Strategic Decision Support:** Provide an executive-level verdict and actionable recommendations regarding future launch iterations.

---

## 🛠️ Data Wrangling & Quality Assurance
The initial raw dataset (`SOL-VASE-14_Raw_Export`, 55 rows) contained significant data quality issues that distorted performance visibility:

* **De-duplication:** Identified and purged **15 exact duplicate records**, yielding an authentic base of **40 records**.
* **Standardization & Whitespace Trimming:**
  * Cleaned 9 fragmented warehouse region entries (`PH`, `ph`, `lagos`, ` Abuja`, `Lagos  `, etc.) into three consistent categories: **Abuja**, **Lagos**, and **Port-Harcourt**.
  * Consolidated disparate SKU/product aliases (`SOL VASE 14`, `sol-vase-14`, etc.) under standard corporate schema **`SOL-VASE-14` / `Solstice Ceramic Vase`**.
* **Missing Value Imputation:** Handled 13 blank sales records in `Units_Sold_LastLaunch` by imputing `0`, recognizing them as active warehouse tracking days without customer orders rather than missing data.
* **Clerical Stock-Count Correction:**
  * **Issue Identified:** On January 6, 2026, Port-Harcourt logged an inventory count of **`25.4`** units on hand. Because ceramic vases are non-divisible goods, this decimal caused Port-Harcourt’s stock total to show as an impossible fraction (`4,608.4`).
  * **Remediation:** Corrected the keystroke error from `25.4` to **`254` units**, bringing Port-Harcourt's verified on-hand stock to **4,837 units** and MRG's total starting stock to **11,112 units**.

---

## 📊 Performance Analysis & Regional Findings

### 1. Cumulative Regional Inventory & Sell-Through

| Warehouse Region | Units on Hand | Units Sold | Initial Stock Available | Sell-Through Rate (%) | Market Share |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Port-Harcourt** | 4,837 | 1,540 | 6,377 | **24.15%** | 51.68% |
| **Lagos** | 4,058 | 955 | 5,013 | **19.05%** | 32.05% |
| **Abuja** | 2,217 | 485 | 2,702 | **17.95%** | 16.28% |
| **Total / Company** | **11,112** | **2,980** | **14,092** | **21.15%** | **100.00%** |

* **Port-Harcourt** led the business across all commercial KPIs, driving more than half (**51.68%**) of nationwide unit volume and achieving the highest regional sell-through.
* **Lagos** demonstrated steady baseline demand, capturing nearly a third of total volume.
* **Abuja** exhibited the lowest conversion velocity despite holding significant allocated stock.

---

### 2. Launch Event Dynamics: Day 1 vs. Day 2 (Unit Price: ₦8,500)

| Region | Day 1 Units | Day 1 Revenue | Day 2 Units | Day 2 Revenue | Total Units | Total Revenue | Regional Share |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Port-Harcourt** | 48 | ₦408,000 | 40 | ₦340,000 | **88** | **₦748,000** | 40.0% |
| **Lagos** | 27 | ₦229,500 | 39 | ₦331,500 | **66** | **₦561,000** | 30.0% |
| **Abuja** | 42 | ₦357,000 | 24 | ₦204,000 | **66** | **₦561,000** | 30.0% |
| **Total** | **117** | **₦994,500** | **103** | **₦875,500** | **220** | **₦1,870,000** | **100.0%** |

* **48-Hour Run Rate:** The launch generated **₦1,870,000 across 220 units**.
* **Launch Decay:** Day 1 captured **53.18%** of total promotional sales, followed by an **11.97% drop** on Day 2.
* **Opposing Regional Trends:** Abuja experienced a **42.86% drop** from Day 1 to Day 2, whereas Lagos picked up momentum on Day 2, growing sales by **44.44%**.

---

## 💡 Executive Verdict & Recommendations
**Verdict: DO NOT repeat the launch approach in its current form.**

1. **Re-align Stock Allocation to Regional Demand Velocity:**
   * Port-Harcourt generated over 50% of total sales volume but held inventory levels comparable to slower-moving hubs. Future allocations must use predictive, demand-weighted distribution rather than arbitrary regional splitting.
2. **Synchronize Launch Calendars:**
   * Staggered go-live timelines created regional marketing blind spots. Launches should go live simultaneously across all digital channels and regional retail showrooms to maximize nationwide promotional buzz.
3. **Implement Input Validation on Inventory Logging:**
   * Upstream warehouse logging systems currently permit floating-point entries on discrete goods (e.g., `25.4`). MRG should enforce strict integer data validation rules and automated reconciliation checks before promotional launches.

---

## 📂 Repository Structure
```plaintext
├── data/
│   ├── raw/
│   │   ├── SOL-VASE-14_Raw_Export.xlsx
│   │   ├── SOL-VASE-14_Day1_Sales.xlsx
│   │   └── SOL-VASE-14_Day2_Sales.xlsx
│   └── processed/
│       └── SOL-VASE-14_Cleaned_Final.xlsx
├── docs/
│   └── Solstice_Launch_Review_Summary.pdf
└── README.md

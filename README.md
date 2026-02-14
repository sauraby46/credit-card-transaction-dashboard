#  Credit Card Transaction Dashboard

![Power BI](https://img.shields.io/badge/power_bi-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![MySQL](https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-00758F?style=for-the-badge&logo=analysis&logoColor=white)

> **An end-to-end Power BI dashboard connected to a MySQL database to monitor credit card transactions, analyze customer spending patterns, and track financial KPIs using advanced DAX.**

---

##  Project Overview

This project is a comprehensive **Credit Card Weekly Dashboard** developed using **Power BI** and **SQL**. The goal was to provide real-time insights into key performance metrics and trends, enabling stakeholders to monitor credit card operations effectively.

The dashboard streamlines data analysis by integrating a SQL database with Power BI, offering a dual view:
1.  **Transaction Report:** Focuses on revenue, interest, and transaction volume analysis.
2.  **Customer Report:** Analyzes customer demographics, spending behavior, and revenue contribution.

---

##  Dashboard Screenshots

### 1. Transaction Report
*Provides a high-level view of revenue trends by quarter, card category, and expenditure type.*

### 2. Customer Report
*Detailed breakdown of customer revenue by job type, education level, and geography.*

---

##  Technical Architecture

**Data Pipeline:** `CSV Data` ➔ `MySQL Database` ➔ `Power BI` ➔ `Dashboard`

1.  **Data Extraction:** Raw data (`credit_card.csv` and `customer.csv`) containing 10,000+ records.
2.  **Data Processing (SQL):** Imported CSV files into a **MySQL** database to simulate a real-world enterprise environment.
3.  **Data Transformation (Power BI):** Connected Power BI to MySQL for real-time data fetching and performed ETL (Extract, Transform, Load) using Power Query.
4.  **Data Modeling:** Established a Star Schema relationship between the `Transaction` and `Customer` tables using `Client_Num`.
5.  **Visualization:** Built interactive dashboards using DAX measures and custom visuals.

---

## 📈 Key Performance Indicators (KPIs)

The following advanced DAX measures were implemented to track financial health:

| KPI Metric | Description |
| :--- | :--- |
| **Total Revenue** | Sum of all revenue streams (Annual fees, Interest, Transaction amounts). |
| **Total Interest Earned** | Interest income generated from credit lines. |
| **Total Transaction Amount** | The total value of all processed transactions. |
| **Total Transaction Volume** | The distinct count of transactions processed. |
| **Avg Utilization Ratio** | Assessing credit risk by measuring credit limit usage. |
| **WoW Change** | Week-over-Week growth or decline in revenue. |

---

##  DAX Queries Used

Below are some of the key DAX formulas used for calculations:

### 1. Age Grouping
```dax
AgeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[customer_age] < 30, "20-30",
 'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
 'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
 'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
 'public cust_detail'[customer_age] >= 60, "60+",
 "unknown"
)
```
### 2. Income Grouping
```dax
IncomeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[income] < 35000, "Low",
 'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
 'public cust_detail'[income] >= 70000, "High",
 "unknown"
)
```
### 3. Week-over-Week Revenue Calculation
```dax
Current_Week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
  ALL('public cc_detail'),
  'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
 )
)

Previous_Week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
  ALL('public cc_detail'),
  'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
 )
)
```
##  Key Insights Derived
Revenue by Category: Blue Cards contribute to 93% of overall transactions.

Top Contributing States: TX (Texas), NY (New York), and CA (California) generate 68% of the total revenue.

Demographics: Customers in the 40-50 age group contribute the highest revenue.

Occupation: Businessmen and White-collar professionals are the highest spending groups.

Activation Rate: The overall activation rate stands at 57.5%, indicating potential for targeted activation campaigns.

##  How to Run This Project
1. Database Setup
Install MySQL Workbench.

Create a new database and import credit_card.csv and customer.csv.

2. Power BI Setup
Download the .pbix file from this repository.

Open Power BI Desktop.

Go to Transform Data -> Data Source Settings.

Update the MySQL server credentials to match your local host.

3. Refresh Data
Click the "Refresh" button in Power BI to load the data from your local SQL server.

## Author
Saurab Yadav [www.linkedin.com/in/saurab-yadav-767615364] | [https://github.com/sauraby46]

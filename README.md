# AI Sales Intelligence

## 📊 Project Overview

**AI Sales Intelligence** is an end-to-end Data Analytics project designed to transform raw sales data into actionable business insights.

The project follows a complete analytics workflow:

**Raw Data → Data Profiling → Data Quality Investigation → Cleaning → Validation → Data Modeling → SQL Analysis → Power BI Dashboard → Business Insights & Recommendations**

The goal was not only to calculate sales KPIs, but to understand **what is happening in the business, why it matters, and what actions the business can take.**

---

## 🎯 Business Objectives

This project focuses on answering key business questions:

* How is overall sales and profitability performing?
* Which products and categories generate the most revenue and profit?
* Which customers contribute the most value?
* Which regions are performing above or below target?
* How effective are discounts?
* What is the return rate and refund impact?
* Which customers are loyal or at risk?
* Which transactions are loss-making?
* Are there data-quality issues that could affect business decisions?

---

## 🗂️ Dataset

The project uses multiple related datasets representing:

* Sales transactions
* Returns
* Customers
* Products
* Dates
* Regions
* Sales and profit targets

### Dataset Scale

| Table     | Records |
| --------- | ------: |
| Sales     |  74,920 |
| Returns   |   4,500 |
| Customers |   6,000 |
| Products  |     180 |
| Dates     |     926 |
| Regions   |      25 |
| Targets   |   1,500 |

---

## 🔎 Data Quality Investigation

Before performing analysis, I investigated the raw data instead of immediately removing unusual records.

### Sales Data

The initial sales dataset contained:

* 75,000 records
* 350 missing discount values
* 80 records with invalid quantity values
* 907 negative-profit transactions
* Inconsistent formatting such as `online` vs `Online`
* Whitespace issue in `UPI ` payment values

After investigation and cleaning:

* 74,920 valid sales records remained
* Missing values were resolved
* Invalid quantity records were removed
* Channel and payment-method values were standardized
* Negative-profit transactions were retained because they represented legitimate business losses rather than data errors

### Return Data

The return dataset contained 4,500 records.

During relational validation, I identified:

* 250 quantity anomalies
* 3 orphan returns

The 3 orphan returns were investigated against the original sales data and were found to correspond to sales records with zero recorded quantity.

Instead of deleting these records, I preserved them with data-quality flags and excluded them from metrics requiring a valid sales-to-return relationship.

This resulted in:

* 4,247 valid returns
* 250 quantity anomalies
* 3 orphan returns

---

## 🧹 Data Cleaning & Validation

The cleaned analytical model was validated using:

* Primary-key checks
* Missing-value checks
* Duplicate checks
* Foreign-key/relationship checks
* Date validation
* Quantity validation
* Sales/cost validation
* Return validation
* Cross-table consistency checks

### Final Model Status

**PASS — Analytical model ready for KPI development**

The final model contains:

```text
sales
return
customer
product
date
region
target
```

---

## 🏗️ Data Model

The project uses a relational analytical model.

```text
                    customer
                       │
                       │
                       ▼
                    sales ──────────► region
                      │
                      │
              ┌───────┴───────┐
              │               │
              ▼               ▼
           product           date


return
  │
  ├──────────────► customer
  │
  ├──────────────► product
  │
  ├──────────────► date
  │
  └──────────────► sales
```

Returns do not contain a direct `Region_ID`. Regional context for returns is reached through:

**return → sales → region**

---

## 🛠️ Tools & Technologies

### Python

Used for:

* Data loading
* Data profiling
* Data quality investigation
* Cleaning
* Validation
* Analytical model preparation

Main libraries:

* Pandas
* NumPy
* SQLite3
* pathlib

### SQL — SQLite

Used for:

* KPI calculations
* Monthly performance
* MoM and YoY growth
* Product ranking
* Customer ranking
* Customer segmentation
* Target vs actual analysis
* Regional ranking
* Product portfolio analysis
* Customer revenue concentration
* Discount effectiveness
* Return analysis
* Seasonality
* RFM analysis
* Channel performance
* Loss-making transaction analysis

### Power BI

Used for:

* Interactive dashboards
* DAX measures
* Time intelligence
* RFM segmentation
* KPI cards
* Slicers
* Drill-through pages
* Business performance analysis

---

## 📈 Key KPIs

The project calculates:

### Sales

* Total Revenue
* Total Cost
* Total Profit
* Profit Margin %
* Total Orders
* Units Sold
* Average Order Value
* Average Selling Price

### Customer

* Unique Customers
* Revenue per Customer
* Repeat Customers
* One-Time Customers

### Discount

* Average Discount %
* Gross Sales
* Discount Amount

### Returns

* Valid Returned Units
* Return Rate %
* Valid Refund Amount
* Refund to Revenue %

### Targets

* Sales Target
* Profit Target
* Revenue Variance
* Revenue Achievement %
* Profit Variance
* Profit Achievement %

### Time Intelligence

* Previous Month Revenue
* MoM Revenue Growth %
* Previous Year Revenue
* YoY Revenue Growth %
* YTD Revenue
* YTD Profit
* YTD Orders
* YTD Revenue Growth %

---

## 🔬 Advanced SQL Analysis

The SQL analysis covers:

1. Monthly Revenue Growth
2. Year-over-Year Growth
3. Product Ranking
4. Customer Ranking
5. Customer Segmentation
6. Target vs Actual Performance
7. Regional Ranking
8. Top & Bottom Product Analysis
9. Customer Revenue Concentration
10. Discount Effectiveness
11. Return & Product Impact
12. Monthly Business Performance
13. Seasonality
14. Customer RFM Segmentation
15. Sales Channel Performance
16. Category Portfolio Analysis
17. Region × Category Analysis
18. Loss-Making Transactions

SQL window functions such as `LAG()`, `RANK()`, `ROW_NUMBER()` and `NTILE()` were used for advanced analysis.

---

## 📊 Power BI Dashboard

The Power BI report contains multiple analytical pages.

### 1. Executive Overview

Provides:

* Revenue
* Profit
* Profit Margin
* Orders
* Units Sold
* AOV
* Return Rate
* Target Achievement
* Revenue and profit trends
* Regional performance
* Channel performance

### 2. Product & Customer Analysis

Provides:

* Top products
* Product revenue vs profit
* Category performance
* Top customers
* Customer revenue concentration
* Loss-making transactions

### 3. Regional & Risk Analysis

Provides:

* Regional revenue and profit
* Target achievement
* Revenue variance
* Return rate by category
* Refund impact
* Return status
* Return reasons
* Data-quality exceptions

### 4. Customer Intelligence

Provides:

* Customer value
* Repeat vs one-time customers
* RFM segmentation
* Customer revenue
* Customer revenue vs profit
* RFM customer-level analysis

### 5. Product Details

Interactive drill-through page for individual products.

### 6. Customer Details

Interactive drill-through page for individual customers.

---

## 👥 RFM Analysis

Customers are evaluated using:

### Recency

How recently the customer purchased.

### Frequency

How many distinct orders the customer made.

### Monetary

How much revenue the customer generated.

Customers are classified into segments including:

* Champions
* Loyal Customers
* Potential Loyalists
* At Risk
* Lost / Low Value
* Regular Customers

This allows business decisions to move from generic customer analysis to **segment-specific actions**.

---

## 💡 Business Insight Framework

The analysis is designed to identify:

### High Revenue + High Margin

Potential products/regions to protect and scale.

### High Revenue + Low Margin

Areas where pricing, discounting or costs should be investigated.

### Below Target

Regions requiring investigation into sales execution and demand.

### High Return Rate

Categories/products requiring investigation into product or fulfillment issues.

### At-Risk Customers

Customers who may benefit from targeted retention or win-back campaigns.

### Loss-Making Transactions

Transactions that may require investigation into pricing, discounting, cost structure or product economics.

---

## 🚨 Data Quality Approach

A key principle of this project was:

> **An unusual value is not automatically an error.**

For example, negative-profit transactions were investigated and retained because they represented legitimate loss-making business transactions.

Similarly, return anomalies were preserved and flagged instead of simply being deleted.

This approach helps prevent data cleaning from removing important business signals.

---

## 📁 Project Structure

```text
AI_Sales_Intelligence/
│
├── data/
│   ├── raw/
│   │   ├── customer.csv
│   │   ├── date.csv
│   │   ├── product.csv
│   │   ├── region.csv
│   │   ├── returns.csv
│   │   ├── sales.csv
│   │   ├── targets.csv
│   │   └── data_dictionary.csv
│   │
│   ├── cleaned/
│   │   ├── sales_clean.csv
│   │   ├── sales_model.csv
│   │   ├── return_model.csv
│   │   ├── customer_model.csv
│   │   ├── product_model.csv
│   │   ├── date_model.csv
│   │   ├── region_model.csv
│   │   └── target_model.csv
│   │
│   └── sales_intelligence.db
│
└── README.md
```

---

## 🚀 Future Improvements

Potential next steps include:

* Automated data refresh
* More advanced customer segmentation
* Predictive sales forecasting
* Customer churn prediction
* Product return prediction
* Automated anomaly detection
* AI-assisted natural-language business querying
* Deployment of the dashboard for business users

---

## 👨‍💻 Project Focus

This project demonstrates an end-to-end Data Analyst workflow rather than only dashboard creation.

The main focus was:

**Data Quality → Data Modeling → SQL → Power BI → Business Thinking**

The ultimate goal is to convert data into **reliable insights and actionable business decisions**.


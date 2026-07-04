# 🛒 E-Commerce Sales Performance Dashboard — Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![CSV](https://img.shields.io/badge/Data-CSV-green?style=for-the-badge&logo=files&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

> **Resume Title:** *E-Commerce Sales Performance Analysis Dashboard using Power BI*

---

## 📌 Project Overview

A **fully interactive 3-page Power BI dashboard** built for **ShopIndia** — a mid-size Indian e-commerce company selling Electronics, Furniture, and Office Supplies across India.

This project simulates a **real-world data analyst role**, covering the complete analytics workflow — from raw CSV data to executive-ready business insights.

| | |
|---|---|
| 🏢 **Client** | ShopIndia (Simulated) |
| 📅 **Period** | January – December 2024 |
| 🌍 **Regions** | North, South, East, West, Central India |
| 🛍️ **Categories** | Electronics, Furniture, Office Supplies |
| 💳 **Payment Modes** | Online, COD, Cards, EMI |
| 📦 **Total Transactions** | 150+ Orders |

---

## 📂 Datasets

| File | Description | Rows |
|------|-------------|------|
| [`ecommerce_sales_data.csv`](./ecommerce_sales_data.csv) | Main orders table with full transaction details | 150 |
| [`returns_data.csv`](./returns_data.csv) | Product return records linked by Order_ID | 16 |

### Key Columns — Sales Data
- **Order Info:** `Order_ID`, `Order_Date`, `Ship_Date`, `Ship_Mode`
- **Customer Info:** `Customer_ID`, `Customer_Name`, `Segment`
- **Geography:** `City`, `State`, `Region`
- **Product Info:** `Category`, `Sub_Category`, `Product_Name`
- **Financials:** `Sales`, `Quantity`, `Discount`, `Profit`
- **Payment:** `Payment_Mode`

---

## 📁 Project Structure

```
📂 ShopIndia-PowerBI-Dashboard/
├── 📄 ecommerce_sales_data.csv     ← Main dataset (150 transactions)
├── 📄 returns_data.csv             ← Returns dataset (16 records)
├── 📄 ShopIndia_Dashboard.pbix     ← Power BI Dashboard file
└── 📄 README.md                    ← Project documentation
```

---

## 🔧 Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Dashboard design & publishing |
| **Power Query** | Data import, cleaning & transformation |
| **DAX** | Calculated measures & KPIs |
| **Data Modeling** | Star Schema, table relationships |
| **Power BI Service** | Publishing & sharing |

---

## 🧠 Data Model

The project uses a **Star Schema** design:

```
Calendar Table
     │
     │ (One-to-Many on Date)
     ▼
ecommerce_sales_data  ──(One-to-Many on Order_ID)──▶  returns_data
     [Fact Table]                                       [Dimension]
```

A custom **Calendar table** was created using DAX `CALENDARAUTO()` to enable all time intelligence functions (YTD, MTD, QTD, MoM).

---

## 📊 DAX Measures Created (15+)

### Core KPIs
```dax
Total Sales      = SUM(ecommerce_sales_data[Sales])
Total Profit     = SUM(ecommerce_sales_data[Profit])
Total Quantity   = SUM(ecommerce_sales_data[Quantity])
Total Orders     = DISTINCTCOUNT(ecommerce_sales_data[Order_ID])
Profit Margin %  = DIVIDE([Total Profit], [Total Sales], 0) * 100
Avg Order Value  = DIVIDE([Total Sales], [Total Orders], 0)
```

### Time Intelligence
```dax
Sales MTD        = TOTALMTD([Total Sales], Calendar[Date])
Sales QTD        = TOTALQTD([Total Sales], Calendar[Date])
Sales YTD        = TOTALYTD([Total Sales], Calendar[Date])
MoM Growth %     = DIVIDE(CurrentMonth - Previous_Month, Previous_Month, 0) * 100
```

### Returns
```dax
Total Returns    = COUNTROWS(returns_data)
Return Rate %    = DIVIDE([Total Returns], [Total Orders], 0) * 100
```

### Advanced
```dax
Avg Shipping Days = AVERAGEX(ecommerce_sales_data, DATEDIFF([Order_Date], [Ship_Date], DAY))
Profit Status     = IF([Total Profit] > 0, "Profitable", "Loss-Making")
```

---

## 📄 Dashboard Pages

### Page 1 — Executive Summary
> High-level overview for stakeholders

- **KPI Cards:** Total Sales · Total Profit · Total Orders · Profit Margin %
- **Area Chart:** Monthly Sales Trend
- **Donut Chart:** Category-wise Sales Split
- **Clustered Bar Chart:** Regional Performance
- **Matrix Table:** Sub-Category breakdown with Sales, Profit, Quantity
- **Slicers:** Region · Category · Quarter

---

### Page 2 — Product & Profit Analysis
> Deep-dive into product performance and profitability drivers

- **Waterfall Chart:** Profit contributors & drains by Sub-Category
- **Scatter Plot:** Discount vs. Profit Margin % (sized by Sales)
- **Stacked Bar Chart:** Segment contribution by Category
- **Treemap:** Visual hierarchy of Category → Sub-Category → Sales
- **Conditional Formatting Table:** Top/Bottom products (green = profit, red = loss)
- **KPI Cards:** Average Order Value · Return Rate %

---

### Page 3 — Customer & Regional Insights
> Geographic and customer behaviour analysis

- **Map Visual:** State-wise sales heatmap
- **Donut Chart:** Payment Mode preferences
- **Stacked Column Chart:** Region × Category matrix
- **Bar Chart:** Top 10 Customers by Sales (TopN filter)
- **Donut Chart:** Customer Segment split (Consumer / Corporate / Home Office)
- **Line Chart:** Monthly return trends

---

## 💡 Key Business Insights

### 1. 🏷️ Discount Impact on Profitability
> Orders with discounts above **15%** — especially in the Binders sub-category — consistently resulted in **negative profits**. Recommendation: Cap discounts at **10%** for low-margin products.

### 2. 🗺️ Regional Performance Gap
> **South & West regions** contributed over **60% of total revenue**, while the **East region** was underperforming. Targeted marketing campaigns for Eastern cities are recommended.

### 3. 📱 Electronics — High Sales, High Returns
> Electronics had the **highest sales** but also the **highest return rate**. Recommendation: Improve product descriptions and strengthen quality checks.

### 4. 💳 Payment Mode Shift Opportunity
> Online payments led at ~40%, but COD remained significant at ~25%. Offering **small cashback incentives** could shift COD customers to online payments, reducing delivery costs.

### 5. 🤝 Corporate Segment = Highest AOV
> Consumer segment dominated in order volume (~50%), but the **Corporate segment had the highest Average Order Value**. A B2B loyalty program is recommended.

---

## ✅ Skills Demonstrated

| Skill | Evidence |
|-------|----------|
| **Data Import & Cleaning** | Power Query — correct data types, null handling, date validation |
| **Data Modeling** | Star schema, Calendar table, One-to-Many relationships |
| **DAX** | 15+ measures including time intelligence (YTD, MTD, MoM) |
| **Visualization** | 18+ visuals across 3 pages, best-fit chart selection |
| **Interactivity** | Slicers, drill-through, bookmarks, tooltips, navigation buttons |
| **Business Acumen** | 5 actionable insights with concrete recommendations |
| **Storytelling** | Dashboard flows: Overview → Product Detail → Customer/Region |

---

## 🚀 How to Run This Project

1. **Download** [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
2. **Clone** this repository:
   ```bash
   git clone https://github.com/sanT-0/shopindia-powerbi-dashboard.git
   ```
3. **Open** `ShopIndia_Dashboard.pbix` in Power BI Desktop
4. If prompted, **repoint the data sources** to the CSV files in this folder
5. Click **Refresh** to reload the data

---

## 📝 Resume Entry

```
📊 E-Commerce Sales Performance Dashboard | Power BI
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• Built an interactive 3-page Power BI dashboard analyzing 150+ e-commerce
  transactions across 5 Indian regions, 3 product categories, and 4 payment modes
• Created 15+ DAX measures including YTD/MTD sales, MoM growth %, profit margins,
  and return rate analysis using time intelligence functions
• Designed data model with Calendar table, Star Schema relationships, and
  drill-through navigation for executive-level reporting
• Key Insight: Identified that high-discount orders (>15%) resulted in negative
  profit margins, leading to a recommendation to cap discounts at 10%
• Tools: Power BI Desktop, DAX, Power Query, Data Modeling
```

---

## 🔗 Connect

If you found this project helpful or want to discuss the analysis, feel free to connect!

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/santhosh599)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sanT-0)

---

<div align="center">

⭐ **If this project helped you, please give it a star!** ⭐

*Made with ❤️ for data analyst job seekers*

</div>
#

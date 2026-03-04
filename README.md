# Walmart Sales Analysis

# Project Overview

### Goal
Analyze Walmart’s weekly sales performance across stores and departments, identify seasonality and holiday effects, and evaluate whether external economic indicators correlate with sales trends.

---

# Dataset

**Source:**  
Walmart Recruiting – Store Sales Forecasting Dataset (Kaggle)  
https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting/data

### Data Summary
- ~420,000 weekly sales records
- 45 stores
- 99 departments
- Date range: **2010 – 2013**

### Tables Used

**train**  
Fact table containing weekly sales transactions at **Store–Department–Date** level.

**features**  
Contains external economic indicators such as:
- Temperature
- Fuel Price
- CPI
- Unemployment

**stores**  
Contains metadata for each store:
- Store Type
- Store Size

**Date Table**  
Custom calendar dimension created for time intelligence including:
- Year
- Month
- Quarter
- YearMonth

---

# Data Model Relationships

- `train[Store] → stores[Store]` (Many-to-One)
- `train[Store, Date] → features[Store, Date]` (Many-to-One)
- `train[Date] → DateTable[Date]` (Many-to-One)
- `features[Date] → DateTable[Date]` (Many-to-One)

---

# Data Cleaning & Preparation

### Handling Missing Values
- Replaced `NA` values in the **features** dataset with `NULL`
- Removed `Markdown` columns due to more than **90% missing data**
- Verified no missing values in key columns:
  - Store
  - Dept
  - Date
  - Weekly_Sales

### Data Type Corrections
- Converted `Date` fields to **Date format**
- Converted `IsHoliday` to **Boolean (1/0)**
- Ensured numeric columns were stored as **decimal values**
- Ensured `Store` and `Dept` fields were stored as **integers**

### Duplicate Checks
- Verified uniqueness in `train` using **Store + Date + Dept**
- Checked `features` using **Store + Date**
- Confirmed uniqueness of records in the `stores` table

### Outlier Validation
- Observed high sales spikes during holiday periods
- Confirmed these spikes represent valid seasonal demand
- Outliers were **retained** to preserve real business patterns

### Data Transformations
- Trimmed whitespace from text fields
- Standardized boolean values
- Removed unusable columns
- Normalized date fields across tables

---

# Feature Engineering

Created additional analytical features including:

- Custom **Date Table**
- Store **size categories** (Small / Medium / Large)
- DAX Measures including:
  - Total Sales
  - Year-over-Year (YoY) Change
  - YoY Performance Indicator
  - Holiday Sales Average
  - Top Departments by Sales

---

# Dashboard & Visualizations

## Page 1 – Sales Dashboard

Visualizations include:

- Total Sales
- Holiday Sales
- Top Department Sales
- Top Performing Department
- Total Stores
- YoY Sales Performance
- Sales Over Time
- Sales by Store Type
- Top 10 Departments by Sales
- Sales by Store Size
- Holiday Sales Average

---

## Page 2 – Economic Indicators

Analysis of sales against macroeconomic factors:

- Sales vs CPI
- Sales vs Fuel Price
- Sales vs Unemployment
- Sales vs Temperature

All comparisons are visualized using **dual-axis time series charts**.

---

# Key Insights

### Sales Performance
- Weekly sales display strong **holiday-driven spikes**
- **Store Type A** consistently generates the highest sales
- **Large stores** contribute the majority of total revenue
- A small number of departments dominate total sales

### Holiday Impact
- Holiday weeks show **slightly higher average sales**

### Growth Trend
- Overall **YoY sales increased by ~58.9%**

### Economic Indicators
- CPI, fuel price, unemployment, and temperature show **weak correlation with sales**
- Walmart sales during this period appear **relatively resilient to macroeconomic changes**

---

# Tools Used

- **Power BI**
- **DAX**
- **Excel / CSV datasets**


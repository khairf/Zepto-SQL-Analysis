# ⚡ Zepto SQL Data Analysis Project

This is a complete, real-world data analyst portfolio project based on an e-commerce inventory dataset scraped from **Zepto** — one of India’s fastest-growing quick-commerce startups. This project simulates real analyst workflows, from raw data exploration to business-focused data analysis.

### 🎯 This project is perfect for:
* **📊 Data Analyst Aspirants:** Build a strong Portfolio Project for interviews and LinkedIn.
* **📚 SQL Learners:** Practice practical, hands-on SQL queries.
* **💼 Interview Prep:** Prepare for roles in retail, e-commerce, or product analytics.


---

## 📌 Project Overview

The goal of this project is to simulate how actual data analysts in the e-commerce or retail industries work behind the scenes to use SQL to:
* **Set up a messy database:** Build a real-world e-commerce inventory schema.
* **Perform Exploratory Data Analysis (EDA):** Inspect product categories, availability, and pricing inconsistencies.
* **Implement Data Cleaning:** Handle null values, remove invalid entries, and convert pricing metrics.
* **Write Business-Driven SQL Queries:** Derive actionable insights around pricing, inventory, stock availability, and revenue.

---

## 📁 Dataset Overview

The dataset was sourced from Kaggle and was originally scraped from Zepto’s official product listings. It mimics what you’d typically encounter in a real-world e-commerce inventory system.

Each row represents a unique **SKU (Stock Keeping Unit)** for a product. Duplicate product names exist because the same product may appear multiple times in different package sizes, weights, discounts, or categories to improve visibility – exactly how real catalog data looks.

### 🧾 Schema & Column Descriptions

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| **sku_id** | `SERIAL` | Unique identifier for each product entry (Synthetic Primary Key) |
| **name** | `VARCHAR` | Product name as it appears on the app |
| **category** | `VARCHAR` | Product category (e.g., Fruits, Snacks, Beverages) |
| **mrp** | `NUMERIC` | Maximum Retail Price (originally in paise, converted to ₹) |
| **discountPercent** | `NUMERIC` | Discount percentage applied on the MRP |
| **discountedSellingPrice** | `NUMERIC` | Final price after discount (converted to ₹) |
| **availableQuantity** | `INTEGER` | Units available in inventory |
| **weightInGms** | `INTEGER` | Product weight in grams |
| **outOfStock** | `BOOLEAN` | Flag indicating stock availability (True/False) |
| **quantity** | `INTEGER` | Number of units per package (mixed with grams for loose produce) |

---

## 🔧 Project Workflow

### 1. Database & Table Creation
We begin by establishing a robust structure inside PostgreSQL using appropriate constraints and data types:

```sql
CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);
```
---
### 2. Data Import
Loaded the raw data CSV using pgAdmin's native import feature.

Troubleshooting: Resolved standard encoding roadblocks (UTF-8 errors) by explicitly saving and re-encoding the source file into CSV UTF-8 format before staging.
---
### 3. 🔍 Exploratory Data Analysis (EDA)
* Initial database probing to assess data health, structure, and scale:

* Counted the total record volume in the dataset.

* Sampled rows to verify structural data mapping.

* Isolated null and missing fields across all columns.

* Extracted distinct product categories available.

* Aggregated in-stock vs. out-of-stock product counts.

* Analyzed duplicate name structures representing distinct SKUs.
---
### 4. 🧹 Data Cleaning & Preprocessing
* Identified and purged broken rows where the mrp or discountedSellingPrice registered as zero.

* Standardized pricing metrics by converting mrp and discountedSellingPrice from paise to rupees (Divided by 100) to ensure readability and downstream accuracy.

---
### 5. 📊 Business Insights & Analytics
Wrote target-driven SQL business logic to answer critical performance questions:

* Top Value: Isolated the top 10 best-value products by maximum discount depth.

* Risk Management: Flagged high-ticket, high-MRP products currently sitting out of stock.

* Revenue Projections: Calculated estimated potential revenue metrics broken down by product category.

* Margin Analysis: Filtered high-cost products (MRP > ₹500) offered with minimal discounts.

* Category Rank: Ranked the top 5 product categories offering the highest average discount rates.

* Unit Economics: Formulated price-per-gram fields to map out ultimate value-for-money items.

* Inventory Segmenting: Used conditional grouping to segment products into Low, Medium, and Bulk weight categories.

* Logistics Focus: Measured aggregate inventory weight metrics across individual categories.
---
🛠️ How to Use This Project
Prerequisite

Make sure you have a PostgreSQL client installed (like pgAdmin or DBeaver).
---

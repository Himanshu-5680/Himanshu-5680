# Data Wrangling & SQL Quick Notes ![Pandas](https://img.shields.io/badge/Pandas-130754?style=for-the-badge&logo=pandas&logoColor=E70488) ![SQL](https://img.shields.io/badge/SQL-003B57?style=for-the-badge&logo=postgresql&logoColor=white)

> Analysts spend most of their time cleaning data, not modelling it. Get fast at this part and everything else gets easier.

A working reference for **Data Cleansing**, **Data Wrangling** and **Database Queries** in analytics projects.

**Workflow:** inspect → clean → transform → aggregate → visualize → explain.

## 1. 🔍 pandas: Inspect & Cleanse

```python
import pandas as pd
import numpy as np

# Load dataset
df = pd.read_csv("data.csv")

# First look
df.head()
df.info()          # dtypes + non-null counts
df.describe()      # summary statistics
df.shape

# Missing values and duplicates
print(df.isnull().sum())
print(f"Duplicates: {df.duplicated().sum()}")

# Clean
df = df.drop_duplicates()
df["Revenue"] = df["Revenue"].fillna(df["Revenue"].median())
```

**Why median?** It's robust to outliers, so one giant order won't distort your fill value.

### 🧽 More cleaning moves

```python
# Standardize column names
df.columns = df.columns.str.strip().str.lower().str.replace(" ", "_")

# Fix data types
df["order_date"] = pd.to_datetime(df["order_date"], errors="coerce")
df["revenue"] = pd.to_numeric(df["revenue"], errors="coerce")

# Clean text
df["category"] = df["category"].str.strip().str.title()

# Drop rows missing a critical column
df = df.dropna(subset=["order_id"])
```

### 🚨 Outliers with the IQR rule

```python
q1, q3 = df["revenue"].quantile([0.25, 0.75])
iqr = q3 - q1
lower, upper = q1 - 1.5 * iqr, q3 + 1.5 * iqr
outliers = df[(df["revenue"] < lower) | (df["revenue"] > upper)]
```

Flag first, delete later. Sometimes the outlier is the story.

## 2. 🔧 pandas: Wrangle & Aggregate

```python
# Filter with multiple conditions
high_value_orders = df[(df["Revenue"] > 1000) & (df["Status"] == "Delivered")]

# Group and aggregate key metrics
category_summary = (
    df.groupby("Category")
    .agg(
        Total_Orders=("Order_ID", "count"),
        Total_Revenue=("Revenue", "sum"),
        Avg_Rating=("Rating", "mean")
    )
    .reset_index()
    .sort_values(by="Total_Revenue", ascending=False)
)
```

### 🧩 Combine and reshape

```python
# Join two tables (SQL-style)
merged = orders.merge(customers, on="customer_id", how="left")

# Pivot table
pivot = df.pivot_table(
    index="Category", columns="Region",
    values="Revenue", aggfunc="sum", fill_value=0
)

# Time-based grouping
df["month"] = df["order_date"].dt.to_period("M")
monthly = df.groupby("month")["revenue"].sum()

# New column from a condition
df["size"] = np.where(df["revenue"] > 1000, "Large", "Small")
```

## 3. 🗄️ SQL: Essential Queries

```sql
-- Filter, group and sort sales data
SELECT
    category,
    COUNT(order_id)      AS total_orders,
    SUM(sales_amount)    AS total_sales,
    ROUND(AVG(profit), 2) AS avg_profit
FROM orders
WHERE order_date >= '2026-01-01'
GROUP BY category
HAVING SUM(sales_amount) > 10000
ORDER BY total_sales DESC;
```

```sql
-- Join orders with customer details
SELECT
    o.order_id,
    c.customer_name,
    c.region,
    o.sales_amount
FROM orders AS o
INNER JOIN customers AS c
    ON o.customer_id = c.customer_id;
```

### 🚀 Level-up patterns

```sql
-- CASE WHEN: bucket values into labels
SELECT
    order_id,
    sales_amount,
    CASE
        WHEN sales_amount >= 1000 THEN 'Large'
        WHEN sales_amount >= 300  THEN 'Medium'
        ELSE 'Small'
    END AS order_size
FROM orders;

-- CTE: readable, step-by-step logic
WITH monthly_sales AS (
    SELECT
        DATE_TRUNC('month', order_date) AS month,
        SUM(sales_amount) AS total_sales
    FROM orders
    GROUP BY 1
)
SELECT * FROM monthly_sales ORDER BY month;

-- Window function: rank within each category
SELECT
    category,
    order_id,
    sales_amount,
    RANK() OVER (PARTITION BY category ORDER BY sales_amount DESC) AS rank_in_category
FROM orders;
```

> Date functions (`DATE_TRUNC`, etc.) vary by database. The example above is PostgreSQL syntax.

## 🔁 pandas ↔ SQL Translator

| Task | pandas | SQL |
|:-----|:-------|:----|
| Filter rows | `df[df["x"] > 5]` | `WHERE x > 5` |
| Select columns | `df[["a", "b"]]` | `SELECT a, b` |
| Sort | `df.sort_values("x")` | `ORDER BY x` |
| Group + sum | `df.groupby("a")["x"].sum()` | `SELECT a, SUM(x) ... GROUP BY a` |
| Join | `df1.merge(df2, on="id")` | `JOIN ... ON` |
| Remove duplicates | `df.drop_duplicates()` | `SELECT DISTINCT` |
| Count rows | `len(df)` | `COUNT(*)` |

## ✅ Pre-Analysis Checklist

- [ ] Column names standardized
- [ ] Data types correct (dates are dates, numbers are numbers)
- [ ] Missing values handled and documented
- [ ] Duplicates removed
- [ ] Outliers examined
- [ ] Results sanity-checked against the raw data

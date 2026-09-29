# Data Wrangling & SQL Quick Notes ![Pandas](https://img.shields.io/badge/Pandas-130754?style=for-the-badge&logo=pandas&logoColor=E70488) ![SQL](https://img.shields.io/badge/SQL-003B57?style=for-the-badge&logo=postgresql&logoColor=white)

A quick reference sheet for common **Data Cleansing**, **Data Wrangling**, and **Database Queries** used in Data Analytics projects.

## 1. Python (`pandas`) — Data Inspection & Cleansing

```python
import pandas as pd
import numpy as np

# Load CSV dataset
df = pd.read_csv("data.csv")

# Inspect structure & summary statistics
df.info()
df.describe()

# Check missing values and duplicates
print(df.isnull().sum())
print(f"Duplicates: {df.duplicated().sum()}")

# Clean duplicates and fill missing values
df = df.drop_duplicates()
df["Revenue"] = df["Revenue"].fillna(df["Revenue"].median())
```

## 2. Python (`pandas`) — Data Wrangling & Aggregation

```python
# Filtering rows with multiple conditions
high_value_orders = df[(df["Revenue"] > 1000) & (df["Status"] == "Delivered")]

# Grouping and aggregating key metrics
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

## 3. SQL — Essential Database Queries

```sql
-- Filter, Group, and Sort Sales Data
SELECT 
    category,
    COUNT(order_id) AS total_orders,
    SUM(sales_amount) AS total_sales,
    ROUND(AVG(profit), 2) AS avg_profit
FROM orders
WHERE order_date >= '2026-01-01'
GROUP BY category
HAVING SUM(sales_amount) > 10000
ORDER BY total_sales DESC;

-- Join Orders with Customer Details
SELECT 
    o.order_id,
    c.customer_name,
    c.region,
    o.sales_amount
FROM orders AS o
INNER JOIN customers AS c
    ON o.customer_id = c.customer_id;
```

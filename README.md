# ☕ Bright Coffee Shop — Sales Analysis Project

## Project Overview
An end-to-end data analysis project analysing 6 months of transactional sales data from Bright Coffee Shop, a chain with 3 branches. The goal is to uncover insights that can help improve sales performance across stores, products, and time periods.

## Business Questions
This analysis answers the following business questions:

| # | Question | Dimension |
|---|---|---|
| 1 | Which store generates the most revenue? | Where |
| 2 | Which product category earns the most? | What |
| 3 | Which products sell most by volume? | What |
| 4 | How are sales trending month by month? | When |
| 5 | Which days of the week are busiest? | When |
| 6 | What time of day has the most sales? | When |
| 7 | What is the total revenue across 6 months? | How Much |
| 8 | What is the average order value per store? | How Much |


## Dataset
- **Source:** Bright Coffee Shop Sales Dataset
- **Period:** January 2023 – June 2023
- **Stores:** Lower Manhattan · Hell's Kitchen · Astoria
- **Records:** 149,116 transactions
- **Columns:** 11 raw columns → 16 after transformation

  ### Raw Columns
| Column | Data Type | Description |
|---|---|---|
| transaction_id | bigint | Unique identifier per transaction (Primary Key) |
| transaction_date | DATE | Date of sale |
| transaction_time | Timestamp | Time of sale |
| transaction_qty | bigint | Number of units sold |
| store_id | bigint | Store identifier |
| store_location | string | Store branch name |
| product_id | bigint | Product identifier |
| unit_price | double | Price per unit |
| product_category | string | Broad product category |
| product_type | string | Specific product type |
| product_detail | string | Full product name and size |

## Tools Used
| Microsoft Excel | Quick data validation checks |
| Miro | project planning and brainstorming |
| Databricks (SQL) | Data cleaning and transformation |
| Canva | Project phase Update  |
| Microsoft Excel | Data visualisation and dashboard |
| Microsoft PowerPoint | Project Presentation |


## Data Inspection Summary
Before cleaning, the following checks were performed:

| Check | Result |
|---|---|
| Total rows | 149,116 |
| Null values | 0 across all columns |
| Duplicate transaction IDs | 0 |
| Date range | 01 Jan 2023 – 30 Jun 2023 |
| Unit price range | $0.80 – $45.00 |
| Quantity range | 1 – 8 units |


## Data Cleaning & Transformation
The following transformations were applied in Databricks SQL:

**1. Fixed date format**
Converted `transaction_date` from raw text to a readable date format `dd MMMM yyyy`.

**2. Fixed time format**
Converted `transaction_time` to 12-hour format with AM/PM.

**3. Created `total_sales`**
```sql
ROUND(unit_price * transaction_qty, 2) AS total_sales
```

**4. Extracted `month` and `month_name`**
```sql
MONTH(TO_DATE(transaction_date, 'yyyy/MM/dd')) AS month,
DATE_FORMAT(TO_DATE(transaction_date, 'yyyy/MM/dd'), 'MMM') AS month_name
```

**5. Extracted `day_of_week`**
```sql
DATE_FORMAT(TO_DATE(transaction_date, 'yyyy/MM/dd'), 'EEEE') AS day_of_week
```

**6. Created `time_of_day` buckets**
```sql
CASE
    WHEN HOUR(TO_TIMESTAMP(transaction_time, 'HH:mm:ss')) BETWEEN 6  AND 11 THEN 'Morning'
    WHEN HOUR(TO_TIMESTAMP(transaction_time, 'HH:mm:ss')) BETWEEN 12 AND 16 THEN 'Afternoon'
    WHEN HOUR(TO_TIMESTAMP(transaction_time, 'HH:mm:ss')) BETWEEN 17 AND 20 THEN 'Evening'
    ELSE 'Night'
END AS time_of_day
```

---

## Key Findings
*To be updated after analysis is complete.*

---

## Dashboard
* Microsoft Excel dashboard to be added after visualisation step is complete.*

---

## Author
**Tshegofatso L. Senona**
Data Analyst | South Africa

---

## Status
🟡 In Progress — Currently at Step 4: Analysis


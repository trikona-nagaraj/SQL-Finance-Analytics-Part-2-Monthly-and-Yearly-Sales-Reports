
# SQL-Finance-Analytics-for-Atliq-Hardware-Task-2-3

## Gross Sales Report: Total Gross Price

This report analyzes the total gross sales price for transactions made by Croma India, focusing on monthly and yearly aggregation. By leveraging MySQL, we extract and analyze gross sales data to provide valuable insights into financial performance.

---

### Task 2: Monthly Gross Sales Report

#### Task Overview
The goal of this task is to generate monthly gross sales data for Croma India. The steps include:

1. Calculating the gross sales price for each transaction.
2. Aggregating the gross sales for individual months.
3. Ensuring that the data is grouped and ordered correctly for analysis.

#### Steps and Queries



```sql

Step 1: Calculating Gross Price Total for Transactions
The gross price for each transaction is calculated by multiplying the sold quantity by the gross price.

SELECT date, 
       ROUND(sold_quantity * gross_price, 2) AS Gross_price_total
FROM fact_sales_monthly s
JOIN fact_gross_price g
ON s.product_code = g.product_code 
   AND g.fiscal_year = get_fiscal_year(s.date)
WHERE customer_code = 90002002
ORDER BY date ASC


---


Step 2: Aggregating Monthly Gross Sales
To provide a single row per month, gross sales data is aggregated using the SUM function and grouped by the transaction date.

sql
Copy code
SELECT date, 
       ROUND(SUM(sold_quantity * gross_price), 2) AS Gross_price_total
FROM fact_sales_monthly s
JOIN fact_gross_price g
ON s.product_code = g.product_code 
   AND g.fiscal_year = get_fiscal_year(s.date)
WHERE customer_code = 90002002
GROUP BY s.date
ORDER BY date ASC;
---

The result of this query provides insights into monthly sales trends and customer spending patterns.

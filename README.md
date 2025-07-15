# Retail Data Analysis and Reporting
This repository contains SQL queries and generated reports for analyzing customer, sales, and product data within a retail context. The analyses aim to provide insights into customer behavior, product performance, and overall sales trends.

Table of Contents
Project Overview

Analysis Categories

Change Over Time

Cumulative Analysis

Performance Analysis

Part-to-Whole Proportional Analysis

Data Segmentation

Generated Reports

Customer Report

Product Report

Database Schema (Assumed)

Usage

Project Overview
This project utilizes SQL to extract meaningful insights from retail transactional data. It covers various analytical techniques, including time-series analysis, performance comparisons, proportional analysis, and data segmentation. The ultimate goal is to generate comprehensive reports that can inform business strategies related to customer engagement and product management.

Analysis Categories
The Advance Analysis on customer.sql file contains several types of analytical queries:

Change Over Time
This section includes queries to analyze trends in key metrics over time.

Total Sales, Total Customers, and Total Quantity by Month: This query helps understand monthly performance trends.

SQL

SELECT
Month (order_date) as order_year,
Sum(sales_amount) as Total_sales,
Count(DISTINCT customer_key) as Total_Customer,
Sum(quantity) as Total_quantity
FROM gold.fact_sales
Where order_date is not null
Group by Month(order_date)
Order by Month(order_date)
Cumulative Analysis
Queries in this section progressively aggregate data over time to show growth or decline.

Running Total of Sales and Running Average Price by Year: This provides a cumulative view of sales and pricing trends.

SQL

SELECT
order_date,
total_sales,avg_price,
SUM(total_sales) over (Order by order_date) AS Running_total_sales,
AVG(avg_price) over(Order by order_date) as Running_Average_price
FROM
(
SELECT
DATETRUNC(YEAR,order_date) as Order_date,
Sum(sales_amount) as Total_sales,
AVG (price) as avg_price
From gold.fact_sales
Where order_date is Not Null
Group by DATETRUNC(YEAR,order_date)
) t
Performance Analysis
This section focuses on comparing current performance against targets or previous periods.

Yearly Product Performance Analysis: Compares each product's sales to its average sales performance and the previous year's sales. It classifies performance as 'Above Avg', 'Below Avg', or 'AVG' and 'Increasing', 'Decreasing', or 'No Change' year-over-year.

SQL

WITH yearly_product_sales as(
SELECT p.product_name,
YEAR (f.order_date) as order_year,
SUM(f.sales_amount) as current_sales
FROM gold.fact_sales f
LEFT JOIN gold.dim_products p
ON f.product_key=p.product_key
WHERE f.product_key IS NOT NULL
GROUP BY p.product_name, YEAR (f.order_date)
)
SELECT
-- ... (rest of the query for performance analysis)
FROM yearly_product_sales
Order by product_name, order_year
Part-to-Whole Proportional Analysis
These queries help understand the contribution of individual parts to the overall total.

Category Contribution to Overall Sales: Identifies which product categories contribute most to total sales by calculating their percentage of overall sales.

SQL

With Category_sales as(
SELECT
category,
Sum(sales_amount) as Total_sales
From gold.fact_sales f
LEFT JOIN gold.dim_products p
ON f.product_key=p.product_key
GROUP by category
)
SELECT category, Total_sales,
Sum(Total_sales) Over () as Overall_sales,
CONCAT(ROUND((CAST(Total_sales as FLOAT)/Sum(Total_sales) Over ())*100,2),'%') as Percentage_of_total
FROM Category_sales
ORDER BY Total_sales Desc
Data Segmentation
This section includes queries for grouping data based on specific criteria.

Product Segmentation by Cost Range: Segments products into different cost ranges (e.g., 'Below 100', '100-500', '500-1000', 'Above 1000') and counts the number of products in each segment.

SQL

With product_segment as (
Select product_key,product_name,
cost,
Case
	When cost<100 THEN 'Below 100'
	-- ... (rest of the case statement)
END Cost_range
FROM gold.dim_products)
SELECT cost_range,
Count(product_key) as Total_Product
From product_segment
Group by Cost_range
Order by Total_Product DESC
Customer Segmentation by Spending Behavior: Groups customers into 'VIP', 'Regular', and 'New' segments based on their lifespan and total spending.

SQL

WITH Customer_Spending as (
SELECT f.customer_key,
SUM(f.sales_amount) as Total_spend,
MIN(order_date) as first_order,
MAX(order_date) as last_order,
DATEDIFF (MONTH,MIN(order_date),MAX(order_date)) as Lifespan
FROM gold.fact_sales f
LEFT JOIN gold.dim_customers c
ON f.customer_key=c.customer_key
Group by f.customer_key
)
SELECT
COUNT(customer_key) as Total_Customer,
Customer_segment
FROM
(
SELECT
customer_key,
CASE
	WHEN Lifespan>= 12 AND Total_spend>5000 THEN 'VIP'
	-- ... (rest of the case statement)
	ELSE 'New'
END as Customer_segment
FROM Customer_Spending) t
Group by Customer_segment
ORDER BY Total_Customer DESC
Generated Reports
Two comprehensive reports have been generated to provide a holistic view of customer and product performance.

Customer Report
The Customers_Report.sql file (also present in Advance Analysis on customer.sql) defines a view or query for a detailed customer report.

Purpose: Consolidates key customer metrics and behaviors.

Highlights:

Gathers essential fields such as names, ages, and transaction details.

Segments customers into categories (VIP, Regular, New) and age groups.

Aggregates customer-level metrics: total orders, total sales, total quantity purchased, total products, and lifespan (in months).

Calculates valuable KPIs: recency (months since last order), average order value, and average monthly spend.

Product Report
The Product_Report.sql file defines a view or query for a detailed product report.

Purpose: Consolidates key product metrics and behaviors.

Highlights:

Gathers essential fields such as product name, category, subcategory, and cost.

Segments products by revenue to identify High-Performers, Mid-Range, or Low-Performers.

Aggregates product-level metrics: total orders, total sales, total quantity sold, total customers (unique), and lifespan (in months).

Calculates valuable KPIs: recency (months since last sale), average order revenue (AOR), and average monthly revenue.

Database Schema (Assumed)
The queries are built upon an assumed star schema, primarily interacting with the following tables:

gold.fact_sales: Contains sales transaction details (e.g., order_number, product_key, customer_key, order_date, sales_amount, quantity, price).

gold.dim_customers: Contains customer master data (e.g., customer_key, customer_number, first_name, last_name, birthdate).

gold.dim_products: Contains product master data (e.g., product_key, product_name, category, subcategory, cost).

Usage
To use these queries:

Ensure you have access to a SQL database containing the gold.fact_sales, gold.dim_customers, and gold.dim_products tables with appropriate data.

Connect to your SQL database.

Execute the desired queries from Advance Analysis on customer.sql for various analyses or run the Customers_Report.sql and Product_Report.sql files to generate the comprehensive reports.

Modify the queries as needed to fit specific analytical requirements or database variations.

# SQL Advanced Analytics Project

**Welcome to the SQL Advanced Analytics Project repository! 🚀 This project demonstrates comprehensive data analytics and reporting capabilities, from advanced SQL analysis to business intelligence insights.**

## 🏗️ Data Architecture

The data architecture for this project follows Medallion Architecture with **Bronze**, **Silver**, and **Gold** layers:

1. **Bronze Layer**: Stores raw data as-is from the source systems. Data is ingested from CSV Files into SQL Server Database.
2. **Silver Layer**: This layer includes data cleansing, standardization, and normalization processes to prepare data for analysis.
3. **Gold Layer**: Houses business-ready data modeled into a star schema required for reporting and analytics.

## 📖 Project Overview

This project involves:

1. **Advanced SQL Analytics**: Implementing sophisticated analytical queries using window functions, CTEs, and complex aggregations.
2. **Time Series Analysis**: Analyzing trends, cumulative metrics, and year-over-year comparisons.
3. **Performance Analysis**: Comparing current performance against historical data and targets.
4. **Customer Segmentation**: Grouping customers based on spending behavior and lifecycle stages.
5. **Business Intelligence Reports**: Creating comprehensive customer and product reports for stakeholder insights.

## 🚀 Project Requirements

### Advanced Data Analysis (SQL Analytics)

**Objective**
Develop advanced SQL analytics to deliver detailed insights into:
* **Customer Behavior & Segmentation**
* **Product Performance Analysis**
* **Sales Trends & Time Series Analysis**
* **Performance Metrics & KPIs**

**Specifications**
* **Advanced Analytics**: Implement complex analytical patterns including time series, performance analysis, and segmentation.
* **Data Quality**: Ensure robust data handling with null checks and edge case management.
* **Business Intelligence**: Create comprehensive reports consolidating key metrics for decision-making.
* **Scope**: Focus on actionable insights that drive business value and strategic decisions.
* **Documentation**: Provide clear documentation of analytical approaches and business logic.

## 📊 Analytics Components

### 1. Change Over Time Analysis
- **Monthly trend analysis** tracking sales performance, customer counts, and quantity metrics
- **Time-based aggregations** to identify seasonal patterns and growth trends

### 2. Cumulative Analysis
- **Running totals** of sales over time to understand business trajectory
- **Progressive aggregations** showing cumulative growth patterns
- **Moving averages** for price and performance metrics

### 3. Performance Analysis
- **Year-over-year comparisons** for product sales performance
- **Variance analysis** comparing actual vs. average performance
- **Trend classification** (Above/Below Average, Increasing/Decreasing)

### 4. Part-to-Whole Analysis
- **Category contribution analysis** showing which product categories drive the most revenue
- **Percentage calculations** for market share and impact assessment

### 5. Data Segmentation
- **Product cost segmentation** grouping products into price ranges
- **Customer lifecycle segmentation** (VIP, Regular, New customers)
- **Behavioral segmentation** based on spending patterns and tenure

### 6. Comprehensive Reports

#### Customer Report
- **Customer Demographics**: Age groups and customer profiles
- **Customer Segmentation**: VIP, Regular, and New customer classifications
- **Key Metrics**: Total orders, sales, quantity, and product diversity
- **Behavioral KPIs**: Recency, average order value, and monthly spend patterns

#### Product Report
- **Product Performance**: Sales metrics and quantity sold
- **Revenue Segmentation**: High-Performers, Mid-Range, and Low-Performers
- **Product Analytics**: Average selling price, order revenue, and monthly revenue
- **Market Analysis**: Category and subcategory performance insights

## 🎯 Key Features

### Advanced SQL Techniques
- **Window Functions**: LAG, LEAD, ROW_NUMBER, RANK for analytical insights
- **Common Table Expressions (CTEs)**: Complex multi-step analytical queries
- **Conditional Logic**: CASE statements for dynamic categorization
- **Date Functions**: DATETRUNC, DATEDIFF for time-based analysis

### Business Intelligence
- **Customer Lifecycle Analysis**: Understanding customer journey and value
- **Product Performance Metrics**: Revenue analysis and market positioning
- **Trend Analysis**: Identifying growth patterns and business trajectories
- **Segmentation Analysis**: Targeted insights for different customer and product groups

### Data Quality & Handling
- **Null Value Management**: Robust handling of missing data
- **Edge Case Prevention**: NULLIF and division by zero protection
- **Data Type Conversions**: Proper casting for accurate calculations

## 🛠️ Technical Implementation

### Database Schema
- **Fact Table**: `gold.fact_sales` - Central sales transaction data
- **Dimension Tables**: 
  - `gold.dim_customers` - Customer master data
  - `gold.dim_products` - Product catalog information

### Key Analytical Patterns
- **Time Series Analysis**: Month-over-month and year-over-year comparisons
- **Cohort Analysis**: Customer segmentation based on behavior and lifecycle
- **Performance Benchmarking**: Comparing metrics against averages and targets
- **Proportional Analysis**: Understanding contribution to overall business metrics

## 📈 Business Value

### Strategic Insights
- **Customer Segmentation**: Targeted marketing and retention strategies
- **Product Performance**: Inventory optimization and pricing strategies
- **Sales Trends**: Revenue forecasting and business planning
- **Performance Metrics**: Data-driven decision making and goal setting

### Operational Benefits
- **Automated Reporting**: Consistent and reliable business intelligence
- **Scalable Analytics**: Reusable analytical frameworks
- **Data-Driven Culture**: Empowering stakeholders with actionable insights

## 🛡️ License

This project is licensed under the MIT License. You are free to use, modify, and share this project with proper attribution.

## 🌟 About Me

Hi there! I'm passionate about data analytics and business intelligence, transforming raw data into actionable insights that drive business success.

# coffee-Shop-Sales-Using-Power-BI-SQL
![image alt](https://github.com/vidhateshamal2000/coffee-Shop-Sales-Using-Power-BI-SQL/blob/632558aa59eae8167a123ac70b14e42537c54055/coffee%20shop%20sales.png)

# Coffee Shop Sales Analysis

## Overview
This project analyzes sales data from a coffee shop, covering data cleaning, KPI analysis, sales trends, category-based analysis, and time-based sales insights. The SQL scripts help process and extract meaningful business intelligence from the sales dataset.

## Objectives
- Clean and transform raw sales data into a structured format.
- Calculate key performance indicators (KPIs) like total sales, orders, and quantity sold.
- Analyze month-over-month (MoM) sales growth and trends.
- Identify sales performance across locations, product categories, and specific time periods.

## SQL Scripts

### 01_data_cleaning.sql
- Convert `transaction_date` to proper date format.
- Alter `transaction_date` column to `DATE` type.
- Convert `transaction_time` to proper time format.
- Alter `transaction_time` column to `TIME` type.
- Fix column name issues.

### 02_kpi_analysis.sql
- Calculate total sales for a given month.
- Compute month-over-month (MoM) sales growth.

### 03_sales_trends.sql
- Analyze the sales trend over a period.
- Compute the average daily sales for the selected month.

### 04_category_analysis.sql
- Compute sales by store location.
- Identify top-selling product categories.

### 05_time_based_analysis.sql
- Analyze sales trends by hour.
- Identify peak sales hours and sales variations across days of the week.

## Example Queries

### Total Sales Calculation
```sql
SELECT ROUND(SUM(unit_price * transaction_qty)) AS Total_Sales 
FROM coffee_shop_sales 
WHERE MONTH(transaction_date) = 5;
```

### MoM Sales Growth
```sql
SELECT 
    MONTH(transaction_date) AS month,
    ROUND(SUM(unit_price * transaction_qty)) AS total_sales,
    (SUM(unit_price * transaction_qty) - LAG(SUM(unit_price * transaction_qty), 1)
    OVER (ORDER BY MONTH(transaction_date))) / LAG(SUM(unit_price * transaction_qty), 1) 
    OVER (ORDER BY MONTH(transaction_date)) * 100 AS mom_increase_percentage
FROM coffee_shop_sales
WHERE MONTH(transaction_date) IN (4, 5)
GROUP BY MONTH(transaction_date)
ORDER BY MONTH(transaction_date);
```

## Usage
1. Load the sales dataset into a MySQL database.
2. Execute the SQL scripts sequentially for cleaning, transformation, and analysis.
3. Use the queries in `kpi_analysis.sql`, `sales_trends.sql`, and `category_analysis.sql` to generate insights.

## Future Enhancements
- Integration with a visualization tool for dashboards.
- Automation of SQL execution via stored procedures.
- Expansion of analysis to yearly trends and customer segmentation.

-[View Power BI Report](https://app.powerbi.com/groups/me/reports/a2c56160-a797-400e-8d2b-15401d0fb6b0/8c82b84e4dd26a6921a3?experience=power-bi)

<iframe width="800" height="600" src="https://app.powerbi.com/groups/me/reports/a2c56160-a797-400e-8d2b-15401d0fb6b0/8c82b84e4dd26a6921a3?experience=power-bi
" frameborder="0" allowFullScreen="true"></iframe>
 

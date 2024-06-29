
# Pizza Sales Report 

## Project Overview

This project aims to leverage SQL for comprehensive data analysis and Power BI for advanced visualization to deeply understand pizza sales dynamics. By examining sales trends, popular pizza varieties, and customer preferences, the project seeks to optimize operational strategies, enhance marketing initiatives, and improve decision-making processes. The ultimate goal is to derive actionable insights that drive business growth, increase customer satisfaction, and streamline operational efficiency within the pizza sales domain.

![Dashboard](https://github.com/Xharity/Pizza-Sales-Report/assets/173803485/4421aaa6-c329-47df-8002-814f50a031ee)

## Data Sources 

The dataset for this analysis is the Pizza Sales file containing information about the sales made by this Pizza company 

## Tools

- MS OFFICE/ Excel
- SQL
  -MS SQL SERVER
- PowerBI
   - [Dashboard]()

## Data Cleaning and Inspection

In the initial data preparation phase, we performed the following tasks

1. Data Loading and inspection 

2. Handling missing values

3. Data cleaning and formatting 
    ![](https://github.com/Xharity/Pizza-Sales-Report/assets/173803485/45a57d48-da84-4ef6-9dfd-f6e945cbe411)

![](https://github.com/Xharity/Pizza-Sales-Report/assets/173803485/1c1db3e6-5a76-4de1-b53f-d0ca54d6a5bd)

## Business Questions 

1. Analyze key indicators for our pizza sales data to gain insight into performance

2. Daily Trend for total Orders

3. Percentage of Sales by Pizza Category

4. Total pizza sold by Pizza Category

5. Top 5 Best sellers by Revenue, Total Quality and total Orders

## Data Analysis

1. Total Revenue 

`select sum(total_price) as "total_revenue" from pizza_sales`

2. Average Order Value

`select sum(total_price) / count(distinct order_id) as "Avg_ Order_id" from pizza_sales`

3. Total Pizza Sold 

`select sum(quantity) as "total_pizza_sold" from pizza_sales`

4. Total Orders 

`select count(distinct order_id) as "total_orders" from pizza_sales`

5. Averge Pizza Per order 

`Select cast(cast(SUM(quantity) as decimal (10,2))/
cast(COUNT(distinct order_id)as decimal(10,2)) as decimal(10,2)) from pizza_sales
`

6. Daily trend for Total orders 

`select DATENAME(DW, order_date) as order_day, COUNT(distinct order_id) as Total_orders 
from pizza_sales
group by DATENAME(DW, order_date)
`

7. Monthly Trend for Total orders 

`Select DATENAME(month, order_date) as "MONTH_Name", count(distinct order_id) as "total_orders"
from pizza_sales
group by DATENAME( month, order_date) 
order by total_orders desc`

8. Percentage of sales by Pizza size

`Select pizza_category, SUM(total_price)* 100 / (select SUM(total_price) 
from pizza_sales)as PCT
from pizza_sales 
group by  pizza_category`

9. Total Pizza sold by Pizza category

`select pizza_category, SUM(total_price) AS "total_price", SUM(total_price) * 100 / (select SUM(total_price) 
from pizza_sales where MONTH(order_date) = 1)as PCT
from pizza_sales 
where MONTH(order_date) = 1
group by  pizza_category`

10. Top 5 best sellers by Revenue, Total Quantiyu and Total orders 

`select pizza_size, SUM(total_price) AS "total_sales", CAST(SUM(total_price) * 100 
/ (select SUM(total_price) 
from pizza_sales) AS DECIMAL(10,2)) as PCT
from pizza_sales 
group by  pizza_size
order by PCT DESC`

`select pizza_size, CAST(SUM(total_price)AS DECIMAL(10,2)) AS "total_sales",
CAST(SUM(total_price) * 100 
/ (select SUM(total_price) 
from pizza_sales WHERE DATEPART(QUARTER, order_date) = 1) AS DECIMAL(10,2)) as PCT
from pizza_sales 
WHERE DATEPART(QUARTER, order_date) = 1
group by  pizza_size
order by PCT DESC`

A. Top 5 Pizza by Revenue 

`SELECT top 5 Pizza_name, SUM(total_price) as "total_revenue" from pizza_sales
group by pizza_name
order by total_revenue DESC`

B. Bottom 5 Pizaza by Revenue 

`SELECT top 5 Pizza_name, SUM(total_price) as "total_revenue" from pizza_sales
group by pizza_name
order by total_revenue ASC`

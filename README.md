# SQL-Power-BI-Project-Eden Pizza Sales Analysis 
## Business Problem
The owner of the Pizza store would like to have insight information about how his shop performing, he wants to know some KPIs including, total revenue, total orders, most popular pizza etc to help him make some business decisions. As a Data Analyst, I will analyse the raw data by use SQL server and present it in Power BI to the owner, I will also provide some recommendations to the owner for him to make decisions.
## Data Cleaning 
The Original data given by the owner was in in spreadsheet, it has eight categories of Pizza id, order id, pizza name, quantity, order date, order time, unit price, total price, pizza size, pizza catrgory, pizza ingredients and pizza names. All data is in clean formation, with no errors or null values. Imported to SQL Server for analysis
## Data Analysis(SQL)
### KPIs 
### Total Revenue
SELECT SUM(total_price) AS total_revenue
FROM dbo.pizza_sales

![Picture1](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/d4271474-783d-4256-a467-6ac53d7ca477)

### Average Order Value 
The average amount of money each customer spent per order 
SELECT SUM(total_price)/COUNT(distinct order_id ) AS avg_order_value
FROM dbo.pizza_sales

![Picture2](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/56edfc99-6740-4c99-ba1c-b3d069bf54bd)

### Total Pizza Sold
SELECT SUM(quantity) AS Total_sold
FROM dbo.pizza_sales

![Picture3](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/72c29898-421f-4d73-b651-7d358d07d6ef)

### Total Order number
SELECT COUNT(DISTINCT order_id ) AS total_orders
FROM dbo.pizza_sales

![Picture4](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/23fce99d-b45a-49dd-bd16-c1f1a04246ca)

### Average Pizzas per order
SELECT CAST(CAST(SUM(quantity)AS DECIMAL(10,2))/
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS avg_pizzas_per_order 
FROM dbo.pizza_sales

![Picture4](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/d670d2ee-a627-464a-a8c0-1da19e3dcf9f)

### Daily Trend for total orders
SELECT DATENAME(WEEKDAY,order_date) AS order_day,
COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sales
GROUP BY DATENAME(WEEKDAY,order_date)

![Picture6](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/d0443297-b8ae-4a37-b894-b5c6b8808f9b)

### Monthly Trend for total orders
SELECT DATENAME(MONTH,order_date) AS order_month,
COUNT(DISTINCT order_id) AS Total_orders
FROM pizza_sales
GROUP BY DATENAME(MONTH,order_date)
ORDER BY Total_orders DESC

![Picture7](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/36eca094-27d9-4d90-b828-cee5c29d8636)

### Percentage of Sales by Pizza Category
SELECT pizza_category, SUM(total_price) as Total_Sales, SUM(total_price)*100/(SELECT SUM(total_price) FROM pizza_sales ) AS Percentage_Sales
FROM dbo.pizza_sales
GROUP BY pizza_category

![Picture8](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/615bb03a-0114-488b-81d2-ae3740d558c5)

### Percentage of Sales by Pizza Size
SELECT pizza_Size, CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Sales, CAST(SUM(total_price)*100/
(SELECT SUM(total_price) FROM pizza_sales ) AS DECIMAL(10,2)) AS Percentage_Sales
FROM dbo.pizza_sales
GROUP BY pizza_size
ORDER BY Percentage_Sales DESC

![Picture9](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/1afb4407-b007-4334-bdc5-59265debe5fb)

### Top 5 Best Sellers by Revenue
SELECT TOP 5 pizza_name, CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Revenue
FROM dbo.pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC

![Picture10](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/b27a1f6f-8508-4ff6-8490-933a891a6259)

### Bottom 5 Worst Sellers by Revenue
SELECT TOP 5 pizza_name, CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Revenue
FROM dbo.pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC

![Picture11](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/001dd176-4873-4d32-9131-334670fead75)

### Top 5 Best Sellers by Total Quantity
SELECT TOP 5 pizza_name, CAST(SUM(quantity) AS DECIMAL(10,2)) AS Total_Quantity
FROM dbo.pizza_sales
GROUP BY pizza_name
ORDER BY Total_Quantity DESC

![Picture12](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/fcc7a14a-3cab-41f0-85e9-d1d51911ba14)

### Top 5 Best Sellers by Total Orders
SELECT TOP 5 pizza_name, COUNT (DISTINCT order_id) AS Total_Orders
FROM dbo.pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC

![Picture13](https://github.com/dandai509/SQL-Power-BI-Project/assets/106848444/1ca48de6-6f3f-4f92-9b0d-175064aec016)

## Eden Pizza Sales Dashborad 

https://app.powerbi.com/groups/me/reports/a549e64c-5c2b-4696-98c5-a39fc607030b/ReportSection?experience=power-bi
https://app.powerbi.com/groups/me/reports/a549e64c-5c2b-4696-98c5-a39fc607030b/ReportSectionb44cdbbdde8cec96f561?experience=power-bi









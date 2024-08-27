# Bike_Sales_Analysis
This project analyzes bike sales data in 53 States across 6 Countries (United States, United Kingdom, Canada, Australia, France, and Germany) to understand market trends and consumer preferences in 6 years.

```SQL
--TABLE 'SALES'
--This project analyzes the sales of bikes for a period of 6 years in 6 countries

--Display all items in the table 

select * 
from Sales

--how many rows do we have in the table

select count(*) as row_count
from Sales

--total count of age group

select count(distinct age_group) as total_agegroup
from Sales

--Display the age groups from the sales table

select distinct Age_Group 
from sales

--display the total number of product categories, subcategories, and products

select count(distinct product_category) as product_categories 
from sales

select count(distinct sub_category) as sub_categories 
from sales

select count(distinct product) as total_products 
from sales

--number of years

select count(distinct year) as years
from Sales

---Which product category had the highest sales volume
select product_category, sum(revenue) as total_sales
from Sales
group by Product_Category
order by total_sales desc

--Which product subcategory generated the highest revenue
select top 1 sub_category, sum(revenue) as total_sales
from Sales
group by sub_category
order by total_sales desc

---Analyze the sales trends over time 
select year, sum(revenue) as total_sales
from Sales
group by year
order by year desc

--rank them from highest to lowest
select year, sum(revenue) as total_sales,
rank() over(order by sum(revenue) desc) AS sales_rank
from Sales
group by year
order by year desc








```

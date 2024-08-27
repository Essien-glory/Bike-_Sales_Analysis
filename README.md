# Bike_Sales_Analysis
This project analyzes bike sales data in 53 States across 6 Countries (United States, United Kingdom, Canada, Australia, France, and Germany) to understand market trends and consumer preferences in 6 years.

```SQL
--TABLE 'SALES'

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


--EXPLORATORY DATA ANALYSIS

--1. Which product category had the highest sales volume
select product_category, sum(revenue) as total_sales
from Sales
group by Product_Category
order by total_sales desc


--2. Which product subcategory generated the highest revenue
select top 1 sub_category, sum(revenue) as total_sales
from Sales
group by sub_category
order by total_sales desc


--3. Analyze the sales trends over time 
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


--4. Based on revenue and quantity ordered, which gender should we focus on?
select customer_gender, sum(order_quantity) as total_qty_ordered
from sales
group by customer_gender
order by total_qty_ordered desc

--This query was used to get the percentage of males to females 
Select
    round(sum(case when Customer_Gender = 'M' then 1 else 0 end) * 100.0 / count(*),0) AS male_percentage,
  round(sum(case when Customer_Gender = 'F' then 1 else 0 end) * 100.0 / count(*),0) AS female_percentage
from 
    Sales
--The percentage of males to females is 52 to 48


--5. Which gender ordered the highest quantity of bikes
select customer_gender, sum(Order_Quantity) as total_sales
from sales
where Sub_Category like '%bike%'
group by customer_gender
order by total_sales desc


--6. Which age group bought the most bikes
select age_group, sum(order_quantity) as qty_ordered
from sales
where Product_Category like '%bike%'
group by age_group
order by qty_ordered desc


--7. Analyze the total quantity ordered and the sales made per country
select country, sum(revenue) as total_sales, sum(order_quantity) as total_qty_ordered
from sales
group by country
order by total_sales desc


--8. Which are the top 5 states with the highest revenue generated?
select top 5 country, state, sum (revenue) as total_per_state
from sales
group by country, state
order by sum (revenue) desc


--9. Which are the bottom 5 states with the lowest revenue generated?
select top 5 country, state, sum (revenue) as total_per_state
from sales
group by country, state
order by sum (revenue) asc


--10. How does the quantity ordered affect overall revenue and profit
select product_category, sum(order_quantity) as total_qty_ordered,
sum(revenue) as total_sales,
sum(profit) as total_profit
from sales
group by Product_Category
order by total_sales desc

--sales volume is dependent on the unit cost and the qty ordered.


--11. How does the buying behavior differ between various age groups and genders?
select age_group, customer_gender, sum(order_quantity) as total_qty_ordered, sum(revenue) as total_sales
from sales
group by age_group, customer_gender
order by total_sales desc

This Analysis has helped provide valuable insights into the sales of bikes across the six countries.


Kindly refer to my Medium for Insights and Recommendations.

```







```

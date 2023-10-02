# Superstore-Sales-Analysis

Objective: Identifying the patterns in our products, regions, categories and customer segments for efficiency and profit optimization with Excel, SQL and Power BI.

How: Our analysis in question will be carried with Excel, SQL and finally Power BI. Excel will serve as the first repository for our data, SQL will give meaning to our data and Power BI will give a clear face to our data. The following sales performance analysis will follow the 6 steps of Data Analysis which are: Ask, Prepare, Process, Analyze, Share and Act.

**Step 1: Ask**

In this step, we will define the business problem given to us which was interpreted as “What are the best products, regions, categories and customer segments for the Superstore to target or avoid in order to increase profitability?”

Business objectives:
How can we optimize our profits?
What are the emerging trends that we can identify?
How can we take these insights to build recommendations ?

Deliverables:
A clear summary of the business objectives.
A full documentation of all the data cleaning, manipulation and analysis.
A dashboard with visualizations and main outcomes.
Recommendations based on our insights and analysis.

**Step 2: Prepare**

In this phase, we will identify and assess the features of our Superstore Dataset:

The data is publicly available through Kaggle under https://www.kaggle.com/datasets/vivek468/superstore-dataset-final.

It comes with 9995 rows with 9994 being pure data and the other one row being the column headers. It contains data recorded between the 3rd of January 2014 (the first order date) to the 5th of January 2018 (the last shipping date). (The last order date is the 30th of December 2017, so we will instead use the order dates range to represent our 4 years of business).

It contains the data of 793 customers.

The data contains the 21 columns namely; Row ID, Order ID, Order Date, Ship Date, Ship Mode, Customer ID , Customer Name, Segment, Postal Code, City, State, Country, Region, Product ID, Category, Sub-Category, Product Name, Sales, Quantity, Discount and Profit.

The only limitations of our dataset that I could mention is that the most recent data point was almost 6 years ago. So our data is not current. However, our data is quite reliable, original, comprehensive and is cited.

**Step 3: Data Processing**

We will process and clean our data with the help of Excel as the file is already a CSV file so a look through of our data with Excel can be ideal to:

Observe our data
Check for missing data with the help of conditional formating
Remove duplicate rows
Correctly format columns for easy SQL analysis

Now our dataset is ideal for analysis to discover relationships, trends and patterns that will give us a competitive edge and completely solve our business objectives.

**Step 4: Data Analysis**

For the analysis part, we will string out the most important components of our data to answer our business objectives.

Okay, let’s perform an exploratory data analysis with our input on the superstore dataset. A list of tasks will be answered followed by the query input and query result. At the end of our analysis, we will transition to a dashboard reflecting the answers to the most important components that will solve the business problem posed upon us.

**Questions:**
What are total sales and total profits of each year?
	select  DATE_PART('YEAR',  "Order Date") AS year,
		sum("Sales") AS sales_count,
	    sum("Profit") AS profit_count
from superstore
group by 1

What are the total profits and total sales per quarter?
select  EXTRACT(YEAR from "Order Date") AS Year,
		EXTRACT(Quarter from  "Order Date") AS Quarter,
		sum("Sales") AS sales_count,
	    sum("Profit") AS profit_count
from superstore
group by 1,2
order by 1,2

What region generates the highest sales and profits ?
select  "Region",
		sum("Sales") AS sales_count,
	    sum("Profit") AS profit_count
from superstore
group by 1
order by sales_count DESC
limit 1

What state and city brings in the highest sales and profits ?
Top 10 States:
select  "State", 
		sum("Sales") AS sales_count,
	    sum("Profit") AS profit_count,
from superstore
group by 1
order by profit_count DESC
limit 10
Bottom 10 States:
select  "State", 
		sum("Sales") AS sales_count,
	    sum("Profit") AS profit_count,
from superstore
group by 1
order by profit_count ASC
limit 10

Top 10 Cities:
select  "City", 
		sum("Sales") AS sales_count,
	    sum("Profit") AS profit_count
from superstore
group by 1
order by profit_count DESC
limit 10

Bottom 10 Cities:
select  "City", 
		sum("Sales") AS sales_count,
	    sum("Profit") AS profit_count
from superstore
group by 1
order by profit_count ASC
limit 10


The relationship between discount and sales and the total discount per category.
Discount & AVG Sales:
SELECT Discount, AVG(Sales) AS Avg_Sales
FROM superstore
GROUP BY Discount
ORDER BY Discount;

Total Discount per Product Category & Sub Category:
select  "Category", “Sub Category”
		sum("Discount") AS total_discount
from superstore
group by 1,2
order by total_discount DESC

What category generates the highest sales and profits in each region and state ?
State:
SELECT region, category, SUM(sales) AS total_sales, SUM(profit) AS total_profit
FROM superstore
GROUP BY region, category
ORDER BY total_profit DESC;

Region:
SELECT region, category, SUM(sales) AS total_sales, SUM(profit) AS total_profit
FROM superstore
GROUP BY region, category
ORDER BY total_profit DESC;

What subcategory generates the highest sales and profits in each region and state?
State:
SELECT "State", "Sub Category", SUM("Sales") AS total_sales, SUM("Profit") AS total_profit
FROM superstore
GROUP BY "State", "Sub Category"
ORDER BY total_profit DESC;

Region:
SELECT "Region", "Sub Category", SUM("Sales") AS total_sales, SUM("Profit") AS total_profit
FROM superstore
GROUP BY "Region", "Sub Category"
ORDER BY total_profit DESC;

What are the names of the products that are the most and least profitable to us?
Most Profitable Product:
SELECT "Product Name", SUM("Sales") AS total_sales, SUM("Profit") AS total_profit
FROM superstore
GROUP BY "Product Name"
ORDER BY total_profit DESC;

Least Profitable Product:
SELECT "Product Name", SUM("Sales") AS total_sales, SUM("Profit") AS total_profit
FROM superstore
GROUP BY "Product Name"
ORDER BY total_profit ASC;

What segment makes the most of our profits and sales ?
SELECT "Segment", SUM("Sales") AS total_sales, SUM("Profit") AS total_profit
FROM superstore
GROUP BY 1
ORDER BY total_profit DESC;

How many customers do we have (unique customer IDs) in total and how much per region and state?
	Most Customers per each State:
	SELECT "State", COUNT(DISTINCT "Customer ID") AS total_customers
FROM superstore
group by 1
ORDER BY total_customers DESC;

Most Customers per each Region:
SELECT "Region", COUNT(DISTINCT "Customer ID") AS total_customers
FROM superstore
group by 1
ORDER BY total_customers DESC;

Customer rewards program
SELECT  "Customer ID",
		sum("Sales") AS total_sales,
		sum("Profit") AS total_profit
FROM superstore
group by 1
ORDER BY total_sales DESC
limit 20

Average shipping time per class and in total
SELECT "Ship Mode", ROUND(AVG("Ship Date" - "Order Date"),1) AS avg_shipping_time
FROM superstore
group by 1
order by avg_shipping_time

**Step 5: Share**

Power BI Charts

![image](https://github.com/syedshahan/Superstore-Sales-Analysis/assets/67556753/478e0a22-0572-4ba5-a7bf-949369e8639c)

**Step 6: Act**

With everything that was covered, here are our conclusions and future recommendations for the success of our Superstore:
Our profits got progressively better. Our sales too even with a short halt in 2015. We should keep the pace up on that aspect.

Our most profitable quarter all year round was Q4. To maximize even more profits, we must make sure to have enough stock and push our marketing and customer service to make the most out of the October — December festive period.

The most performing regions are the West then the East, South and Central regions in that order. The Central region brings in at least $100,000 more in sales than the South region but still makes less profits than it. There is work to be done in the Central region if we really want to keep that market. However, I believe it is better to take some of the resources in our Central region to instead our West region stores as we are more profitable there and could really establish ourselves as kingpin in that region.
California, New York and Washington are our most profitable markets and most present ones especially in terms of sales as states. We have to focus more on them. Our least profitable markets are Texas, Ohio, and Pennsylvania. Which I believe that we should decrease our presence there or even put a halt at our store locations there as sales in Texas and Pennsylvania are in the $100,000s but are unable to convert to profits.

New York City, Los Angeles and Seattle are our most profitable cities and we list them as being a top priority because it is easier to rule a city than ruling a state. If we gain the city, gaining the state will be less challenging. Philadelphia, Houston and San Antonio are the cities where we lose the most money. We have 2 cities from Texas in our top 3 cities so it is clear that we have start rethinking about really wanting to carry business there, the better option would be to stop.
Out of the 3 categories, Technology and Office Supplies are the best in terms of profits. Plus they seem like a good investment because of their profit margins. Furnitures are still making profits but do not convert well in overall. With low profits and low profit margins, we should start to see what more we can bring to the furniture department. The sales are there but they do not translate smoothly.

Still under categories but regionally, Office supplies in the West brings the most profit so we must increase the cap of those materials over there. Same thing with the East and office supplies and both the East and West with Technology. However, furniture in the Central region is the only category that doesn’t convert to profits so it would be better to take some of these resources to the West region which is the biggest gainer in terms of Furniture.

Statewise, Technology and Office supplies brings us the most profit in the state of New York and California. We have to increase the availability of these goods in these states for better profits. However, Office supplies in Texas, Technology in Ohio and Furniture in Texas and Illinois are our biggest losses so we have to drastically reduce these type of products in those areas.

Out of our 17 subcategories nationwide, our biggest profits comes from Copiers, Phones, Accessories and Paper. The profits and profit margins on Copiers and Papers especially are interesting for the long run. We should immediately push these products as we have a great market share with these items. Our losses came from Tables, Bookcases and Supplies where we are uncapable of breaking even. We must spend less time and money with them. Especially with tables because compared to our only 3 losses, Tables lost us $17725 which is huge compared to our other losses of $3472 and $1188 which came from Bookcases and Supplies respectively.

For subcategories regionally, Copiers in the West and East with Accessories and Binders in the West are products that we always have to have in stock and promote for more profit. While Tables in the East, South and Central with furnishings in the Central region are the top products where we lose money so we should direct our attention elsewhere.
In what concerns subcategories by state, Machines, Phones and Binders perform very well in New York. Followed by Accessories and Binders in California and Michigan respectively so there is a need to accentuate our business there with those products. For our biggest losses, Binders in Texas and Illinois with machines in Ohio are not profitable at all. We have to decrease stock in those places.

For the particular products, The Canon imageClass 2200 Advanced Copier, Fellowes PB500 Electric Punch Plastic Comb Binding Machine with Manual Bind and the Hewlett Packard LaserJet 3310 Copier are our top 3 in profits. We must always keep up the stock with these. For our losses, The Cubify CubeX 3D Printer Double Head Print, Lexmark MX611dhe Monochrome Laser Printer and the Cubify CubeX 3D Printer Triple Head Print are the products that operate the most at a loss. We should certainly discontinue those products.
Out of the 3 segments, The consumer segment brings in the most profit followed by Corporate and then Home office. We must give more importance to the consumer segment even if all the 3 are profitable.

Finally, for our clientele, we have 793 customers total, and we have the most customers in California, New York and Texas. The case of Texas is pretty ironic since it is also the state that losses us the most money. So we must take a critical decision about Texas first as we absolutely can’t break through now. California and New York are pretty obvious, we have to be outstanding and be the best of what there is to offer in our respective niche.




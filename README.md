# Northwind_Traders

## Project Overview
Northwind Traders is a global supplier of speciality food products. This project focuses on analyzing customer orders, product performance, shipping efficiency and sales trend to help optimize their operations. 

I was responsible for designing and building a database from the provided dataset, then querying it to extract meaningful insights. Using SQL and Power BI, I explored key business metrics, answered crital business questions and developed an interactive dashboard.

The goal was to uncover growth opportunities, improve operational efficiency and support data-deriven decision making.

### Dashboard Requirement

 - Key Metrics:
    - Total Orders
    - Total Revenue
    - Average Order Value
    - Shipping Efficiency (Average Shipping Time)
- Business Questions:
    - Are there any noticeable sales trends over time?
    - Which are the best and worst selling products?
    - Can you identify any key customers?
    - Are shipping costs consistent across providers?
    - How fast is their delivery service, how many orders are delivered on time or late?

### Tools Used
- Excel - Data cleaning and Preparation
- Structure Query Language (SQL) - Querying and extracting insights from the database
- Power Bi - Interactive dashboard creation for visualization and analysis

  ### Data Source
The dataset used for this analysis can be accessed in Microsoft Excel download here

### Data Cleaning
- the dataset was cleaned in excel to ensure consistency and accuracy before analysis.
- Duplicate were identified and removed.
- Missing values were handled usind the mean, replacing them with the average avaliable data.

### Exploratory Data Analysis (EDA)
- Using postgress SQL the dataset was queried to uncover sale trend, product performance, customer behaviour and shipping efficiency
- Identified patterns, seasonality and correlations.
- Using Power Bi I visualized Key Metrics and buusiness questions by creating an interactive dashboard. 

### SQL Query
- Key Metrics

Total Orders
```sql
SELECT
	COUNT(DISTINCT order_id) AS Total_orders
FROM orders;
Total Revenue
```

```sql
SELECT
	SUM(od.quantity * p.unit_price *(1-od.discount)) AS total_revenue
FROM order_details AS od
JOIN products p
ON od.product_id = p.product_id;
Average Order Value
```

```sql
SELECT
 	SUM(od.quantity * p.unit_price*(1-od.discount))/
	COUNT(DISTINCT o.order_id) AS Average_order_Value
FROM orders AS o
JOIN order_details od
ON o.order_id = od.order_id
JOIN products p
ON od.product_id = p.product_id;
Shipping Efficiency (Average Shipping Time)
```

```sql
SELECT
CAST(AVG(shipped_date - order_date) AS INTEGER) AS Average_shipping_time
FROM orders;
```

- Business Questions
1. Are there any noticeable sales trends over time?

```sql
SELECT
	CASE
	WHEN month = 1 THEN 'January'
	WHEN month = 2 THEN 'February'
	WHEN month = 3 THEN 'March'
	WHEN month = 4 THEN 'April'
	WHEN month = 5 THEN 'May'
	WHEN month = 6 THEN 'June'
	WHEN month = 7 THEN 'July'
	WHEN month = 8 THEN 'August'
	WHEN month = 9 THEN 'September'
	WHEN month = 10 THEN 'October'
	WHEN month = 11 THEN 'November'
	WHEN month = 12 THEN 'December'
	END AS month_name, total_sales
FROM (
	SELECT
	EXTRACT(MONTH FROM order_date) AS month,
	SUM(od.quantity * p.unit_price *(1-od.discount)) AS total_sales
FROM orders AS o
JOIN order_details od
ON o.order_id = od.order_id
JOIN products p
	ON od.product_id = p.product_id 
GROUP BY EXTRACT(MONTH FROM order_date)
) AS subquery
ORDER BY total_sales DESC;
```

- Year
```sql
SELECT
	EXTRACT(YEAR FROM order_date) AS YEAR,
	SUM(od.quantity * p.unit_price *(1-od.discount)) AS total_sales
FROM orders AS o
JOIN order_details od
ON o.order_id = od.order_id
JOIN products p
	ON od.product_id = p.product_id 
GROUP BY EXTRACT(YEAR FROM order_date)
ORDER BY total_sales DESC;
```

2.	Which are the best and worst selling products?
-	Best Selling Product

  ```sql
SELECT
	product_name,
	SUM(od.quantity) AS total_quantity,
	SUM(od.quantity * p.unit_price *(1-od.discount)) AS total_revenue
FROM products AS p
JOIN order_details od
	ON p.product_id = od.product_id 
GROUP BY product_name
ORDER BY total_quantity DESC
LIMIT 5;
```

- Worst Selling Products

```sql
SELECT
	product_name,
	SUM(od.quantity) AS total_quantity,
	SUM(od.quantity * p.unit_price *(1-od.discount)) AS total_revenue
FROM products AS p
JOIN order_details od
	ON p.product_id = od.product_id 
GROUP BY product_name
ORDER BY total_quantity ASC
LIMIT 5;
```

3.	Can you identify any key customers?

```sql   
SELECT
	c.customer_id,
	c.company_name,
	SUM(od.quantity * p.unit_price *(1-od.discount)) AS total_revenue
FROM customers AS c
JOIN orders o
ON c.customer_id = o.customer_id
JOIN order_details od
ON o.order_id = od.order_id
JOIN products p
ON od.product_id = p.product_id
GROUP BY c.customer_id
ORDER BY total_revenue DESC
LIMIT 5;
```

4.	Are shipping costs consistent across providers?

```sql   
SELECT
	s.company_name,
	ROUND(AVG(o.freight), 2) AS average_shipping_cost,
	MAX(o.freight) AS max_shipping_cost,
	MIN(o.freight) AS min_shipping_cost,
	ROUND(STDDEV_SAMP(o.freight), 2) AS stddev_shipping_cost,
	(MAX(o.freight) - MIN(o.freight)) AS range_shipping_cost
FROM shippers AS s
JOIN orders o
ON s.shipper_id = o.shipper_id
GROUP BY s.company_name 
ORDER BY stddev_shipping_cost DESC;
```

5.	How fast is their delivery service, how many orders are delivered on time or late?

```sql
SELECT
	CASE
	 WHEN shipped_date <= required_date THEN 'On time'
	 ELSE 'late'
	 END AS delivery_status,
	 COUNT(order_id) AS total_orders
FROM orders
GROUP BY delivery_status;
```

### Key Insight 
- Revenue Fluctuation
   - Northwind revenue fluctuated due to the dataset covering only the second half of 2013, the fll year of 2014 and the first half of 2015.
   - The partial dataset affects revenue comparison across all states.

- Are there any noticeable sales trends over time?
   - There is a downward noticeable sales trend overtime.
   - Peak sales occurs from October to April, indicating strong demand during these months.
   - Sales decline between May to September, showing a seasonal drop in demand.

- Best/Worst selling product
   - Products performance varied by year, with some items performing well in one year but declining in another.
   - This shows change in customer preferences and market demand.
 
- Key customer
   - SAVEA is the key customer, generating $94,063 in revenue, followed by ERNSH with $85,630.
   - SAVEA consistently remained the key customer from 2014 to 2015, indicating repeat purchased and strong loyalty.
     
- Shipping cost Consistency
   -  Shipping cost vary significantly across different providers.
   -  Federal shipping has the higest shipping cost, while Speedy Express offers the lowest rate.
 
- Delivery service performance
  - On time delivery is generally consistent across all providers, indicating efficient logistics and order fufillment.

### Recomendations
- deeper analysis of revenue fluctuations should be conducted to understand the major impact of seasonal trend.
- Implement targeted marketing campagins and promotions during low sales month to drive sales.
- Best performing product should be stocked up more and under performing products should be discontinued orprice should be adjusted in other to increase sales.
- Relationship with key customers should be strengthen like SAVEA and ERNISH by offering discounts and gifts.
- Use customer purchase behaviour analysis to create personalized marketing strategies.
- Social media and digital marketing should be well utilized to drive brand awareness and customer acqusitions.
- Shipping companies offering fast and reliable services at competitive rate should be partenered with.



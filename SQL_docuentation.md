# This files contains all the Sql Queries used in this analysis

### SQL Query
- Key Metrics

Total Orders
```sql
SELECT
	COUNT(DISTINCT order_id) AS Total_orders
FROM orders;
```

Total Revenue
```sql
SELECT
	SUM(od.quantity * p.unit_price *(1-od.discount)) AS total_revenue
FROM order_details AS od
JOIN products p
ON od.product_id = p.product_id;
```

Average Order Value
```sql
SELECT
CAST(AVG(shipped_date - order_date) AS INTEGER) AS Average_shipping_time
FROM orders;
```

## Business Questions
- Are there any noticeable sales trends over time?

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

- Calculating for year trend
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

1 - Which are the best and worst selling products?
    - Best Selling Product

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

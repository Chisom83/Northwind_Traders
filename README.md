
# Northwind_Traders

![Pizza Pro](https://github.com/Chisom83/Northwind_Traders/blob/main/Image%202/N.orthwind.jpg?raw=true)

## Table of Content
[Project Overview](#project-overview)

[SQL Query](#sql-query)

[DAX Measures](#dax-measures)

[Key Insight](#key-insight)

[Recomendations](#recomendations)

[Dashboard](#dashboard)


## Project Overview
Northwind Traders is a global supplier of speciality food products. This project focuses on analyzing customer orders, product performance, shipping efficiency and sales trend to help optimize their operations. 

I was responsible for designing and building a database from the provided dataset, then querying it to extract meaningful insights. Using SQL and Power BI, I explored key business metrics, answered crital business questions and developed an interactive dashboard.

The goal was to uncover growth opportunities, improve operational efficiency and support data-deriven decision making.

### KPIs and Business Requirement

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
- Missing values were handled using the mean, replacing them with the average avaliable data.

### Exploratory Data Analysis (EDA)
- Using postgress SQL the dataset was queried to uncover sale trend, product performance, customer behaviour and shipping efficiency
- Identified patterns, seasonality and correlations.
- Using Power Bi I visualized Key Metrics and buusiness questions by creating an interactive dashboard. 

### SQL Query
View all SQL queries for this analysis [View SQL Queries](./SQL_docuentation.md)   

### DAX Measures
[View DAX Measures](./DAX_Measures.md)   

### Key Insight 
- This analysis covers sales from mid 2013 to mid 2015.
### KPI
#### Total Revenue
![Total Revenue](https://github.com/Chisom83/Northwind_Traders/blob/main/Image%202/N.Rev.png?raw=true)

- Insight:
- A total of $1 million in revenue was generated across the period.
     - 2013 generated $227K covers only the second half of the year data.
     - 2014 generated 565K for full year data.
     - 2015 generated 339K covers only the first half of the year data.
     - In 2014 revenue increased by apporimately 149% compared to 2013. While in 2015 revenue droped by 40% relative to the previous year.    
- Measure Used: [Total Revenue](DAX_Measures.md#total-revenue), [PYRevenue](DAX_Measures.md#pyrevenue)
 
#### Total Orders
![Total Orders](https://github.com/Chisom83/Northwind_Traders/blob/main/Image%202/N.Ord.png?raw=true)

- Insight:
 A total of 700 orders were recorded.
     - 2013: 130 orders.
     - 2014: 359 orders.
     - 2015: 211 orders.
  
- Measure Used: [Total Orders](DAX_Measures.md#total-orders), [PYOrders](DAX_Measures.md#pyorders)
  
#### Average Order Value
![AOV](https://github.com/Chisom83/Northwind_Traders/blob/main/Image%202/N.AOV.png?raw=true)

- Insight:
$1.62K is the overall AOV.
    - 2013: $1.75K.
    - 2014: $1.58K.
    - 2015: $1.60K.
    - In 2013, AOV exceeded the overall AOV which shows that customers made fewer but larger purchase.
    - While in 2014 the AOV is slghtly low because it had more diverse spending patterns which balanced out the higher AOV in 2013. 

- Measure Used: [AOV](DAX_Measures.md#aov), [PYAOV](DAX_Measures.md#pyaov)

#### Shipping Efficiency (Average Shipping Time)
![Average Shipping Time](https://github.com/Chisom83/Northwind_Traders/blob/main/Image%202/N.AST.png?raw=true)

- Insight:
- Shipping time ranged between 8-9 days, which is considered reasonable fo standard delivery
     - 2013: 8 days
     - 2014: 9 days
     - 2015: 8 days
     - 2014 had slightly longer shipping time compared to other years, but overall delivery performance remained within an acceptable range.

- Measure Used: [Average Shipping Time](DAX_Measures.md#average-shipping-time)

### Business Requirement Insight

#### 1. Are there any noticeable sales trends over time?
![Trend](https://github.com/Chisom83/Northwind_Traders/blob/main/Image/N.Trend.png?raw=true)

- Insight
   - There is a downward noticeable sales trend overtime.
   - Peak sales occurs from October to April, indicating strong demand during these months.
   - Sales decline between May to September, showing a seasonal drop in demand.
- Measure Used:[Total Revenue](DAX_Measures.md#total-revenue) and the Month column.

#### 2. Which are the best and worst selling products?

##### Best Performing

![Best Performing](https://github.com/Chisom83/Northwind_Traders/blob/main/Image/N.TandB.png?raw=true)

##### Worst Performing

![Worst Performing](https://github.com/Chisom83/Northwind_Traders/blob/main/Image/N.W.png?raw=true)

- Insight
   - Products performance varied by year, with some items performing strongly in one year and declining in another indicating shifts in customer preference and market demand.
 
- Measure Used:[Switch Product Top/Bottom](DAX_Measures.md#swith-product-top-bottom) and the the ProductName column.
 
#### 3. Identify any key customers?
![Key Customer](https://github.com/Chisom83/Northwind_Traders/blob/main/Image/N%C3%87ust.png?raw=true)

- Insight
   - SAVEA is the key customer, generating $94,063 in revenue, followed by ERNSH with $85,630.
   - SAVEA consistently remained the key customer from 2014 to 2015, indicating repeat purchased and strong brand loyalty.
- Measure Used:[Total Revenue](DAX_Measures.md#total-revenue) and the CustomerID column.
     
#### 4.Are shipping costs consistent across providers?
   
![Average Shipping Cost](https://github.com/Chisom83/Northwind_Traders/blob/main/Image/N.A.png?raw=true)

- Insight
   -  Shipping cost vary significantly across different providers.
   -  Federal shipping has the higest shipping cost, while Speedy Express offers the lowest rate.
- Measure Used:[Average Freight](DAX_Measures.md#average-freight) and CompanyName column.
 
##### 5. How fast is their delivery service, how many orders are delivered on time or late?

![Late/Ontime Delivery](https://github.com/Chisom83/Northwind_Traders/blob/main/Image/N.LandT.png?raw=true)

- Insight
  - In general delivery is on time and consistent across the three providers, indicating efficient logistics and order fufillment.
     - Ontime delivery: 95.43%
     - Late delivery: 4.57%.

- Measure Used:[OnTimeDelivery](DAX_Measures.md#on-time-delivery), [LateDelivery](DAX_Measures.md#late-delivery).

### Recomendations
- Deeper analysis on revenue fluctuations should be conducted to understand the major impact of seasonal trend.
- Launch targeted marketing campagins and promotions during low sales month (May to september) to drive sales.
- Best performing product should be stocked up more while reviewing or discontinung underperforming product. 
- Relationship with key customers should be strengthen like SAVEA and ERNISH by offering incentives such exclusive discounts or gifts.
- Utilize digital marketing presence (Social media, SEO, email marketing) to  improve brand visibilty and customer acquisition.
- Shipping companies offering fast and reliable services at competitive rate should be partenered with.

### Dashboard
- A screenshot of the dashboard
![Dashboard](https://github.com/Chisom83/Northwind_Traders/blob/main/Image%202/N.Dashboard.png?raw=true)

- Link to dashboard

### Conclusion
By implementing the above recommendations,Northwind Traders can significantly optimize operations and drive strategic growth in subsequent years. Enhancing the company's digital marketing presence especially during low demand periods will boost brand visibility, increase customers acquisition and drive sustainable revenue growth.

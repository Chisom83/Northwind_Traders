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
View all SQL queries for this analysis [View SQL Queries](https://github.com/Chisom83/Northwind_Traders/blob/main/SQL_docuentation.md)

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

### Dashboard
- A screenshot of the dashboard

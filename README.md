# Analysis of sales Data and performance of Products of Axon Company. 

## Table of Contents
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [ Tools](#tools)
- [Data Preparation](#data-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Visualizations](#visualizations)
- [Findings](#findings)
- [Recommendations](#recommendations)
- [References](#references)          

### Project Overview 

This data analysis project aims to provide insights into the sales performance of an Axon company which is a retailer selling classic cars and other product line. By analyzing various aspects of the sales data, we seek to identify trends, make data-driven recommendations, and gain a deeper understanding of the company's performance.

### Data Sources 

Sales Data: The primary dataset used for this analysis is the "Productline.sql" file, containing detailed information about sales,customers,employees ,orders and payments of the company.

### Tools

- SQL Server - Data cleaning and analysis [Download here](https://www.mysql.com/downloads/)

- PowerBI - Data Modeling and Report creation [Download here](https://www.microsoft.com/en-us/download/details.aspx?id=58494)

### Data Preparation

In the initial data preparation phase, we performed the following tasks:

1. Data loading and inspection in Mysql.
2. Connected Mysql with Power Bi by using drivers.
3. Loaded data into power bi.
4. Handled missing values,Replaced null values by useful data when needed,changed data types as per need.
5. Changed columns names for easy understanding and analysis.
6. Removed duplicates whenever need to remove.
7. Deleted unneccesary columns
8. Go through each tables and columns and data cleaning and formatting done.
9. calculated columns generated based on existing columns.

### Exploratory Data Analysis

EDA involved exploring the sales data to answer key questions, such as:

- To display the top 10 products sold from product line available. 
- To Calculate how much revenue generated from each product line .
- To know year on year growth of sales and profit
- To find Who are the top customers in each category 
- To find Country wise sales . 
- Top performing employees. 
- Calculate the pendency in payment by Customers and Countries.
- To show the market share of top brands
- To show trend of sales over time for each car model 
- Which office is most performing .

### Data Analysis  

Calculated column Sales and Profit is generated as  by using  the quantity order and selling price columns and for profit selling price and buy price columns use.
For creating new column following DAX expression was written;

        Sales = 'Order details'[Quantity Ordered]*'Order details'[Selling Price]

        Profit = 'Order details'[Selling Price]-'Order details'[Buy Price]

Snap of new calculated columns:








<img width="155" alt="sales profit github" src="https://github.com/SUMIK01/Axon-company-Products-Performance-analysis/assets/146610054/bb9a11fe-0a56-4463-84bd-132c48ba46ee">



New measure was created to calculate year on year basis sales.

For creating measure following dax function is used,

                 Sales YoY% = 
                 IF(
	            ISFILTERED('Orders'[Order Date]),
	            ERROR("Time intelligence quick measures can only be grouped or filtered by the Power BI-provided date hierarchy or primary date 
                    column."),
	            VAR __PREV_YEAR =
		         CALCULATE(
			     SUM('Order details'[Sales]),
			     DATEADD('Orders'[Order Date].[Date], -1, YEAR)
		         )
	             RETURN
		        DIVIDE(SUM('Order details'[Sales]) - __PREV_YEAR, __PREV_YEAR)
                    )

A visual which represnt the Year on year basis Sales which is calculated by above DAX formula 

<img width="253" alt="YoY" src="https://github.com/SUMIK01/Axon-company-Products-Performance-analysis/assets/146610054/d160074f-fa23-415c-bd24-ecea583a72b0">



The Quick measure created to calculate profit year on year basis 

    Profit YoY% = 
          IF(
	    ISFILTERED('Orders'[Order Date]),
	    ERROR("Time intelligence quick measures can only be grouped or filtered by the Power BI-provided date hierarchy or primary date column."),
	    VAR __PREV_YEAR =
	         CALCULATE(
		     SUM('Order details'[Profit]),
		     DATEADD('Orders'[Order Date].[Date], -1, YEAR)
		)
	   RETURN
	      DIVIDE(SUM('Order details'[Profit]) - __PREV_YEAR, __PREV_YEAR)
            )


New measure Profit margin is created with the help of profit and sales.

The DAX formula used to create this mesure is as below,

                 Profit Margin = SUMX('Order details',('Order details'[Profit] /SUM('Order details'[Sales]) ))

To calculate the pending amount I have created new measure pending payment using following DAX formula.

                 Payment Pending = sum('Order details'[Sales]) - sum(Payments[Amount])

   

By using above measure some useful visuals were created which gave useful insights shown below.

<img width="464" alt="pending payment  for github" src="https://github.com/SUMIK01/Axon-company-Products-Performance-analysis/assets/146610054/7f3fda70-d243-434a-9b9c-052b6a1cd14a">


### Visualizations 

On the basis of objective of the project the useful visualization were created in page wise report and out of which some importants interactive visualizations were added in Overview report which is attached below.



<img width="586" alt="The report github" src="https://github.com/SUMIK01/Axon-company-Products-Performance-analysis/assets/146610054/23c6c5c2-c5c7-4036-ab3a-bba5fada9f10">




### Findings 

The analysis results are summarized as follows:

#### Product lines:
- Total sales of all product line is $9.6 M and profit $108.44K 
- Classic Cars product line having highest sale and profit of $3.85 M and 
  $43.16K.
- Trains are having lowest in sale and profit is also less as only 3 articles are 
  available .
- Ferrari 360 Spider red is the top performing product from all the products
- Vintage cars and motorcycles are having more profit margin on average 
  1.17% 
- Need to think about the profit margin of Porsche 356A coupe of classic car 
  product line as sale is good but profit is less .

#### Sales:
- USA has most sales amongst all Countries
- France overtaken USA in sale in year 2005
- Inside USA San Francisco generated maximum sales 16.11 K 
- The year 2005 has lowest sales Year on year basis
- he growth of company is declining

#### Customers
- USA received most orders (56.25%)
- The top customer is Euro shopping channel from Spain placed 26 orders 
  with highest sale and profit 
- The Paris office is top performing in the world which generated 106 order 
  by maximum sale and profit
  
#### Employees:
- Total Employees are 23 and out of which 17 employees are sales 
  representative.
- Employees from London office are more hardworking as 2 employees made 
  47 orders.
- Tokyo office employees are below performer as only 16 orders generated 
- Gerard Hernandez is the top performing sales representative from Paris 
  office completed 43 orders alone and generated $1.25 M sales and $13.7K 
  profit.

 #### Payments:
 
- USA is having most pendency in payment at about $233.25k .
- Euro shopping channel customer from Spain is having amount to be paid 
  $104.95K
- The sharp Gifts Warehouse customer from USA is also having pendency of 
  payment of amount $83.98K.
- Customers those are from countries Norway,Japan,Germany,Canada,Hong 
  Kong and Ireland paid all the amount

### Recommendations

- As year on year sales and profit are decreasing comapany should do business audit and try to find out the reasons of negative growth
- Paris office are giving 3 times more business than others so should implement the same strategies in other offices also or they can give training to other employees.
- Should be focus on product promotions and marketing .

### References
   Sales Dashboard: This project involves creating a dashboard to visualize sales data using PowerBI. It includes charts, graphs, and tables that provide insights into 
   sales performance over time, customer demographics, and product popularity. (https://www.netsolutions.com/casestudy-ecom-dashboard)
   
   SQL Sales Analysis: This project involves using SQL to perform advanced analytics on sales data and extract insights that can inform decision-making. It includes tasks 
   such as creating pivot tables, running queries, and creating views. (https://medium.com/swlh/data-anlysis-project-for-retail-sales-performance-report-using-sql- 
   6ef1d4443712)

   Referred website https://www.investopedia.com/terms/p/product-line.asp
  
  




   

   

           


  

    

   

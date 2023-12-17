# Analysis of sales Data and performance of Products of Axon Company. 

### Project Overview 

This data analysis project aims to provide insights into the sales performance of an Axon company which is a retailer selling classic cars and other products. By analyzing various aspects of the sales data, we seek to identify trends, make data-driven recommendations, and gain a deeper understanding of the company's performance.

### Data Sources 

Sales Data: The primary dataset used for this analysis is the "Productline.sql" file, containing detailed information about each sale made by the company.

### Tools

- SQL Server - Data cleaning and analysis [Download here](https://www.mysql.com/downloads/)

- PowerBI - Data Modeling and Report creation [Download here](https://www.microsoft.com/en-us/download/details.aspx?id=58494)

### Data Cleaning/Preparation

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
           


  

    

   

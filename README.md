# FESTIVEBUYS-STORES-ANALYSIS
## Introduction:

This project aims to show my data analysis and visualization skills using SQL, 
MS Excel and data modelling skills using powerBI. The problem statement is an imaginary concept
I think the stakeholders would be intrested in.

## PROBLEM STATEMENT

FestiveBuys is a fictional American retail store chain on the cusp of an exciting expansion with retail outlets in 3 states.
As the company prepares to establish its new headquarters, the stakes are high.
The opening event promises not only to celebrate the brand's success but also to 
recognize and reward exceptional contributors. 

After citical thinking, three pivotal questions demand answers:

1. In which location have we achieved the highest sales?
2. Which sales representative has consistently achieved the highest sales figures?
3. Who among our esteemed customers has made the most substantial purchases, contributing significantly to our success?

 
## DATA SOURCING

Dataset was gotten from kaggle in a csv format.
The information where categorically seperated into 9 different tables.
The Tables include:

1. production.products
2. production.brands
3. production.categories
4. sales.stores
5. sales.staff
6. sales.staff
7. sales.orderItems
8. production.stocks
9. sales.customers



Data was imported into Microsoft SQL server and wranggled.

I used SQL joins to form the table that contained all the information I needed for this project...Click here to see the SQL queries

```SQL

  SELECT 
  ord.order_id,
  CONCAT(cus.first_name, ' ', cus.last_name) AS customers,
  cus.city,
  cus.state,
  ord.order_date,
  SUM(ite.quantity) AS 'total_units',
  SUM(ite.quantity * ite.list_price) AS revenue,
  pro.product_name,
  cat.category_name,
  sto.store_name,
  CONCAT(sta.first_name, '', sta.last_name) AS salesMan


  FROM 
  sales.orders ord
  JOIN sales.customers cus
  ON ord.customer_id = cus.customer_id
  JOIN sales.order_items  ite
  ON ord.order_id = ite.order_id
  JOIN production.products pro
  ON ite.product_id = pro.product_id
  JOIN production.categories cat 
  ON pro.category_id = cat.category_id
  JOIN sales.stores sto
  ON ord.store_id = sto.store_id
  JOIN sales.staffs sta
  ON ord.staff_id = sta.staff_id
 

	GROUP BY
		ord.order_id,
		CONCAT(cus.first_name, ' ', cus.last_name) ,
		cus.city,
		cus.state,
		ord.order_date,
		pro.product_name,
		cat.category_name,
		sto.store_name,
		CONCAT(sta.first_name, '', sta.last_name)
```

View data source [Here](https://kaggle.com)


## DATA TRANSFORMATION

The dataset was imported into Power Bi from SQL.
Power Query was used to perform data cleaning. After properly cross-checking all the columns they were found
to be valid, complete, and void of null values.
However unwanted and irrelevant columns such as the category_name column were removed. The data type of the date was properly 
formatted.

Below screenshot of power cleaning with power query.

![](powerQuery.png)





## DATA VISUALIZATION

A power BI dashboard was designed to visualize our findings from the dataset 
provided.
Below is a screenshot of the dashboard for the executives.

![](festiveBuys_Dashboard.png)

View Dashboard [Here](BikeStore Visualize.pbix)



## CONCLUSIONS AND RECOMMENDATIONS.

1. The state of New York happens to generate the highest revenue for the company.
   Hence it's the most appropriate to locate the new office headquarters.

2. Marcelen Boyer is the salesman with the highest sales in terms of revenue raked in.
   Hence he should be considered for the sales manager position at the new office headquarters.

3. Pamella Newman is our top customer and should be recognized, awarded, and given company incentives such as 
   a car, a vacation, and discounts on subsequent purchases.







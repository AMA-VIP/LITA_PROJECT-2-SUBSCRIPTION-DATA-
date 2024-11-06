# LITA_PROJECT2: SUBSCRIPTION_DATA
SUBSCRIPTION DATA

## OVERVIEW
The project involves analysing subscription data to understand customer trends, retention rates, and other key performannce indicators. 

## AIM
This analysis aims at:
- Providing insights into subscriber behaviours
- Identify areas for potential growth

## DATA DESCRIPTION
The dataseet include the following on subscribers, their subscription plans, and their engagement with the service. Key columns in the data includes:
- CustomerID: Unique idedntifier for each customer
- Subscription_Start_Date: Date the customer's started their subscription
- Subscription_End_Date: Date the customer's subscription ended
- Subscription_Plan: The type of plan the custmer subscribed to.

## OBJECTIVES 
The primary objectives of this analysis are 
1. Customer Retention: Analysing retention rates to understand how long customer stayed subscribed
2. Churn Analysis: Identify possible reasons why customer stopped using a subscription type
3. Revenue Insights: Understanding the revenue contributions from different subscription plans, and different region
4. Engagements Trends: Observing usage pattern across various customer segements

## DATA CLEANING 
To ensure data quality, the following cleaning steps was carefully observed 
- Handling Missing Values: The data was critically observed for missing values
- Removed Duplicates: Duplicate entries were carefully checked for
- Outlier Detection: I carefully checked out for unusual values in Subscription duration

## EXPLORATORY DATA ANALYSIS (EDA)
Key analysis and visualization includes 
- Sum Of Revenue by Region: Clustered Column Chart was used to find the sum of revenue gotten from each region
- Sum of Revenues: The card chart was used to show the total sum of revenue gotten from the period of time
- Count of CustomerID by Cancelled: this was used to analyse the churn rate - the percentage of customers who cancelled their subscriptions (FALSE) 
- Subscription_Type by Revenue: Table was used to show the Subscription Type and revnue gotten from each subscription type.
- Total_Number_of_Customer: The total number of customer was displayed using a card Chart
- Cancelled_Subscription: Cancelled subscription was displayed using a card chart
- Retention_Rate: Retention rate was also displayed using a card chart

## INSIGHT AND FINDINGS

- High retention by subscription type: More persons subscribed to the basic subscription type with 10 customers in total, 7 returned and 3 cancelled, which means high retention rate was find in the basic subscripton type.

## TOOLS 
1. Excel: Pivot table was used to gain insight
    
2. SQL
- Retrieve the total number of customers from each region. 
   ```SQL
   select Region, count(distinct customerID) as Total_Customers
   from [dbo].[Customer subscription data]
   group by Region
   ```
- Find the most popular subscription type by the number of customers.
  ```SQL
  select top 1  SubscriptionType,
  count (distinct CustomerID) as Customer_Count
  from [dbo].[Customer subscription data]
  group by SubscriptionType
  order by Customer_Count desc
  ```
 - Find customers who canceled their subscription within 6 months.
    ```SQL
    select top 10 *
    from [dbo].[Customer subscription data]
    ```
    
  ```SQL
  select
  CustomerName,
  Subscription_Start,
  Subscription_End
  from[dbo].[Customer subscription data]
  where
  Cancelled = 'TRUE'
  ```

  ```SQL
  select
  CustomerName,
  Subscription_Start,
  Subscription_End
  from
  [dbo].[Customer subscription data]
  where
  cancelled = 'TRUE'
  and Datediff(month,
  Subscription_Start, Subscription_End) <= 6
  ```
- Calculate the average subscription duration for all customers.
  ```SQL
  select
  AVG(DATEDIFF(day,
  try_cast(Subscription_Start as date), try_cast(Subscription_End as date))) as 
  Average_Subscription_Duration
  from
  [dbo].[Customer subscription data]
  where
  Subscription_Start is not null and Subscription_End is not null
  ```
- Find customers with subscriptions longer than 12 months.
  ```SQL
  select
  CustomerID,
  CustomerName,
  Subscription_Start,
  Subscription_End,
  datediff(month,
  try_cast(Subscription_Start as Date), try_cast(Subscription_End as Date)) as 
  Subscription_Duration_Months
  from
  [dbo].[Customer subscription data]
  where
  datediff(month,
  try_cast(Subscription_Start as Date), try_cast(Subscription_End as Date)) > 12;
  ```

- Calculate total revenue by subscription type.
  ```SQL
  select
  SubscriptionType,
  sum(try_cast(Revenue As decimal(10,2))) as Total_Revenue
  from
  [dbo].[Customer subscription data]
  group by 
  SubscriptionType
  ```
- Find the top 3 regions by subscription cancellations.
  ```SQL
  select
  Region,
  count (*) as Cancellation
  from
  [dbo].[Customer subscription data]
  where
  Cancelled = 'TRUE'
  group by 
  Region
  order by 
  Cancellation desc
  ```

- find the total number of active and canceled subscriptions.
  ```SQL
  select
  count(case when cancelled = 
  'FALSE' then 1 end) as
  Active_Subscriptions,
  count(case when cancelled =
  'TRUE' then 1 end) as Cancelled_Subscriptions
  from
  [dbo].[Customer subscription data]
  ```

4. PowerBI: More measures were created to find more insights on total number of customers, cancelled customers that stopped subscriptions, and retention rates. The following queries 
   were used to create the following measures.
   
- To calculate the total number of returning customers
  
     ```PowerBI
     Returning_Customers = calculate(
     DISTINCTCOUNT('Customer subscription data'[CustomerID]),
     FILTER('Customer subscription data', 'Customer subscription data'[Cancelled] = FALSE)
     )
     ```
- Calculate Retenton Rate
  
    ```PowerBI
    Retention_Rate =
    DIVIDE([Returing_Customer],
    [Total_Customers], 0)
    ```

- Calculate Cancelled Customer 

   ```PowerBI
   Cancelled_Customer = CALCULATE(
   DISTINCTCOUNT('Customer subscription data'[CustomerID]),
  'Customer subscription data'[Cancelled] = TRUE
   )
  ```
  
    

  

# LITA_PROJECT2: SUBSCRIPTION-DATA-
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
4. PowerBI

  

# LITA-CAPSTONE-PROJECT-CUSTOMER-DATA

# LITA-Capstone-project

### Project Title : Customer segmentation for a Subscription Service 

[Project Overview](#project-overview)

[Data Sources](#data-sources)

[Tools Used](#tools-used)

[Data Cleaning and Preparation](#data-cleaning-and-preparation)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)




### Project Overview
---
This customer subscription service segmentation analysis provides valuable insights for a subscription service over a specified timeframe. By examining various parameters within the data, I gained a comprehensive understanding that facilitated informed decision-making. This process allowed me to derive narratives from the insights obtained, enriching my understanding of customer subscription.

### Data Sources 
---
The primary source of data here is LITA Capstone Dataset(sales data) which was provided by my facilitator 

### Tools Used 
---
-Microsoft Excel  
   1. Data cleaning
   2. Analysis
   3. Visualization
      
-SQL- Structured Query Language
   1. Querying of data
      
-Power BI
   1. Data analysis
   2. Visualization

### Data Cleaning and Preparation
---
Cleaning of the data was the first phase to enable me have a clean data to work on so as to get the accurate result.
  1. Data loading and review
  2. Removing of Duplicate data
  3. Data formatting
### Exploratory Data Analysis 
---
This invloves analyzing the data to enable better understanding of the data set, they include;
  1. Average subscription duration
  2. Most Popular subscription type
  3. Subscription by revenue 
  4. Region by average revenue 
  5. subscription type by duration
   

### Data Analysis
---
This includes some of the codes or queries i used to analyze the data 
When analyzing on Microsoft Excel below forumar was used
   - subscription duration =DATEDIF(E2,F2,"y")

When Analyzing for SQL below formular was used 

Select * from[dbo].[CUSTOMERDATA]

---retrieve the total number of customers from each region---

SELECT REGION,
SUM (CUSTOMERID) AS TOTAL_CUSTOMER
FROM[dbo].[CUSTOMERDATA]
GROUP BY REGION

---most popular subscription type by the number of customers--

Select top 1 subscriptiontype,
count(customerid) as number_of_customers
from[dbo].[CUSTOMERDATA]
group by subscriptiontype
order by number_of_customers
desc

---customers who canceled their subscription within 6 months---

SELECT customerid, subscriptionstart,SubscriptionEnd  
FROM [dbo].[CUSTOMERDATA]
WHERE SubscriptionEnd is not null  
  AND datediff(month,subscriptionstart,subscriptionend)<=6

  ---average subscription duration for all customers--
  
SELECT AVG(DATEDIFF(month, SubscriptionStart,
COALESCE(SubscriptionEnd,Canceled,GETDATE()))) AS
Average_Duration_month
FROM [dbo].[CUSTOMERDATA]
WHERE SubscriptionStart IS NOT NULL;

---customers with subscriptions longer than 12 months---

select customerid,subscriptionstart,
coalesce(subscriptionend,getdate()) as subscription_end_date
from[dbo].[CUSTOMERDATA]
where DATEDIFF(month, subscriptionstart,coalesce(subscriptionend,getdate())) >12

---total revenue by subscription type----

select subscriptiontype,
sum(Revenue) as total_revenue
from[dbo].[CUSTOMERDATA]
group by subscriptiontype

---top 3 regions by subscription cancellations---

select top 3 region,
count(*) as cancellation_count
from [dbo].[CUSTOMERDATA]
where SubscriptionEnd is not null
group by region
order by cancellation_count desc

---total number of active and canceled subscriptions---

select sum (case when subscriptionend is null then 1 else 0 end) as Active_subscriptions,
sum(case when subscriptionend is not null then 1 else 0 end) as Canceled_subscription
from[dbo].[CUSTOMERDATA]



### Data Visualization 

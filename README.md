# PLANT_Company_Dashboard_by_POWER_BI


![](plantes.jpg)

---
## Introduction

The "Othmane-Data LLC Sales Performance Dashboard 2023" provides an in-depth analysis of the company's sales, gross profit, and other key performance indicators (KPIs). The dashboard uses various visualizations to track progress year-to-date (YTD) versus the prior year-to-date (PYTD), identify areas of growth and decline, and assess profitability by country, product type, and account segmentation.

## Dashboard File

My final [dashboard](all_dash_llc.pdf)

## Problem statement

1. Highlight the countries with the lowest sales performance, identifying significant declines compared to the previous year.
2. Understand which product categories are driving overall sales performance.
3. Track monthly sales performance and compare trends between YTD and PYTD for all product types.
4. Evaluate the relationship between gross profit percentage (GP%) and sales volume for different accounts.
5. Provide a quick summary of overall sales performance metrics.


## Skills/ concepts demonstrated

- 🧮 Data Cleaning and Dax
- 📉 Charts and Visualization
- ❎ Conclusion and Recommendations

### 🧮 Data Cleaning and Dax :

#### Measures:

___Column Chart Title;___
```sql
Column Chart Title =
SELECTEDVALUE
(SK_Values[Values]) & " YTD & PYTD | Month "

```

___Report Title;___
```sql
Report Title =
 " Othmane-Data LLC " & SELECTEDVALUE(SK_Values[Values]) & " Performance " &
SELECTEDVALUE(Dim_date[Date].[Year])

```

___Scatter Title;___
```sql
Scatter Title =
" Account Profitability Segmentation | GP% and " &
SELECTEDVALUE(SK_Values[Values])

```

___Waterfull Title;___
```sql
Waterfull Title =
SELECTEDVALUE(SK_Values[Values]) &
" YTD vs PYTD | Month - Country - Product "

```

#### Base Measures:

___Quantity;___
```sql
Quantity = SUM(fact_sales[quantity])
```

___sales;___
```sql
sales = SUM(fact_sales[Sales_USD])

```

___Cross_Profit;___
```sql
Cross_Profit = [sales]-[COGS]

```

___GP%;___
```sql
GP% = DIVIDE([Cross_Profit],[sales])

```

#### PYTD:
___PYTD_CrossProfit;___
```sql
PYTD_CrossProfit = 
CALCULATE(
    [Cross_Profit], 
    SAMEPERIODLASTYEAR(Dim_date[Date]),
    Dim_date[INPAST] = TRUE
)
```

___PYTD_Quantity;___
```sql
PYTD_Quantity = 
CALCULATE(
    [Quantity], 
    SAMEPERIODLASTYEAR(Dim_date[Date]),
    Dim_date[INPAST] = TRUE
)
```

___PYTD_Sales;___
```sql
PYTD_Sales = 
CALCULATE(
    [Sales], 
    SAMEPERIODLASTYEAR(Dim_date[Date]),
    Dim_date[INPAST] = TRUE
)

```

#### Switch :

___S_PYTD;___
```sql
S_PYTD = 
VAR SelectedValue = SELECTEDVALUE(SK_Values[Values]) 
VAR Result =
    SWITCH(
        SelectedValue, 
        "Sales", [PYTD_Sales], 
        "Quantity", [PYTD_Quantity], 
        "Gross Profit", [PYTD_CrossProfit], 
        BLANK()
    ) 
RETURN 
    Result

```

___S_YTD;___
```sql
S_YTD = 
VAR SelectedValue = SELECTEDVALUE(SK_Values[Values]) 
VAR Result =
    SWITCH(
        SelectedValue, 
        "Sales", [YTD_Sales], 
        "Quantity", [YTD_Quantity], 
        "Gross Profit", [YTD_CrossProfit], 
        BLANK()
    ) 
RETURN 
    Result

```

___YTD vs PYTD;___
```sql
YTD vs PYTD = [S_YTD]-[S_PYTD] 

```

#### YTD :
___YTD_CrossProfit;___
```sql
YTD_CrossProfit =
TOTALYTD
([Cross_Profit],fact_sales[Date_Time])

```

___YTD_Quantity;___
```sql
YTD_Quantity =
TOTALYTD
([Quantity],fact_sales[Date_Time])

```

___YTD_Sales;___
```sql
YTD_Sales =
TOTALYTD
([sales],fact_sales[Date_Time])

```


### 📉 Charts and Visualization :

KPI's Requirements   
1.	Sales YTD: $5.25M  
* Tracks total sales revenue for the current year to date.  
2.	Sales PYTD: $4.54M  
* Compares total sales revenue from the same period in the previous year.  
3.	YTD vs PYTD Growth: +711.30K (+15.66%)  
* Measures the growth in sales revenue between the current YTD and PYTD.  
4.	Gross Profit Percentage (GP%): 40.3%  
* Represents the profitability percentage, calculated as gross profit divided by total sales revenue.


The report comprises 4 charts:

___1. Sales Performance by Country (Bottom 10);___


___2. Sales by Product Type;___


___3. Monthly Sales Trends;___


___4. Account Profitability Segmentation.___







 the all dashboard ![](all-dashboard.PNG)

___KPI's Requirements___

![](plant-keys.PNG)


__Objective:__ Provide a quick summary of overall sales performance metrics.  
__Problem Statement:__ The company achieved a 5.25M YTD sales with a GP% of 40.3%, reflecting positive growth compared to PYTD (4.54M). Further optimization is needed to maintain momentum.  
___KPI Requirements:___

* Total sales YTD and PYTD.
* GP% and its trend.
* Variance analysis of sales growth.

  
___1. Sales Performance by Country (Bottom 10);___

![](bottom-ytdvspytd_country.PNG)

__Objective:__ Highlight the countries with the lowest sales performance, identifying significant declines compared to the previous year.  
__Problem Statement:__ Sales in Poland, Sweden, and France have shown significant negative trends, with Poland experiencing the largest drop (-134.09K). These trends could reflect market challenges or ineffective strategies.  

___KPI Requirements:___

* Total sales YTD vs PYTD per country.
* Percentage change in sales performance.
* Highlight regions with the most significant declines.

  
___2. Sales by Product Type;___


![](sales_ytd_vs_pytd_month.PNG)

__Objective:__ Understand which product categories are driving overall sales performance.  
__Problem Statement:__ Product categories such as "Outdoor" and "Indoor" are performing well, whereas others are lagging, requiring a deeper understanding of demand and profitability by product.  

___KPI Requirements:___

* Sales distribution by product type.
* Contribution of each category to total sales YTD.

  
___3. Monthly Sales Trends;___


![](sale_ytd-vs-pytd.PNG)

__Objective:__ Track monthly sales performance and compare trends between YTD and PYTD for all product types.  
__Problem Statement:__ While sales have generally improved YTD, the trends are inconsistent across months, suggesting possible seasonality or market fluctuations.  

___KPI Requirements:___

* Monthly sales YTD and PYTD.
* Growth trends for each product type.

  

___4. Account Profitability Segmentation.___

![](account_profitability_segmentation.PNG)

__Objective:__ Evaluate the relationship between gross profit percentage (GP%) and sales volume for different accounts.  
__Problem Statement:__ Certain accounts contribute high sales volumes but have low GP%, which could negatively impact profitability.  

___KPI Requirements:___

* Scatter plot of GP% versus sales.
* Identification of high-sales, low-profit accounts.

  

### ❎ Conclusion and Recommendations:

#### Conclusion

The dashboard successfully identifies key areas of growth and concern for Othmane-Data LLC. Positive trends in YTD sales compared to PYTD are evident, but challenges remain, particularly in underperforming regions and products with low profitability.

#### Recommendations

__1. Focus on Underperforming Countries:__ Develop targeted strategies for Poland, Sweden, and France, such as marketing campaigns or pricing adjustments.
__2. Optimize Product Portfolio:__ Prioritize products with higher GP% while addressing the underperformance of lagging categories.
__3. Leverage Monthly Trends:__ Use seasonal insights to prepare for peak sales periods and mitigate slumps.
__4. Profitability Management:__ Reassess account-level profitability to balance high sales with adequate margins.
__5. Continuous Monitoring:__ Regularly update the dashboard with real-time data to track performance and adapt strategies effectively.

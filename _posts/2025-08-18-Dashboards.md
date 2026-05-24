---
title:  "Dashboards"
layout: single
---

This page shows a few examples of dashboards I have built using different tools such as Tableau, Excel, and Google Looker Studio. 

![Stock Comparison Dashboard](/images/StockComparisonDashboard.png)


The Stock Comparison Dashboard is an Excel dashboard that automatically updates to reflect current stock prices, historical stock prices, daily changes, and hypothetical growth calculations. The dashboard uses references so that the user can change the stocks in the dashboard easily. It refreshes every five minutes so that the user always views up-to-date price data without having to do any manual updates.

### Data

The dashboard uses data from Google sheets using the “GOOGLEFINANCE” function and is imported into Excel through the “Get External Data” feature in Excel. A similar dashboard could also be made directly in Google Sheets. The data includes historical prices from the last three years. 

The “QUERY” function in Google Sheets is used to specify the column names. The “TODAY” function is used to access data based on the current date. 
Features

### Current Price and Daily Change Ribbon 

Ribbon at the top of the dashboard displaying the current price, updating every 5 minutes, of each stock, and the percent change from yesterday’s closing price. Each stock’s prices and percent changes update automatically using references and formulas.


### Historical Price Drop Down

This section includes a data drop down that allows you to select a date and see the stock prices for each stock on the selected date. The drop down is created with the Excel Data Validation tool, and the prices of each stock are updated with a Vlookup formulas referencing the date selected in the drop down tool.

### Hypothetical Growth Calculator

This section computes the hypothetical growth of an initial investment in each stock. It uses starting amount, start date, and end date user inputs. It calculates the end amount, rate or return over the investment period, and dollar amount change from the start to end date.  These calculations are done using Excel formulas. 

### Historical Price Graph

This graph shows the change in stock prices over time using the historical stock prices downloaded into the Excel workbook from Google Sheets.

### Hypothetical Growth Graph

This graph uses the percentage change for each day calculated from the historical prices multiplied by an initial investment amount inputted by the user. It uses the data from these calculations to show the hypothetical growth of an investment over time. 

### Stock Data Tab

The data that reads into the dashboard is stored in the stock data tab. This tab uses the ‘Get Data’ function in Excel to pull data from the published Google Sheets file. I pulled data from the Google Sheets file because stock data is free to access in Google Sheets, but the built-in stock function in Excel requires a paid subscription. 
The stock data tab also includes the data for the percentage change and hypothetical growth graphs and calculations. These numbers are calculated as using formulas referencing the historical price data.

### Google Sheets File

The Google Sheets file uses the “GOOGLEFINANCE” function to update individual stock data. This sheet updates automatically, so when the Excel dashboard refreshes, it will pull updated data from the Google sheet, and all referenced data in the dashboard will update automatically as well. 

## Tableau Dashboards

![Coffee Bean Sales Dashboard](/images/Coffee_Bean_Sales_Dashboard.png)

The Coffee Bean Sales Dashboard was made using a coffee bean sales dataset downloaded from Kaggle. The dashboard is built to showcase key sales metrics at the top including total sales in dollars, total sales in number of transactions, and the number of unique customers. The graphs provide more depth into sales and transactions by city and by product along side visualizations for the geographic location of sales and distribution of sales by product. 

This dashboard is interactive, with filters at the top. The interactive version of this dashboard can be accessed on my Tabluea public profile found [here][https://public.tableau.com/views/CoffeeBeanSales_17695427478370/CoffeeBeanSales?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link]. 

![Website Analytics Dashboard](/images/Web_Analytics_Dashboard.png)

The website analytics dashboard allows stakeholders to view website engagement according to various metrics including total views, unique users, and average engagement time per session. This dashboard features a line graph plotting engagement metrics by month. Above the graph is a timeline. Combining these two visualizations together allows stakeholders to view changes in website engagement alongside events that may impact engagement such as outreach events or events that affect website engagement on a recurring basis such as holiday breaks. Towards the bottom of the dashboard, there is a table of website engagement metrics allowing the dashboard user to more easily visualize exact numbers. 

This dashboard is interactive, and the interactive version can be accessed on my Tableau public profile, found [here][https://public.tableau.com/views/WebsiteAnalyticsDashboard_17786239859750/WebsiteAnalyticsDashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link].

## Google Looker Studio Dashboard

![Generic Race Analytics Dashboard](/images/Generic_Race_Dashboard.png)

This dashboard was made with Google Looker Studio and was built to track race registraction analytics. It highlights important metrics at the top such as total number of runners registered, revenue, average runner age, and the number of cities participants come from. It was built using simulated race data and will update automatically to reflect real race registration metrics if connected to real race data. 

The dashboard is organized with data related to runners in the top section and data related to revenue in the bottom section. It provides insights into changes in runner participation and revenue from one year to the next while also breaking down runner participation and revenue by race type and city. 


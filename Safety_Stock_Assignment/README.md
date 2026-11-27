# Safety Stock Assignment

## Background 
Inventory management is one of the most critical operational tasks, where this role is responsible for understanding, managing, and maintaining inventory/stock. Most often, this task relies on behind the scenes data analysis, such as: Forecasting, determining optimal quantities, supplier selection, warehouse/inventory optimization, and more. 

## Objective
...

## Data Source
This data source is provided from the OM620 Tools and Technology course. The data provided is a transaction dataset that tracks the production of various items to stock in 784,638 observations. This data shows: The SKU item's inventory type, stocking type, lead time in days, their unit price, manufacturing site, the business ID code assigned to the item, transaction date, and the order quantity within the transaction. This data can be found in the "Data" folder of this repository. 

The Meta data to describe the features is the following: 

<img width="600" height="350" alt="Screenshot 2026-11-27 142904" src="https://github.com/user-attachments/assets/1ffe0bce-9756-400f-8580-12a09ddfa2c1" />


## Analysis
### Prior Analysis
The steps taken prior to starting our safety stock calculation and analysis involve: Re-formatting our data, inspection for cleaning where we change values due to quality mistakes, fixing missing values, applying broader breakdowns through countries, and exploring helpful dimensional information. 

Please refer to the assignments or completed notebooks to view the data cleaning and transformation necessary to perform our analysis. 

### Helpful Dimensional Information
After performing the necessary initial changes to our data we want to understand some helpful dimensional information before calculating safety stock. We first subset the inventory type to make-to-stock finished goods. We do this by applying a query function to only select finished goods from the inventory type, and make-to-stock from the stocking type. After doing this we now know we are working with 368 unique SKUs, 19 unique manufacturing sites, and 54 unique divisions. To view the top 10 and bottom 10 transactions by order quantity and sales value, please refer to the notebooks. 

### Safety Stock Calculation
In the calculation of our safety stock we need to keep something in mind. We are assuming that our data is a normal distribution, which is why we calculate the z scores in the manner demonstrated in the notebook. Additionally, we calculate three safety stocks under three different service level coefficients (75%, 90%, and 95%). In doing so we are able to see the different tradeoffs at these levels taken to reduce risks of stock outs. 

finish

change complete file

find a way to connect to page

zip to turn in 

## Provided Resources




## Additional Resources for Assignments




# Safety Stock Assignment

## Background 
Inventory management is one of the most critical operational tasks, where this role is responsible for understanding, managing, and maintaining inventory/stock. Most often, this task relies on behind the scenes data analysis, such as: Forecasting, determining optimal quantities, supplier selection, warehouse/inventory optimization, and more. 

## Objective
...

## Data Source
This data source is provided from the OM620 Tools and Technology course. The data provided is a transaction dataset that tracks the production of various items to stock in 784,638 observations. This data shows: The SKU item's inventory type, stocking type, lead time in days, their unit price, manufacturing site, the business ID code assigned to the item, transaction date, and the order quantity within the transaction. This data can be found in the "Data" folder of this repository. 

Please refer to the assignments or completed notebooks to view the data cleaning and transformation necessary to perform our analysis.

The Meta data to describe the features is the following: 

<img width="600" height="350" alt="Screenshot 2026-11-27 142904" src="https://github.com/user-attachments/assets/1ffe0bce-9756-400f-8580-12a09ddfa2c1" />


## Analysis

### Helpful Dimensional Information
After performing the necessary initial changes to our data we want to understand some helpful dimensional information before calculating safety stock. We first subset the inventory type to make-to-stock finished goods. We do this by applying a query function to only select finished goods from the inventory type, and make-to-stock from the stocking type. After doing this we now know we are working with 368 unique SKUs, 19 unique manufacturing sites, and 54 unique divisions. To view the top 10 and bottom 10 transactions by order quantity and sales value, please refer to the notebooks. 

### Safety Stock Calculation
A2








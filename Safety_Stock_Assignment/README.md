# Safety Stock Assignment

## Background 
Inventory management is one of the most critical operational tasks, where this role is responsible for understanding, managing, and maintaining inventory/stock. Most often, this task relies on behind the scenes data analysis, such as: Forecasting, determining optimal quantities, supplier selection, warehouse/inventory optimization, and more. 

For many,if not all companies, avoiding a stock out is very important. A stock out is when the site that products are sold completely run out of inventory for an item, the downside to this happening is the loss of potential revenue from customers, not meeting customer demand, and ultimately resulting in the loss of customer trust. Inventory management becomes in charge of avoiding this unfortunate outcome by performing stock out risk analysis and ordering safety stock for items to meet the demand for these items. 

## Objective
In this repository we demonstrate this process by calculating the safety stock of items within a transactional data set. 

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

We first prepare the safety stock calculation with setting up a data frame that shows the following statistics: minimum, maximum, average, median, variance, and standard deviation of quantity, along with average lead time. 
```
#Create new data frame grouped by sku and aggregated quantity and lead time for Safety Stock calculation
mts_df =(mts
         .groupby("sku_number")
         .agg(min_qty=("order_quantity", "min"),
              max_qty=("order_quantity", "max"),
              avg_qty=("order_quantity", "mean"),
              median_qty=("order_quantity", "median"),
              variance_qty=("order_quantity", "var"),
              std_qty=("order_quantity", "std"),
              avg_lead_time=("lead_time", "mean"))
              .reset_index())
mts_df
```
Next we prepare the Z score for each service level: 
```
mts_z75 = stats.norm.ppf(.75)
mts_z90 = stats.norm.ppf(.90)
mts_z95 = stats.norm.ppf(.95)
```
Lastly we add the safety stock calculation feature to the data frame. An example to this step is to the following:
```
#Add column for safety stock at 75% service level
mts_df["safety_stock_75"] = (
    mts_z75
    *mts_df["std_qty"]
    *mts_df["avg_lead_time"]** 0.5      #The "** 0.5" calculates the square root by applying the power of 0.5 to the value. (same as square root)
)
mts_df
```
This code is applied to all three service levels. 

### Results
Within this data set we discover the SKU with the largest safety stock at 95% service level is SKU `9B9EBBD2`, which has an order quantity of 349.976005 units, which we round up to 350 units. In context, for this item to not be in the risk of a stock out, the company would have to order roughly 350 more units with the intent they will be finished goods that are made to stock just in case the selling storefront gets low on inventory. 

The code and result to get to this calculation is the following: 
```
#95% safety stock
#Sort for largest
mts_df.sort_values(by="safety_stock_95", ascending=False).head(1)
```
<img width="1080" height="55" alt="Screenshot 2026-11-27 160510" src="https://github.com/user-attachments/assets/f7240c92-5ff6-43f2-a2de-d81c26f0a445" />



The SKU with the smallest safety stock, at a 95% service level coefficient, is `A9E754AB` with a quantity of 32.288292 units, which we will round to 33 units. This item has the lowest safety stock under this threshold across all the data set.


The code and result to get to this calculation is the following: 
```
#Sort for smallest
mts_df.sort_values(by="safety_stock_95").head(1)
```
<img width="1071" height="57" alt="image" src="https://github.com/user-attachments/assets/d1d410d2-1bbe-4524-bf90-69709eac14b7" />


The average safety stock across all SKUs is about 103.6 units, meaning on average this company would want to plan on bringing in about 100 extra items that are finished goods and made to stock to avoid the risk of a stock out. 


The code and result to get to this calculation is the following: 
```
#Mean of safety stock column across all SKUs
mts_df["safety_stock_95"].mean()
```

## Conclusion
There demonstrated we have calculated the safety stock for the provided transactional data. To look through the code and commentary for this please refer to the "Completed Notebook" folder within my "OM620-Tools-Technologies" repository. 

## Provided Resources: 
...............

## Additional Resources Used:

- Bobbitt, Z. (2021, April 26). Percentile vs. quartile vs. quantile: What’s the difference? Statology. https://www.statology.org/percentile-vs-quartile-vs-quantile/


- Stack Overflow(2022). "How do I calculate square root in Python?". Retrieved November 17, 2026. https://stackoverflow.com/questions/70793490/how-do-i-calculate-square-root-in-python 


When searching for "How to square root in python" on Stack Overflow, we come across a post (Stack Overflow, 2022) that has last been edited this year on August 24th that indicates the snippet below:

```
Option 2: Fractional exponent
The power operator (**) or the built-in pow() function can also be used to calculate a square root. Mathematically speaking, the square root of a equals a to the power of 1/2.

The power operator requires numeric types and matches the conversion rules for binary arithmetic operators, so in this case it will return either a float or a complex number

>>> 9 ** (1/2)
3.0
>>> 9 ** .5  # Same thing
3.0
>>> 2 ** .5
1.4142135623730951

```



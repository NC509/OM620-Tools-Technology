# Assignments

In this folder you can view **assignment 1** and **assignment 2**. The purpose of these assignments were to break apart the task of calculating safety stocks for the make-to-stock items. 

In **assignment 1**, we set up the transactional data in preparation for our calculations. In doing so we had to re-format the data frame, inspect our data for any data quality fixes, fix missing values, apply broader breakdowns of this data through countries, and last explore some helpful dimensional information. 

- Prior to assignment 2, we needed to make some fixes to the first assignment before proceeding. This fix was to make missing SKU numbers, originally we removed these observations, but due to data loss, we change the missing values to "missing". This step can be seen in the initial steps of assignment 2. 

In **assignment 2**, we calculate the safety stock for the make-to-stock inventory items amongst different service level coefficients. Following these calculations we explore the the SKUs with the least and most safety stock, and the average safety stock across all values. In addition to this task we explore a _side quest_. In this side quest we explore further analysis by calculating the safety stock values using a simple non-parametric quantile function. 

- Prior to bringing both assignments together we noticed a small issue, that is resolved in the complete notebook. In **assignment 2** our initial transformation only included subsetting our data to make-to-stock items, without altering the inventory type to finished goods. This change is up to date in the complete safety stock notebook. 

Please refer to the "Completed Notebook" folder for complete analysis. 

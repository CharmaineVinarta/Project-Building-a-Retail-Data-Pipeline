# Project-Building-a-Retail-Data-Pipeline

# Project Instructions
•	Theextract() function should combine grocery_sales table and extra_data.parquet file. It should return a DataFrame and be stored as the merged_df variable.
•	Thetransform() should take the merged_df as input, fill missing values, add a column "Month", keep the rows where the sales are over $10,000, and drop the index. Ultimately, it should return a DataFrame and be stored as the clean_data variable.
•	The avg_monthly_sales() should take clean_data as input and returns an aggregated DataFrame containing two columns - "Month" and "Avg_Sales" (rounded to 2 decimals). You should store it as the agg_sales variable.
•	The load() function should take in the cleaned and aggregated DataFrames, and their paths and saves them as clean_data.csv and agg_data.csv respectively, without an index.
•	Finally, the validation() function should check whether the two csv files from the load() exist in the current working directory.

# GUIDES: 
## 1.	Extracting the data
- Extract the data from PostgreSQL and parquet file.
- Extracting the data from PostgreSQL database
•	Write the query in the cell dedicated to SQL queries. 
•	You have to extract all columns from the grocery_sales table using a SQL query.
•	The SELECT statement is used to specify which columns to select, FROM statement is used to specify the table from which you are extracting data. 
- Creating a function to extract data
•	The extract() function should accept: the DataFrame you've extracted using SQL and a parquet file.
•	You can use pd.read_parquet() to read a parquet file in as a pandas DataFrame.
•	Before merging, check which column the two DataFrames have in common, then use merge() to join them using the column in common.
•	Store the merged DataFrame as merged_df.

## 2.	Transforming the data
- Imputation, filtering, and cleaning.
- Creating the transform function
•	The transform() function should accept one argument: the merged DataFrame you got from extract() function.
- Imputing missing values
•	You can use .fillna() function on either multiple columns at once or individual columns. Here is an example of applying it to multiple columns: df.fillna( { 'col1': df['col1'].mean(), 'col2': df['col2'].mode(), }, inplace = True 
Filtering data
•	To extract data from certain months only, you first have to convert Date column to datetime using pd.to_datetime() and specifying format "%Y-%m-%d".Then, you should create a column that extracts month from Date column. 
•	Finally, you can filter the DataFrame using the new column and function .isin(). Remember to extract not only the holiday months, but also the months following and preceding those months. 
•	To filter sales data, use .loc() function and Weekly_Sales columns. Here is an example: data = data.loc[data["sales"] > 23, :] 
•	Drop the index column as it's not needed in the analysis. Don't forget to specify axis argument in drop() function.
- Storing transformations
•	Pass the right DataFrame to the transform() function and store the output as a variable called clean_data.

## 3.	Preliminary analysis of the sales data
- After cleaning the data, you will perform some simple analysis.
- Creating the function
•	The avg_monthly_sales() function should accept one argument: the cleaned DataFrame you got from transform() function.
- Subsetting the data
•	For the analysis, you should only keep the columns: Month and Weekly_Sales
•	You can use the following syntax to select the necessary columns: df[["Col1", "Col2"]] 

- Aggregate the sales data
•	First, you have to group your data using the Month column
•	Then, you can apply aggregate function to compute the average using the Weekly_Sales column and rename it to Avg_Sales
•	Finally, you have to round() the Avg_Sales column to the two decimal places and store the results in the sales_per_month variable.

## 4.	Loading and validating the data
- Final step is to store your transformed data and validate that it was stored correctly.
- Save the data as a csv file
•	Function load() should accept two arguments: variable that stores your transformed DataFrame and file path.
•	Use pandas .to_csv() method to write DataFrame to a csv file. Specify file path as "clean_data.csv" for the full DataFrame and "sales_per_month.csv" for the aggregated data.
•	Make sure to include index = False to avoid storing the index column.

- Validation
•	The validation() function should accept one argument: file path you have used to store your csv file
•	You can use path.exists() function from the os package to check whether the file path exists. 
•	Create an ìf statement that will raise Exception in case file doesn't exist. 


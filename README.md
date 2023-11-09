# Project: Building a Retail Data Pipeline

## Project Instructions

The project involves creating a data pipeline for analyzing demand and supply around the holidays. You will work with two data sources: `grocery_sales` from a PostgreSQL database and `extra_data.parquet` for complementary data. The following instructions will guide you through the project.

### Functions to Implement

1. `extract()`
   - Combine `grocery_sales` table and `extra_data.parquet` file.
   - Return a DataFrame as `merged_df`.

2. `transform(merged_df)`
   - Take the `merged_df` as input.
   - Fill missing values, add a "Month" column, keep rows with sales over $10,000, and drop the index.
   - Return a DataFrame as `clean_data`.

3. `avg_monthly_sales(clean_data)`
   - Accept `clean_data` as input.
   - Aggregate data to compute the average sales per month.
   - Return an aggregated DataFrame with "Month" and "Avg_Sales" (rounded to 2 decimals) as `agg_sales`.

4. `load(clean_data, agg_sales)`
   - Take cleaned and aggregated DataFrames along with their paths.
   - Save them as `clean_data.csv` and `agg_data.csv`, respectively, without an index.

5. `validation(file_path)`
   - Check whether the CSV files from the `load()` function exist in the current working directory.
   - Raise an Exception if the file doesn't exist.

## Guides

### 1. Extracting the Data
- Extract data from PostgreSQL and a parquet file.
- Extracting data from the PostgreSQL database:
   - Write a SQL query to extract all columns from the `grocery_sales` table.
   - Use the `SELECT` statement to specify columns and the `FROM` statement to specify the table.
- Creating a function to extract data:
   - The `extract()` function should accept the DataFrame extracted using SQL and a parquet file.
   - Use `pd.read_parquet()` to read the parquet file and merge the DataFrames based on a common column.

### 2. Transforming the Data
- Perform imputation, filtering, and cleaning.
- Creating the `transform` function:
   - The `transform()` function should accept the merged DataFrame from the `extract()` function.
- Imputing missing values:
   - Use `.fillna()` on multiple columns or individual columns to handle missing data.
- Filtering data:
   - Convert the Date column to a datetime format and extract the month.
   - Filter the DataFrame based on specific months and sales values.
   - Drop the index column.
- Storing transformations:
   - Pass the DataFrame to the `transform()` function and store the output as `clean_data`.

### 3. Preliminary Analysis of the Sales Data
- After cleaning the data, perform simple analysis.
- Creating the `avg_monthly_sales()` function:
   - Accept the cleaned DataFrame from the `transform()` function.
- Subsetting the data:
   - Keep only the "Month" and "Weekly_Sales" columns.
- Aggregate the sales data:
   - Group data by the "Month" column and compute the average sales.
   - Round the "Avg_Sales" column to two decimal places and store the results.

### 4. Loading and Validating the Data
- The final step is to store transformed data and validate the storage.
- Saving the data as a CSV file:
   - The `load()` function should accept cleaned and aggregated DataFrames and their paths.
   - Use `pandas.to_csv()` to write DataFrames to CSV files with specified names.
   - Include `index = False` to avoid storing the index column.
- Validation:
   - The `validation()` function should accept a file path used to store CSV files.
   - Use `path.exists()` from the `os` package to check if the file path exists.
   - Raise an Exception if the file doesn't exist.

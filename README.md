# Data Cleaning with Python & Pandas

A growing collection of real-world messy datasets cleaned using Python and pandas.
Each project documents the cleaning process, key decisions, and lessons learned.

---

## Projects

| # | Dataset | Source | Cleaning Focus |
|---|---------|--------|---------------|
| 1 | [Netflix Titles](#1-netflix-titles) | Kaggle | Dropping redundant columns, renaming, duplicates, null values |
| 2 | [E-commerce Fashion Dataset](#2-e-commerce-fashion-dataset) | Kaggle | Column cleanup, duplicate index fix, text formatting, missing value imputation by group |
| 3 | [Sales Data](#3-sales-data) | GitHub (Onurbltc) | Invalid value detection, type conversion, group-based imputation, datetime cleaning, EDA visualisations |
---

## Project Details

### 1. Netflix Titles
**Source:** Kaggle — [Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows)

**What I did:**
- Dropped redundant and irrelevant columns
- Renamed columns for consistency and readability
- Removed duplicate records
- Handled missing/null values
- Data type conversions
- Structural and formatting transformations

**Lessons learned:** Not all columns add analytical value — inspecting relevance before cleaning saves time. Null handling depends on context; dropping vs imputing is ultimately a business decision. Standardising column names early avoids confusion downstream in SQL and dbt.

[View Notebook](Netflix/Notebook.ipynb)

### 2. E-commerce Fashion Dataset
**Source:** Kaggle — [E-commerce Fashion Dataset](https://www.kaggle.com/datasets/mukuldeshantri/ecommerce-fashion-dataset)

**What I did:**
- Dropped the unnecessary `Unnamed: 0` column
- Corrected a typo in the `Details` column name
- Removed duplicate entries, then re-indexed the dataset to align the index with the actual row count
- Dropped the leftover `Index` column after re-indexing
- Capitalised brand names in the `BrandName` column for consistency
- Identified that thousands of `Discount` values weren't appearing in value counts because they weren't true NaNs — replaced them with proper NumPy NaN values
- Converted the `Discount` column from object to numeric type by extracting the numeric portion from string values like `"20%"` using `str.extract`
- Filled missing `Discount` values with the median discount **grouped by product category**, for a more accurate representation than a flat median
- Cleaned the `MRP` column by removing the `Rs` prefix and newline characters, then standardised non-standard missing value formats into proper NaNs
- Filled missing `MRP` values using the same category-grouped median approach

**Lessons learned:** Missing values don't always show up as `NaN` — sometimes they're disguised as strings, blanks, or inconsistent placeholders, and need to be explicitly converted before they can be handled. Grouped imputation (median by category) gives a far more accurate fill than a single global median, especially when categories vary widely in pricing or discounting. Cleaning numeric-looking columns that are stored as text (like `"20%"` or `"Rs 999"`) requires extracting the actual numeric value before any aggregation or imputation can happen.

[View Notebook](e-commerce1/mynotebook.ipynb)

### 3. Cafe Sales Data
**Source:** [Onurbltc/SalesData (GitHub)](https://github.com/Onurbltc/SalesData)

**What I did:**
- Identified invalid placeholder values (`ERROR`, `UNKNOWN`, `nan`) across the `Quantity`, `Price Per Unit`, and `Total Spent` columns, and converted them to proper missing values before imputation
- Converted `Price Per Unit` and `Total Spent` from object to numeric type
- Imputed missing `Price Per Unit` values using the group median
- Imputed missing `Total Spent` values by recalculating them from `Quantity × Price Per Unit`
- Filled missing and invalid entries in `Payment Method` with `"Unknown"` to preserve the signal that data was missing, rather than dropping or guessing
- Converted `Transaction Date` from text to datetime, after identifying invalid placeholder values in the column
- Dropped rows with missing `Transaction Date` values (4.6% of the data) since the column is critical for time-based analysis and imputing it risked introducing bias
- Explored the cleaned data through visualisations: top 10 items by revenue, payment method distribution, revenue by payment method, and a price vs quantity scatter plot

**Lessons learned:** Missing values aren't always blank — they can be disguised as misleading strings like `"ERROR"` or `"UNKNOWN"`, and need to be explicitly identified before any imputation logic will work correctly. Not every missing value should be imputed the same way: numeric columns can often be reconstructed from other columns (like `Total Spent` from `Quantity × Price`), categorical columns are sometimes better served by an explicit `"Unknown"` label, and some columns are critical enough that dropping missing rows is safer than imputing them. The visualisations also reinforced that cleaning isn't the end goal — it's what makes the EDA and charts trustworthy in the first place.

[View Notebook](Cafe_sales/sales_notebook.ipynb)
[View Plots](Cafe_sales/plots.ipynb)
---

## Tools
- Python 3.9
- pandas
- matplotlib
- Numpy
- Jupyter Notebook

---

*This repository is updated regularly as I work through more datasets across different domains.*

# Data Cleaning with Python & Pandas

A growing collection of real-world messy datasets cleaned using Python and pandas.
Each project documents the cleaning process, key decisions, and lessons learned.

---

## Projects

| # | Dataset | Source | Cleaning Focus |
|---|---------|--------|---------------|
| 1 | [Netflix Titles](#1-netflix-titles) | Kaggle | Dropping redundant columns, renaming, duplicates, null values |

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



---

## Tools
- Python 3.9
- pandas
- Jupyter Notebook

---

*This repository is updated regularly as I work through more datasets across different domains.*

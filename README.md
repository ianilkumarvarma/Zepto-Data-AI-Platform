# Zepto-Data-AI-Platform
The  Zepto Data &amp; AI Platform is an end-to-end AI/ML engineering project that demonstrates how raw data can be transformed into useful analytics and intelligent customer support. 
# Zepto Data Pipeline

## Overview

This module implements an end-to-end web scraping and data engineering pipeline for the Zepto Data & AI Platform capstone.

The pipeline:

1. Scrapes books from the Books to Scrape website using `requests` and `BeautifulSoup`.
2. Collects book title, price, star rating, availability and category.
3. Cleans and converts the scraped fields into analysis-ready data types.
4. Converts GBP prices into INR using the required fixed project baseline.
5. Stores the normalized data in a SQLite database.
6. Executes SQL queries demonstrating filtering, sorting, limiting, distinct values, range filtering and table joins.
7. Reproduces the SQL JOIN using `pandas.merge()` and compares the results.

## Dataset

The pipeline automatically scrapes the first five pages of the Books to Scrape "All Products" catalogue.

Each page contains approximately 20 books, resulting in approximately 100 scraped book records.

The final dataset must contain at least 60 valid book records.

## Fields

The final dataset contains:

* `title` — Book title
* `price_gbp` — Book price as a floating-point GBP value
* `price_inr` — Book price converted to INR
* `rating` — Star rating converted from text to an integer from 1 to 5
* `in_stock` — Boolean stock availability
* `category` — Book category

## Currency Conversion

The project uses the required fixed conversion baseline:

**1 GBP = 105.50 INR**

This is an artificial, project-defined constant for the assignment. It is not a live exchange rate and does not require an external API or date reference.

The calculation is:

```text
price_inr = price_gbp × 105.50
```

## Data Cleaning

### Price

The `£` currency symbol and other non-numeric characters are removed before converting the value to `float`.

### Rating

The textual ratings:

```text
One
Two
Three
Four
Five
```

are converted to:

```text
1
2
3
4
5
```

### Availability

Values beginning with `In stock` are converted to `True`.

Values beginning with `Out of stock` are converted to `False`.

Unexpected availability values are treated as invalid.

### Missing Values

Numeric parsing failures for `price_gbp` and `rating` are handled using median imputation.

Critical non-numeric fields such as title, category and availability are dropped if they cannot be parsed because a reliable replacement value cannot be inferred.

This prevents individual malformed records from crashing the complete pipeline.

## SQLite Schema

The database contains two normalized tables.

### categories

```text
category_id INTEGER PRIMARY KEY
category_name TEXT UNIQUE
```

### books

```text
book_id INTEGER PRIMARY KEY
title TEXT
price_gbp REAL
price_inr REAL
rating INTEGER
in_stock INTEGER
category_id INTEGER FOREIGN KEY
```

The `books.category_id` column references `categories.category_id`.

## SQL Analysis

The notebook demonstrates:

* `SELECT`
* `WHERE`
* `ORDER BY`
* `LIMIT`
* `DISTINCT`
* `BETWEEN`
* `IN`
* `JOIN`

The SQL query results are displayed in the notebook.

At least two SQL query results are read into pandas using `pd.read_sql()`.

The JOIN result is independently reproduced using `pandas.merge()` and the two results are compared for equivalence.

Installation

From the repository root:

pip install -r requirements.txt
Running the Pipeline

Open the notebook:

jupyter notebook

Then open:

data_pipeline/data_pipeline.ipynb




# Module 2 — Analytics Pipeline

## 1. Dataset

## 2. Raw Dataset Loading

## 3. Missing Value Analysis

## 4. Missing Value Decisions

## 5. Univariate Analysis

### Age
### Fare
### IQR Outliers
### Fare Distribution

## 6. Bivariate Analysis

### Survival by Sex
### Survival by Passenger Class
### Survival by Sex and Class

## 7. Correlation Analysis

### Strongest Correlation 1
### Strongest Correlation 2

## 8. Multivariate Data Story

### Chart 1 Interpretation
### Chart 2 Interpretation
### Chart 3 Interpretation
### Chart 4 Interpretation

## 9. Standardization Check

## 10. Train/Test Split

## 11. Preprocessing

## 12. Classification Models

## 13. Classification Evaluation

## 14. Class Imbalance

## 15. Random Forest GridSearchCV

## 16. Regression

## 17. Model Comparison

## 18. Final Recommendation

## 19. Saved Pipeline

## 20. How to Run




Run all cells from top to bottom.

Alternatively, run the Python script:

python data_pipeline.py

The pipeline creates:

books.db
books_cleaned.csv
Reproducibility

The pipeline does not require manual copy-pasting of scraped data.

Running the notebook/script from scratch downloads the source pages, performs the cleaning and conversion steps, creates the SQLite schema and populates the database automatically.

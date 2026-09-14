# YouTube Channels Data Cleaning

## Overview
This project involved cleaning and structuring a real-world dataset of the top 995 YouTube channels globally. The goal was to identify data quality issues in the raw dataset and resolve them using Google Sheets, producing a clean, analysis-ready file.

**Source**: Original dataset — "Global YouTube Statistics 2023" by Nidula Elgiriyewithana ([Kaggle](https://www.kaggle.com/datasets/nelgiriyewithana/global-youtube-statistics-2023)). Provided for practice by Alex The Analyst.

## Files
- `data/raw/` — original, unmodified dataset
- `data/clean/` — cleaned dataset, ready for analysis

## Data Quality Issues Found & How They Were Fixed

**1. Scientific notation stored as text**
The `video_views` column contained large numbers written in scientific notation (e.g. `2.28E+11`), some of which were stored as plain text rather than numeric values. Fixed using `VALUE()` combined with `SUBSTITUTE()` to handle locale decimal formatting, then converted to fixed values with Paste Special > Values Only.

**2. Corrupted channel names**
99 rows had channel names containing unreadable characters (�) due to encoding loss in the original source file — not recoverable. Instead of deleting these rows (which would discard valid numeric data), each row was flagged with a `Status_name` column (`ok` / `corrupted`), so affected rows can be included or excluded depending on the analysis.

**3. Split date columns**
Channel creation date was originally split across three columns (`created_year`, `created_month` as text, `created_day`). Added a `Created_month_number` column using `MATCH()` to convert month abbreviations into numbers, and a combined `Created_date` column.

**4. Missing values**
Several columns (`Country`, `subscribers_for_last_30_days`, `category`, and others) contain missing values in the original dataset. These were intentionally left blank rather than filled with 0 or estimated values, since "missing" and "zero" mean different things — filling them in would have distorted any growth or geographic analysis.

**5. Duplicate check**
Verified no duplicate rows or duplicate channel names exist in the dataset.

## Tools Used
Google Sheets (formulas: `VALUE`, `SUBSTITUTE`, `TRIM`, `MATCH`, `REGEXMATCH`, Conditional Formatting, Data Validation)

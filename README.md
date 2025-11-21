📊 Sales Trend Analysis Using Aggregations (SQLite)

This project performs monthly sales trend analysis using the Superstore Sales Dataset and SQLite.
It demonstrates how to extract time-based insights such as monthly revenue and order volume using SQL aggregation functions.

📝 Task Overview

Task Name: Sales Trend Analysis Using Aggregations
Objective: Analyze monthly revenue and order volume from a sales dataset.
Tools Used: SQLite (DB Browser for SQLite)
Deliverables:

SQL script (task6_sales_trend.sql)

Results table (task6_results.csv)

📂 Dataset Used

Dataset: Superstore Sales Dataset
(Uploaded as train.csv in this repository)

Important columns used:

Order Date

Order ID

Sales

Product ID

🏗️ Project Steps
1. Imported the Superstore CSV into SQLite

Using DB Browser for SQLite:

Created a new database: task6_superstore.db

Imported the dataset → Table created: superstore

2. Cleaned the Date Format

Superstore dates are in MM/DD/YYYY.
SQLite requires YYYY-MM-DD for time functions.

Added a new clean date column:

ALTER TABLE superstore
ADD COLUMN order_date_clean TEXT;


Filled it with a formatted date:

UPDATE superstore
SET order_date_clean = substr([Order Date], 7, 4) || '-' ||
                       substr([Order Date], 1, 2) || '-' ||
                       substr([Order Date], 4, 2);

3. Performed Monthly Sales Trend Analysis

The final SQL query used to compute:

Monthly Revenue → SUM(Sales)

Order Volume → COUNT(DISTINCT Order ID)

Grouped by Year & Month

SELECT 
    strftime('%Y', order_date_clean) AS year,
    strftime('%m', order_date_clean) AS month,
    SUM(Sales) AS monthly_revenue,
    COUNT(DISTINCT [Order ID]) AS order_volume
FROM superstore
GROUP BY year, month
ORDER BY year, month;

📈 Output

The results generate a table like:

Year	Month	Monthly Revenue	Order Volume
2015	01	XXXXX	XXX
2015	02	XXXXX	XXX
...	...	...	...

This table is exported as:
📄 task6_results.csv

📜 SQL Script File

The SQL used for analysis is stored in:
📄 task6_sales_trend.sql

This script contains:

Table modification

Date cleaning

Monthly aggregation query

🎯 Outcome / What You Learn

Through this task, you learn:

✔ How to import datasets into SQLite
✔ How to clean and transform date fields
✔ How to use aggregation functions:

SUM()

COUNT()
✔ How to extract month & year using:

strftime('%m', date)

strftime('%Y', date)
✔ How to create monthly trend tables
✔ How to use GROUP BY, ORDER BY
✔ How to export SQL results

🚀 How to Reproduce This Project

Open DB Browser for SQLite

Create a new database

Import train.csv as a table named superstore

Run the SQL scripts from task6_sales_trend.sql

Export the result table as CSV

This repository is created as beginer for learning purpose only!

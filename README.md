# Elevate-Labs-Internship-Task-2

## Superstore Sales Dashboard — Power BI 

This project analyzes the Sample Superstore dataset and presents key sales insights through an interactive Power BI dashboard of 3 pages in total. "Overview", "Detailed View" and "Insights". 
The dashboard is designed using field parameters, dynamic titles, and dynamic formatting, enabling users to switch between multiple metrics without recreating visuals or using extra pages.

## Objective

To help business stakeholders understand sales performance and customer behavior by analyzing:

Total Sales

Total Quantity Sold

Average Discount

Profit

Profit %

The dashboard allows seamless switching between these metrics using field parameters, updating all visuals and titles automatically.

## Dataset

The dataset contains order-level transactional data with:

Sales, Quantity, Discount, Profit

Customer details

Product segments & categories

Order/Ship Dates

Ship Mode

Region, State, City

Product ID, Order ID

Time Period Identified: 2014 – 2017, with some Ship Dates extending to early 2018.

## Dashboard Structure
Page 1 — KPI Overview

Contains 10 primary KPIs:

Sales (Sum)

Profit (Sum)

Profit %

Total Orders

Total Customers

Units Sold

Total Products

Region Count

State Count

Average Discount

Percentage KPIs originally showed decimals (0.12 → 12%), so dynamic formatting was applied.

## Page 2 — Detailed Insights (Dynamic Metrics)

For each metric, the following 5 visuals update dynamically:

Line Chart:
Metric by Order Date (with average reference line)

Bar Chart:
Top 10 States by Metric

Bar Chart:
Metric by Region

Donut Chart:
Metric by Category

Pie Chart:
Metric by Segment

These work for all 5 metrics:

Sales (Page 2 in pdf)

Quantity (page 3 in pdf)

Avg Discount Page 4 in pdf)

Profit (page 5 in pdf)

Profit % (page 6 in pdf)

## Field Parameters Setup

Created a parameter table called Metric Selector with:

Display label (Sales, Quantity, Profit…)

Measure reference (SumSales, SumQuantity, etc.)

Sort order

Example entry:

Metric Selector = {
    ("Sales", NAMEOF('Sample - Superstore'[SumSales]), 0),
    ("Quantity", NAMEOF('Sample - Superstore'[SumQuantity]), 1),
    ("Discount (Avg.)", NAMEOF('Sample - Superstore'[AvgDiscount]), 2),
    ("Profit", NAMEOF('Sample - Superstore'[SumProfit]), 3),
    ("Profit %", NAMEOF('Sample - Superstore'[Profit %]), 4)
}


This parameter was placed as a slicer (toggle-style buttons) to switch metrics across visuals.

Created Measures

To drive the parameter, the following measures were created:

SumSales = SUM('Sample - Superstore'[Sales])

SumQuantity = SUM('Sample - Superstore'[Quantity])

AvgDiscount = AVERAGE('Sample - Superstore'[Discount])

SumProfit = SUM('Sample - Superstore'[Profit])

Profit % = DIVIDE([SumProfit], [SumSales])

## Dynamic Titles (Using SELECTEDVALUE)

Each visual title updates automatically based on the selected metric.

Example title measure for the line chart:

BY_ORDER_DATE = SELECTEDVALUE('Metric Selector'[Metric Selector]) 
    & " by Order Date"


Each visual uses its own title logic (Order Date, Region, State, Segment, Category).

## Dynamic Formatting (Format Strings)

To handle different number formats:

Sales, Profit → currency

Quantity → whole number

Avg Discount, Profit % → percentage

Used Dynamic Format Strings in Power BI:

Format = 

SWITCH(
    SELECTEDMEASURENAME(),
    "AvgDiscount", "0.00%",
    "Profit %", "0.0%",
    "SumSales", "$#,##0",
    "SumProfit", "$#,##0",
    "SumQuantity", "#,##0",
    "0"
)


This ensures charts switch cleanly without layout issues.

## Insights This Dashboard Can Answer

Which year recorded the highest and lowest sales performance?

Which region generated the greatest profit, and what percentage of total profit does it represent?

Which states demonstrate the highest purchasing activity based on total units sold?

Which customer segment should be prioritized, and what data supports this recommendation?

Which product categories contribute the most to sales volume and revenue growth?

Which states require strategic action—either increased focus or reduced investment—based on declining sales trends or negative profitability?

Should the company adjust its average discount levels to improve sales, and what evidence supports this decision?

## Final Result

A fully dynamic business dashboard where:

One parameter controls five visuals simultaneously

Every title adjusts automatically

Units & formatting change depending on the metric

Users can switch between Sales → Profit → Quantity → Avg Discount → Profit % without rebuilding visuals.

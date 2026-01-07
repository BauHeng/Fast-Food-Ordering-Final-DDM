# Fast-Food-Ordering-Final-DDDM

This project analyzes sales data for Balaji Fast Food. We built a sales performance dashboard to help the business understand trends and improve operations. The project follows a 5-week work breakdown structure from data cleaning to final presentation.

## Table of Contents
* [Project Overview](#project-overview)
* [Dataset Description](#dataset-description)
* [Business Questions](#business-questions)
* [Methodology](#methodology)
* [Data Model](#data-model)
* [Key Insights](#key-insights)
* [Recommendations](#recommendations)
* [Team](#team)

## Project Overview
**Goal:** Build a dashboard to track sales performance. This includes analyzing time of sale, item popularity, payment types, and staff performance.

**Objectives:**
* Understand customer ordering behavior.
* Evaluate delivery efficiency by city.
* Identify high revenue cuisine categories.

## Dataset Description
The dataset contains **500 rows and 8 columns**. It represents transactional data from the business.

**Source:** `fast_food_ordering_dataset.csv`

**Columns:**
* `order_id`: Unique identifier for each order.
* `order_time`: Timestamp of the order.
* `city`: Location of the customer.
* `cuisine_type`: Category of the food (e.g., Mexican, Fast Food).
* `order_value`: The total cost of the order.
* `delivery_time_minutes`: Duration taken for delivery.
* `payment_method`: Method used to pay (e.g., Cash, UPI, Credit Card).
* `items_count`: Number of items in the order.

**Data Quality:**
* Missing Values: 0 (Complete dataset).
* Duplicates: 0 (No duplicate orders).
* Delivery times range from 15 to 74 minutes.

## Business Questions
We designed the analysis to answer these specific questions:
1.  **Product Strategy:** Which cuisine type has the highest Average Order Value (AOV)?
2.  **Operations:** Which city has the longest average delivery time?
3.  **Growth:** Which city contributes the most to total revenue?

## Methodology
We followed a structured process over several weeks:

* **Week 1 and 2: Setup and Cleaning**
    * We defined business questions and explored the dataset.
    * We cleaned the data and fixed formats for dates and currency.
* **Week 3: SQL Modeling and Preparation**
    * We used SQL to remove null values and standardize data types.
    * We created SQL Views for the dashboard.
    * We planned the data model and DAX measures.
* **Week 4: Dashboard Build**
    * We built an Executive Scorecard to track Revenue, Orders, and AOV.
    * We created visualizations for hourly trends and category performance.

## Data Model
We implemented a **Star Schema** to optimize query performance in Power BI.

* **Fact Table:** `Fact_Orders` (Contains metrics like Revenue, Quantity, Time).
* **Dimension Tables:**
    * `Dim_City` (Context for location).
    * `Dim_Cuisine` (Context for food categories).

## Key Insights
Based on our analysis of the data:
1.  **Peak Operations:** There is a big surge in orders between **12:00 PM and 1:00 PM** (Lunch Rush).
2.  **Downtime:** Activity is very low after 10:00 PM.
3.  **Top Performers:** South Indian and Italian cuisines generate the highest share of revenue.

## Recommendations
We suggest the following strategies to improve the business:
1.  **Resource Allocation:** Increase kitchen and delivery staff levels during the **11:00 AM to 2:00 PM** window to handle the rush.
2.  **Inventory Optimization:** Prioritize stock for **South Indian** ingredients to prevent running out during high demand.
3.  **Marketing Strategy:** Run "Happy Hour" promotions during off peak hours (**3:00 PM to 5:00 PM**) to get more orders during slow times.

## Team
**Team 3**
* **Strengths:** Diverse skill set (coding, design, business thinking) and strong teamwork.

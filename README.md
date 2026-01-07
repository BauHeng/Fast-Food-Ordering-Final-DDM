# Fast-Food-Ordering-Final-DDDM

# Optimizing Balaji Fast Food Operations through Sales Data Analysis

**Tools Used:** SQL, Power BI, Excel

## Table of Contents
* [Project Background](#project-background)
* [Data Structure](#data-structure)
* [Executive Summary](#executive-summary)
* [Business Questions](#business-questions)
* [Key Insights](#key-insights)
* [Recommendations](#recommendations)
* [Technical Methodology](#technical-methodology)
* [SQL Logic](#sql-logic)

## Project Background
[cite_start]This project focuses on building a sales performance dashboard for Balaji Fast Food[cite: 6, 9]. [cite_start]The business required a way to analyze their rich dataset to gain insights[cite: 8].

The main goal is to optimize operations by analyzing transaction data. [cite_start]We examine the time of sale, item popularity, payment types, and staff performance[cite: 6].

**Team 3:**
* [cite_start]We used a diverse skill set including coding, design, and business thinking[cite: 56].
* [cite_start]We followed a fixed weekly meeting schedule to ensure progress[cite: 57].

## Data Structure
[cite_start]The dataset consists of **500 rows and 8 columns**[cite: 84]. [cite_start]It contains transactional data used to understand customer behavior and delivery efficiency[cite: 90, 91].

[cite_start]**Source File:** `fast_food_ordering_dataset.csv` [cite: 82]

**Data Dictionary:**
* [cite_start]**order_id:** Unique identifier for each order[cite: 85].
* [cite_start]**order_time:** Timestamp of the order[cite: 86].
* [cite_start]**city:** Customer location[cite: 87].
* [cite_start]**cuisine_type:** Type of cuisine (Categorical)[cite: 87].
* [cite_start]**order_value:** Order value (Numerical)[cite: 88].
* [cite_start]**delivery_time_minutes:** Delivery duration in minutes[cite: 89].
* **payment_method:** Method of payment (Example: Cash, UPI).
* **items_count:** Quantity of items ordered.

**Data Quality Check:**
* [cite_start]**Missing Values:** 0 (The dataset is complete)[cite: 97].
* [cite_start]**Duplicates:** 0 (There are no duplicate orders)[cite: 98].
* [cite_start]**Consistency:** All metrics are reasonable and there are no negative order values[cite: 99, 101].

## Executive Summary
[cite_start]We built a dashboard to track Revenue, Orders, and Average Order Value in real time[cite: 149]. [cite_start]The analysis highlights peak operational hours and identifies the most profitable cuisine categories[cite: 150, 151].

## Business Questions
[cite_start]We used data to answer three specific questions for the business[cite: 115]:

1.  [cite_start]**Product Strategy:** Which cuisine type has the highest Average Order Value (AOV)? [cite: 107]
    * [cite_start]**Purpose:** To focus on promoting high profit groups like North Indian and Mexican cuisines[cite: 108].
2.  [cite_start]**Operations:** Which city has the longest average delivery time? [cite: 110]
    * [cite_start]**Purpose:** To optimize the delivery fleet or reroute drivers in that area[cite: 111].
3.  [cite_start]**Growth:** Which city contributes the most in total revenue? [cite: 113]
    * [cite_start]**Purpose:** To identify key markets for further marketing investment[cite: 114].

## Key Insights
[cite_start]Our analysis of the temporal trends and product dynamics revealed the following[cite: 152, 153, 157]:

* [cite_start]**Peak Operations:** There is a significant surge in order volume between **12:00 PM and 1:00 PM** which is the Lunch Rush[cite: 154].
* [cite_start]**Downtime:** There is minimal activity observed after **10:00 PM**[cite: 155].
* [cite_start]**Top Performers:** South Indian and Italian cuisines generate the highest revenue share[cite: 158].

## Recommendations
[cite_start]Based on the insights we propose the following strategic actions[cite: 159]:

1.  **Resource Allocation:**
    * Increase kitchen and delivery staffing levels during the **11:00 AM to 2:00 PM** window. [cite_start]This will help mitigate delays during the lunch rush[cite: 161].
2.  **Inventory Optimization:**
    * Prioritize stock for **South Indian** ingredients. [cite_start]This will prevent stockouts during high demand periods[cite: 164].
3.  **Marketing Strategy:**
    * Implement "Happy Hour" promotions during off peak hours from **3:00 PM to 5:00 PM**. [cite_start]This will flatten the demand curve[cite: 167].

## Technical Methodology
[cite_start]We followed a 5 week work breakdown structure[cite: 41].

* [cite_start]**Week 1 and 2:** We defined the business questions and explored the dataset[cite: 26, 25]. [cite_start]We cleaned the data and standardized formats for dates and currency[cite: 34].
* **Week 3:** We focused on SQL modeling. [cite_start]We removed null values and created clean master tables[cite: 178, 181]. [cite_start]We established a Star Schema to optimize query performance[cite: 143].
* [cite_start]**Week 4:** We built the dashboard with an Executive Scorecard and Time Series Analysis[cite: 149, 150].

### Data Model
[cite_start]We used a Star Schema structure[cite: 143].
* [cite_start]**Fact Table:** `Fact_Orders` contains metrics like Revenue and Quantity[cite: 146].
* [cite_start]**Dimensions:** `Dim_City` and `Dim_Cuisine` contain attributes for filtering[cite: 147].

## SQL Logic
[cite_start]We used SQL to clean the data and create views for Power BI[cite: 173].

```sql
-- 1. CLEANING
-- We remove null values and ensure order_id is present
CREATE TABLE staging_orders AS
SELECT DISTINCT *
FROM raw_fast_food_data
WHERE order_id IS NOT NULL;

-- 2. NORMALIZATION (Star Schema)
-- Creating the City Dimension
CREATE TABLE Dim_City (
    city_id INT PRIMARY KEY AUTO_INCREMENT,
    city_name VARCHAR(255)
);
INSERT INTO Dim_City (city_name)
SELECT DISTINCT city FROM staging_orders;

-- Creating the Cuisine Dimension
CREATE TABLE Dim_Cuisine (
    cuisine_id INT PRIMARY KEY AUTO_INCREMENT,
    cuisine_type VARCHAR(255)
);
INSERT INTO Dim_Cuisine (cuisine_type)
SELECT DISTINCT cuisine_type FROM staging_orders;

-- Creating the Fact Table
CREATE TABLE Fact_Orders AS
SELECT 
    s.order_id,
    s.order_time,
    c.city_id,
    k.cuisine_id,
    s.order_value,
    s.items_count,
    s.delivery_time_minutes
FROM staging_orders s
JOIN Dim_City c ON s.city = c.city_name
JOIN Dim_Cuisine k ON s.cuisine_type = k.cuisine_type;

-- 3. KPI VIEWS
-- View for Hourly Trends to identify peak windows
CREATE VIEW V_Hourly_Trends AS
SELECT 
    EXTRACT(HOUR FROM order_time) AS order_hour,
    COUNT(order_id) AS total_orders,
    SUM(order_value) AS total_revenue
FROM Fact_Orders
GROUP BY EXTRACT(HOUR FROM order_time)
ORDER BY total_orders DESC;
**Team 3**
* **Strengths:** Diverse skill set (coding, design, business thinking) and strong teamwork.

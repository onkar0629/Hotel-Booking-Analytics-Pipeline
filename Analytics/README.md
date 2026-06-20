# Business Analytics using Hive

## Objective

After ingesting and optimizing the hotel booking dataset using Hive Partitioning and Bucketing, analytical queries were performed to derive business insights.

The goal is to answer key business questions related to bookings, revenue, cancellations, customer behavior, and market trends.

---

## Dataset Summary

| Metric        | Value                    |
| ------------- | ------------------------ |
| Total Records | 119,390                  |
| Source        | MySQL                    |
| Storage       | HDFS                     |
| Query Engine  | Hive                     |
| Optimization  | Partitioning & Bucketing |

---

# Analysis 1: Total Bookings

## Business Question

How many bookings are present in the dataset?

## Query

```sql
SELECT COUNT(*) AS total_bookings
FROM hotel_bucket;
```

## Insight

Provides the total booking volume available for analysis.

---

# Analysis 2: Hotel Type Distribution

## Business Question

Which hotel type receives more bookings?

## Query

```sql
SELECT hotel,
COUNT(*) AS total_bookings
FROM hotel_bucket
GROUP BY hotel
ORDER BY total_bookings DESC;
```

## Insight

Helps identify the most preferred hotel category.

---

# Analysis 3: Cancellation Analysis

## Business Question

How many bookings were cancelled?

## Query

```sql
SELECT reservation_status,
COUNT(*) AS bookings
FROM hotel_bucket
GROUP BY reservation_status;
```

## Insight

Measures customer cancellation behavior and booking reliability.

---

# Analysis 4: Top Countries by Booking Volume

## Business Question

Which countries generate the highest number of bookings?

## Query

```sql
SELECT country,
COUNT(*) AS total_bookings
FROM hotel_bucket
GROUP BY country
ORDER BY total_bookings DESC
LIMIT 10;
```

## Insight

Identifies major customer markets.

---

# Analysis 5: Revenue by Hotel Type

## Business Question

Which hotel category generates higher revenue?

## Query

```sql
SELECT hotel,
ROUND(SUM(adr),2) AS revenue
FROM hotel_bucket
GROUP BY hotel;
```

## Insight

Compares revenue contribution by hotel type.

---

# Analysis 6: Year-wise Revenue

## Business Question

How does revenue vary by year?

## Query

```sql
SELECT arrival_date_year,
ROUND(SUM(adr),2) AS total_revenue
FROM hotel_bucket
GROUP BY arrival_date_year
ORDER BY arrival_date_year;
```

## Insight

Measures yearly business growth.

---

# Analysis 7: Monthly Booking Trend

## Business Question

Which months receive the highest number of bookings?

## Query

```sql
SELECT arrival_date_month,
COUNT(*) AS bookings
FROM hotel_bucket
GROUP BY arrival_date_month
ORDER BY bookings DESC;
```

## Insight

Identifies seasonal demand patterns.

---

# Analysis 8: Market Segment Analysis

## Business Question

Which market segment contributes the most bookings?

## Query

```sql
SELECT market_segment,
COUNT(*) AS bookings
FROM hotel_bucket
GROUP BY market_segment
ORDER BY bookings DESC;
```

## Insight

Evaluates booking source effectiveness.

---

# Analysis 9: Customer Type Analysis

## Business Question

Which customer category generates the most bookings?

## Query

```sql
SELECT customer_type,
COUNT(*) AS bookings
FROM hotel_bucket
GROUP BY customer_type
ORDER BY bookings DESC;
```

## Insight

Provides customer segmentation insights.

---

# Analysis 10: Average Daily Rate by Country

## Business Question

Which countries generate the highest average room rates?

## Query

```sql
SELECT country,
ROUND(AVG(adr),2) AS avg_rate
FROM hotel_bucket
GROUP BY country
ORDER BY avg_rate DESC
LIMIT 10;
```

## Insight

Highlights high-value customer markets.

---

# Optimization Used

## Partitioning

```text
arrival_date_year
```

Benefits:

* Reduced data scanning
* Faster filtering
* Partition pruning

---

## Bucketing

```text
country
```

Benefits:

* Better query performance
* Efficient joins
* Improved sampling

---

# Business Outcomes

The project successfully demonstrates:

* Data ingestion from MySQL using Sqoop
* Distributed storage using HDFS
* Query optimization using Hive Partitioning and Bucketing
* Analytical processing using HiveQL
* Extraction of actionable business insights from hotel booking data

---

# Screenshots

### Total Bookings

*Add screenshot*

### Cancellation Analysis

*Add screenshot*

### Top Countries

*Add screenshot*

### Revenue Analysis

*Add screenshot*

### Monthly Trend Analysis

*Add screenshot*

### Customer Analysis

*Add screenshot*

---

# Key Learnings

* MySQL to Hadoop ingestion using Sqoop
* HDFS storage architecture
* Hive External Tables
* Dynamic Partitioning
* Bucketing Concepts
* Hive Query Optimization
* Business Analytics using HiveQL

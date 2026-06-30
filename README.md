# Hotel Booking Analytics Pipeline

## Project Overview

This project demonstrates an end-to-end Data Engineering pipeline built on the Hadoop ecosystem using Cloudera QuickStart VM.

The pipeline extracts hotel booking data from MySQL, imports it into Hadoop using Sqoop, stores data in HDFS, optimizes query performance using Hive Partitioning and Bucketing, and generates business insights using HiveQL

---

## Business Problem

Hotel booking data is generated from multiple booking channels and stored in relational databases. As data volume grows, analytical queries become slower and more expensive.

This project demonstrates how Hadoop can be used to:

- Ingest large datasets from relational databases
- Store data in distributed storage (HDFS)
- Optimize data retrieval using Partitioning and Bucketing
- Perform large-scale analytical processing using Hive

---

## Architecture

```text
Hotel Booking Dataset
        │
        ▼
      MySQL
        │
        ▼
      Sqoop
        │
        ▼
       HDFS
        │
        ▼
 Hive External Table
        │
        ▼
   Partitioning
        │
        ▼
    Bucketing
        │
        ▼
 Business Analytics
```

---

## Tech Stack

| Technology | Purpose |
|------------|---------|
| MySQL | Source Database |
| Sqoop | Data Ingestion |
| Hadoop HDFS | Distributed Storage |
| Hive | Data Warehouse |
| Cloudera QuickStart VM | Hadoop Environment |

---

## Dataset Information

### Dataset Name

Hotel Booking Demand Dataset

### Dataset Size

- Records: 119,390
- Columns: 20

### Selected Columns

- booking_id
- hotel
- is_canceled
- lead_time
- arrival_date_year
- arrival_date_month
- arrival_date_week_number
- stays_in_weekend_nights
- stays_in_week_nights
- adults
- children
- babies
- meal
- country
- market_segment
- distribution_channel
- customer_type
- adr
- total_of_special_requests
- reservation_status

---

## Data Optimization Strategy

### Partition Column

```sql
arrival_date_year
```

Reason:

- Frequently used in analytical filtering
- Demonstrates partition pruning
- Improves query performance

### Bucket Column

```sql
country
```

Reason:

- High-cardinality column
- Frequently used in aggregations
- Improves query execution efficiency

---

## Project Modules

### 1. MySQL

- Database Creation
- Table Design
- Data Loading
- Validation

### 2. Sqoop

- Import Data from MySQL
- Data Validation
- HDFS Verification

### 3. HDFS

- Store Imported Data
- File Verification
- Directory Management

### 4. Hive

- External Table Creation
- Partitioning
- Bucketing

### 5. Analytics

- Revenue Analysis
- Cancellation Analysis
- Country Analysis
- Customer Analysis
- Booking Trend Analysis

---

## Repository Structure

```text
hotel-booking-analytics-pipeline/
│
├── README.md
│
├── MySQL/
│   └── README.md
│
├── Sqoop/
│   └── README.md
│
├── HDFS/
│   └── README.md
│
├── Hive/
│   └── README.md
│
├── Analytics/
│   └── README.md
│
├── Screenshots/
│
│
└── Dataset/

```

---

## Author

Onkar Ankush Jadhav

Aspiring Data Engineer | Hadoop Ecosystem Learner | Big Data Enthusiast

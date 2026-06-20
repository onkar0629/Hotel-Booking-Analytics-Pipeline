# Hotel Booking Analytics Pipeline

## Project Overview

This project demonstrates an end-to-end Data Engineering pipeline using the Hadoop ecosystem.

The project imports hotel booking data from MySQL into Hadoop using Sqoop, stores data in HDFS, performs Hive-based optimization using Partitioning and Bucketing, and generates business insights through HiveQL.

---

## Tech Stack

- MySQL
- Sqoop
- Hadoop
- HDFS
- Hive
- Git & GitHub

---

## Architecture

```text
Hotel Booking Dataset
        ↓
      MySQL
        ↓
      Sqoop
        ↓
      HDFS
        ↓
 Hive External Table
        ↓
 Partitioning
        ↓
 Bucketing
        ↓
 Hive Analytics
```

---

## Dataset Details

| Attribute | Value                |
|-----------|----------------------|
| Dataset   | Hotel Booking Demand |
| Records   | 119,390              |
| Columns   | 21                   |
| Source    | Kaggle               |  

---

## Project Modules

### 1. MySQL
- Database Creation
- Table Design
- Data Loading

### 2. Sqoop
- Import Data from MySQL
- Store Data in HDFS

### 3. Hive
- External Table Creation
- Partitioning
- Bucketing

### 4. Analytics
- Revenue Analysis
- Cancellation Analysis
- Country Analysis
- Customer Analysis

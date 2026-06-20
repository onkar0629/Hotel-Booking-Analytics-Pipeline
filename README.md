# Hotel Booking Analytics Pipeline

## Overview

This project demonstrates an end-to-end Data Engineering workflow using the Hadoop ecosystem on Cloudera QuickStart VM.

The pipeline extracts hotel booking data from MySQL, imports it into Hadoop using Sqoop, stores it in HDFS, optimizes storage and query performance using Hive Partitioning and Bucketing, and performs analytical reporting using HiveQL.

---

## Tech Stack

- MySQL
- Sqoop
- Hadoop HDFS
- Hive
- Git
- GitHub
- Cloudera QuickStart VM

---

## Dataset

Hotel Booking Demand Dataset

Total Records: 119,390

Total Columns: 20

Kaggle : 

---

## Architecture/Project Flow

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
 Business Analytics

---
```

---

## Dataset Details

| Attribute | Value                |
|-----------|----------------------|
| Dataset   | Hotel Booking Demand |
| Records   | 119,390              |
| Columns   | 20                   |
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

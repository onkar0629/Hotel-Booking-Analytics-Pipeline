# Sqoop Implementation

## Objective

After storing the Hotel Booking dataset in MySQL, the next step is to transfer the data into the Hadoop ecosystem.

Apache Sqoop is used to import data from MySQL into HDFS efficiently. Sqoop automates data transfer between relational databases and Hadoop, eliminating the need for manual CSV exports and uploads.

---

## Why Sqoop?

Traditional methods of moving data from relational databases to Hadoop involve:

1. Exporting data into CSV files.
2. Copying files manually.
3. Uploading files into HDFS.

This process becomes inefficient for large datasets.

Sqoop provides:

* Fast data transfer
* Parallel processing using mappers
* Direct integration with MySQL
* Automated import and export operations
* Reduced manual effort

---

## Data Flow

```text
MySQL
   │
   ▼
 Sqoop Import
   │
   ▼
   HDFS
```

---

## Source Details

### Database

```text
hotel_project
```

### Table

```text
hotel_bookings
```

### Total Records

```text
119,390
```

---

## Import Strategy

The dataset contains approximately 119K records.

Since this is a learning project running on Cloudera QuickStart VM with limited resources, a single mapper was used.

### Why One Mapper?

* Stable execution on local VM
* Easier validation
* Avoids unnecessary resource consumption

For production-scale datasets, multiple mappers would be preferred.

---

## Sqoop Import Command

```bash
sqoop import \
--connect jdbc:mysql://localhost/hotel_project \
--username root -P \
--table hotel_bookings \
--target-dir /project/hotel_bookings \
--m 1
```

---

## Command Explanation

| Parameter    | Description                |
| ------------ | -------------------------- |
| --connect    | JDBC connection string     |
| --username   | root username             |
| -P           | MySQL password             |
| --table      | Source table name          |
| --target-dir | Destination HDFS directory |
| --m 1        | Number of mappers          |

---

## Import Verification

After successful execution, verify the imported files.

### Check Directory

```bash
hdfs dfs -ls /project/hotel_bookings
```

### Check Record Sample

```bash
hdfs dfs -cat /project/hotel_bookings/part-m-00000 | head
```

### Count Imported Files

```bash
hdfs dfs -count /project/hotel_bookings
```

---

## Data Validation

### Verify Source Record Count

```sql
SELECT COUNT(*)
FROM hotel_bookings;
```

Expected Output:

```text
119390
```

### Verify Imported Data

```bash
hdfs dfs -cat /project/hotel_bookings/part-m-00000 | wc -l
```

The imported record count should match the source table count.

---

## Challenges Faced

### JDBC Connectivity

Sqoop requires a JDBC driver to communicate with MySQL.

The MySQL connector JAR must be placed inside the Sqoop library directory.

### Data Type Mapping

Sqoop automatically maps MySQL datatypes to Hadoop-compatible datatypes.

Example:

| MySQL   | Hadoop |
| ------- | ------ |
| VARCHAR | STRING |
| INT     | INT    |
| DECIMAL | DOUBLE |
| DATE    | STRING |

---

## Business Value

This stage demonstrates how enterprise data stored in relational databases can be ingested into Hadoop for large-scale analytics.

Benefits:

* Automated ingestion
* Scalable data movement
* Reduced manual intervention
* Foundation for Hive analytics

---

## Output

Successfully imported 119,390 hotel booking records from MySQL into HDFS using Apache Sqoop.

---

## Screenshots

### MySQL Source Table

*Add screenshot here*

### Sqoop Execution

*Add screenshot here*

### HDFS Verification

*Add screenshot here*

### Imported Files

*Add screenshot here*

---

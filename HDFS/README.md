# HDFS Implementation

## Objective

After importing data from MySQL using Sqoop, the dataset is stored in Hadoop Distributed File System (HDFS).

HDFS serves as the storage layer of Hadoop and provides scalable, fault-tolerant distributed storage for large datasets.

---

## Why HDFS?

Traditional file systems have limitations when handling large-scale data.

HDFS provides:

* Distributed storage
* Fault tolerance
* High availability
* Scalability
* Parallel processing support

---

## Data Flow

```text
MySQL
   │
   ▼
 Sqoop
   │
   ▼
 HDFS
```

---

## HDFS Target Directory

```text
/project/hotel_bookings
```

---

## Verify Directory Creation

```bash
hdfs dfs -ls /project
```

Output:

```text
Found 1 items
drwxr-xr-x   - cloudera supergroup          0 YYYY-MM-DD HH:MM /project/hotel_bookings
```

---

## Verify Imported Files

```bash
hdfs dfs -ls /project/hotel_bookings
```

Example Output:

```text
part-m-00000
_SUCCESS
```

---

## View Sample Records

```bash
hdfs dfs -cat /project/hotel_bookings/part-m-00000 | head
```

Purpose:

* Verify imported data
* Check delimiters
* Validate record structure

---

## Count Records

```bash
hdfs dfs -cat /project/hotel_bookings/part-m-00000 | wc -l
```

Expected Output:

```text
119390
```

---

## Important HDFS Commands Used

### List Files

```bash
hdfs dfs -ls /project/hotel_bookings
```

### View Data

```bash
hdfs dfs -cat /project/hotel_bookings/part-m-00000 | head
```

### Check Storage Usage

```bash
hdfs dfs -du -h /project/hotel_bookings
```

### Count Files and Directories

```bash
hdfs dfs -count /project/hotel_bookings
```

---

## Data Validation

### Source Record Count

```sql
SELECT COUNT(*)
FROM hotel_bookings;
```

Output:

```text
119390
```

### HDFS Record Count

```bash
hdfs dfs -cat /project/hotel_bookings/part-m-00000 | wc -l
```

Output:

```text
119390
```

Result:

Source and HDFS record counts matched successfully.

---

## Business Value

HDFS acts as the central storage layer for analytical processing.

Benefits:

* Distributed storage
* Fault tolerance
* High throughput
* Integration with Hive

---

## Output

Successfully stored 119,390 hotel booking records in HDFS for downstream Hive processing.

---

## Screenshots

### HDFS Directory

*Add screenshot here*

### Imported Files

*Add screenshot here*

### Sample Records

*Add screenshot here*

### Record Validation

*Add screenshot here*

---

## Interview Questions

### What is HDFS?

HDFS (Hadoop Distributed File System) is the storage layer of Hadoop designed to store large datasets across multiple machines.

### Why is HDFS needed?

HDFS provides scalable and fault-tolerant storage for Big Data workloads.

### What files were generated after Sqoop import?

* part-m-00000
* _SUCCESS

### What is the purpose of the _SUCCESS file?

It indicates that the import job completed successfully.

### How did you validate data after import?

By comparing MySQL record counts with HDFS record counts.

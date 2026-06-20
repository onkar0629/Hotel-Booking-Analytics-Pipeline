# Hive Implementation

## Objective

After storing the dataset in HDFS, Apache Hive is used to perform analytical processing.

Hive provides an SQL-like language called HiveQL that allows users to query large datasets stored in Hadoop without writing MapReduce programs.

---

## Why Hive?

Working directly with MapReduce is complex and time-consuming.

Hive simplifies Big Data analytics by providing:

* SQL-like syntax
* Easy querying
* Integration with HDFS
* Data optimization techniques
* Support for large-scale analytical workloads

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
   │
   ▼
Hive External Table
   │
   ▼
Partitioning
   │
   ▼
Bucketing
```

---

# External Table

## Why External Table?

The dataset already exists in HDFS.

Using an External Table allows Hive to access data without moving or duplicating it.

Benefits:

* Faster setup
* No data duplication
* Data remains in HDFS even if the table is dropped

---

## External Table Creation

```sql
CREATE EXTERNAL TABLE hotel_raw(
booking_id STRING,
hotel STRING,
is_canceled INT,
lead_time INT,
arrival_date_year INT,
arrival_date_month STRING,
arrival_date_week_number INT,
stays_in_weekend_nights INT,
stays_in_week_nights INT,
adults INT,
children INT,
babies INT,
meal STRING,
country STRING,
market_segment STRING,
distribution_channel STRING,
customer_type STRING,
adr DOUBLE,
total_of_special_requests INT,
reservation_status STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LOCATION '/project/hotel_bookings';
```

---

## Validate Data

```sql
SELECT *
FROM hotel_raw
LIMIT 10;
```

```sql
SELECT COUNT(*)
FROM hotel_raw;
```

Expected Output:

```text
119390
```

---

# Partitioning

## Why Partitioning?

Without partitioning, Hive scans the entire dataset.

Partitioning divides data into smaller directories based on a column value.

Benefits:

* Faster query execution
* Reduced I/O
* Partition pruning

---

## Partition Column

```text
arrival_date_year
```

Reason:

* Frequently used in reporting
* Only a few distinct values
* Ideal partition candidate

---

## Create Partitioned Table

```sql
CREATE TABLE hotel_part(
booking_id STRING,
hotel STRING,
is_canceled INT,
lead_time INT,
arrival_date_month STRING,
arrival_date_week_number INT,
stays_in_weekend_nights INT,
stays_in_week_nights INT,
adults INT,
children INT,
babies INT,
meal STRING,
country STRING,
market_segment STRING,
distribution_channel STRING,
customer_type STRING,
adr DOUBLE,
total_of_special_requests INT,
reservation_status STRING,
)
PARTITIONED BY(arrival_date_year INT);
```

---

## Enable Dynamic Partitioning

```sql
SET hive.exec.dynamic.partition=true;

SET hive.exec.dynamic.partition.mode=nonstrict;
```

---

## Load Data into Partitioned Table

```sql
INSERT INTO hotel_part
PARTITION(arrival_date_year)
SELECT
booking_id,
hotel,
is_canceled,
lead_time,
arrival_date_month,
arrival_date_week_number,
stays_in_weekend_nights,
stays_in_week_nights,
adults,
children,
babies,
meal,
country,
market_segment,
distribution_channel,
customer_type,
adr,
total_of_special_requests,
reservation_status,
arrival_date_year
FROM hotel_raw;
```

---

## Verify Partitions

```sql
SHOW PARTITIONS hotel_part;
```

Expected:

```text
arrival_date_year=2015
arrival_date_year=2016
arrival_date_year=2017
```

---

# Bucketing

## Why Bucketing?

Partitioning works best on low-cardinality columns.

Country contains many unique values and is a good candidate for bucketing.

Benefits:

* Faster joins
* Better sampling
* Improved query performance

---

## Bucket Column

```text
country
```

---

## Create Bucketed Table

```sql
CREATE TABLE hotel_bucket(
booking_id STRING,
hotel STRING,
is_canceled INT,
lead_time INT,
arrival_date_month STRING,
arrival_date_week_number INT,
stays_in_weekend_nights INT,
stays_in_week_nights INT,
adults INT,
children INT,
babies INT,
meal STRING,
country STRING,
market_segment STRING,
distribution_channel STRING,
customer_type STRING,
adr DOUBLE,
total_of_special_requests INT,
reservation_status STRING,
arrival_date_year INT
)
CLUSTERED BY(country)
INTO 8 BUCKETS
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ',';
```

---

## Enable Bucketing

```sql
SET hive.enforce.bucketing=true;
```

---

## Load Bucketed Table

```sql
INSERT INTO hotel_bucket
SELECT *
FROM hotel_part;
```

---

## Verify Buckets

```bash
hdfs dfs -ls /user/hive/warehouse/hotel_bucket
```

Multiple bucket files should be generated.

---

## Output

Successfully created:

* External Table
* Partitioned Table
* Bucketed Table

for optimized analytical processing.

---

## Screenshots

### External Table Creation

*Add screenshot here*

### Partition Creation

*Add screenshot here*

### Show Partitions

*Add screenshot here*

### Bucket Files

*Add screenshot here*

---


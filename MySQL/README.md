# MySQL Implementation

## Objective

The first stage of the pipeline is to store the Hotel Booking dataset in MySQL. In real-world organizations, transactional and operational data is commonly stored in relational databases before being moved to Big Data platforms for analytics.

In this project, MySQL acts as the source system from which data is imported into Hadoop using Sqoop.

---

## Why MySQL?

MySQL was chosen because:

* It is one of the most widely used relational databases.
* It stores structured data efficiently.
* It supports SQL for data manipulation and validation.
* Sqoop provides native integration with MySQL through JDBC.
* It simulates a real-world OLTP (Online Transaction Processing) source system.

---

## Database Creation

A dedicated database was created to store the hotel booking dataset.

```sql
CREATE DATABASE hotel_project;

USE hotel_project;
```

---

## Table Design

The dataset contains hotel booking information such as customer details, booking status, arrival dates, distribution channels, and revenue-related metrics.

### Design Considerations

#### Booking ID

The original dataset does not contain a primary key. Therefore, a custom booking identifier was created.

Example:

```text
BK-001
BK-002
BK-003
```

Since the identifier contains both alphabets and numbers, the `VARCHAR` datatype was used instead of `INT`.

#### Revenue Column

The `adr` (Average Daily Rate) column stores monetary values. Therefore, the `DECIMAL` datatype was chosen to maintain precision.

---

## Table Creation

```sql
CREATE TABLE hotel_bookings (
    booking_id VARCHAR(20) PRIMARY KEY,
    hotel VARCHAR(50),
    is_canceled TINYINT,
    lead_time INT,
    arrival_date_year INT,
    arrival_date_month VARCHAR(20),
    arrival_date_week_number INT,
    stays_in_weekend_nights INT,
    stays_in_week_nights INT,
    adults INT,
    children INT,
    babies INT,
    meal VARCHAR(30),
    country VARCHAR(10),
    market_segment VARCHAR(50),
    distribution_channel VARCHAR(50),
    customer_type VARCHAR(50),
    adr DECIMAL(10,2),
    total_of_special_requests INT,
    reservation_status VARCHAR(30)
);
```

---

## Data Loading

 The Hotel Booking dataset was imported into MySQL using LOAD Command .

 ```sql
LOAD DATA LOCAL INFILE '/home/cloudera/Desktop/bookings.csv'
INTO TABLE hotel_bookings
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
```

---

## Data Validation

After loading the dataset, validation queries were executed to ensure successful ingestion.

### Record Count

```sql
SELECT COUNT(*)
FROM hotel_bookings;
```

Expected Output:

```text
119390
```

### Sample Data Verification

```sql
SELECT *
FROM hotel_bookings
LIMIT 10;
```

### Table Structure Verification

```sql
DESC hotel_bookings;
```

---

## Business Value of This Stage

At this stage:

* Raw booking data is successfully stored in a relational database.
* Data quality can be validated before ingestion into Hadoop.
* The database serves as the source system for Sqoop import operations.

---

## Challenges Faced

* Creating a unique identifier because the original dataset lacked a primary key.
* Selecting appropriate datatypes for analytical processing.
* Ensuring date values were loaded correctly.

---

## Outcome

Successfully stored 119,390 hotel booking records in MySQL and prepared the dataset for ingestion into Hadoop using Sqoop.

---

## Screenshots

### Database Creation

<img width="518" height="94" alt="Create database" src="https://github.com/user-attachments/assets/72df6d3d-7cfb-49f2-9dc0-191854ca15a6" />


### Table Creation

<img width="516" height="329" alt="create table" src="https://github.com/user-attachments/assets/9ff17c3d-fd5c-4218-95e7-619ee9c98a0d" />

### Table Structure Verification

<img width="559" height="370" alt="Screenshot 2026-06-20 231339" src="https://github.com/user-attachments/assets/23484d19-71cc-43d8-a4b2-956750687597" />

### Data Import

<img width="584" height="124" alt="Screenshot 2026-06-20 232154" src="https://github.com/user-attachments/assets/c14d37b8-e5b3-48e1-9205-35ee68454995" />


### Validation Queries

<img width="542" height="109" alt="Screenshot 2026-06-20 232314" src="https://github.com/user-attachments/assets/2319dd81-a2b1-4c93-8167-4508766f6e91" />

```sql
mysql> SELECT * FROM hotel_bookings LIMIT 10;
+------------+--------------+-------------+-----------+-------------------+--------------------+--------------------------+-------------------------+----------------------+--------+----------+--------+------+---------+----------------+----------------------+---------------+--------+---------------------------+--------------------+
| booking_id | hotel        | is_canceled | lead_time | arrival_date_year | arrival_date_month | arrival_date_week_number | stays_in_weekend_nights | stays_in_week_nights | adults | children | babies | meal | country | market_segment | distribution_channel | customer_type | adr    | total_of_special_requests | reservation_status |
+------------+--------------+-------------+-----------+-------------------+--------------------+--------------------------+-------------------------+----------------------+--------+----------+--------+------+---------+----------------+----------------------+---------------+--------+---------------------------+--------------------+
         |   | Resort Hotel |           0 |       342 |              2015 | July               |                       27 |                       0 |                    0 |      2 |        0 |      0 | BB   | PRT     | Direct         | Direct               | Transient     |   0.00 |                         0 | Check-Out
         |   | Resort Hotel |           0 |       737 |              2015 | July               |                       27 |                       0 |                    0 |      2 |        0 |      0 | BB   | PRT     | Direct         | Direct               | Transient     |   0.00 |                         0 | Check-Out
         |   | Resort Hotel |           0 |         7 |              2015 | July               |                       27 |                       0 |                    1 |      1 |        0 |      0 | BB   | GBR     | Direct         | Direct               | Transient     |  75.00 |                         0 | Check-Out
         |   | Resort Hotel |           0 |        13 |              2015 | July               |                       27 |                       0 |                    1 |      1 |        0 |      0 | BB   | GBR     | Corporate      | Corporate            | Transient     |  75.00 |                         0 | Check-Out
         |   | Resort Hotel |           0 |        14 |              2015 | July               |                       27 |                       0 |                    2 |      2 |        0 |      0 | BB   | GBR     | Online TA      | TA/TO                | Transient     |  98.00 |                         1 | Check-Out
         |   | Resort Hotel |           0 |        14 |              2015 | July               |                       27 |                       0 |                    2 |      2 |        0 |      0 | BB   | GBR     | Online TA      | TA/TO                | Transient     |  98.00 |                         1 | Check-Out
         |   | Resort Hotel |           0 |         0 |              2015 | July               |                       27 |                       0 |                    2 |      2 |        0 |      0 | BB   | PRT     | Direct         | Direct               | Transient     | 107.00 |                         0 | Check-Out
         |   | Resort Hotel |           0 |         9 |              2015 | July               |                       27 |                       0 |                    2 |      2 |        0 |      0 | FB   | PRT     | Direct         | Direct               | Transient     | 103.00 |                         1 | Check-Out
         |   | Resort Hotel |           1 |        85 |              2015 | July               |                       27 |                       0 |                    3 |      2 |        0 |      0 | BB   | PRT     | Online TA      | TA/TO                | Transient     |  82.00 |                         1 | Canceled
         |   | Resort Hotel |           1 |        75 |              2015 | July               |                       27 |                       0 |                    3 |      2 |        0 |      0 | HB   | PRT     | Offline TA/TO  | TA/TO                | Transient     | 105.50 |                         0 | Canceled
+------------+--------------+-------------+-----------+-------------------+--------------------+--------------------------+-------------------------+----------------------+--------+----------+--------+------+---------+----------------+----------------------+---------------+--------+---------------------------+--------------------+
10 rows in set (0.00 sec)
```
---

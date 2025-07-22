# 📈 stock-market-data-pipeline

## Real-Time Stock Market Data Pipeline using Kafka and AWS

This project implements an end-to-end **real-time data pipeline** that ingests stock market data using **Apache Kafka**, stores each record in **Amazon S3** as JSON, processes the data with **AWS Glue**, and enables querying via **Amazon Athena**.

---

## 📌 Pipeline Overview

- **Kafka Producer** reads stock data from a CSV file and sends each row as a message to a Kafka topic.
- **Kafka Consumer** listens to that topic and writes each message as an individual `.json` file to **Amazon S3**.
- **AWS Services** used:
  - **Amazon EC2** – Hosts Kafka and Zookeeper (self-managed).
  - **Amazon S3** – Stores JSON data written by the Kafka consumer.
  - **AWS Glue Crawler** – Scans S3 to catalog the JSON data.
  - **AWS Glue Data Catalog** – Holds metadata/schema inferred from the JSON files.
  - **Amazon Athena** – Queries the data in S3 using the schema from Glue Data Catalog.

---
## 🚀 Running the Pipeline
- Start Kafka & Zookeeper on EC2.
- Run the producer script to publish data from the CSV.
- Run the consumer script to write each record to S3 as a JSON file.
- Set up a Glue Crawler pointing to the S3 bucket to build the catalog.
- Use Athena to run SQL queries on the cataloged data.

---
## 🧱 Architecture
```text
[stock_data.csv]
    ↓
[Kafka Producer (Python)]
    ↓
[Kafka Topic: stock-data]
    ↓
[Kafka Consumer (Python)]
    ↓
[Amazon S3 (raw JSON files)]
    ↓
[AWS Glue Crawler]
    ↓
[AWS Glue Data Catalog]
    ↓
[Amazon Athena (SQL Queries)]


## 🎧 Spotify ETL Pipeline on AWS

A fully automated ETL (Extract, Transform, Load) data pipeline built using Spotify API, Python, and AWS cloud services.

This project demonstrates how to extract real-time music data from Spotify, process it using serverless AWS services, and make it queryable using Amazon Athena.

📌 Project Overview

## This project follows a modern serverless data engineering architecture:

Extract data from Spotify API using Python

Store raw data in Amazon S3

Use AWS Lambda for automated transformations

Trigger workflows using S3 events

Scan schema using AWS Glue

Query transformed data using Amazon Athena

The entire pipeline is automated and scalable.

## 🏗️ Architecture Overview
Data Flow:

Spotify API
⬇
Python Script
⬇
Amazon CloudWatch (Trigger Scheduling)
⬇
AWS Lambda (Extraction)
⬇
Amazon S3 (Raw Data Storage)
⬇
S3 Trigger
⬇
AWS Lambda (Transformation)
⬇
Amazon S3 (Transformed Data)
⬇
AWS Glue Crawler
⬇
Amazon Athena (SQL Queries)

## 🔧 Technologies Used

Python

Spotify Web API

AWS Lambda

Amazon CloudWatch

Amazon S3

AWS Glue

Amazon Athena

IAM (Access Management)

## 🚀 Step-by-Step Pipeline Explanation
### 1️⃣ Data Extraction – Spotify API (Python)

Python is used to connect to the Spotify API.

Authentication is handled using Spotify developer credentials.

Data such as:

Albums

Artists

Tracks

Release dates

Popularity metrics

JSON data is collected.

The script:

Requests data from Spotify

Parses the JSON response

Structures the data

Sends it to AWS Lambda for processing

## 2️⃣ Scheduling with Amazon CloudWatch

Amazon CloudWatch is used to:

Schedule Lambda execution

Automatically trigger data extraction

Run at defined intervals (e.g., daily)

This removes the need for manual execution.

## 3️⃣ AWS Lambda – Extraction Layer

AWS Lambda:

Runs the Python extraction code

Receives Spotify API response

Stores raw JSON data into S3

This is serverless:

No infrastructure management

Auto-scaling

Pay-per-use

## 4️⃣ Amazon S3 – Raw Data Layer

S3 acts as a data lake.

Structure example:

s3://spotify-etl-project/
   raw_data/
       to_processed/
       processed/


Raw JSON files are stored in:

raw_data/to_processed/


This keeps original data unchanged for audit purposes.

## 5️⃣ S3 Trigger – Automatic Transformation

When new raw data is uploaded:

S3 event trigger activates

Transformation Lambda function runs automatically

No manual process required.

## 6️⃣ AWS Lambda – Transformation Layer

This Lambda:

Reads raw JSON

Cleans and normalizes data

Extracts:

Album table

Artist table

Track table

Converts data into structured format (CSV/Parquet)

Outputs transformed data to:

transformed_data/

## 7️⃣ Amazon S3 – Transformed Data Layer

This layer contains:

Cleaned data

Structured tables

Analytics-ready datasets

This follows a simple Data Lake architecture:

Raw layer

Processed layer

Analytics layer

## 8️⃣ AWS Glue – Schema Detection

AWS Glue Crawler:

Scans transformed S3 data

Detects schema automatically

Creates metadata tables

Registers tables inside AWS Glue Data Catalog

No manual schema definition required.

## 9️⃣ Amazon Athena – Query Layer

Amazon Athena allows:

SQL querying directly on S3

No database setup required

Serverless analytics

Example Query:

SELECT artist_name, COUNT(track_id)
FROM spotify_tracks
GROUP BY artist_name
ORDER BY COUNT(track_id) DESC;


Athena uses Glue Data Catalog metadata to query data.

📂 Project Structure
spotify-etl-project/
│
├── lambda_extract.py
├── lambda_transform.py
├── README.md
├── requirements.txt
└── architecture-diagram.png

🔐 IAM & Security

IAM roles created for:

Lambda execution

S3 access

Glue access

Least privilege principle applied.

Spotify credentials stored securely.

## 💡 Key Learning Outcomes

This project demonstrates:

Building serverless ETL pipelines

Working with REST APIs

JSON data parsing

Event-driven architecture

Data Lake design

AWS Glue metadata management

SQL querying with Athena

## 📈 Why This Project Matters

This project shows practical experience in:

Cloud Data Engineering

Automated Data Pipelines

AWS Serverless Architecture

Data Transformation Workflows

Production-ready ETL design

It reflects real-world data engineering workflow used in modern analytics teams.

## 🧠 Future Improvements

Add Parquet format for cost-efficient querying

Implement partitioning in S3

Add Step Functions for orchestration

Build dashboard using Power BI or QuickSight

Add CI/CD pipeline for deployment

## 📊 Conclusion

This Spotify ETL pipeline demonstrates how to:

✔ Extract real-time API data
✔ Automate cloud workflows
✔ Transform and structure datasets
✔ Query data using SQL
✔ Build scalable, serverless data architecture

# Airflow-for-Retail-Analysis

## Project Overview
This project demonstrates an end-to-end data pipeline for analyzing retail data using Airflow, Snowflake, dbt, and Metabase. It ingests data from a CSV file, stores it in Snowflake, transforms it using dbt models, and creates dashboards in Metabase for visualization and analysis.

![Alt text](airflow_bigquery_dbt_pipeline.png?raw=true "Title")

## Project Components

Airflow: Orchestrates the data pipeline workflow and schedules tasks.
BigQuery: Cloud-based data warehouse for storing and querying retail data.
dbt: Transforms raw data into dimensional and fact tables for analysis.
Soda: Performs data quality checks on raw and transformed data.
Astro SDK: Facilitates interactions with Google Cloud Storage and BigQuery (in earlier stages of the project).
Metabase: Provides interactive dashboards for data exploration and reporting.

## Workflow

1) Start of the workflow: The DAG starts with a task that triggers the entire pipeline. This task can be a manual trigger, a scheduled trigger, or an external dependency.

2) Data Ingestion: The next task in the DAG is responsible for ingesting data from the CSV file. This task uses the LocalFilesystemToGCSOperator operator to load the data into Google Cloud Storage (GCS) Bucket.

3) Data Storage: Once the data is in GCS, the DAG uses the BigQueryCreateEmptyDatasetOperator operator to create empty Bigquery table and then convert the csv to Bigquery format using load file.

4) Data Transformation: After the data is in BigQuery, the DAG uses the DbtTaskGroup operator to run dbt models and transform the data into dimensional and fact tables.

5) Data Quality: After each trasnformation, the Airflow uses the SodaCheckOperator operator to perform data quality checks on both the raw and transformed data.

6) Data Visualization: Finally, the DAG uses the Metabase to create dashboards in Metabase for visualizing and analyzing the data.

7) End of the workflow: The DAG ends with a task that signals the completion of the pipeline. This task can be used to trigger downstream workflows or send notifications.

## Benefits of using Airflow DAG

•Orchestration: Airflow DAG provides a central location to define and manage the entire data pipeline workflow.
•Scheduling: Tasks in the DAG can be scheduled to run at specific intervals or based on dependencies.
•Monitoring: Airflow provides a web interface to monitor the progress of the pipeline and identify any errors or failures.
•Scalability: The DAG can be easily scaled to accommodate increasing data volumes.

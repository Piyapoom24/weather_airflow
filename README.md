# Hourly Weather & Air Quality Data Pipeline with Airflow

An automated hourly data pipeline that ingests real-time weather and air quality data for Nan Province, Thailand using Apache Airflow on Google Cloud Composer, stores raw data in Google Cloud Storage, and loads processed data into BigQuery for dashboard visualization.

---
 
## Architecture
><img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/de91bf36-0e7a-4ddf-bbce-02b55957971c" />

| Layer | Tool |
|---|---|
| Orchestration | Apache Airflow (Cloud Composer) |
| Data Source | Open-Meteo API (Free, no API key required) |
| Data Lake | Google Cloud Storage (GCS) |
| Data Transformation | Python, Pandas |
| Data Warehouse | BigQuery |
| Dashboard | Looker Studio |
 
---
 
## Tech Stack
- Apache Airflow
- Google Cloud Platform (GCS, Composer, BigQuery)
- Python
- Pandas

---

## Pipeline Overview
 
The pipeline runs automatically **every hour** via Airflow scheduler and consists of 5 tasks:

><img width="678" height="118" alt="image" src="https://github.com/user-attachments/assets/42ae5a1a-5eb6-408b-8123-ed903f52514c" /><img width="899" height="383" alt="image" src="https://github.com/user-attachments/assets/875afbd8-9adc-43c1-bbfb-7ec274756633" />

| Task | Description |
|---|---|
| `get_weather_data` | Fetches current temperature, humidity, apparent temperature, and rainfall from Open-Meteo API |
| `get_PM25_data` | Fetches current US AQI from Open-Meteo Air Quality API |
| `data2gcs` | Saves raw JSON response to Google Cloud Storage as Data Lake |
| `transform_data` | Transforms and formats data including timestamp conversion to Asia/Bangkok timezone |
| `load_data_to_bq` | Appends processed data into BigQuery table every hour |

---

## Preview Data (BigQuery)
**Schema**
><img width="538" height="310" alt="image" src="https://github.com/user-attachments/assets/1f479f5a-82b1-441c-bf86-6574cb8bf9f4" />

**Data**
><img width="1189" height="518" alt="image" src="https://github.com/user-attachments/assets/601836d9-2c97-4975-9e72-4b361275b934" />


 
## Dashboard

Click --> [Dashboard](https://lookerstudio.google.com/embed/u/0/reporting/8666d841-a087-4c5c-8ced-ead8f36f7f9c/page/3V6tF)
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/c1553ca4-ba63-4886-ab3f-22d76adff6fe" />

---

## What I Learned
 
- Building an end-to-end data pipeline using **Apache Airflow** with the TaskFlow API (`@dag`, `@task`)
- Handling API data ingestion, JSON transformation, and timezone conversion with **Pandas**
- Using **Cloud Composer** to orchestrate and schedule production-grade pipelines
- Loading data into **BigQuery** with append strategy using Python BigQuery Client
- Connecting **BigQuery to Looker Studio** for real-time dashboard visualization
 







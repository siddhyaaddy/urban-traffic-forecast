# urban-traffic-forecast

A full end-to-end ML pipeline project using the NYC Yellow Taxi trip data (2023–2024) built with AWS services. This pipeline ingests, processes, models, and visualizes taxi demand predictions using LightGBM models and a real-time dashboard powered by Streamlit.

---

## 📦 Project Overview

This project builds a **cloud-based machine learning pipeline** for forecasting hourly taxi demand across NYC using AWS Lambda, Glue, Athena, RDS, and Streamlit. The project includes:

- Raw data ingestion from the NYC Taxi data repo (2023 & 2024)
- ETL using AWS Glue
- Predictive modeling using LightGBM
- Prediction storage and querying via S3, Athena, and RDS
- A live Streamlit dashboard deployed on AWS Elastic Beanstalk

---

## 🔁 Pipeline Architecture

```plaintext
S3 (raw) ──▶ Lambda (triggered) 
           └──▶ Glue Job (filter + transform)
                         └──▶ S3 (filtered, transformed)
                                       └──▶ Glue Crawler + Athena Table
                                                       └──▶ LightGBM Modeling
                                                                   └──▶ Predictions to S3 + RDS
                                                                                   └──▶ Streamlit Dashboard



```

## 📁 taxi-pipeline-forecast/

├── lambda/
│   ├── download_data.py
│   └── trigger_glue.py
├── glue/
│   ├── filter_transform_job.py
│   └── create_crawler.py
├── modeling/
│   ├── model_1_lag_features.py
│   ├── model_2_feature_selection.py
│   └── batch_inference.py
├── rds/
│   ├── postgres_uploader.py
│   └── schema.sql
├── streamlit_app/
│   ├── app.py
│   └── dashboard_utils.py
├── utils/
│   └── athena_queries.py
├── README.md
---
```

```
📁 S3 Folder Structure

s3://<bucket_name>/taxi/
│
├── raw/year=<YYYY>/month=<MM>/
├── filtered/year=<YYYY>/month=<MM>/
├── transformed/year=<YYYY>/month=<MM>/
└── predictions/model=<model_id>/location_id=<ID>/year=<YYYY>/month=<MM>/day=<DD>/hour=<HH>/
---

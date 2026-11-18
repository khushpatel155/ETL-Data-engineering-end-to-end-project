# End-to-End E-Commerce Analytics Data Platform

An end-to-end data engineering portfolio project built around the public [Brazilian E-Commerce dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce). The platform will ingest the source CSVs, validate and transform them into analytics-ready models, orchestrate repeatable runs, and serve business metrics in a dashboard.

## Project brief

**Business question:** How do sales, delivery performance, customer reviews, and product categories change over time, and where are the main operational bottlenecks?

**Users:** Business and operations analysts who need trusted order, revenue, customer, and delivery metrics.

**Data:** Olist's public, anonymized Brazilian marketplace data, covering roughly 100,000 orders from 2016–2018. The dataset is distributed as CSV files; it is historical data, so this project demonstrates batch analytics rather than real-time operations.

## Planned architecture

```text
Olist CSV files
      │
      ▼
Python ingestion ──► PostgreSQL raw schema
                           │
                           ▼
                     dbt transformations
                staging → intermediate → marts
                           │
               dbt tests and documentation
                           │
                           ▼
                    Analytics dashboard

Airflow orchestrates ingestion, transformation, and quality checks.
Docker Compose runs the local services; GitHub Actions checks code changes.
```

## Planned analytics

- Orders, gross payment value, and average order value over time
- Sales by product category, seller region, and payment type
- On-time delivery rate and delivery duration
- Review scores alongside delivery performance
- Customer repeat-order behavior, with customer identity caveats documented

Metric definitions and grain will be documented in the dbt marts. Payment value will be clearly distinguished from recognized revenue because the source does not provide accounting or refund data sufficient to establish revenue.

## Build plan

1. **Project foundation (current):** define the use case, source, scope, architecture, and milestones.
2. **Data setup:** download the Olist CSV archive, inspect the files and schemas, and keep source data out of Git.
3. **Ingestion:** implement a configurable Python loader into PostgreSQL raw tables, with logging and safe reruns.
4. **Transformation:** add dbt staging, intermediate, and analytics models plus schema and relationship tests.
5. **Orchestration:** create an Airflow DAG with dependencies, retries, and clear failure behavior.
6. **Analytics:** connect a dashboard tool to the marts and publish a few focused business views.
7. **Delivery polish:** Docker Compose, CI checks, architecture/data-model documentation, screenshots, and an accurate resume bullet.

## Definition of done

A reviewer can follow the setup guide, run the pipeline from the raw Olist files through tested analytics tables, and inspect the resulting dashboard. The repository explains how to configure the services, where to obtain the dataset, how to run each component, and what each published metric means.

## Source and access

The dataset is available on [Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce). Kaggle may require an account and acceptance of its dataset terms. The archive is not committed to this repository; later setup steps will document the expected local data path and an ignore rule.

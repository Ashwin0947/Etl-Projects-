# Etl-Projects-
name: Snowflake ETL Deployment
on:
push:
branches:
- main
workflow_dispatch:
jobs:
deploy:
runs-on: ubuntu-latest
steps:
- name: Checkout code
uses: actions/checkout@v3
1.3
- name: Install SnowSQL CLI
run: |
pip install snowflake-cli-labs
- name: Deploy Snowflake SQL Scripts
run: |
snowsql -a ${{ secrets.SNOWFLAKE_ACCOUNT }} \
-u ${{ secrets.SNOWFLAKE_USER }} \
-p ${{ secrets.SNOWFLAKE_PASSWORD }} \
-d ${{ secrets.SNOWFLAKE_DB }} \
-s ${{ secrets.SNOWFLAKE_SCHEMA }} \
-w ${{ secrets.SNOWFLAKE_WH }} \
-f ./sql/deploy_pipeline.sql
Add the following GitHub repo secrets:
SNOWFLAKE_ACCOUNT
SNOWFLAKE_USER
SNOWFLAKE_PASSWORD
SNOWFLAKE_DB , SCHEMA , WH
📎 Project Structure
├── sqlserver-kafka-snowflake-etl
│ ├── sql
│ │ └── deploy_pipeline.sql
│ ├── spark
│ │ └── etl_spark_job.py
│ └── README.md
│
├── teradata-hadoop-etl
│ ├── data
│ │ └── orders.csv
│ ├── spark
│ │ └── etl_teradata_to_hadoop.py
│ └── README.md
│
└── .github
└── workflows
└── etl_pipeline.yml

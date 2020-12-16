---
title: "[SQL] Kaggle Course - SQL"
date: 2020-12-08 22:13:13
categories:
- [Note, SQL]
tags:
- Kaggle
- SQL
- BigQuery
---

Learn SQL by using Google BigQuery

<!-- more -->

---

BigQuery是Google提供一個無需伺服器的資料倉儲與分析服務系統，以SQL查詢資料。

# 1. 事前準備

【建立Google Cloud專案】

[Go to the project selector page](https://console.cloud.google.com/projectselector2/home/dashboard?_ga=2.181894574.847070024.1607437297-688873900.1607437297&_gac=1.91197544.1607438686.Cj0KCQiA5bz-BRD-ARIsABjT4ngzMSMkc9Akyr7tYV7Ur0d0H4HqeveucJybK1swRhZ5yJ2uZCohYawaApHvEALw_wcB)

【啟用BigQuery API】

[Enable the API](https://console.cloud.google.com/flows/enableapi?apiid=bigquery&_ga=2.177659564.847070024.1607437297-688873900.1607437297&_gac=1.192852184.1607438686.Cj0KCQiA5bz-BRD-ARIsABjT4ngzMSMkc9Akyr7tYV7Ur0d0H4HqeveucJybK1swRhZ5yJ2uZCohYawaApHvEALw_wcB)

【設定憑證】

[Go to the Create Service Account Key page](https://console.cloud.google.com/apis/credentials/serviceaccountkey?_ga=2.172948010.847070024.1607437297-688873900.1607437297&_gac=1.81295845.1607438686.Cj0KCQiA5bz-BRD-ARIsABjT4ngzMSMkc9Akyr7tYV7Ur0d0H4HqeveucJybK1swRhZ5yJ2uZCohYawaApHvEALw_wcB)

New a service account - Enter service account name
Select role list - Choose JSON format

【載入金鑰】
```python
import os
os.environ[“GOOGLE_APPLICATION_CREDENTIALS”] = "Project_name-Prject_number.json"
```

# 2. 使用BigQuery

`Client` hold projects and a connection to the Big Query service.

```python
# Import Python package
from google.cloud import bigquery
# Create a "Client" object
client = bigquery.Client()
```

Fetch the dataset
```python
# Construct a reference to the dataset
dataset_ref = client.dataset("dataset_name", project="bigquery-public-data")
# API request - fetch the dataset
dataset = client.get_dataset(dataset_ref)
```

List all the tables
```python
# List all the tables in the dataset
tables = list(client.list_tables(dataset))
# Print names of all tables in the dataset
for table in tables:  
    print(table.table_id)
```

Fetch the table
```python
# Construct a reference to the table
table_ref = dataset_ref.table("table name")
# API request - fetch the table
table = client.get_table(table_ref)
```

# 3. Table Schema

Structure of a table, includes:

- The `name` of the column
- The `datatype` in the column
- The `mode` of the column
- A `description` of the data in that column

```python
# Print information
table.schema
```

use `list_rows()` returns a BigQuery `RowIterator` object
```python
# Preview the first five entries in the "by" column of the "full" table
client.list_rows(table, selected_fields=table.schema[:1], max_results=5).to_dataframe()
```

# 4. SQL clauses

## Select, From & Where

```sql
query = """
		SELECT col_name 
		FROM `project.dataset.table` 
		WHERE condition / WHERE col_name LIKE 'text(%term%)'
		"""
```
```python
# Set up the query
query_job = client.query(query)
# API request - run the query, and return a pandas DataFrame
query_result = query_job.to_dataframe()
```

`QueryJobConfig` to estimate the size of any query.
- `dry_run` parameter for without running query.
- `maximum_bytes_billed` parameter for limit the query.

```python
# Create a QueryJobConfig object to estimate size of query without running it
dry_run_config = bigquery.QueryJobConfig(dry_run=True)
# API request - dry run query to estimate costs
dry_run_query_job = client.query(query, job_config=dry_run_config)
print("This query will process {} bytes.".format(dry_run_query_job.total_bytes_processed))

# Only run the query if it's less than 1 MB
ONE_MB = 1000*1000
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=ONE_MB)
# Set up the query (will only run if it's less than 1 MB)
safe_query_job = client.query(query, job_config=safe_config)
# API request - try to run the query, and return a pandas DataFrame
safe_query_job.to_dataframe()
```

## Group By, Having & Count

```sql
query = """
		SELECT col_name, COUNT(col_id) AS alias_name
		FROM `project.dataset.table` 
		GROUP BY col_name
		HAVING criteria
		"""
```
> If using any `GROUP BY` clause, all the variables must be passed to a `GROUP BY` command or an aggregation function.


## Order By

[Date and time functions](https://cloud.google.com/bigquery/docs/reference/legacy-sql#datetimefunctions)
```sql
# Query to find out the number of accidents for each day of the week
query = """
        SELECT COUNT(col_num) AS num_aname, 
               EXTRACT(DAY FROM col_date) AS day_aname
        FROM `project.dataset.table`
        GROUP BY day_aname
        ORDER BY num_aname DESC
        """
```

## As & With

Common Table Expression (CTE) : A temporary table for splitting your queries into readable chunks.
```sql
query = """
		WITH tmp_table AS
		(
			SELECT col_name
			FROM 'project.database.table'
			WHERE criteria
		)
		SELECT col_name
		FROM tmp_table
		"""
```

## Joining Data

```sql
query = """
		SELECT p.Name AS Parent_Name, c.Name AS Child_Name
		FROM `project.dataset.table_P` AS p
		INNER JOIN `project.dataset.table_C` AS c
			  ON p.c_ID = c.ID
		"""
```


# 參考資料

[Kaggle Course - SQL](https://www.kaggle.com/learn/intro-to-sql)

[Google Cloud BigQuery](https://cloud.google.com/bigquery)

[GCPUG - BigQuery 簡介](https://gcpug-tw.gitbook.io/google-cloud-platform-in-practice/google-cloud-shang-de-da-zi-liao-chu-li-fu-wu/bigquery/bigquery-jian-jie)
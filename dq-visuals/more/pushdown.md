---
description: Pushdown feature description
---

# Pushdown

Some of the DQ features support pushdown to avoid transferring large dataset from data source (Database, Cloud storage, file systems etc.) into Spark. When pushdown is enabled and supported, the DQ Job will generate SQL queries to offload the compute to the data source, reducing the amount of data transfer and Spark computation of the DQ Job. Not all features support pushdown nor pushdown completely eliminate data transfer.

## Why use pushdown

To analyze a dataset for DQ findings as part of a DQ Job, CDQ uses Spark as the compute engine to power the analysis. This requires the dataset to be loaded into Spark as a Spark DataFrame, and the DQ Job performance (job completion speed) is limited by Spark resources available and the complexity of the job. This data transfer from data source to Spark is dependent on two of the following factors:

1. Bandwidth limitation at the data source\
   If the DQ Job requires pulling 100 million rows from a SQL Database, then the Input/Output limit of transferring data out of SQL Database into the Spark cluster will greatly increase the overall speed of the DQ Job.&#x20;
2. Compute limitation at the data source for complex queries\
   If the DQ Job requires complex queries to create the dataset (via `-q`), then this computation is done at the SQL Database level. Some examples of "complex" queries are:\
   \
   `-q "SELECT * FROM public.very_long_table_of_transactions WHERE date = ${rd} and department = 'finance'"`\
   This query can take long time at the database level due to `WHERE` clause filtering a very long table on columns `date` and `department` that may not be indexed properly, leading to a full table scan without a `LIMIT` clause specified.\
   \
   `-q "SELECT * FROM public.very_long_table_of_transactions transactions INNER JOIN public.departments departments ON transactions.department_id = departiments.id WHERE transactions.date = ${rd} and departments.name = 'finance'"`\
   This query can take long time at the database level due to a join between tables.
3. Resource limitation at the data source\
   The data source may not have enough hardware resource available to efficiently fulfill the query and/or handle multiple DQ Jobs & other non-CDQ applications requesting data.

The bottleneck due to data transfer can be viewed in Jobs page > Job Logs > LOAD stage. This data loading step is the first step for all DQ Jobs. However, pushdown feature can be used to _reduce_ (NOT eliminate) the data transfer & compute to Spark from the data source, if the DQ Job specified does not require loading all the data into Spark. \
\
In summary, speed of loading the data from data source to Spark is a `-q query compute time at data source`  + `network transfer of -q result between data source and Spark`. Pushdown can reduce both elements, but the efficiency gained is dependent on the complexity of `-q` query and how big the dataset from `-q`result would have been without pushdown.

## How pushdown is efficient

Some of the Spark compute performed by the DQ Job can be translated into SQL queries that most relational databases support natively. In such a case, the DQ Job does not need to load all the rows of the dataset. Instead, the DQ Job can query the data source for the results of those SQL queries and reduce the amount of data transferring out of the data source. The results of these SQL queries are almost always lead to smaller amount of data compared to the full dataset defined by `-q`. Only some of the DQ Job features require the full dataset to be loaded into Spark. Therefore, pushdown can be a useful tool to speed up the overall DQ Job speed -- **provided that the speed of executing these SQL queries are faster than the speed of transferring the data out of the data source into Spark**. In most use cases, pushdown leads to faster DQ Job execution for large datasets. If the `-q` query is sufficiently complex, then the speed reduced by transferring less data into Spark can be cancelled out by the multiple frequent SQL queries made to the data source by the Pushdown process (because each query may have have redundant compute due to the complexity of `-q`)

## How pushdown works in CDQ

Using pushdown only _reduces_ the amount of data transferred out of the data source. It does NOT skip the LOAD stage in DQ Job. Every DQ Job requires a small sample of rows (10-20) of the dataset defined by `-q`  in order to generate Data Preview and analyze schema information for the dataset run. This means the `-q` query may be fully computed at data source before the sampling can occur (depending on the complexity of the `-q`). In such a case, sampling 10-20 rows of data is not a quick and immediate LOAD stage and only efficiency gain comes from lack of transferring data between data source and Spark. \
\
Therefore, pushdown feature would be most efficient if `-q` is a simple select query with simple where filtering. The benefit comes from the fact that if your dataset defined by `-q` results in 100 million rows, only 10-20 rows of the dataset defined by `-q` will be loaded into Spark.

Profile with pushdown will then generate a series of SQL queries and query the data source again for aggregate metric data. Depending on the dataset, these multiple SQL queries can be more efficient than loading all the data into Spark and computing these aggregate metric in Spark. The results between _Profile with pushdown_ and _Profile without pushdown_ are (practically) identical.

## Profile: pushdown vs no pushdown

Here is the summary of Profile activity with details regarding pushdown support

| Feature              | Supports pushdown | Description                                                                                                                                                                                                                                                                                                                   |
| -------------------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Row Count            | Yes               | Computes row count of the dataset.                                                                                                                                                                                                                                                                                            |
| Distinct Count       | Yes               | The number of distinct values in a column                                                                                                                                                                                                                                                                                     |
| Mean                 | Yes               | The average of all the values in the column. Supports numeric columns only.                                                                                                                                                                                                                                                   |
| Min / Max            | Yes               | The minimum and maximum values of the column. Supports numeric and boolean columns only                                                                                                                                                                                                                                       |
| NULL Count           | Yes               | The number of null values in the column.                                                                                                                                                                                                                                                                                      |
| EMPTY Count          | Yes               | The number of empty values in the column. Supports string columns only.                                                                                                                                                                                                                                                       |
| TYPE Count           | Yes               | The number of different types inferred in a column (if any)                                                                                                                                                                                                                                                                   |
| TopN / BottomN       | No                | <p>Computes the top 5 most frequent (TopN) and least frequent (BottomN) values. Supports all types. <br><br>This result is displayed as a frequency bar chart in Profile page. If pushdown is enabled, then TopN and BottomN values are not displayed. Related features like Stat Rules (Distribution) are also disabled.</p> |
| Data Shape Detection | No                | Detects shapes of the values based on Shape parameters provided (automatic or manual).                                                                                                                                                                                                                                        |
| Histogram            | No                | Creates histogram of the values in the column.                                                                                                                                                                                                                                                                                |
| Correlation Matrix   | No                | Creates correlation matrix. Supports only numeric columns                                                                                                                                                                                                                                                                     |


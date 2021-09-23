---
description: A list of supported data source connection types.
---

# Supported Drivers

The following is a list of drivers certified for production use.

| Connection Type | Driver | Certification | Grade | Reason |
| :--- | :--- | :--- | :--- | :--- |
| Teradata | Native | Production | B+ |  |
| Oracle | Native | Production | A- | Performance based on how the DB is configured and fetch size in driver. |
| MS SQL Server | Native | Production | A- | allows whitespace in column headers |
| Snowflake | Native | Production | A+ | easy to use and performs well |
| S3 | S3 SDK in Web / S3a connector in Core | Production | A | Supports bucket keys, IAM roles and caching |
| Hive | Simba JDBC | Production | B+ | Too many variations of Tez, mapReduce and other nuances that make it difficult to get started. |
| Impala | Simba JDBC | Production | A- | Tends to be a quicker start than Hive but still has many config nuances |
| Postgres | Native | Production | A+ | easy to use performs well |
| MySql | Native | Production | A+ | easy to use performs well |
| Kafka | Native | Production | B+ | Most cases the group doesn't know enough about kafka administration, schema registry and other nuances. |
| DB2 | Native | Production | A- | easy to use performs well, fetch syntax vs limit and other nuances |
| GreenPlum | Postgres | Production | A- |  |
| HDFS | HDFS connector | Production | B | works well but usually a few hadoop spark nuances to get right |

The following is a list of drivers which are for test purposes \(not certified yet for production usage\).

| Connection Type | Driver | Certification |
| :--- | :--- | :--- |
| MongoDB | unityJDBC | Preview |
| MapR Hive | MapR Hive Driver | Preview |
| Redshift | Simba JDBC | Preview |
| Athena | Simba JDBC | Preview |
| Presto | Simba JDBC | Preview |
| BigQuery | Simba JDBC for Web / Bigquery Spark Connector in Core | Preview |
| GCS \(Google Cloud Storage\) | Google Cloud SDK for Web / GCS Spark Connector in Core | Preview |
| Azure Cloud Storage \(ADLSv2\) | Azure SDK for Web / Azure Data Explorer connector for Spark in Core \(Authtypes are Key or Service-Prinicipal\) | Preview |
| Solr | Solr JDBC | Preview |
| Phoenix | Native | Preview |
| Cassandra | Native | Preview |
| MS SQL Data Warehouse | Native | Preview |
| Delta Lake | Native | Preview |
| SAP HANA | Native | Preview |
| MariaDB | MySQL Driver | Preview |
| Dremio | Dremio JDBC | Preview |

| File Type Support | Grade | Reason |
| :--- | :--- | :--- |
| Parquet | B+ | schema in file, less common but works well |
| CSV \(and all delimiters\) | A+ | very common easy to use |
| JSON | A- | works great depends how many levels nested |
| XML | B | recommend json |
| AVRO | B |  |


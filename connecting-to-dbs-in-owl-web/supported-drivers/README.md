---
description: A list of supported data source connection types.
---

# Supported Connections

## Production

The following is a list of drivers certified for production use.

| Connection Type   | Driver                                | Certification | Grade | Auth Type                                   | Comments                                                                                       |
| ----------------- | ------------------------------------- | ------------- | ----- | ------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Teradata**      | Native                                | Production    | B+    | User / Pass                                 | Some sql nuances, fairly easy to use and performs well                                         |
| **Oracle**        | Native                                | Production    | A-    | User / Pass                                 | Performance based on how the DB is configured and fetch size in driver.                        |
| **MS SQL Server** | Native                                | Production    | A-    | User / Pass                                 | allows whitespace in column headers                                                            |
| **Snowflake**     | Native                                | Production    | A+    | User / Pass                                 | easy to use and performs well                                                                  |
| **S3**            | S3 SDK in Web / S3a connector in Core | Production    | A     | Secret / Key, Instance Profile, Assume Role | Supports bucket keys, IAM roles and caching                                                    |
| **Hive**          | Simba JDBC                            | Production    | B+    | User / Pass, Kerberos                       | Too many variations of Tez, mapReduce and other nuances that make it difficult to get started. |
| **Impala**        | Simba JDBC                            | Production    | A-    | User / Pass                                 | Tends to be a quicker start than Hive but still has many config nuances                        |
| **Postgres**      | Native                                | Production    | A+    | User / Pass                                 | easy to use performs well                                                                      |
| **MySql**         | Native                                | Production    | A+    | User / Pass                                 | easy to use performs well                                                                      |
| **DB2**           | Native                                | Production    | A-    | User / Pass, Kerberos                       | easy to use performs well, fetch syntax vs limit and other nuances                             |
| **GreenPlum**     | Postgres                              | Production    | A-    | User / Pass                                 | easy to use performs well                                                                      |
| **Redshift**      | Simba JDBC                            | Production    | B+    |                                             |                                                                                                |
| **Athena**        | Simba JDBC                            | Production    | B+    |                                             |                                                                                                |
| **HDFS**          | HDFS connector                        | Production    | B     | Kerberos                                    | works well but usually a few hadoop spark nuances to get right                                 |

## Preview

The following is a list of drivers which are for test purposes (not certified yet for production usage).

| Connection Type                  | Driver                                                                            | Certification | Grade | Auth Type               | Comments                                                                                                                      |
| -------------------------------- | --------------------------------------------------------------------------------- | ------------- | ----- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **MongoDB**                      | unityJDBC                                                                         | Preview       | B     | User / Pass             | Depends which driver you use to turn a document store into a relational view.                                                 |
| **MapR Hive**                    | MapR Hive Driver                                                                  | Preview       | C+    | User / Pass             | End of Life                                                                                                                   |
| **Presto**                       | Simba JDBC                                                                        | Preview       | B+    | User / Pass             |                                                                                                                               |
| **BigQuery**                     | <p>Simba JDBC  (Web) </p><p>Spark Connector (Core)</p>                            | Preview       | B+    | JSON service account    | Requires 20 jars as compared to 1 jar and accepts pushdown but has nuances. Views are not supported. Joins are not supported. |
| **GCS (Google Cloud Storage)**   | <p>Google Cloud SDK for Web / </p><p>GCS Spark Connector in Core</p>              | Preview       | B     | JSON service account    | more config than usual                                                                                                        |
| **Azure Cloud Storage (ADLSv2)** | <p>Azure SDK for Web / </p><p>Azure Data Explorer connector for Spark in Core</p> | Preview       | B-    | Key / Service Principal | more config than avg                                                                                                          |
| **Solr**                         | Solr JDBC                                                                         | Preview       | B-    | User / Pass             | not a relational store so requires some understanding of Solr                                                                 |
| **Phoenix**                      | Native                                                                            | Preview       | C+    |                         | requires knowledge of phoenix and hbase                                                                                       |
| **Cassandra**                    | Native                                                                            | Preview       | C+    | User / Pass             | CQL vs SQL and other nuances                                                                                                  |
| **MS SQL Data Warehouse**        | Native                                                                            | Preview       | B+    | User / Pass             |                                                                                                                               |
| **Delta Lake**                   | Native                                                                            | Preview       | B-    | User / Pass             | Requires knowledge of databricks                                                                                              |
| **SAP HANA**                     | Native                                                                            | Preview       | B+    | User / Pass             | works with most common data types                                                                                             |
| **MariaDB**                      | MySQL Driver                                                                      | Preview       | B+    | User / Pass             | Uses mysql driver, some nuances                                                                                               |
| **Dremio**                       | Dremio JDBC                                                                       | Preview       | B     | User / Pass             |                                                                                                                               |
| **Kafka**                        | Native                                                                            | Preview       | B-    |                         | Most cases the group doesn't know enough about kafka administration, schema registry and other nuances.                       |
| **Sybase**                       | Native                                                                            | Preview       | B+    |                         |                                                                                                                               |

## Files

| File Type Support            | Grade | Comments                                   |
| ---------------------------- | ----- | ------------------------------------------ |
| **Parquet**                  | B+    | schema in file, less common but works well |
| **CSV** (and all delimiters) | A+    | very common easy to use                    |
| **JSON**                     | A-    | works great depends how many levels nested |
| **XML**                      | B     | recommend json                             |
| **AVRO**                     | B     |                                            |

### **File Limitations**

**File Sizes**

* Files with more than 250 columns supported in File Explorer, unless you have Livy enabled.
* Files larger than 5gb are not supported in File Explorer, unless you have Livy enabled.&#x20;
* Smaller file sizes will allow for skip scanning and more efficient processing
* Advanced features like replay, scheduling, and historical lookbacks require a date signature in the folder of file path

**S3**

* Please ensure no spaces in S3 connection name
* Please remember to select 'Save Credentials' checkbox upon establishing connection
* Please point to **root** bucket, not sub folders

**Local Files**

* Local files can only be run using NO\_AGENT default
* This is for quick testing, smaller files, and demonstration purposes.&#x20;
* Local file scanning is not intended for large scale production use.

#### Spark Engine Support

* MapR is EOL and MapR spark engine not supported to run CDQ jobs.

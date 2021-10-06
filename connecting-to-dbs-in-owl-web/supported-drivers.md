---
description: A list of supported data source connection types.
---

# Supported Drivers

The following is a list of drivers certified for production use.

| Connection Type | Driver | Certification | Grade | Auth Type | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Teradata** | Native | Production | B+ | User / Pass | Some sql nuances, fairly easy to use and performs well |
| **Oracle** | Native | Production | A- | User / Pass | Performance based on how the DB is configured and fetch size in driver. |
| **MS SQL Server** | Native | Production | A- | User / Pass | allows whitespace in column headers |
| **Snowflake** | Native | Production | A+ | User / Pass | easy to use and performs well |
| **S3** | S3 SDK in Web / S3a connector in Core | Production | A | Secret / Key, Instance Profile, Assume Role | Supports bucket keys, IAM roles and caching |
| **Hive** | Simba JDBC | Production | B+ | User / Pass, Kerberos | Too many variations of Tez, mapReduce and other nuances that make it difficult to get started. |
| **Impala** | Simba JDBC | Production | A- | User / Pass | Tends to be a quicker start than Hive but still has many config nuances |
| **Postgres** | Native | Production | A+ | User / Pass | easy to use performs well |
| **MySql** | Native | Production | A+ | User / Pass | easy to use performs well |
| **Kafka** | Native | Production | B+ |  | Most cases the group doesn't know enough about kafka administration, schema registry and other nuances. |
| **DB2** | Native | Production | A- | User / Pass, Kerberos | easy to use performs well, fetch syntax vs limit and other nuances |
| **GreenPlum** | Postgres | Production | A- | User / Pass | easy to use performs well |
| **HDFS** | HDFS connector | Production | B | Kerberos | works well but usually a few hadoop spark nuances to get right |

The following is a list of drivers which are for test purposes \(not certified yet for production usage\).

<table>
  <thead>
    <tr>
      <th style="text-align:left">Connection Type</th>
      <th style="text-align:left">Driver</th>
      <th style="text-align:left">Certification</th>
      <th style="text-align:left">Grade</th>
      <th style="text-align:left">Auth Type</th>
      <th style="text-align:left">Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>MongoDB</b>
      </td>
      <td style="text-align:left">unityJDBC</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left">Depends which driver you use to turn a document store into a relational
        view.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>MapR Hive</b>
      </td>
      <td style="text-align:left">MapR Hive Driver</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">C+</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left">End of Life</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Redshift</b>
      </td>
      <td style="text-align:left">Simba JDBC</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B+</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left">A few unsupported data types</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Athena</b>
      </td>
      <td style="text-align:left">Simba JDBC</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B+</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left">A few unsupported data types</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Presto</b>
      </td>
      <td style="text-align:left">Simba JDBC</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B+</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>BigQuery</b>
      </td>
      <td style="text-align:left">
        <p>Simba JDBC (Web)</p>
        <p>Spark Connector (Core)</p>
      </td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B+</td>
      <td style="text-align:left">JSON service account</td>
      <td style="text-align:left">Requires 20 jars as compared to 1 jar and accepts pushdown but has nuances.
        Views are not supported.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>GCS (Google Cloud Storage)</b>
      </td>
      <td style="text-align:left">
        <p>Google Cloud SDK for Web /</p>
        <p>GCS Spark Connector in Core</p>
      </td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B</td>
      <td style="text-align:left">JSON service account</td>
      <td style="text-align:left">more config than usual</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Azure Cloud Storage (ADLSv2)</b>
      </td>
      <td style="text-align:left">
        <p>Azure SDK for Web /</p>
        <p>Azure Data Explorer connector for Spark in Core</p>
      </td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B-</td>
      <td style="text-align:left">Key / Service Principal</td>
      <td style="text-align:left">more config than avg</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Solr</b>
      </td>
      <td style="text-align:left">Solr JDBC</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B-</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left">not a relational store so requires some understanding of Solr</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Phoenix</b>
      </td>
      <td style="text-align:left">Native</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">C+</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">requires knowledge of phoenix and hbase</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Cassandra</b>
      </td>
      <td style="text-align:left">Native</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">C+</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left">CQL vs SQL and other nuances</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>MS SQL Data Warehouse</b>
      </td>
      <td style="text-align:left">Native</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B+</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Delta Lake</b>
      </td>
      <td style="text-align:left">Native</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B-</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left">Requires knowledge of databricks</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SAP HANA</b>
      </td>
      <td style="text-align:left">Native</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B+</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left">works with most common data types</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>MariaDB</b>
      </td>
      <td style="text-align:left">MySQL Driver</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B+</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left">Uses mysql driver, some nuances</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Dremio</b>
      </td>
      <td style="text-align:left">Dremio JDBC</td>
      <td style="text-align:left">Preview</td>
      <td style="text-align:left">B</td>
      <td style="text-align:left">User / Pass</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

| File Type Support | Grade | Comments |
| :--- | :--- | :--- |
| **Parquet** | B+ | schema in file, less common but works well |
| **CSV** \(and all delimiters\) | A+ | very common easy to use |
| **JSON** | A- | works great depends how many levels nested |
| **XML** | B | recommend json |
| **AVRO** | B |  |

## FAQ / Tips

**File Sizes**

* Files with more than 250 columns supported in File Explorer, unless you have Livy enabled.
* Files larger than 5gb are not supported in File Explorer, unless you have Livy enabled. 

**S3**

* Please ensure no spaces in S3 connection name
* Please remember to select 'Save Credentials' checkbox upon establishing connection


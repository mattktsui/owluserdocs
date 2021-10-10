# Performance Tests

## Cells Per Second Performance Theory (9.5M CPS)

![](<../.gitbook/assets/Screen Shot 2020-12-01 at 10.31.09 AM.png>)

## Load and Profile

| <p>Dataset </p><p>Name</p> | <p>GBs in</p><p>Memory</p> | <p></p><p>Rows</p> | <p></p><p>Cols</p> | <p></p><p>Cells</p> | <p>Num </p><p>Execs</p> | <p>Num</p><p>Cores</p> | <p>Exec</p><p>Memory</p> | <p>Network </p><p>Time</p> | <p>Total </p><p>Time</p> |
| -------------------------- | -------------------------- | ------------------ | ------------------ | ------------------- | ----------------------- | ---------------------- | ------------------------ | -------------------------- | ------------------------ |
| NYSE                       | 0.1G                       | 103K               | 9                  | 816K                | 1                       | 1                      | 1G                       | 00:00:15                   | 00:00:48                 |
| AUM                        | 14G                        | 9M                 | 48                 | 432M                | 5                       | 1                      | 4G                       | 00:01:20                   | 00:03:50                 |
| ENERGY                     | 5G                         | 43M                | 6                  | 258M                | 8                       | 3                      | 3G                       | 00:00:00                   | 00:04:35                 |
| INVEST_DATA                | 20G                        | 3.8M               | 158                | 590M                | 3                       | 2                      | 3G                       | 00:00:40                   | 00:03:32                 |

### NYSE

Postgres database call, no concurrent processing, simple case, small data.

```bash
-bhtimeoff -numexecutors 1 
-lib "/opt/owl/drivers/postgres" 
-executormemory 1g 
-h metastore01.us-east1-b.c.owl-hadoop-cdh.internal:5432/dev?currentSchema=public 
-drivermemory 1g -master k8s:// -ds public.nyse_128 -deploymode cluster 
-q "select * from public.nyse" -bhlb 10 -rd "2020-10-26" 
-driver "org.postgresql.Driver" -bhminoff 
-loglevel INFO -cxn postgres-gcp -bhmaxoff
```

### AUM

Postgres database call uses parallel JDBC, split on aum_id serial id.  

```bash
-owluser kirk 
-lib "/opt/owl/drivers/postgres" -datashapeoff 
-numpartitions 6 -ds public.aum_dt2_50 
-deploymode cluster -bhlb 10 -bhminoff 
-cxn postgres-gcp -bhmaxoff -bhtimeoff 
-numexecutors 6 
-executormemory 4g -semanticoff 
-h metastore01.us-east1-b.c.owl-hadoop-cdh.internal:5432/dev?currentSchema=public 
-columnname aum_id -corroff -drivermemory 4g -master k8s:// 
-q "select * from public.aum_dt2" -histoff -rd "2020-10-27" 
-driver "org.postgresql.Driver" -loglevel INFO -agentjobid 7664
```

### ENERGY

HDFS file with 43 million rows, converting a string date to date type, deploy mode client.

```bash
-f "hdfs:///demo/owl_usage_all.csv" \
-rd "2019-02-02" \
-ds energy_file \
-loglevel DEBUG -readonly \
-d "," -df dd-MMM-yy \
-master yarn \
-deploymode client  \
-numexecutors 3 \
-executormemory 10g
```

## Load Profile Outliers

### NYSE - 1:10 total runtime.  20 seconds for outliers

```bash
-bhtimeoff -owluser kirk -numexecutors 1 
-lib "/opt/owl/drivers/postgres" -executormemory 1g 
-dl -h metastore01.us-east1-b.c.owl-hadoop-cdh.internal:5432/dev?currentSchema=public 
-drivermemory 1g -master k8s:// -ds public.nyse_128 -deploymode cluster 
-q "select * from public.nyse" -bhlb 10 
-rd "2020-10-27" -driver "org.postgresql.Driver" 
-bhminoff -loglevel INFO -cxn postgres-gcp -bhmaxoff -agentjobid 7721 
```

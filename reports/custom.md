---
description: BI Integrations
---

# Custom

Custom reports can be leveraged by connecting your favorite BI tool on the underlying reporting mart. Below are a few queries that can be used as inspiration for building your own reports. Please refer to the[ ERD diagram ](../architecture/diagram/erd.md)for a larger list of tables.

**Long Running Jobs**

`select dataset,run_id,total_time from dataset_activity where total_time is not null order by total_time desc`

**Jobs Submitted**

`select * from owlcheck_q`

**Jobs by User**&#x20;

`select count(*) as owlchecks, username from owlcheck_q where updt_ts < now() group by username order by owlchecks desc`

**Jobs by User, Dataset**

`select count(*), user_nm, dataset from dev.public.owl_check_history group by user_nm, dataset order by count desc`

**Largest by Row Count**&#x20;

`select dataset,rc as row_count from dataset_scan order by rc desc`

**Jobs by Month**&#x20;

`with grp as ( select date_trunc('MONTH', run_id) as by_month from dataset_scan where run_id < now() ) select count(*) as owlchecks, by_month from grp group by by_month order by by_month desc`

**Rules by User**

`select count(*) as rules, user_nm from owl_rule group by user_nm order by rules desc`

**By Spark(Cluster) Usage**

`select * from opt_spark order by num_executors desc`

**Jobs IDs from Agent**

`select remote_job_id from agent_q where remote_job_id is not null`

**Dataset Activity**&#x20;

`select dataset,run_id,total_time from dataset_activity where total_time is not null order by total_time desc`

**Jobs with Enriched Metrics**&#x20;

`with activity as ( select dataset,run_id,total_time from dataset_activity where total_time is not null order by total_time desc limit 100), scans as ( select * from dataset_scan where dataset in (select dataset from activity) ), configs as ( select * from opt_spark where dataset in (select dataset from activity)), schema as ( select count(*) as col_cnt, dataset from dataset_schema where dataset in (select dataset from activity) group by dataset ) SELECT A.dataset, A.run_id, C.total_time, A.rc, D.col_cnt, B.driver_memory, B.num_executors,B.executor_cores, B.executor_memory, B.master FROM scans A INNER JOIN configs B ON A.dataset = B.dataset INNER JOIN activity C ON A.dataset = C.dataset and A.run_id = C.run_id INNER JOIN schema D on A.dataset = D.dataset ORDER BY C.total_time desc`

**Jobs. Load Times and Resources**

`with activity as ( select dataset,run_id,total_time from public.dataset_activity where total_time is not null order by total_time), scans as ( select * from public.dataset_scan where dataset in (select dataset from activity) ), configs as ( select * from public.opt_spark where dataset in (select dataset from activity)), schema as ( select count(*) as col_cnt, dataset from public.dataset_schema where dataset in (select dataset from activity) group by dataset ) SELECT A.dataset, A.run_id, A.updt_ts, C.total_time, A.rc, D.col_cnt, B.driver_memory, B.num_executors,B.executor_cores, B.executor_memory, B.master FROM scans A INNER JOIN configs B ON A.dataset = B.dataset INNER JOIN activity C ON A.dataset = C.dataset and A.run_id = C.run_id INNER JOIN schema D on A.dataset = D.dataset ORDER BY A.updt_ts desc limit 10`

**Dataset Scans and Scores By Schema**

`select * from public.dataset_scan where dataset like 'public.%';`

**Dataset Scans and Scores By Name**

`select * from public.dataset_scan where dataset ='public.atm_customer';`

**Scans By Month By Schema - 'Public'**

`select dataset, DATE_TRUNC('MONTH', run_id) as run_id, count(*) as Total_Scans from dataset_scan where dataset like 'public%' group by dataset, run_id order by run_id asc`

**Rule Breaks Past 30 Days**

`select * from rule_output where run_id < NOW() - INTERVAL '30 DAY';`

**Scheduled Jobs Queue**

`select job_id,agent_id,dataset,run_id,status,activity,start_time from public.owlcheck_q;`

**Column Counts from Dataset Schema**

`select dataset, count(*) from dataset_schema group by dataset;`

**Profiling Stats**

`select dataset, run_id, field_nm, (null_ratio * 100) as null_percent, (empty_ratio * 100) as empty_percent, ROUND( CAST( ( 100 - ((null_ratio * 100) + (empty_ratio * 100)) ) as numeric), 3) as completeness from public.dataset_field where updt_ts > '2020-06-01' and dataset = 'ProcessOrder' and run_id > '2021-03-17 00:00:00+00' order by completeness desc`

**Metadata / Schema / Datatypes**

`select * from public.dataset_schema;`

**Profile Stats**

`select * from public.dataset_field;`

**Locate Similar Columns**

`select distinct dataset, field_nm, max_abs from dataset_field where max_abs = 'Wireless Telecommunications'`

**Same Column Names**&#x20;

`select distinct dataset, field_nm from dataset_field where field_nm = 'authenticated_user'`

**Similar Column Names**

&#x20;`select distinct dataset,field_nm from dataset_field where field_nm like '%id%'`

**Behavior Findings**

&#x20;`select * from behavior where dataset='esg_data'`

**All Columns for Schema from Postgres Stats**

`SELECT table_name FROM information_schema.tables WHERE table_schema = 'public' ORDER BY table_name`

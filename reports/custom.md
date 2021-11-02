---
description: BI Integrations
---

# Custom

Custom reports can be leveraged by connecting your favorite BI tool on the underlying reporting mart.

**Long Running Jobs**

`select dataset,run_id,total_time from dataset_activity where total_time is not null order by total_time desc`

**Jobs Submitted**

`select * from owlcheck_q`

**Jobs by User**&#x20;

`select count(*) as owlchecks, username from owlcheck_q where updt_ts < now() group by username order by owlchecks desc`

**Jobs by User, Dataset**

`select count(*), user_nm, dataset from dev.public.owl_check_history group by user_nm, dataset order by count desc`

**Largest by Row Count **

`select dataset,rc as row_count from dataset_scan order by rc desc`

**Jobs by Month **

`with grp as ( select date_trunc('MONTH', run_id) as by_month from dataset_scan where run_id < now() ) select count(*) as owlchecks, by_month from grp group by by_month order by by_month desc`

**Rules by User**

`select count(*) as rules, user_nm from owl_rule group by user_nm order by rules desc`

**By Spark(Cluster) Usage**

`select * from opt_spark order by num_executors desc`

**Jobs IDs from Agent**

select remote\_job\_id from agent\_q where remote\_job\_id is not null

**Dataset Activity **

select dataset,run\_id,total\_time from dataset\_activity where total\_time is not null order by total\_time desc

**Jobs with Enriched Metrics **

with activity as ( select dataset,run\_id,total\_time from dataset\_activity where total\_time is not null order by total\_time desc limit 100), scans as ( select \* from dataset\_scan where dataset in (select dataset from activity) ), configs as ( select \* from opt\_spark where dataset in (select dataset from activity)), schema as ( select count(\*) as col\_cnt, dataset from dataset\_schema where dataset in (select dataset from activity) group by dataset ) SELECT A.dataset, A.run\_id, C.total\_time, A.rc, D.col\_cnt, B.driver\_memory, B.num\_executors,B.executor\_cores, B.executor\_memory, B.master FROM scans A INNER JOIN configs B ON A.dataset = B.dataset INNER JOIN activity C ON A.dataset = C.dataset and A.run\_id = C.run\_id INNER JOIN schema D on A.dataset = D.dataset ORDER BY C.total\_time desc

**Jobs. Load Times and Resources**

&#x20;with activity as ( select dataset,run\_id,total\_time from public.dataset\_activity where total\_time is not null order by total\_time), scans as ( select \* from public.dataset\_scan where dataset in (select dataset from activity) ), configs as ( select \* from public.opt\_spark where dataset in (select dataset from activity)), schema as ( select count(\*) as col\_cnt, dataset from public.dataset\_schema where dataset in (select dataset from activity) group by dataset ) SELECT A.dataset, A.run\_id, A.updt\_ts, C.total\_time, A.rc, D.col\_cnt, B.driver\_memory, B.num\_executors,B.executor\_cores, B.executor\_memory, B.master FROM scans A INNER JOIN configs B ON A.dataset = B.dataset INNER JOIN activity C ON A.dataset = C.dataset and A.run\_id = C.run\_id INNER JOIN schema D on A.dataset = D.dataset ORDER BY A.updt\_ts desc limit 10

**Dataset Scans and Scores By Schema**

select \* from public.dataset\_scan where dataset like 'public.%';

**Dataset Scans and Scores By Name**

select \* from public.dataset\_scan where dataset ='public.atm\_customer';

**Scans By Month By Schema - 'Public'**

select dataset, DATE\_TRUNC('MONTH', run\_id) as run\_id, count(\*) as Total\_Scans from dataset\_scan where dataset like 'public%' group by dataset, run\_id order by run\_id asc

**Rule Breaks Past 30 Days**

select \* from rule\_output where run\_id < NOW() - INTERVAL '30 DAY';

**Scheduled Jobs Queue**

select job\_id,agent\_id,dataset,run\_id,status,activity,start\_time from public.owlcheck\_q;

**Column Counts from Dataset Schema**

select dataset, count(\*) from dataset\_schema group by dataset;

**Profiling Stats**

select dataset, run\_id, field\_nm, (null\_ratio \* 100) as null\_percent, (empty\_ratio \* 100) as empty\_percent, ROUND( CAST( ( 100 - ((null\_ratio \* 100) + (empty\_ratio \* 100)) ) as numeric), 3) as completeness from public.dataset\_field where updt\_ts > '2020-06-01' and dataset = 'ProcessOrder' and run\_id > '2021-03-17 00:00:00+00' order by completeness desc

**Metadata / Schema / Datatypes**

select \* from public.dataset\_schema;

**Profile Stats**

select \* from public.dataset\_field;

**Locate Similar Columns**

select distinct dataset, field\_nm, max\_abs from dataset\_field where max\_abs = 'Wireless Telecommunications'

**Same Column Names**&#x20;

select distinct dataset, field\_nm from dataset\_field where field\_nm = 'authenticated\_user'

**Similar Column Names**

&#x20;select distinct dataset,field\_nm from dataset\_field where field\_nm like '%id%'

**Behavior Findings**

&#x20;select \* from behavior where dataset='demo.esg\_data\_october\_22'

**All Columns for Schema from Postgres Stats**

&#x20;SELECT table\_name FROM information\_schema.tables WHERE table\_schema = 'public' ORDER BY table\_name;


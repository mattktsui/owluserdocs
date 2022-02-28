# Best Practices

### **Understanding owl activities and what the key/date columns mean for each**

* Starting with profile and expanding to rules and then other advanced capabilities. &#x20;
  * [https://dq-docs.collibra.com/dq-visuals/profile](https://dq-docs.collibra.com/dq-visuals/profile)
* Training with Owl-team Zoom/On-site support&#x20;
* Running with sample data&#x20;
* Introducing anomalies on sample data and running an owlcheck to see the anomalies.

### **Using the tool with practical scenarios**

* Having Well Defined Use Cases
  * Determine a single table (dataset) that you would like to scan
  * Have an expectation of what you would expect Owl to find in this dataset
  * Understand which activities would capture the expected findings
* Target internal datasets with known data issues
* Historical Comparisons:
  * If pre-cleaned data is available with data findings that have been cleaned via legacy methods such as internal rules, run these datasets and compare the results from Owl to Internal findings.
* Work with data owners to understand findings or review expected findings

### Explorer

* The date selected with the calendar widget in the Scope (home) tab should align with the calendar widget assigned on the final (Save/Run) tab.&#x20;
* If you elect to Unlock the cmd line and override the final parameters, do not re-lock or the changes will be overwritten.  In general, only advanced users should override the guided settings.
* Pushdown and parallel JDBC cannot be used together. If you are using pushdown, do not select the parallel JDBC option

### Files

* File paths should not contain spaces or special characters.&#x20;
* Backrun (replay) and advanced features are best suited for JDBC connections.  Some features are unavailable if file and storage naming conventions do not consistently contain a date signature.&#x20;

### Connection Pool

If you see this message, update the agent configs in owl-env.sh or agent confg map for k8 deployments.

```
Failed to obtain JDBC Connection; nested exception is org.apache.tomcat.jdbc.pool.PoolExhaustedException: [pool-29-thread-2] Timeout: Pool empty. Unable to fetch a connection in 0 seconds, none available[size:2; busy:1; idle:0; lastwait:200].
```

Adjust these configs to modify the connection pool available.

```
export SPRING_DATASOURCE_POOL_MAX_WAIT=500
export SPRING_DATASOURCE_POOL_MAX_SIZE=10
export SPRING_DATASOURCE_POOL_INITIAL_SIZE=5
```

### Freeform Agent Configs

When configuring the DQ Agent and using the Free Form Parameters at the bottom of the dialogue, you need to comma separate multiple -conf key/value pairs. I am going to write this as a forum post but use this format: "-conf some.key=x, some.other.key=y"

### K8 Secrets

The following Env Vars are now managed as a Secret instead of as a Configmap

LICENSE\_KEY LIVY\_SSL\_KEY\_PASS SERVER\_SSL\_KEY\_PASS SPRING\_AGENT\_DATASOURCE\_PASSWORD SPRING\_AGENT\_DATASOURCE\_USERNAME SPRING\_DATASOURCE\_PASSWORD SPRING\_DATASOURCE\_USERNAME

### DQ Job Stages

DQ job failure is one of the most frequently asked. This outlines the DQ Job Lifecycle and where to find logs for each phase. Every DQ Job goes through a three stage Lifecycle:&#x20;

#### Stage 1

Agent picks up job from the Metastore and translates it into a valid Spark Submit request. This includes credential acquisition and injection for Cloud and Kerberos. If a job never makes it out of STAGING, the first thing to do is to check the Agent logs (\<INSTALL\_HOME>/log/agent.log or on K8s kubectl logs -n .&#x20;

#### Stage 2&#x20;

Agent hands off the DQ check to Spark via Spark Submit, maintaining a handle on the Spark Submit request. At this point the Job is in Spark’s custody but not yet running (Spark Submit creates its own JVM to manage the submission of the Spark Job to the cluster/runtime). If the job fails with a message saying something like “Failed with reason NULL” on the Jobs page, check the Stage 2 logs (there will be a separate log for each Job). These can be found either on the Agent itself (\<INSTALL\_HOME>/log/.log) or whenever possible on the Jobs page Action Dropdown on the job entry. Stage 3: Spark Submit instantiates the Job in the target Spark Runtime (Hadoop/K8s/Spark-Master). At this point, the DQ core code is active and DQ is back in control of the job. Typically, if a job makes it to this stage, it will no longer be in STAGING status and you should see an error message on the Jobs Page. Typically, the full Stage 3 log is required to trouble shoot a problem that happens in Core.&#x20;

#### Stage 3

logs can be obtained from the Actions drop down for the job entry. If log extraction failed, job logs will need to be gathered from the Spark Runtime directly (Hadoop Resource Manager, K8s API via Kubectl or vendor provided UI, Spark Master UI or directly from the Spark Master Host).

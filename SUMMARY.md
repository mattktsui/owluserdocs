# Table of contents

* [Collibra Data Quality](README.md)
* [Release Notes](release-notes.md)
* [Our Approach](why-owl.md)
* [Our Story](our-story.md)
* [What is OwlDQ](what-is-owldq.md)

## Installation

* [Basic Install](installation/basic-install.md)
* [Full Standalone Install](installation/full-install.md)
* [Standalone Upgrade](installation/standalone-upgrade.md)
* [Hadoop Integration](installation/hadoop-integration.md)
* [Agent Configuration](installation/agent-configuration.md)
* [EMR / Dataproc / HDI](installation/emr.md)
* [Preparing for Cloud Native Deployment](installation/preparing-for-deployment.md)
* [Cloud Native OwlDQ](installation/cloud-native-owldq.md)
* [Deploying Cloud Native OwlDQ](installation/deploying-cloud-native-owldq.md)
* [AKS / EKS / GKE: Kubernetes Deployment](installation/aks-eks-gke-kubernetes-deployment.md)

## Connections <a href="connecting-to-dbs-in-owl-web" id="connecting-to-dbs-in-owl-web"></a>

* [Supported Drivers](connecting-to-dbs-in-owl-web/supported-drivers.md)
* [General](connecting-to-dbs-in-owl-web/owl-db-connection.md)
* [Connectivity to Athena](connecting-to-dbs-in-owl-web/connectivity-to-athena.md)
* [Connectivity to BigQuery](connecting-to-dbs-in-owl-web/connectivity-to-bigquery.md)
* [Connectivity to Hive](connecting-to-dbs-in-owl-web/connectivity-to-hive/README.md)
  * [Connecting to CDH 5.16 Hive SSL/TLS/Kerberos Setup](connecting-to-dbs-in-owl-web/connectivity-to-hive/connecting-to-cdh-5.16-hive-ssl-tls-kerberos-setup.md)
* [Connectivity to Oracle](connecting-to-dbs-in-owl-web/connectivity-to-oracle.md)
* [Connectivity to Presto](connecting-to-dbs-in-owl-web/connectivity-to-presto.md)
* [Connectivity to Redshift](connecting-to-dbs-in-owl-web/connectivity-to-redshift.md)
* [Connectivity to Snowflake](connecting-to-dbs-in-owl-web/connectivity-to-snowflake.md)
* [Connectivity to SQL Server](connecting-to-dbs-in-owl-web/connectivity-to-sql-server.md)
* [Add Connection to Agent](connecting-to-dbs-in-owl-web/add-connection-to-agent.md)

## Core Components <a href="dq-visuals" id="dq-visuals"></a>

* [Overview](dq-visuals/overview.md)
* [Explorer](dq-visuals/explorer-2.md)
* [Profile](dq-visuals/profile/README.md)
  * [AutoProfile](dq-visuals/profile/autoprofile.md)
* [Behaviors](dq-visuals/behaviors.md)
* [Rules](dq-visuals/rules/README.md)
  * [Creating a Rule](dq-visuals/rules/creating-a-business-rule.md)
  * [Rule Library](dq-visuals/rules/dq-rule-automation.md)
  * [Cross-Dataset Rules](dq-visuals/rules/easier-rule-examples.md)
  * [Data Concepts and Semantics](dq-visuals/rules/data-concepts-and-semantics.md)
* [Schema Evolution](dq-visuals/schema-evolution.md)
* [Shapes](dq-visuals/shapes.md)
* [Duplicates (advanced)](dq-visuals/duplicates.md)
* [Outliers (advanced)](dq-visuals/outliers.md)
* [Patterns (advanced)](dq-visuals/pattern-mining/README.md)
  * [Bloomberg Data](dq-visuals/pattern-mining/bloomberg-data.md)
* [Records (advanced)](dq-visuals/missing-records.md)
* [Validate Source (advanced)](dq-visuals/validate-source.md)
* [Explorer (cont'd)](dq-visuals/explorer.md)
* [9 Dimensions of DQ](dq-visuals/owl-dq-screen-shots.md)

## DQ JOB Examples

* [DQ Job JDBC](dq-job-examples/job-jdbc.md)
* [DQ Job BigQuery](dq-job-examples/owlcheck-bigquery.md)
* [DQ Job Hive](dq-job-examples/job-hive.md)
* [DQ Job Files](dq-job-examples/job-files.md)
* [DQ Job JSON](dq-job-examples/job-json.md)
* [DQ Job Kafka](dq-job-examples/job-kafka.md)
* [DQ Job MySql](dq-job-examples/job-mysql.md)
* [Data Quality Pipelines](dq-job-examples/data-quality-pipelines/README.md)
  * [Simple Spark Data Pipeline](dq-job-examples/data-quality-pipelines/simple-spark-data-pipeline.md)
  * [Notebook Outlier Example](dq-job-examples/data-quality-pipelines/notebook-outlier-example.md)
  * [Notebook ColMatch Example](dq-job-examples/data-quality-pipelines/notebook-colmatch-example.md)
  * [Owl Options API](dq-job-examples/data-quality-pipelines/owl-options-api.md)
  * [Owl Rules - DQ Pipeline](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/README.md)
    * [Global rules](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/global-rules.md)
    * [SQL based rules](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/README.md)
      * [Simple rule](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/simple-rule.md)
      * [Freeform SQL](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/freeform-sql.md)
      * [Native SQL](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/native-sql.md)
      * [Function](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/function.md)
    * [Data type based rules](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/data-type-based-rules.md)
    * [FAQs](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/frequently-asked-questions.md)
  * [AWS DataBricks - DQ Pipeline](dq-job-examples/data-quality-pipelines/aws-databricks-dq-pipeline.md)
  * [Azure DataBricks - DQ Pipeline](dq-job-examples/data-quality-pipelines/azure-databricks-dq-pipeline.md)
  * [Spark - DQ Pipeline](dq-job-examples/data-quality-pipelines/spark-dq-pipeline.md)
* [DQ Job Spark](dq-job-examples/owlcheck-spark.md)
* [DQ Job Databricks](dq-job-examples/owlcheck-databricks.md)
* [DQ Job Cron](dq-job-examples/owlcheck-cron.md)
* [DQ Job Snowflake](dq-job-examples/owlcheck-snowflake.md)
* [DQ Job S3](dq-job-examples/owlcheck-s3.md)
* [DQ Job HDFS](dq-job-examples/owlcheck-hdfs.md)
* [DQ Job MongoDB](dq-job-examples/owlcheck-mongodb.md)
* [DQ Job Zeppelin](dq-job-examples/owlcheck-zeppelin.md)
* [DQ Job LinkId](dq-job-examples/owlcheck-linkid.md)
* [DQ Job Back Run](dq-job-examples/owlcheck-backrun.md)
* [DQ Job Validate Source](dq-job-examples/owlcheck-validate-source.md)
* [DQ Job 43M rows](dq-job-examples/owlcheck-43m-rows.md)
* [More...](dq-job-examples/owlcheck/README.md)
  * [OwlCheck JSON](dq-job-examples/owlcheck/owlcheck-json.md)

## Integration

* [Collibra Native DQ Connector](integration/dq-connector.md)
* [DQ Workflows in Collibra DIC](integration/dq-workflows-in-collibra-dic.md)

## Scorecards

* [Dataset Scorecard](scorecards/dataset-scorecard.md)
* [Group Scorecard](scorecards/group-scorecard.md)
* [List View](scorecards/list-view.md)

## Scheduler

* [Schedule Management](scheduler/schedule-management.md)
* [Schedule Owlchecks](scheduler/schedule-owlchecks.md)
* [View/Re-Run Scheduled Jobs](scheduler/view-re-run-scheduled-jobs.md)

## WORKFLOWS / ALERTS <a href="workflows" id="workflows"></a>

* [Email Alerts](workflows/email-alerts.md)
* [Assignment Queue(s)](workflows/assignment-queue-s.md)
* [Internal Assignment](workflows/internal-assignment.md)
* [External Assignment](workflows/external-assignment.md)
* [FAQ](workflows/faq.md)

## Labeling / Training

* [Item Labeling](labeling-training/item-labeling.md)
* [Peak vs Off Peak](labeling-training/peak-vs-off-peak.md)

## Catalog

* [Business Units](catalog/business-units.md)
* [Catalog](catalog/catalog.md)
* [Catalog Bulk Actions](catalog/catalog-bulk-actions.md)
* [Cluster Health Report](catalog/cluster-health-report.md)

## Reports

* [Completeness Report](reports/completeness-report.md)
* [Summary Reports](reports/owl-summary-reports.md)
* [Dataset Report](reports/profile.md)
* [Coverage Report](reports/coverage-report.md)

## APIs

* [REST APIs](apis/rest-apis.md)
* [Swagger](apis/swagger.md)
* [Job Server](apis/job-server.md)
* [Custom Configurations](apis/custom-configurations.md)
* [Assignment API](apis/assignmentapi.md)
* [Time Zone API](apis/owl-time-zone-api.md)
* [Notebook API](apis/notebook-api/README.md)
  * [OwlOptions (base)](apis/notebook-api/owloptions-base.md)

## API-Core <a href="api" id="api"></a>

* [Notebook/Spark](api/notebook/README.md)
  * [Spark-shell Sample](api/notebook/spark-shell-sample.md)
  * [Dupe](api/notebook/dupe.md)
  * [Load](api/notebook/load.md)
  * [Source](api/notebook/source.md)
  * [Profile](api/notebook/profile.md)
* [JWT](api/jwt.md)
* [Cookie](api/cookie.md)

## API-MIGRATION <a href="migration-and-promoting" id="migration-and-promoting"></a>

* [Export and Import API](migration-and-promoting/export-and-import-api.md)
* [Rules Import Export](migration-and-promoting/rules-import-export.md)

## Advanced

* [Add Date Column](advanced/add-date-column.md)
* [Date Time Variable Options](advanced/date-time-variable-options.md)
* [File Look Back](advanced/file-lookback.md)
* [Filter & Filter Not](advanced/filter.md)
* [Multiple Pattern Relationships](advanced/multiple-pattern-combinations.md)
* [Nulls in Datasets](advanced/zero-if-null.md)
* [Transform](advanced/owlcheck-transform.md)

## Use Cases

* [Bank Loans](use-cases/bank-loans.md)
* [Financial FxRate Data](use-cases/financial-fxrate-data.md)
* [Intraday Positions](use-cases/intraday-positions.md)
* [Creating a Data Quality Pipeline](use-cases/creating-a-data-quality-pipeline.md)
* [Security Reference Data](use-cases/security-reference-data.md)
* [Copying or Moving data](use-cases/copying-or-moving-data.md)
* [Cyber Anomalies in Real-Time](use-cases/cyber-anomalies-in-real-time.md)
* [Healthcare  Data Quality](use-cases/healthcare-dq-in-2-minutes.md)
* [Smart Meter Data](use-cases/smart-meter-data.md)
* [Health Insurance Claims Data](use-cases/insurance-data.md)

## Solutions <a href="projects" id="projects"></a>

* [Best Practices](projects/best-practices.md)
* [Prescriptive Personas](projects/prescriptive-personas.md)
* [Builds a Better DQ Dashboard](projects/builds-a-better-dq-dashboard.md)
* [Ensures CCPA & GDPR](projects/ccpa-and-gdpr.md)
* [Makes your Data Lake better.](projects/data-quality-monitoring.md)
* [Speeds Migrations/Enables Replications](projects/migrations.md)
* [Assists Data Aggregation](projects/assists-data-aggregation.md)
* [DQ is the difference](projects/data-quality.md)

## Troubleshooting

* [Cloudera CLASSPATH](troubleshooting/cloudera-classpath.md)
* [Performance Tuning](troubleshooting/performance-tuning.md)
* [Deploy Mode](troubleshooting/deploy-mode.md)

## Benchmarks

* [Performance Tests](benchmarks/performance-tests.md)
* [FAQ](benchmarks/benchmark-faq.md)

## Architecture

* [ERD](architecture/erd.md)
* [Architecture Diagram](architecture/diagram.md)
* [System Requirements](architecture/system-requirements.md)

## Admin

* [Admin Console Overview](admin/admin-console-overview.md)
* [System Setup](admin/system-setup.md)
* [Dataset Audit Trail](admin/dataset-audit-trail.md)
* [Security Audit Trail](admin/security-audit-trail.md)
* [User Audit Trail](admin/user-audit-trail.md)
* [Multi-Tenancy](admin/multi-tenancy.md)
* [SMTP Setup](admin/smtp-setup.md)
* [SSL Setup (HTTPS)](admin/ssl-setup-https.md)
* [Securing Passwords](admin/securing-passwords.md)
* [Time Based Data Retention](admin/time-based-data-retention.md)

## Security

* [Active Directory LDAP](security/authentication-with-active-directory-ldap/README.md)
  * [AD Group to Owl Role Mapping](security/authentication-with-active-directory-ldap/ad-group-to-owl-role-mapping.md)
* [SAML IDP](security/authentication-with-saml-idp.md)
* [Local User Store Authentication](security/authentication-with-local-user-store/README.md)
  * [Adding Local Users](security/authentication-with-local-user-store/adding-local-users.md)
* [Role Based Access Control (RBAC)](security/role-based-access-control-rbac.md)
* [Connection Security](security/connection-security.md)
* [Dataset Security](security/dataset-security.md)
* [Dataset Masking](security/dataset-masking.md)
* [Owl Security](security/owl-security.md)

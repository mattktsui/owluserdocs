# Table of contents

* [Collibra Data Quality](README.md)
* [Release Notes](release-notes.md)

## Installation

* [Standalone](installation/standalone/README.md)
  * [Standalone Install](installation/standalone/full-install.md)
  * [Standalone Upgrade](installation/standalone/standalone-upgrade.md)
  * [Standalone Sizing](installation/standalone/standalone-sizing.md)
* [Hadoop](installation/hadoop/README.md)
  * [Hadoop Install](installation/hadoop/hadoop-integration.md)
  * [EMR / Dataproc / HDI](installation/hadoop/emr.md)
* [Cloud Native](installation/cloud-native-owldq/README.md)
  * [Cloud Native Install](installation/cloud-native-owldq/deploying-cloud-native-owldq.md)
  * [Cloud Native Requirements](installation/cloud-native-owldq/preparing-for-deployment.md)
  * [EKS / GKE / AKS](installation/cloud-native-owldq/aks-eks-gke-kubernetes-deployment.md)
* [Agent](installation/agent-configuration.md)

## Connections <a href="connecting-to-dbs-in-owl-web" id="connecting-to-dbs-in-owl-web"></a>

* [Supported Connections](connecting-to-dbs-in-owl-web/supported-drivers/README.md)
  * [Connectivity to Athena](connecting-to-dbs-in-owl-web/supported-drivers/connectivity-to-athena.md)
  * [Connectivity to BigQuery](connecting-to-dbs-in-owl-web/supported-drivers/connectivity-to-bigquery.md)
  * [Connectivity to Hive](connecting-to-dbs-in-owl-web/supported-drivers/connectivity-to-hive/README.md)
    * [Connecting to CDH 5.16 Hive SSL/TLS/Kerberos Setup](connecting-to-dbs-in-owl-web/supported-drivers/connectivity-to-hive/connecting-to-cdh-5.16-hive-ssl-tls-kerberos-setup.md)
  * [Connectivity to Oracle](connecting-to-dbs-in-owl-web/supported-drivers/connectivity-to-oracle.md)
  * [Connectivity to Presto](connecting-to-dbs-in-owl-web/supported-drivers/connectivity-to-presto.md)
  * [Connectivity to Redshift](connecting-to-dbs-in-owl-web/supported-drivers/connectivity-to-redshift.md)
  * [Connectivity to Snowflake](connecting-to-dbs-in-owl-web/supported-drivers/connectivity-to-snowflake.md)
  * [Connectivity to SQL Server](connecting-to-dbs-in-owl-web/supported-drivers/connectivity-to-sql-server.md)
* [Add a Connection](connecting-to-dbs-in-owl-web/owl-db-connection.md)
* [Add Connection to Agent](connecting-to-dbs-in-owl-web/add-connection-to-agent.md)

## Features <a href="dq-visuals" id="dq-visuals"></a>

* [Overview](dq-visuals/overview.md)
* [Explorer (no-code)](dq-visuals/explorer-2/README.md)
  * [Explorer (advanced)](dq-visuals/explorer-2/explorer.md)
* [Profile (no-code)](dq-visuals/profile/README.md)
  * [AutoProfile](dq-visuals/profile/autoprofile.md)
* [Behavior (automatic)](dq-visuals/behaviors.md)
* [Rules (user-defined)](dq-visuals/rules/README.md)
  * [Adding a Rule](dq-visuals/rules/creating-a-business-rule.md)
  * [Rule Types](dq-visuals/rules/rule-types/README.md)
    * [SQL Based Rules](dq-visuals/rules/rule-types/sql-based-rules/README.md)
      * [Simple](dq-visuals/rules/rule-types/sql-based-rules/simple.md)
      * [Freeform](dq-visuals/rules/rule-types/sql-based-rules/freeform/README.md)
        * [Cross-Dataset Rules](dq-visuals/rules/rule-types/sql-based-rules/freeform/easier-rule-examples.md)
      * [Native](dq-visuals/rules/rule-types/sql-based-rules/native-sql.md)
    * [Stat Rules](dq-visuals/rules/rule-types/stat-rules/README.md)
      * [Data Type Rules](dq-visuals/rules/rule-types/stat-rules/data-type-rules.md)
  * [Rule Templates](dq-visuals/rules/rule-templates.md)
  * [Rule Library](dq-visuals/rules/dq-rule-automation.md)
  * [Rule Discovery](dq-visuals/rules/data-concepts-and-semantics.md)
* [More...](dq-visuals/more.../README.md)
  * [Schema (automatic)](dq-visuals/more.../schema-evolution.md)
  * [Shapes (automatic)](dq-visuals/more.../shapes.md)
  * [Duplicates (advanced)](dq-visuals/more.../duplicates.md)
  * [Outliers (advanced)](dq-visuals/more.../outliers.md)
  * [Patterns (advanced)](dq-visuals/more.../pattern-mining.md)
  * [Records (advanced)](dq-visuals/more.../missing-records.md)
  * [Source (advanced)](dq-visuals/more.../validate-source.md)

## DQ JOB Examples

* [Batch](dq-job-examples/owlcheck-spark/README.md)
  * [DQ Job JDBC](dq-job-examples/owlcheck-spark/job-jdbc.md)
  * [DQ Job BigQuery](dq-job-examples/owlcheck-spark/owlcheck-bigquery.md)
  * [DQ Job Databricks](dq-job-examples/owlcheck-spark/owlcheck-databricks.md)
  * [DQ Job Hive](dq-job-examples/owlcheck-spark/job-hive.md)
  * [DQ Job Files](dq-job-examples/owlcheck-spark/job-files.md)
  * [DQ Job HDFS](dq-job-examples/owlcheck-spark/owlcheck-hdfs.md)
  * [DQ Job JSON](dq-job-examples/owlcheck-spark/job-json.md)
  * [DQ Job MySql](dq-job-examples/owlcheck-spark/job-mysql.md)
  * [DQ Job MongoDB](dq-job-examples/owlcheck-spark/owlcheck-mongodb.md)
  * [DQ Job S3](dq-job-examples/owlcheck-spark/owlcheck-s3.md)
  * [DQ Job Snowflake](dq-job-examples/owlcheck-spark/owlcheck-snowflake.md)
* [Pipelines](dq-job-examples/data-quality-pipelines/README.md)
  * [Simple](dq-job-examples/data-quality-pipelines/simple-spark-data-pipeline.md)
  * [Advanced](dq-job-examples/data-quality-pipelines/spark-dq-pipeline.md)
  * [Rules](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/README.md)
    * [Global rules](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/global-rules.md)
    * [SQL based rules](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/README.md)
      * [Simple rule](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/simple-rule.md)
      * [Freeform SQL](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/sql-based-rules/freeform-sql.md)
    * [Data type based rules](dq-job-examples/data-quality-pipelines/owl-rules-dq-pipeline/data-type-based-rules.md)
  * [Outliers](dq-job-examples/data-quality-pipelines/notebook-outlier-example.md)
  * [Column Match](dq-job-examples/data-quality-pipelines/notebook-colmatch-example.md)
  * [AWS DataBricks](dq-job-examples/data-quality-pipelines/aws-databricks-dq-pipeline.md)
  * [Azure DataBricks](dq-job-examples/data-quality-pipelines/azure-databricks-dq-pipeline.md)
  * [Options API](dq-job-examples/data-quality-pipelines/owl-options-api.md)
  * [FAQs](dq-job-examples/data-quality-pipelines/frequently-asked-questions.md)
* [Advanced...](dq-job-examples/owlcheck/README.md)
  * [DQ Job Back Run](dq-job-examples/owlcheck/owlcheck-backrun.md)
  * [DQ Job Cron](dq-job-examples/owlcheck/owlcheck-cron.md)
  * [DQ Job Kafka](dq-job-examples/owlcheck/job-kafka.md)
  * [DQ Job LinkId](dq-job-examples/owlcheck/owlcheck-linkid.md)
  * [DQ Job Validate Source](dq-job-examples/owlcheck/owlcheck-validate-source.md)
  * [DQ Job 43M rows](dq-job-examples/owlcheck/owlcheck-43m-rows.md)

## Collibra DIC Integration <a href="integration" id="integration"></a>

* [DQ Connector](integration/dq-connector.md)
* [DQ Workflows](integration/dq-workflows-in-collibra-dic.md)

## Scorecards

* [Overview](scorecards/dataset-scorecard.md)
* [Page View](scorecards/group-scorecard.md)
* [List View](scorecards/list-view.md)
* [DQ Scoring](scorecards/owl-dq-screen-shots.md)

## Scheduler

* [Schedule a Job](scheduler/schedule-owlchecks.md)
* [Schedule Management](scheduler/schedule-management.md)
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
* [Coverage Report](reports/coverage-report.md)
* [Dataset Report](reports/profile.md)
* [Summary Reports](reports/owl-summary-reports.md)

## APIs

* [REST APIs](apis/rest-apis.md)
* [Swagger](apis/swagger.md)
* [Job Server](apis/job-server.md)
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
* [Export and Import Example](migration-and-promoting/rules-import-export.md)

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
* [Bloomberg Data](dq-visuals/pattern-mining/bloomberg-data.md)
* [Financial FxRate Data](use-cases/financial-fxrate-data.md)
* [Intraday Positions](use-cases/intraday-positions.md)
* [Creating a Data Quality Pipeline](use-cases/creating-a-data-quality-pipeline.md)
* [Security Reference Data](use-cases/security-reference-data.md)
* [Validating Data Movement](use-cases/copying-or-moving-data.md)
* [Cyber Anomalies in Real-Time](use-cases/cyber-anomalies-in-real-time.md)
* [Healthcare  Data Quality](use-cases/healthcare-dq-in-2-minutes.md)
* [Smart Meter Data](use-cases/smart-meter-data.md)
* [Health Insurance Claims Data](use-cases/insurance-data.md)

## Solutions <a href="projects" id="projects"></a>

* [Our Approach](projects/why-owl.md)
* [Our Story](projects/our-story.md)
* [What is OwlDQ](projects/what-is-owldq.md)
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
* [Hardware Sizing](architecture/hardware-sizing.md)
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
* [Custom Configurations](admin/custom-configurations.md)

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

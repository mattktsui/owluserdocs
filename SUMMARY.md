# Table of contents

* [Collibra Data Quality & Observability](README.md)
* [Release Notes](release-notes.md)

## Installation

* [Standalone](installation/standalone/README.md)
  * [Standalone Install](installation/standalone/full-install.md)
  * [Standalone Upgrade](installation/standalone/standalone-upgrade.md)
  * [Standalone Sizing](installation/standalone/standalone-sizing.md)
* [Hadoop](installation/hadoop/README.md)
  * [Hadoop Install](installation/hadoop/hadoop-integration.md)
  * [EMR / Dataproc / HDI](installation/hadoop/emr.md)
* [Cloud native](installation/cloud-native-owldq/README.md)
  * [Cloud native requirements](installation/cloud-native-owldq/preparing-for-deployment.md)
  * [Cloud native install](installation/cloud-native-owldq/deploying-cloud-native-owldq.md)
  * [EKS / GKE / AKS](installation/cloud-native-owldq/aks-eks-gke-kubernetes-deployment.md)
* [Agent](installation/agent-configuration.md)

## Connections <a href="#connecting-to-dbs-in-owl-web" id="connecting-to-dbs-in-owl-web"></a>

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

## Features <a href="#dq-visuals" id="dq-visuals"></a>

* [Profile (automatic)](dq-visuals/profile.md)
* [Behavior (automatic)](dq-visuals/behaviors.md)
* [Rules (user-defined)](dq-visuals/rules/README.md)
  * [Adding a Rule](dq-visuals/rules/creating-a-business-rule.md)
  * [Scores](dq-visuals/rules/scores.md)
  * [Dimensions](dq-visuals/rules/dimensions.md)
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
* [More](dq-visuals/more.../README.md)
  * [Explorer (no-code)](dq-visuals/more.../explorer-2.md)
  * [Schema (automatic)](dq-visuals/more.../schema-evolution.md)
  * [Shapes (automatic)](dq-visuals/more.../shapes.md)
  * [Duplicates (advanced)](dq-visuals/more.../duplicates.md)
  * [Outliers (advanced)](dq-visuals/more.../outliers.md)
  * [Patterns (advanced)](dq-visuals/more.../pattern-mining.md)
  * [Records (advanced)](dq-visuals/more.../missing-records.md)
  * [Source (advanced)](dq-visuals/more.../validate-source.md)
  * [Pushdown](dq-visuals/more.../pushdown.md)
  * [Summary](dq-visuals/more.../overview.md)

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
  * [Add Date Column](dq-job-examples/owlcheck/add-date-column.md)
  * [AutoProfile](dq-job-examples/owlcheck/autoprofile.md)
  * [Cloudera CLASSPATH](dq-job-examples/owlcheck/cloudera-classpath.md)
  * [Column Matching](dq-job-examples/owlcheck/cluster-health-report.md)
  * [Date Time Variable Options](dq-job-examples/owlcheck/date-time-variable-options.md)
  * [Deploy Mode](dq-job-examples/owlcheck/deploy-mode.md)
  * [Explorer (advanced)](dq-job-examples/owlcheck/explorer.md)
  * [File Look Back](dq-job-examples/owlcheck/file-lookback.md)
  * [Filter & Filter Not](dq-job-examples/owlcheck/filter.md)
  * [Multiple Pattern Relationships](dq-job-examples/owlcheck/multiple-pattern-combinations.md)
  * [Nulls in Datasets](dq-job-examples/owlcheck/zero-if-null.md)
  * [Transform](dq-job-examples/owlcheck/owlcheck-transform.md)

## Collibra DIC Integration <a href="#integration" id="integration"></a>

* [DQ Connector](integration/dq-connector.md)
* [DQ Workflows](integration/dq-workflows-in-collibra-dic.md)

## Scorecards

* [Overview](scorecards/dataset-scorecard/README.md)
  * [Scoring](scorecards/dataset-scorecard/owl-dq-screen-shots.md)
* [Page View](scorecards/group-scorecard.md)
* [List View](scorecards/list-view.md)

## Scheduler

* [Schedule a Job](scheduler/schedule-owlchecks.md)
* [Schedule Management](scheduler/schedule-management/README.md)
  * [View/Re-Run Scheduled Jobs](scheduler/schedule-management/view-re-run-scheduled-jobs.md)

## WORKFLOWS / ALERTS <a href="#workflows" id="workflows"></a>

* [Email Alerts](workflows/email-alerts.md)
* [Assignment Queue(s)](workflows/assignment-queue-s/README.md)
  * [Internal Assignment](workflows/assignment-queue-s/internal-assignment.md)
  * [External assignment](workflows/assignment-queue-s/external-assignment.md)
  * [FAQ](workflows/assignment-queue-s/faq.md)

## Labeling / Training

* [Item Labeling](labeling-training/item-labeling.md)
* [Peak vs Off Peak](labeling-training/peak-vs-off-peak.md)

## Catalog

* [Overview](catalog/catalog.md)
* [Business Units](catalog/business-units.md)
* [Catalog Bulk Actions](catalog/catalog-bulk-actions.md)

## Reports

* [Built-In](reports/built-in/README.md)
  * [Completeness Report](reports/built-in/completeness-report.md)
  * [Coverage Report](reports/built-in/coverage-report.md)
  * [Dataset Report](reports/built-in/profile.md)
  * [Summary Reports](reports/built-in/owl-summary-reports.md)
* [Custom](reports/custom.md)

## APIs

* [REST APIs](apis/rest-apis/README.md)
  * [Find the endpoint](apis/rest-apis/find-the-endpoint.md)
  * [Assignment API](apis/rest-apis/assignmentapi.md)
  * [Export and Import API](apis/rest-apis/export-and-import-api.md)
  * [Export and Import Example](apis/rest-apis/rules-import-export.md)
  * [Time Zone API](apis/rest-apis/owl-time-zone-api.md)
* [Swagger](apis/swagger.md)
* [Notebook/Spark](apis/notebook/README.md)
  * [Spark-shell Sample](apis/notebook/spark-shell-sample.md)
  * [Dupe](apis/notebook/dupe.md)
  * [Load](apis/notebook/load.md)
  * [Source](apis/notebook/source.md)
  * [Profile](apis/notebook/profile.md)
  * [Notebook API](apis/notebook/notebook-api/README.md)
    * [OwlOptions (base)](apis/notebook/notebook-api/owloptions-base.md)
  * [JWT](apis/notebook/jwt.md)
  * [Cookie](apis/notebook/cookie.md)

## Solutions <a href="#projects" id="projects"></a>

* [Our Approach](projects/why-owl/README.md)
  * [Our Story](projects/why-owl/our-story.md)
  * [What is OwlDQ](projects/why-owl/what-is-owldq.md)
  * [DQ is the difference](projects/why-owl/data-quality.md)
* [Best Practices](projects/best-practices/README.md)
  * [Prescriptive Personas](projects/best-practices/prescriptive-personas.md)
* [Data Projects](projects/data-projects/README.md)
  * [Builds a Better DQ Dashboard](projects/data-projects/builds-a-better-dq-dashboard.md)
  * [Ensures CCPA & GDPR](projects/data-projects/ccpa-and-gdpr.md)
  * [Makes your Data Lake better.](projects/data-projects/data-quality-monitoring.md)
  * [Speeds Migrations/Enables Replications](projects/data-projects/migrations.md)
  * [Assists Data Aggregation](projects/data-projects/assists-data-aggregation.md)
  * [Creating a Data Quality Pipeline](projects/data-projects/creating-a-data-quality-pipeline.md)
* [Use Cases](projects/use-cases/README.md)
  * [Bank Loans](projects/use-cases/bank-loans.md)
  * [Bloomberg Data](projects/use-cases/bloomberg-data.md)
  * [Cyber Anomalies in Real-Time](projects/use-cases/cyber-anomalies-in-real-time.md)
  * [Financial FxRate Data](projects/use-cases/financial-fxrate-data.md)
  * [Healthcare Data Quality](projects/use-cases/healthcare-dq-in-2-minutes.md)
  * [Health Insurance Claims Data](projects/use-cases/insurance-data.md)
  * [Intraday Positions](projects/use-cases/intraday-positions.md)
  * [Security Reference Data](projects/use-cases/security-reference-data.md)
  * [Smart Meter Data](projects/use-cases/smart-meter-data.md)
  * [Validating Data Movement](projects/use-cases/copying-or-moving-data.md)

## Benchmarks

* [Performance Settings](benchmarks/performance-settings.md)
* [Performance Tests](benchmarks/performance-tests.md)
* [Performance Tuning](benchmarks/performance-tuning/README.md)
  * [Performance Considerations](benchmarks/performance-tuning/benchmark-faq.md)

## Architecture

* [Architecture Diagram](architecture/diagram/README.md)
  * [ERD](architecture/diagram/erd.md)
* [System Requirements](architecture/system-requirements/README.md)
  * [Hardware Sizing](architecture/system-requirements/hardware-sizing.md)

## Admin

* [Overview](admin/admin-console-overview.md)
* [Configuration](admin/configuration/README.md)
  * [Multi-Tenancy](admin/configuration/multi-tenancy.md)
  * [Time Based Data Retention](admin/configuration/time-based-data-retention.md)
  * [Set up SMTP](admin/configuration/smtp-setup.md)
  * [Advanced](admin/configuration/custom-configurations.md)
* [Audit](admin/audit/README.md)
  * [Dataset Audit Trail](admin/audit/dataset-audit-trail.md)
  * [Security Audit Trail](admin/audit/security-audit-trail.md)
  * [User Audit Trail](admin/audit/user-audit-trail.md)

## Security

* [Overview](security/owl-security.md)
* [Configuration](security/configuration/README.md)
  * [Active Directory LDAP](security/configuration/authentication-with-active-directory-ldap/README.md)
    * [AD Group to Owl Role Mapping](security/configuration/authentication-with-active-directory-ldap/ad-group-to-owl-role-mapping.md)
  * [Connection Security](security/configuration/connection-security.md)
  * [Dataset Security](security/configuration/dataset-security/README.md)
    * [Dataset Masking](security/configuration/dataset-security/dataset-masking.md)
  * [Local User Store Authentication](security/configuration/authentication-with-local-user-store/README.md)
    * [Adding Local Users](security/configuration/authentication-with-local-user-store/adding-local-users.md)
  * [Role Based Access Control (RBAC)](security/configuration/role-based-access-control-rbac.md)
  * [SAML Authentication](security/configuration/authentication-with-saml-idp/README.md)
    * [Multi-tenancy support through SAML RelayState](security/configuration/authentication-with-saml-idp/multi-tenancy-support-through-saml-relaystate.md)
  * [Securing Passwords](security/configuration/securing-passwords.md)
  * [SSL Setup (HTTPS)](security/configuration/ssl-setup-https.md)

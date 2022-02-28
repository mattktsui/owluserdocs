# Release Notes

## 2022.02 (In Progress)

* DQ Job
  * Improved DQ Job page load performance by optimizing calls
  * Fixed issue DQ jobs would fail when -rd is in "yyyy-mm-dd HH" format
* Outliers
  * \*Tech Preview\* \[TP] Outlier Recalibration
* Alerts
  * Ability to navigate to dataset specific Alerts from DQ Job page
  * Ability to test SMTP alert configurations when adding an email relay
  * Fixed issue where 'Reply Email' field did not properly accept user input value
    * Please note there are no (Collibra imposed) domain restrictions on Reply Email field
* Security
  * Mitigated 64 critical, 15 high, and 12 medium vulnerabilities identified by JFrog ([internal-only report link](https://docs.google.com/spreadsheets/d/1yDfqfBO3T3uyw9z\_-zr2SESinTuRWmP\_TgYf\_tlHlk8/edit#gid=0))
  * Upgrade Log4J to 2.17.1
    * Please follow [upgrade steps](release-notes.md#note-to-standalone-collibra-dq-customer-upgrades-we-have-upgraded-to-log4j-2.17-please-refer-to-for)&#x20;
  * Added connection security checks to users to prevent running jobs and query the tables that are not authorized per connection. This is applicable when `DB Connection Security` is enabled in the Admin Console under `General`.
  * Implemented stricter session management
  * Implemented CORS restriction to mitigate potential CSRF vulnerability
* \*Tech Preview\* \[TP] [Collibra Native DQ Connector](integration/dq-connector.md)
  * Fixed issue where tenant specified on DQ Connector configuration (issuer of the jwt token field within DGC Edge Management page) was not properly accepted; only rules that existed with 'public' schema were brought over; now the DQ Connector will accept the proper values
* Agent
  * Upon potential deletion of an agent, added server side validation to indicate number of scheduled jobs so that users can understand if jobs fail going forward
* Rules
  * Enhanced stability on Parallel Rule execution to ensure all rules load by reverting back to fixed thread counts
  * Display exceptions upon rule execution failure to improve rule management experience
  * Improvements to user experience in Rule Library tab (within Rules page) including filters and column alignment
  * Quick Rule dropdown within the Rules page will save with default severity of 1 point and a threshold of 1 percent
  * Enhanced validation for rules generated in Profile tab
  * Fixed issue where removing semantic tag may not have removed corresponding auto-generated rule
  * Rule name character limit of 100
  * Rule Builder page now returns error messages where the dataset contained 0 records
* Catalog
  * Fixed issue where child of business unit could be assigned as parent
  * Bulk actions support for Data Concepts
  * Fixed issue where clearing individual filters were not functioning
* Validate Source
  * New collapsible section for Query in Source tab; enables users to use custom srcq, similar to query on section on Home tab so that users do not need to edit -srcq in cmd line editor on Run tab
  * Introducing new observation types via `-valscrshowmissingkey` flag
    * Key not in source
    * Key not in target
  * Source Name should be fetched as part of getcatalogandconnsrcnamebydataset API call for a given dataset
  * Fixed issue which prevented Hive from working as Target
* Export / Import
  * Fixed issue that import could not accommodate more than one table insert
  * Fixed bug where certain values were inadvertently inserted into RegEx rules upon Export
* Connection
  * Fixed Out Of Memory issue with Dremio
    * Explicitly added limit clause in the preview query within Update Scope
    * Dremio driver requires double quotes in Schema, Table, and Column names e.g. "SchemaName"."TableName"
  * Fixed Oracle TIMESTAMPLTZ conversion error
* Explorer
  * Fixed issue where 'Analyze Table' option did not populate for Hive
  * Fixed the static date values showing up in Managed Template and Run Check while running the job via v2/runtemplate API call from swagger UI
* Files
  * File names with spaces are now handled with double quotes t
  * Implemented Supported File Type Check at time of uploading the Temp Files via Explorer
    * Default supported file types are “csv,json,parquet,avro,delta".&#x20;
    * In order to add/update the supported file types and ensure validation, a new environment variable needs to be added in owl-env.sh as below: `export ALLOWED_UPLOAD_FILE_TYPES="csv,json,parquet,avro,delta"`
    * Tip: For remote files with delimiter, please use the csv dropdown options for files with .txt extension
  * \*Tech Preview\* \[TP] Users have ability to assign an agent when using temp file and local file Explorer paths without manually appending -master to agent or job (previous known limitation)
  * LIMIT values are now properly accepted on the Scope & Range query panel
* Dupes
  * Fixed issue where column selections were not retained from the original DQ Job with Dupes ON for future runs

#### Known Limitations

* Rules
  * Cannot currently create rule with API /v3/rules; will be fixed in future release
    * Please use /v2/createrule API
* DQ Job
  * /v2/runtemplate API still creates 'zombie' job
    * Please use /v3/jobs/run
* Outliers
  * Outlier Recalibrate
    *

## 2022.01

#### Enhancements

* DQ Job
  * Fixed issue where backrun "-br" flag was inadvertently added on future runs (error contained in 2021.12) if the initial DQ Job setup Explorer selected backrun
  * Improved validation to not allow for slashes in dataset name
* Validate Source
  * Fixed potential DQ Job failure with Source turned on for some legacy installations when upgrading from older versions to 2021.11 and newer
* Explorer
  * `DB_VIEWS_ON` can be added with TRUE or FALSE values by adding new App Config (Add Custom within Admin -> Configuration)
  * \-Addlib flag now working across JDBC connections
  * Update Scope now supports rdEnd
* Rules
  * When creating rules, run-time limit for each rule (in minutes) can be set on the Rule page UI and on the V3 API (by setting `runTimeLimit` property). The default is 30 minutes if not explicitly set. This 30 minute limit sets the overall timeout limit for all rules in a particular job. For example, if there are 10 rules with 9 rules with 30 min limit and 1 rule as 90 min limit, then the DQ Job will wait up to 90 min for all 10 rules to finish. This is because all rules must finish before the Rule stage in DQ Job to finish and move to the next stage. We do not support async stages where one long running rule is running while the job itself moves on to the next stage.
  * Added ability to specify score of 0 to a rule
  * Improvement to Stat Rules to fail without exception when result is not within range&#x20;
* Profile
  * Fixed ability to remove a business unit from a dataset
  * Fixed issue where data concepts were not correctly displaying on a dataset's Profile page
  * Fixed sensitive labels not being assigned from Discovery
  * Treat certain doubles, floats, decimal types as Decimal format that preserves length and prevents Java from truncating to E11 format
  * Removed commas when displaying date columns &#x20;
* Security
  * SAML Login fix for IDPs that use POST binding as default
* S3
  * Enhanced support where "." in column headers were causing large jobs to not complete
    * Underscores now replace periods and large jobs should no longer hang
* Connections
  * Updated default Snowflake template connection properties
    * Corrected 'db' parameter placeholder on connection string versus former 'databaseName'
  * Added [BigQuery connection troubleshooting](connecting-to-dbs-in-owl-web/supported-drivers/connectivity-to-bigquery.md#views) information

#### Known Limitations

* Local files using NO\_AGENT require a valid $SPARK\_HOME on the machine where the web server is running.
* Supported data types
  * CLOB datatypes are unsupported
* Explorer
  * \-Addlib not yet supported for Remote Files e.g. S3

#### \[Informational Only] Changes To Metastore Made In 2022.01

```
ALTER TABLE owl_rule ADD COLUMN IF NOT EXISTS run_time_limit DOUBLE PRECISION NOT NULL DEFAULT 30.0;
ALTER TABLE owl_rule ADD COLUMN IF NOT EXISTS scoring_scheme INT4 NOT NULL DEFAULT 0;

ALTER TABLE job_log ALTER COLUMN stage TYPE character varying; -- stage set to varchar because RULE logs rule_nm into stage
ALTER TABLE job_log ALTER COLUMN log_desc TYPE character varying;
ALTER TABLE job_log ALTER COLUMN log_hint TYPE character varying;
```

## 2021.12

#### \*Note to Standalone Collibra DQ Customer Upgrades\*: We have upgraded to Log4J 2.17, please refer to [standalone-upgrade.md](installation/standalone/standalone-upgrade.md "mention") for additional steps

#### Enhancements

* Rules
  * Semantic and data concept management: Run Discovery feature
    * Run Discovery feature can be accessed from Catalog by selecting 'Data Concept' option from Actions or clicking the 'Run Discovery' button on the Rules tab of the DQ Job page. This will run a DQ Scan to detect for the semantics assigned to the selected data concept
    * Algorithm now selects best match if column matches 2 or more data classes based on % match and name distance
  * \*Tech Preview\* \[TP] Configurable rule break preview limit
    * Global default is 6 max rows per rule
    * Any change from 6 must be specified with previewLimit (API /v2/createrule) or in the Preview Limit field (UI)
    * Maximum of 50 from UI
  * Introducing additional Stat Rules including minPrecision, maxPrecision, minScale, maxScale
* Behavior
  * Min and max value checks are now triggered for all numeric columns when selected, even if column contains zeroes in lookback period
  * AR column view graph now shows theMean value for current day (runId). No re-run of DQ Job is necessary. The displayed Mean makes it clear that the % change is the % change from the mean, not runId - 1 day.
  * Findings in behaviors that were directly correlated to a row count shift as the root cause have been optimized, such that a major deviation in row count will no longer down-score related fields in the dataset to reduce noise
* Catalog
  * Catalog now features intelligent ranking based on Recency, Most Scanned, User
* Outliers
  * [Dynamic minimum history](dq-visuals/more/outliers.md#dynamic-history-options) allows for gaps in dates when establishing lookback period, which is established by history with row count > x (specified by user)
  * Fixed issue where outlier data preview graphics were not displayed
  * Fixed issue where outlier results did not honor the initial scope where clause, in particular for Remote Files (S3)
* Connections
  * BigQuery: Enhanced support for cataloging host name
* Pulse View
  * Pulse view can filter Connections and Users
  * Pulse view can serve as proxy verification on whether scheduled jobs were successfully completed
* Profile
  * Viewable precision and scale statistics for double, float, and decimal data types
* Shapes
  * Fixed issue where data shape preview not available when same shape is detected on the same row for different columns
* Files
  * \*Tech Preview\* \[TP] Users have ability to assign an agent when using temp file and local file Explorer paths
    * Known limitation: -master must be freeform appended to the agent or to each job
  * Support for multicharacter delimiters
  * Improved delimiter support to distinguish string commas versus actual CSV commas to align data to respective columns
* Agent
  * Fixed issue where certain completed jobs could not be re-run on the DQ Jobs page. In other words, NO\_AGENT was the only available option in the Agent dropdown. Now, users can select valid agents in the dropdown and this will persist for future scheduled jobs
* Schedule
  * Implemented validation to enforce user to choose days when picking schedule to avoid Java error messages
* Explorer
  * Fixed issue where '&' was not properly supported when adding additional parameters
* API
  * JSESSIONID session time is configurable
  * Bearer token and JSESSIONID authentication paths are properly forked
* Pattern
  * Patterns activity now shows Count (number of times the current dataset has the Pattern breaks). This Count is interpreted the same way as Outlier activity Count

## 2021.11

#### Enhancements

* Rules
  * \*Tech Preview\* \[TP] [Semantics and data concepts management](dq-visuals/rules/data-concepts-and-semantics.md)
    * The application now supports dynamic semantics checks. This allows you to create custom semantics that can be checked for when running a DQ check on a data set. Previously the application checked against a predefined set of semantics. You also have access to controls to organize and apply these semantics checks. The following is a list of changes:
      * There is a new data concepts management page. You can access it from Catalog or Admin Console. You can assign multiple semantics to a data concept.
      * When running a DQ check, you can select a data concept. The semantics assigned to this data concept will be checked against each column of dataset.
      * You have a list of predefined semantics that are not editable. You also have the ability to create/edit/delete custom semantics.
      * Repo on rules page has been added to Rules Library where semantics will be viewable.
* Resource Limits
  * You can edit the [Performance Settings](benchmarks/performance-settings.md) to supply limits to executors, cores, memory and cells so that a user can be warned if submitting a job that requires a lot of resources and admins can control maximum resources submitted.

#### Enhancements

* Explorer
  * \*Tech Preview\* \[TP] Dynamic query reload allows you to view JOIN query columns in other activities.
    * User can update and reload the schema table with the custom query in the scope section by clicking the \[Update Scope] button. It will enable using the new columns from the custom query in all activities (Profile, Outlier, Dupes, Patterns, Source)
    * Since the first tab is for compositing the query, updating fields will change the user's custom query. Therefore, all areas are locked except the "query" field in the first tab to keep the query unchanged after updating the scope table
  * Support for some special characters in table name.
  * Fixed the ability to add additional libs that were previously not being properly saved on subsequent runs. Under DQ Job tag, please utilize -fllb boolean (union lookback) and libsrc input box for lib directory path (will materialize as -addlib).
* Connections
  * \*Tech Preview\* \[TP] BigQuery Views and Joins
  * Please add the following to the BigQuery connection property

```
viewsEnabled=true
```

* API
  * You can perform multiple imports without conflicts.
  * You can have an incremental import such as updating matching records / insert new / leave existing. There is no requirement to delete tables first before running import.
* Profile
  * Fixed backrun timebin to work with weeks and quarters instead of days.
* Outliers
  * Split historical load to avoid historical query rounding up.
  * \*Tech Preview\* \[TP] [Dynamic minimum history](dq-visuals/more/outliers.md#dynamic-history-options).
* Source
  * Fixed an issue where settings were not sticky for subsequent runs.
* Security
  * SAML Enhancements
    * New [configuration settings](security/configuration/authentication-with-saml-idp/#set-the-saml-authentication-properties) are available when the Load Balancer is set for SSL Termination.
    * You can now set the [**RelayState** property](security/configuration/authentication-with-saml-idp/multi-tenancy-support-through-saml-relaystate.md) to route SSO to the proper tenant.

#### Patches

* 2021.11.1 Explorer
  * Allow ampersand in metastore host name for additional parameters&#x20;
  * In below example, support for ampersand needed for required SSL flags

```
metastore01.us-east1-b.c.customer-dq-prod.internal:5432/dev?sslmode=required&currentSchema=public
```

#### Known Limitations

* Rules
  * Semantics and data concepts:
    * Not supported in pushdown mode
    * Exporting RegEx semantics not currently supported
  * While it is possible to create joins and cross-dataset rules using Freeform SQL, it is best practice to create a view and handle the join prior to running the DQ Job.
* Behavior
  * Schema is not eligible for invalidate
* Files
  * Local files using UPLOAD\_PATH, UPLOAD\_FILE\_PATH, and temp files are only eligible to be deployed using the default NO\_AGENT option. These are only intended for quick tests and not intended for production-scale use. Best practice is to use a remote file system connection (S3, Google storage or ADLS).&#x20;
  * Delimiter support for special characters is limited.  Supported file delimiters are comma, pipe, tab, semicolon, double quote and single quote. Custom delimiters will work for many characters, but not all combinations.
  * Temp files and NO\_AGENT should have -master local\[\*] or -master spark://:7077 defined in freeform append of the agent options
* DQ Job
  * When submitting jobs via API from a different machine with a different timezone, timezone discrepancies are not accounted for automatically.  Best practice is to align each component to use UTC.
  * Jobs submitted via API with a run date that include HH:MM in the -rd (run date) will submit to the job queue and leave a remnant ‘STAGED’ job &#x20;
* Connections
  * Postgres limits max connections per spark job.  The default is 100. Please refer to Postgres official documentation how to increase max\_connection and shared\_buffers.
    * https://www.postgresql.org/docs/9.6/runtime-config-connection.html
  * BigQuery
    * Updating scope to include joins in BigQuery can only be materialized when tables are part of the same dataset collection
    * Should you receive an error for pre-existing BigQuery jobs, please add -dssafeoff to the cmd line or select ‘Allow Overwrite’ to enable this from Edit mode in the Explorer
* Alerts
  * After an upgrade to 2021.11, you may need to set the environment variable `ALERT_SCHEDULE_ENABLED=true` in **owl-env.sh** and restart **owl-web** to enable email alerts to work again.

## 2021.10

#### Enhancements

* DQ Job
  * Refactored DQ Job Score to Gauge Chart
* Explorer
  * Fixed issue where permissions are checked on datasets that do not yet exist
* Connections
  * Sybase 'Test / Preview' now available
  * Updated web model of saving additional connection properties
  * Fixed scenario where editing connection yields null instead of empty for multiple values
* Rules
  * Placeholder new searchable Rule Summary Page for Rule statistics / insights
* Alerts
  * Updated Alert Mailer to TLS 1.2 to resolve Third Party Error exception
  * Fixed issue where alerts are deleted even when clicking cancel button
* Behavior
  * Fixed issue where user must refresh to have invalidated item removed from UI
* Search
  * Fixed search on Audit Datasets and Dataset Management page
* Scorecards
  * Date ranges are now customizable
* Validate Source
  * Added feature that provides 'trim' option on String columns when running source-target validation, extra spaces in the cell are trimmed on both ends (left and right)
* Dupes
  * Resolved issue with white spaces in column headers blocking duplicate detection
* Security
  * Added configuration for setting the SAML\_ENTITY\_BASEURL, which sets the Consumer service url for the SP Metadata
* Shapes
  * Fixed issue where custom values override even after toggling Shapes back to auto or off
* Console
  * Fixed uncaught TypeError on login screen
  * Fixed GET timeout error on registration page
* Export/Import API
  * Users will be able to run the export/import API calls to conduct multiple promotions on the repo, schedule, and rule tables.

#### Patches

* 2021.10.1 Import / Export API without constraint conflicts
  * Import must match exactly to the format of our export in order to parse out columns and values to perform an update when existing records are already there

```
owl_rule
owl_check_repo
job_schedule
rule_repo
```

#### Known Limitations

* File sizes
  * Individual files greater than 5gb will experience performance degradation in Explorer for Standalone installs. Best practice is to save in smaller chunks and use bypass schema in the Explorer if needed.
  * Individual files greater than 25gb will experience performance degradation in Core for Standalone installs.
* Files
  * Explorer / browser will generally have difficulty supporting > 250 columns in files
* Profiling
  * Pushdown profiling on Bigquery, Redshift, Athena and Presto is available for specific datatypes.
  * Backrun option and flag will persist beyond the first run (-br). Please remove this flag if you do not want to backrun again.
* Explorer
  * QUARTER and WEEK are not supported time bins in this release.
  * On non-csv files, Explorer will not automatically infer file types. Users must change file type to the required value and click Step 2 "Load File". Nothing will change in Step 1 "File Information". A future enhancement will be added to automatically check filetypes by reading the first file
  * Dataset names should not contain special characters
* Rules
  * Out of the box semantic rules cannot be edited (STATECHECK, GENDERCHECK, etc). Users can still apply their own global rules which can be customized.
  * LinkId does not support alias columns that are not part of the -LinkId definition
* Connections
  * Connection names should not contain spaces
* Validate Source
  * Complex Validate Source queries can only be edited from the CMD line or JSON directly before hitting Run.
* Security
  * Active Directory in Azure SQL can connect via LDAP (basic auth) or Kerberos.
* S3 / GS / ADLS
  * Remote storage connections should be defined using the root bucket only.
* Estimate Job is only available for files when Livy is being used.
* Stop Job on jobs page is limited and does not work for all installation types.
* Bigquery connector does not work with views

## 2021.09 (09-2021)

#### New Feature

* Alert
  * Alert notification page displaying a searchable list of alerts emails sent. [Email Alerts](workflows/email-alerts.md#example-alert-in-your-inbox)
* Job Page
  * UI refresh
  * New chart with successful and failed jobs

#### Enhancements

* Profile
  * When faced with a few errors e.g. 0.005% null, highlight issues more clearly and visibly instead of the notion of rounding up to and displaying 100.0%
* Jobs
  * Enhanced query and file date templating and variable options. This allows easier scheduling and programmatic templating for common date variables
  * Job Template corrupt time portion of ${rd} on last run of replay
  * Refactor job actions column
* Catalog
  * Completeness report refactor / consolidation to improve performance
* Export
  * Outlier tab in DQ Job page (hoot page) displays linkIds and included in the export
* Security
  * Added property for authentication age to reduce token expiration
  * UI labels more generic when configuring a connection with password manager script
* Agent
  * Agent no longer shows as red if services are correctly running
* Logging
  * Jobs log retention policy now configurable in Admin Console -> App Config via "JOB\_LOG\_RETENTION\_HR" (variable must be added along with value). If not added, default to 72 hours
  * Platform logs retention policy now configurable in Admin Console -> App Config via "PLATFORM\_LOG\_RETENTION\_HR" (variable must be added along with value). If not added, default to 24 hours
* Outliers
  * Fixed connection properties behavior given how multiple custom properties are handled in Hive
  * Fixed outliers issue that ignored WHERE clause on remote files
* Scorecards
  * Fixed missing search results issue in list view for Patterns type
* Connections
  * New templates for Redshift and Solr
* Connections Security
  * Ticket Granting Ticket (TGT) authentication for HDFS & Hive
    * You can now choose the TGT auth model for connections and point to a TGT file as an additional kerberos authentication model
  * Kerberos Principal + Password Manager for Hive
    * You can now use a password manager script to fetch a hive password for a princiapl to authenticate
  * S3 SAML Auth (TP)
    * DQ is configured to use SAML based authentication to S3 buckets with password manager or provided credentials. Testing is limited to OneLogin for SAML Provider in this tech preview release

**Patches**

* 2021.09.1 Validate Source
* 2021.09.2 Validate Source Large DB load
* 2021.09.3 Save on datashapes from new DQ Job

## 2021.08 (**08-2021)**

_Please note updated Collibra release name methodology_

#### Enhancements

* Explorer
  * Support for handling large tables
  * Implemented pagination function for navigation
  * Improved error handling for unsupported java data types
  * Fix preview for uploaded temp files
* Collibra DQ V3 REST APIs
  * Additional rest APIs for easier programmatic job initiation, job response status, and job result decisioning (used in pipelines). Streamlined documentation and user inputs allow users to choose any language for their orchestration wrapper (python, c#, java, etc). [More info on Collibra DQ Rest APIs](https://docs.owl-analytics.com/rest-api/apis)
* Patterns
  * Fix load query generation issue when WHERE clause is specified
* Behaviors
  * Fix behavior score calculation after suppressing AR
  * Fix percent change calculations in behavior AR after retrain
  * Mean Value Drift \[New Feature] [Behaviors](dq-visuals/behaviors.md#using-behavioral-analytics-change-detection)
* Security
  * Introduce new role of ROLE\_DATA\_GOVERNANCE\_MANAGER with ability to manage (create / update / delete) Business Units and Data Concepts. [More info on Collibra DQ Security Roles](https://docs.owl-analytics.com/v/2021.08/security/owl-security/role-based-access-control-rbac)
  * Relaxed field requirements for password manager connections for App ID, Safe, and Password Manager Name
* Scorecard
  * Enhanced page loading speeds for scorecard pages
* Rules
  * Rule activity is now more efficiently parallelized across available resources
* Validate Source
  * Pie chart will highlight clearly visible ‘issue’ wedge for anything less than 100%
* UI/UX
  * Updated with more distinct icon set

## 2021.07 (**07-09-2021)**

_Please note updated Collibra release name methodology_

#### Enhancements

* \*Tech Preview\* \[TP] [Collibra Native DQ Connector](integration/dq-connector.md)
  * No-code, native integration between Collibra DQ and Collibra Catalog
* UX/UX
  * Full redesign of web user experience and standardization to match Collibra layout
  * Search any dataset from any page
* Hoot
  * Rules Display with \[more] links to better use the page space
  * Auditing for changes per scan
* Explorer
  * JDBC Filter enablement by just search input
* Profile
  * Add more support for data-concepts from UI or future release
* Behaviors
  * Down-training per issue type
  * AR user feedback loop (pass/fail) for learning phase
* Scheduler
  * [Time based cleanup routine](https://docs.owl-analytics.com/data-retention/time-based-data-retention)
* Security
  * SQL View data by role vs just Admin
* Reports
  * OTB completeness reports from reports section. [Completeness Report](reports/built-in/completeness-report.md)

## 2.15.0 (**05-31-2021)**

#### Enhancements

* Hoot
  * Down-training per activity vs globally
* Logging
  * Expose server logs on the jobs page from the agent and cluster
* Explorer
  * Enhanced Experience for display of stats for database tables
  * Validation for Dupes section to ensure all input is validated before save
  * Support for edit mode with Dremio connections
  * Allow file scan skip-N to skip a number of rows if extra headers are present in the file
  * Support Livy sessions over SSL for files
* Profile
  * Add quick click rules based on profile distribution stats
* Behaviors
  * Down-training per issue type
* Scheduler
  * Support for $rdEnd in the template
  * Auto update schedule template based on last successful run
  * Support S3 custom config values in scheduled template
* Security
  * SAML Auth
  * Support for JWT Authentication to the Multi-Tenant management section
* Multi-Tenant
  * Support for an alternate display name for each tenant to be displayed in the UI and login tenant selection

## 2.14.0 (**03-31-2021)**

#### Enhancements

* Hoot
  * Edit mode on Password Manager supported connections
  * Edit mode on complex query
  * Behavior chart display of last 2 runs
* Explorer
  * ValSrc auto Save
  * Remote File
    * Support for Google Cloud Storage (GCS)
    * Support for Google Big Query
    * Folder Scans in Val Src
    * Auto generate ds name
    * FullFile for S3
    * {rd} in file path naming
    * Estimate Jobs (Only on K8s)
    * Analyze Days (Only on K8s)
    * Preview Data (Only on K8s)
* Connection
  * Store source name to connect a column to its source db/table/schema
  * Custom driver props for remote file connection
* Profile
  * Filtergrams for Password Manager connections
  * Filtergrams for Alternate agent path connections
  * Filtergrams on S3/GCS data source (Only on K8s)
* Rules
  * UX on page size options
* Scheduler
  * Support multiple db timezone vs dataset timezone
* Outliers
  * Notebook API returns true physical null value in DataFrame instead of string "null"
* Shapes
  * Expanded options for numeric/alpha
  * Expanded options for length on alphanumerics

## 2.13.0 (**12-20-2020)**

#### Enhancements

* Schema
  * Notify of quality issue on special characters in column names
* Shapes
  * Shape Top-N display in profile
* Behaviors
  * Chart enhancements including visible Min/Max ranges on AR drill in
  * Force pass/fail at AR item level
* Explorer
  * Menu driven selections on existing datasets
  * Run remote file scans at parent folder level
* Scheduler
  * Allow scheduling based on dataset timezone (previously all UTC)
* Profile
  * Enhanced Drill in display including new AR view & Shape Top-N values
  * Data Preview Filtergram Export of distinct column values
* Validate Source
  * Additional UI parameters exposed: File Type/ File Delimiter
  * Edit support in Explorer Wizard step
  * Grouped display on Hoot Page with aggregate statistics
* Business Units
  * Organize datasets by [business-units](https://docs.owl-analytics.com/observation-assignments/business-units) visible in catalog and profile views
* Hoot Page
  * Ability to Clone datasets from a given dataset run
* Rules Page
  * Allow Vertical Resize
* Catalog
  * Searchable filters for: rows, columns, scans, and more
* Performance
  * 2X faster on data loading activity based on revised caching and surrogate I

# Release Notes

## 2021.11 (In Progress)

#### New Features

* Rules
  * \*Tech Preview\* \[TP] [Semantics and data concepts management](dq-visuals/rules/data-concepts-and-semantics.md)
    * The application now supports dynamic semantics checks. This allows the user to create custom semantics that can be checked for when running a DQ check on a data set. Previously the application checked against a pre defined set of semantics. Controls to organize and apply these semantics checks have also been added. The following is a list of changes:
    * A new data concepts management page has been added. This can be accessed from catalog or admin console and the user can assign many semantics to a data concept.
    * When running a DQ check the user can select a data concept. The semantics assigned to this data concept will be checked against each column of dataset.
    * Users will have a list of pre defined semantics that are not editable. They will also have the ability to create/edit/delete custom semantics.
    * Repo on rules page has been added to Rules Library where semantics will be viewable.

#### Enhancements

* Explorer
  * \*Tech Preview\* \[TP] Dynamic query reload allows you to view JOIN query columns in other activities
  * Support for some special characters in table name
  * Fixed ability to add additional libs that were previously not being properly saved on subsequent runs. Under DQ Job tag, please utilize -fllb boolean (union lookback) and libsrc input box for lib directory path (will materialize as -addlib)
* Connections
  * \*Tech Preview\* \[TP] BigQuery Views and Joins Preliminary Support
* API
  * Allows multiple imports without conflicts
* Profile
  * Fixed backrun timebin to work with weeks and quarters instead of days
* Outliers
  * Split historical load to avoid historical query rounding up
  * \*Tech Preview\* \[TP] Minimum / ragged history
* Source
  * Fixed issue where settings were not sticking
* Security
  * _SAML Enhancements_

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

* Collibra Native DQ Connector
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
  * OTB completeness reports from reports section. [Completeness Report](reports/completeness-report.md)

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
  * 2X faster on data loading activity based on revised caching and surrogate ID.

## 2.12.1 (11-1-2020)

#### Stability Enhancements

* Pattern
  * Pattern no longer overflows when too many keys are selected
  * Fix for Pattern Activity failing when no key is provided
  * Pattern now inherits its default values from the first record
* Dupe
  * Fix Dupe Case Sensitivity toggle in Wizard
* Shapes
  * Fix Shape settings being overridden
* Outlier
  * Improved validation for Outlier definition in Explorer
  * Outlier now inherits its default values from the first record
* Behaviors
  * Behaviors row count modal now correctly clears previously viewed topN and bottomN results
* Explorer
  * Fix for specifying the file type for Local and Temporary files
  * Remove hardcoded file limit of 30MB for temp files
  * Datasets can no longer be renamed in edit mode
  * Backrun is now off by default when a job is edited
  * Pattern reload now correctly displays on/off status
  * Explorer banner is now properly displayed
  * Fix for agent list not refreshing after clicking the Refresh icon
  * Fix for Analyze date field in Athena
  * Explorer now runs analyze based on transform if it is selected
  * Fix for job estimator in Athena
* Scheduler
  * Fix Kerberos authentication for scheduled jobs running on Hive
  * PwdMgr now gets connection details by tenant for scheduled jobs
  * Scheduled jobs modal now properly displays the status of the last three jobs
* Alert
  * Alert setup no longer breaks OwlCheck jobs
* Backend
  * Fix for handling reserved word 'date' in Hive.
  * Generic template is now displayed by default, even when no other connection templates have been defined
  * MIN/MAX Load Time now defaults to Off
* Install
  * Version bump and rpm style installation for a local postgres in the Owl install script

## 2.12.0 (10-01-2020)

**Enhancements**

* Rule Page Builder Enhancements
  * Native Rule Updates (push-down)
  * Rule Freeform Section Usability
  * Run with default Agent
* AWS S3 Role Based Authorization
  * Leverage Instance Profile to assume a Role for authorization of S3 access
* Enable LinkID in Owlcheck Explorer
  * Designate a column that contains a unique record identifier. The value contained in this column will be captured and stored along with DQ findings. This identifier enables data stewards to quickly find and remediate DQ findings in the source data.
* Wizard driven windowed aggregates on datasets
  * A user can apply a SUM(DURATION) OVER (PARTITION BY GRADE)
* Bulk Delete From CatalogSecurity admin role
  * A user can bulk delete based on time since last run, # of total runs.
* Rule Breaks to allow for different columns
  * A user can apply a rule that has different columns and we catch exception gracefully
* Edit OwlCheck created from CLI
  * Allow Edit for Owlchecks initiated from CLI instead of directly from OwlDQ Explorer.
* Explorer Edit on File Data Source
  * Ability to edit existing Olwchecks created on remote and local files. Expanded capabilities for editing Owlchecks on JDBC sources
* Edit Score Card capabilities
* Search and index dataset\_schema col in CATALOG
* Notebook API - Expanded Outliers and Patterns Results Outliers output displays
  * Key Column names and an aggregate view that merges duplicate Outlier findings to display the number of occurrences. Patterns aggregate output denotes columns not relevant to a given finding.
* TECH PREVIEW - Kubernetes Support (V1)
  * Deploy OwlDQ and run Owlchecks on Kubernetes
* TECH PREVIEW - Streaming Owlchecks - SSL Authentication
  * Run Streaming Owlchecks on Kafka topics protected by 2-Way SSL
* TECH PREVIEW - Validate Source Drill-in
  * Source activity shows more details regarding source findings. Currently view-only. Use the existing table for invalidation.

## 2.11.0 (8-1-2020)

**Enhancements**

* Notebook API Enhancements
  * Support @dataset and @t1 syntax in freeform SQL for business rules
  * Multiple Outlier definitions supporting full object
  * Multiple Pattern definitions supporting full object
  * Display full rulebreak rows in output Dataframe
* Owlcheck Wizard supports multiple Outlier grouping with different keys
  * Wizard supports definition of multiple distinct Outlier definitions using includes and keys
* Owlcheck Wizard supports multiple Pattern grouping with different keys
  * Wizard supports definition of multiple distinct Pattern definitions using includes and keys

## 2.10.1 (6-1-2020)

**Enhancements**

* Scheduler Enhancements ([docs](https://docs.owl-analytics.com/scheduler/schedule-management))
  * Manage Schedule Restricted Times
  * Schedule Jobs By quarter
  * UX Mods on Schedule Template Save From Hoot
  * Optional Schedule Save with custom Run Date for Reporting/Charting
* Alert Enhancements ([docs](https://docs.owl-analytics.com/alerts/email-alerts))
  * Setup alert batches for quick distribution list and consolidated alerts per dataset
  * Configure all alerts to run via OwlWeb
* Behaviors ([docs](https://docs.owl-analytics.com/dq-visuals/behaviors))
  * Ability to suppress behavior items
  * UX modal enhancement for additional display values (chart/top-N/functions)
* Jobs ([docs](https://docs.owl-analytics.com/apis/job-server))
  * Export All (export all checkbox)
  * Detailed logging per job (click jobs link)
* Scorecard Pages
  * Require Page Name
* Rules UX Enhancements ([docs](https://docs.owl-analytics.com/dq-visuals/rules))
  * Required/Non-Required Styling
  * Display with ellipsis on long rule names in hoot findings

**Known Issues**

* Auto Profile AGENT status indicator (GREEN/RED) missing
* Can not run multiple patterns or outliers from UX on Tech Preview explorer2

## 2.10.0 (5-1-2020)

**Features**

* Assignment Queue ([docs](https://docs.owl-analytics.com/observation-assignments/assignment-queue-s))
  * Assign review and resolution of data quality issues to responsible users
  * Push assignments to Service Now
* Rules Features ([docs](https://docs.owl-analytics.com/dq-visuals/rules))
  * Enriched Regex Builder to assist in Rule definition
* Auto Profile Phase 2 ([docs](https://docs.owl-analytics.com/dq-visuals/profile/autoprofile))
  * Schema filter (option to limit fields profiled per table)
  * Profile Pushdown (push compute to data warehouse)
  * Scan concurrency throttle (limit number of simultaneous Profiling jobs)
  * Date filter (option to focus profiling to a date orange per table)
* Profile UX Enhancements ([docs](https://docs.owl-analytics.com/dq-visuals/profile))
  * Add Business terms/descriptions to profiled columns
  * PII/MNPI designations automagically identified by Owl (Profile Semantic) can be removed by the user from the dataset Profile screen
  * One click to create a rule based on TopN values
* Catalog UX Enhancements ([docs](https://docs.owl-analytics.com/catalog/catalog))
  * List of Actions to edit/govern datasets
  * Publish Dataset
* Explorer 2 Enhancements ([docs](https://docs.owl-analytics.com/dq-visuals/explorer-2))
  * Support for HDFS
  * Support for ad-hoc files
* Pushdown Processing to the Data Warehouse storing the data ([docs](https://docs.owl-analytics.com/dq-visuals/profile))
  * Push compute of Profile to the Data Warehouse where the data is stored
  * Push compute of Validate Source to the Data Warehouse where the data is stored. Schema and Row Counts only, validate values functionality not supported when pushdown is enabled
* Outliers ([docs](https://docs.owl-analytics.com/dq-visuals/outliers))
  * Functionality (Categorical Outliers)
    * Categorical Outliers take history into account when date column is provided
    * Categorical Outliers offers visualization of Most frequent along side of the Outlier for context
  * Performance (Numerical Outliers)
    * Improved performance when limit on number of Outliers is increased
    * improved performance when No Date and/or Key is provided
    * Outlier key values are delimited by a user defined delimiter (\~\~ by default)
* Validate Source ([docs](https://docs.owl-analytics.com/dq-visuals/validate-source))
  * Improved performance when validate values function is enabled
* Behaviors ([docs](https://docs.owl-analytics.com/dq-visuals/behaviors))
  * Control behavior module by subtype
* Notebook API
  * option.keyDelimiter - Outlier key values are delimited by a user defined delimiter (\~\~ by default)
  * option.coreMaxActiveConnections - Maximum number of threads that an Owlcheck metastore connection pool contain. This option is only honored when the connection pool first initializes (Typically when the Spark Session first initializes).
  * option.profile.behaviorRowCheck - Controls if behavioral model factors in row count stats
  * option.profile.behaviorTimeCheck - Controls if behavioral model factors in load time stats
  * option.profile.behaviorMinValueCheck - Controls if behavioral model factors in min value stats
  * option.profile.behaviorMaxValueCheck - Controls if behavioral model factors in max value stats
  * option.profile.behaviorNullCheck - Controls if behavioral model factors in Null count stats
  * option.profile.behaviorEmptyCheck - Controls if behavioral model factors in Empty count stats
  * option.profile.behaviorUniqueCheck - Controls if behavioral model factors in Cardinality count stats
* Caching Efficiency
  * Improved efficiency of memory usage

**Known Issues**

* Estimate Jobs function may produce suboptimal configuration
* Kerberos Exception when attempting to generate preview for JSON/XML files on HDF
* Auto Profile AGENT status indicator (GREEN/RED) missing

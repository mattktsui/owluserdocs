---
description: Setup and Configuration
---

# Time Based Data Retention

## **Setting up Retention Based Data Purge**

Retention based purge of data can be turned on to allow data to automatically be cleaned based on an organization's data retention policy.

### **Benefit**

Once enabled, what type of data is removed?

* Dataset statistics
* Data\_Preview
* Dataset\_Field
* Rule\_Breaks
* Job Ledger

### **Setup**

In order to set up retention based data purge, three (3) environment variables need to be set up in the owl-env.sh configuration script.  Note:  a restart of the webapp is required for this configuration to take place.

* **cleaner\_retention\_enabled**
  * TRUE or FALSE on whether this feature is enabled
* **cleaner\_retention\_days**
  * Number of days to retain data
* **cleaner\_retention\_field**
  * Controls which field to use to select eligible dataset runs
  * Potential values
    * updt\_ts:  consider the last time a dataset run was updated
    * run\_id:  consider the run id field of the dataset

### Configuration

**Example configuration in owl-env.sh**

Organization wants to purge data where the updt\_ts is more than 1 year old

**In owl-env.sh, add the following lines**

```
export cleaner_retention_enabled=TRUE
export cleaner_retention_days=365
export cleaner_retention_field="updt_ts" 
```

### Config Map

```
autoClean: "false"
cleaner_retention_days: "180"
cleaner_retention_field: updt_ts
cleaner_retention_enabled: "true"
```

### Defaults for Auto Clean Process

{% hint style="info" %}
This is a separate rolling purge that is **distinct from the time-based retention.** This is **on by default** and uses the pre-defined limits below.  You will see audit records for this clean-up process in the audit history of the admin console.
{% endhint %}

Separate from the time-based retention there is also a default auto clean mechanism that actively purges your old records.  This is enabled by default and can be modified by use of the autoClean (AUTOCLEAN) boolean parameter.&#x20;

```
AUTOCLEAN=false or autoClean="false" 

### Depending whether this is part of owl-env.sh 
### or the configMap of the web pod
```

These are the defaults. The row count threshold is the global limit when this is triggered.  This is based on the records in the data\_preview table.  The runs threshold and the dataset per row threshold are dataset-level limits that require a dataset to have at least 4 scans and at least 1000 rows.

This is an example using the owl-env.sh file to control these settings.

```
export AUTOCLEAN=true
export DATASETS_PER_ROW=1000
export RUNS_THRESHOLD=4
export ROW_COUNT_THRESHOLD=200000
```

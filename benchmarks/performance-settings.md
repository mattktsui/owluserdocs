# Performance Settings

### Job Limits

Limits can be set to limit resources that are requested.  There are options for cores, memory, executors, and cells (maxexecutorcores, maxexecutormemory, maxnumexecutors and maxcellcountforparalleljdbc)&#x20;

![](../.gitbook/assets/limits.gif)

If you request more cells than the limit, the user should see a warning message before hitting run.&#x20;

![](<../.gitbook/assets/image (99).png>)

### Agent Defaults

Set defaults at the agent level.  These should be right-sized to your environment and be used as defaults for jobs with when estimate is not available (primarily local files and remote files).

![](<../.gitbook/assets/image (103).png>)

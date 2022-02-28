---
description: >-
  With Native SQL expressions we provide capability to use your existing
  validation statements, even if they are using database specific
  (Postgre/DB2/Oracle/MSSQL/etc...) functions or expressions.
---

# Native

This is commonly used when using pushdown profiling and/or pre-existing SQL validations exist in a specific syntax.  Native rules are often referred to as pushdown rules.

![](<../../../../.gitbook/assets/image (113).png>)

If you have rules already written in Oracle, Sybase, or DB2 syntax - Copy/Paste the rule directly into the Native SQL section.&#x20;

When creating a Native SQL rule, keep the following in mind:

* The SQL query must be a valid expression that can be run as a subquery. To avoid pulling large amounts of data into memory, Collibra DQ will wrap your expression so it only fetches the number of rows returned. Rules should be written such that the query returns the anomalous rows.
* The SQL query must take less than 30 minutes to run. It is recommended to use partitioned columns for efficiency.
* When testing the SQL query from the app, it is helpful if it take less than 30 seconds to run. You can add a limit to reduce query time, or test the query in your SQL Editor.

{% hint style="info" %}
Testing native rules can be done quickly by limiting the results or using an external SQL IDE as well.
{% endhint %}

{% hint style="warning" %}
At this rule type you won't have mismatch highlighting and record breakdown on the UI, just the score itself!&#x20;
{% endhint %}

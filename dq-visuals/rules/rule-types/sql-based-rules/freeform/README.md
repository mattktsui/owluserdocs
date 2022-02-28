---
description: Fully defined SQL for more detailed checks
---

# Freeform

Where 'Simple' rules just use the condition, 'Freeform' rules use the complete SQL statement. When more complex SQL is required, you can express more with Freeform including joins, CTE's and window statements.

```
select * from @DATASET_NAME where 
email_address is not null and email_address != '' 
```

{% hint style="danger" %}
Freeform rules should include a semi-colon at the end of the rule value.
{% endhint %}

{% hint style="info" %}
All built-in spark functions are available to use. ([https://spark.apache.org/docs/2.3.0/api/sql/](https://spark.apache.org/docs/2.3.0/api/sql/)) for simple and freeform sql rules.‌
{% endhint %}

### Cross-Connection Libraries

![](<../../../../../.gitbook/assets/image (141).png>)

{% hint style="warning" %}
When applying cross-connection rules please use the -addlib to submit the job with the appropriate jar files.  In this example, a secondary set of jars is added through the Explorer. These files are located in the /opt/owl/drivers/mysql directory. The path should not contain double quotes or single quotes.  It should point to a directory without spaces in the path.
{% endhint %}

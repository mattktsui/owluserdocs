---
description: Just the condition after the "where" clause
---

# Simple

Depending on the complexity, users can choose from short form or long form rules. 

#### **Simple** 

Just the condition (short form).  For example, using the column email_address. This runs against the dataframe and uses Spark SQL syntax.  An easy way to think about Simple rules is 'everything after the where clause'. 

```
email_address is not null and email_address != '' 
```

{% hint style="info" %}
All built-in spark functions are available to use. ([https://spark.apache.org/docs/2.3.0/api/sql/](https://spark.apache.org/docs/2.3.0/api/sql/)) for simple and freeform sql rules.‌
{% endhint %}

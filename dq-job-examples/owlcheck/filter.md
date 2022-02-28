---
description: Similar to a grep for limiting a dataframe to rows containing a substring
---

# Filter & Filter Not

{% hint style="info" %}
This feature should only be used when -q (query) and -fq (filequery) are not applicable.  This feature is primarily used with raw files for limited filtering and not advanced conditional logic.
{% endhint %}

## Example

```bash
./owlcheck \
-ds "dataset_name" \
-rd "2018-07-23 10" \
-d "," \
-f "/Users/Documents/file.csv" \
-filter "2018-07-23"
```

{% hint style="info" %}
**-filter "2018-07-23"**

If file.csv contained multiple strings, but you only wanted rows containing "2018-07-23"
{% endhint %}

## The inverse

{% hint style="info" %}
**-filternot "2018-07-23"**

To exclude rows containing "2018-07-23"
{% endhint %}


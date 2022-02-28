# Rule Types

## SQL-Based Rules

Depending on the complexity, users can choose from short form or long form rules.&#x20;

#### **Simple**&#x20;

Just the condition (short form).  For example, using the column email\_address. This runs against the dataframe and uses Spark SQL syntax.  An easy way to think about Simple rules is 'everything after the where clause'.&#x20;

```
email_address is not null and email_address != '' 
```

#### Freeform

Where 'Simple' rules just use the condition, 'Freeform' rules use the complete SQL statement. When more complex SQL is required, you can express more with Freeform including joins, CTE's and window statements.

```
select * from @DATASET_NAME where 
email_address is not null and email_address != '' 
```

{% hint style="info" %}
All built-in spark functions are available to use. ([https://spark.apache.org/docs/2.3.0/api/sql/](https://spark.apache.org/docs/2.3.0/api/sql/)) for simple and freeform sql rules.‌
{% endhint %}

#### Native

Native rules use the SQL dialect of the underlying connection and database.  Files are not eligible for native SQL rules.  This is ideal if you want to use push-down profiling and you want to use existing SQL logic.  When coupled with push-down profiling, you can achieve a very minimal infrastructure footprint.

See the [native rules section](sql-based-rules/native-sql.md) for more details.

## Stat

Write rules against meta data and profiling stats.  Complex counts and ratios can be referenced with simple syntax. &#x20;

See the[ stat rules section ](stat-rules/)for more details.

### Data Type

* **Empty check**
  * Rule type: EMPTYCHECK
  * Description: Checking whether the target column has empty values or not
* **Null check**
  * Rule type: NULLCHECK
  * Description: Checking whether the target column has _NULL_ values or not
* **Date check**
  * Rule type: DATECHECK
  * Description: Checking whether the target column has only DATE values or not
* **Integer check**
  * Rule type: INTCHECK
  * Description: Checking whether the target column has only INTEGER values or not
* **Double check**
  * Rule type: DOUBLECHECK
  * Description: Checking whether the target column has only DOUBLE values or not
* **String check**
  * Rule type: STRINGCHECK
  * Description: Checking whether the target column has only STRING values or not.
* **Mixed datatype check**
  * Rule type: DATATYPECHECK
  * **Description:** ---




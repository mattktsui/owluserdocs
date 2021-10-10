---
description: >-
  In this section you can learn how to work with Rules in Notebooks written in
  Scala.
---

# Owl Rules - DQ Pipeline

## Instantiation

| Code                                     | Description                                                                                                                                               |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| val rule = new Rule()                    | Instantiating a Rule object                                                                                                                               |
| rule.setDataset(_\<DATASET>_)            | Adding the name of the dataset                                                                                                                            |
| rule.setRuleNm(_\<RULE_NAME>_)           | Adding the name of the given rule                                                                                                                         |
| rule.setRuleValue(_\<RULE_EXPRESSION>_)  | Setting the simple _RULE_EXPRESSION_                                                                                                                      |
| rule.setRuleType(_\<RULE_TYPE>_)         | Setting the rule type                                                                                                                                     |
| rule.setPerc(_\<RULE_PERCENTAGE>_)       | Setting the percentage                                                                                                                                    |
| rule.setPoints(_\<RULE_POINT>_)          | <p>Setting how many points<br>will be deducted from total<br>for each percentage</p>                                                                      |
| rule.setIsActive(_\<RULE_IS_ACTIVE>_)    | <p>Making rule active/inactive</p><p>Possible values:</p><ul><li>ACTIVE: <strong>1 / true</strong></li><li>INACTIVE: <strong>0 / false</strong></li></ul> |
| rule.setUserNm(_\<RULE_OWNER_USERNAME>_) | Adding the owner                                                                                                                                          |

## Rule types

{% content-ref url="sql-based-rules/" %}
[sql-based-rules](sql-based-rules/)
{% endcontent-ref %}

{% content-ref url="global-rules.md" %}
[global-rules.md](global-rules.md)
{% endcontent-ref %}

{% content-ref url="data-type-based-rules.md" %}
[data-type-based-rules.md](data-type-based-rules.md)
{% endcontent-ref %}

## Requirements

#### Required imports

```scala
import com.owl.core.Owl
import com.owl.core.util.OwlUtils
import com.owl.common.options.OwlOptions
import com.owl.common.{Props, Utils}

import com.owl.common.domain2.Rule

import org.apache.spark.sql.functions._
```

#### SparkSession initialization

DataBricks and other notebook execution frameworks are working with managed/shared spark session, therefor we recommend to use this code snippet in your notebook to initialize the current spark session properly.

```scala
//----- Init Spark ----- //
def sparkInit(): Unit = {
  sparkSession = SparkSession.builder
    .master("local")
    .appName("test")
    .getOrCreate()
}
```

{% hint style="danger" %}
Don't call **spark.stop** at any of your notebooks, otherwise the execution engine will exit immediately!
{% endhint %}

{% hint style="warning" %}
Make sure OwlContext is **already** created before using any method from OwlUtils!
{% endhint %}


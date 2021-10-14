---
description: Ideal for rules that apply to more than one dataset. Write once, apply many.
---

# Rule Templates

Templates are great for regex, format, and compliance checks. 

A template rule will substitute the dataset and column at runtime. This commonly saves hundreds of redundant rules that do the same thing but on different column names.

Templated rules can be found in the 'type' dropdown as well as the 'quick rules' drop-down.  The complete list of template rules is located in the Rule Library section. These meant for global rules that are ideal for code sets, compliance checks, and regex checks. These are ideal for checks that apply to many tables. 

Rule templates will utilized SQLG (simple) and occasionally SQLF (Freeform) types under the hood. Rule templates will appear in the Rule Library after they are created. 

See the [rule library section](dq-rule-automation.md) for more details.

{% hint style="info" %}
Customized discovery routines can be run using the [rule library](rule-templates.md#rule-library) together with [data concepts and semantics.](data-concepts-and-semantics.md)
{% endhint %}

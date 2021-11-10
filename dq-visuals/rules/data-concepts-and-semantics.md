---
description: >-
  Custom data discovery and enforcement using rule templates (data concepts and
  semantics)
---

# Rule Discovery

## Data Concepts

A data concept is the class or family of a dataset for example:  _Loan Data, Stock Data, Position Limit Data, Retail Product Data, Patient Health Data, Interest Rate Data, etc... _By giving data classes or "classifying" datasets we can transfer common understanding, rules and ML to datasets. This powerful technique allows a data steward to set up concepts once and enables the entire organization the ability to unify and standardize on common rules and terms, solving many metadata scale challenges.

{% hint style="info" %}
Dataset Level

**Security Reference Data **- Bloomberg financial data**                                                                      Home Loan Data** - Mortgage application data
{% endhint %}

## Semantics

{% hint style="info" %}
Column Level

EMAIL, ZIP CODE, SSN, CUSIP, GENDER, ADDRESS, CURRENCY CD, SKU, EIN, IP ADDRESS, PHONE, LICENSE, VIN, CREDIT CARD
{% endhint %}

A semantic is the "semantic type" of a column or attribute of a dataset.  All columns have a physical type such as String, Int, Date etc... but the semantic understanding of what type of String is in the column can be very important.  I also allows us to enforce DQ validation rules out of the box.&#x20;

Owl's semantic scanning self identifies standard columns and automatically provides the proper protection. This makes it easy to get started adding common rules for specific use-cases.&#x20;

**Owl offers out of the box rules for 1-click rule creation**

![](../../.gitbook/assets/auto-rules.png)

## Sensitive Data

{% hint style="info" %}
Column Level

**PII** - personally identifiable information                                                                                             **MNPI** - materially non public information\
**PCI** - credit information like a credit card number                                                                              **PHI** - Hippa medical information
{% endhint %}

## Data Discovery: The Power of Combining All Three into One Domain&#x20;

{% embed url="https://www.youtube.com/watch?v=ahfIe3Qv9SU" %}

Now imagine if you could classify your datasets as concepts, then automatically have all the columns be recognized semantically(with validation rules in place) as well as have the columns labeled with sensitivity tags.  It might look something like the below.

![](../../.gitbook/assets/screen-shot-2021-09-15-at-1.11.06-pm.png)

## Administering Data Concepts

Setup your data concepts once and let the entire organization benefit by unifying all datasets to a common understanding in the admin Data Concepts page.&#x20;

![](../../.gitbook/assets/screen-shot-2021-09-15-at-1.14.42-pm.png)

## Physical Schemas to Semantics

Below you can see the benefit of organized metadata.  PDEs or `physical data elements` organized/tagged by semantics.  This allows for sub-second searches while in catalog or searching for data to figure out where all your PII data lives, or what systems have "loan data".

![](../../.gitbook/assets/screen-shot-2021-09-15-at-4.32.09-pm.png)

Above you can see Data Concepts in Yellow, Semantics in Gray and Sensitive labels in Orange.  Enabling you to organize all your data in classes, search and discover types no matter what system they live in or what the PDE column name is.  Transforming technical types into business metadata.

## Business Unit Roll up Reporting

Now that we have all PDEs discovered and tagged and rolled up into business terms, we can roll up technical assets like database tables and files into business reports across departments and non technical concepts.

![](../../.gitbook/assets/screen-shot-2021-09-15-at-5.17.14-pm.png)

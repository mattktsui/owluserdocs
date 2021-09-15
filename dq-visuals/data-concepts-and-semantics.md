# Data Concepts and Semantics

## Data Concepts

A data concept is the class or family of a dataset for example:  _Loan Data, Stock Data, Position Limit Data, Retail Product Data, Patient Health Data, Interest Rate Data, etc..._ By giving data classes or "classifying" datasets we can transfer common understanding, rules and ML to datasets. This powerful technique allows a data steward to set up concepts once and enables the entire organization the ability to unify and standardize on common rules and terms, solving many metadata scale challenges.

{% hint style="info" %}
Dataset Level

**Security Reference Data** - Bloomberg financial data                                                                      **Home Loan Data** - Mortgage application data
{% endhint %}

## Semantics

{% hint style="info" %}
Column Level

EMAIL, ZIP CODE, SSN, CUSIP, GENDER, ADDRESS, CURRENCY CD, SKU, EIN, IP ADDRESS, PHONE, LICENSE, VIN, CREDIT CARD
{% endhint %}

A semantic is the "semantic type" of a column or attribute of a dataset.  All columns have a physical type such as String, Int, Date etc... but the semantic understanding of what type of String is in the column can be very important.  I also allows us to enforce DQ validation rules out of the box. 

## Sensitive Data

{% hint style="info" %}
Column Level

**PII** - personally identifiable information                                                                                             **MNPI** - materially non public information  
**PCI** - credit information like a credit card number                                                                              **PHI** - Hippa medical information
{% endhint %}

## The Power of combining all Three into One Domain 

Now imagine if you could classify your datasets as concepts, then automatically have all the columns be recognized semantically\(with validation rules in place\) as well as have the columns labeled with sensitivity tags.  It might look something like the below.

![](../.gitbook/assets/screen-shot-2021-09-15-at-1.11.06-pm.png)

## Administering Data Concepts

Setup your data concepts once and let the entire organization benefit by unifying all datasets to a common understanding in the admin Data Concepts page. 

![](../.gitbook/assets/screen-shot-2021-09-15-at-1.14.42-pm.png)


# Scoring

Scoring can be completely controlled by the end-user with out of the box defaults.

![](../../.gitbook/assets/scoring.gif)

Owl provides a data quality assessment that scans 9 dimensions of a data set to assure the integrity of that data. The 9 dimensions are behavior, rules, outliers, pattern, source, record, schema, duplicates, and shapes.&#x20;

OwlCheck produces a data quality score from 0-100. 100 represents that there were no integrity issues found in the data set. The score numerically represents the integrity of that data. For example, the score of 100 would tell the data analyst that zero data quality issues in that data set.

Owl will scan your data with the same frequency, that you load your data - Owl scans 9 dimensions of DQ and summarizes the results into a score from 0-100. &#x20;

#### Aggregate Score

![The score starts with 100 and individual dimensions deduct from the total.](<../../.gitbook/assets/image (90) (1) (1).png>)

{% hint style="info" %}
Each dimension can be custom weighted and rules can contain custom scoring severity. In this example, the deducted score (59) from the starting score (100) equals an overall score of 41.
{% endhint %}

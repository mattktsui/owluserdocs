---
description: A no-code option to get started quickly and onboard a dataset.
---

# Explorer (no-code)

![](<../../.gitbook/assets/explorer (3).gif>)

## Getting Started

This page can be accessed by clicked the Explorer option (the compass icon).

![](<../../.gitbook/assets/image (96).png>)

{% hint style="info" %}
All UI functionality has corresponding API endpoints to define, run, and get results programmatically.
{% endhint %}

## Select Your Data Source

![](<../../.gitbook/assets/image (105).png>)

## Create a new DQ Job by clicking +Create DQ Job

![](<../../.gitbook/assets/image (126).png>)

#### **View Data is an interactive option to run queries and explore the data**

#### The bar chart icon will take you to a profile page of the dataset created prior to Explorer 2&#x20;

## Select The Scope and Define a Query

![](<../../.gitbook/assets/image (128).png>)

#### Pick Date Column if your dataset contains an appropriate time filter&#x20;

#### Click Build Model -> to Save and Continue&#x20;

![](<../../.gitbook/assets/image (139).png>)

## Transform Tab (advanced / optional)

{% content-ref url="../../dq-job-examples/owlcheck/owlcheck-transform.md" %}
[owlcheck-transform.md](../../dq-job-examples/owlcheck/owlcheck-transform.md)
{% endcontent-ref %}

#### Click Build Model -> to Save and Continue&#x20;

## Profile

![](<../../.gitbook/assets/image (97).png>)

#### Use the drop-downs to enable different analysis. Best practice is to leave the defaults.

## Pattern (advanced / optional)

Toggle on Pattern to enable this layer

Click +Add to define a group and series of columns&#x20;

{% content-ref url="pattern-mining.md" %}
[pattern-mining.md](pattern-mining.md)
{% endcontent-ref %}

#### Click Save to and Click Outlier to Continue&#x20;

## Outlier (advanced / optional)

{% content-ref url="outliers.md" %}
[outliers.md](outliers.md)
{% endcontent-ref %}

#### Click Save to and Click Dupe to Continue&#x20;

## Dupe (advanced / optional)

{% content-ref url="duplicates.md" %}
[duplicates.md](duplicates.md)
{% endcontent-ref %}

#### Click Save to and Click Source to Continue&#x20;

## Source (advanced / optional)

Navigate to the source dataset

Click Preview to interlace the columns

Manually map the columns by dragging left to right or deselect columns&#x20;

{% content-ref url="validate-source.md" %}
[validate-source.md](validate-source.md)
{% endcontent-ref %}

#### Click Save to and Click Save/Run to Continue&#x20;

## Run

1. Select an agent
2. Click Estimate Job
3. Click Run to start the job

![](<../../.gitbook/assets/image (116).png>)

![](<../../.gitbook/assets/image (145).png>)

{% hint style="info" %}
\*Note if you do not see your agent, please verify the agent has been assigned to your connection via:
{% endhint %}

{% content-ref url="../../connecting-to-dbs-in-owl-web/add-connection-to-agent.md" %}
[add-connection-to-agent.md](../../connecting-to-dbs-in-owl-web/add-connection-to-agent.md)
{% endcontent-ref %}

_Admin Console-->Remote Agent--> (Link icon on far right)-->Map connections to this agent and then reload the explorer page_

## ****

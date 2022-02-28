# DQ Workflows

## Benefits <a href="#benefits" id="benefits"></a>

The DQ Workflows package listed on Collibra Marketplace allows you to 1) create and manage Data Quality Issues, 2) receive Notifications on Rule Metrics, and 3) request Rule Creation and Modification within **Collibra Data Intelligence Cloud**. Data stewards will be able to organize and prioritize all requests within DIC before they take any action within **Collibra Data Quality**.

Once deployed, the workflows will facilitate quicker data issue remediation by involving business analysts and other personas who can now participate in your data quality workstreams.

_Please note: DQ Workflows are listed on Collibra Marketplace and are templates to get customers started. Collibra-provided Marketplace listings are not subject to the same SLA obligations (_[_https://marketplace.collibra.com/marketplace-terms/_](https://marketplace.collibra.com/marketplace-terms/)_) In addition, they can only be leveraged within Collibra Data Intelligence Cloud. In the future, we will work towards releasing bi-directional workflows._

## Step 0: Prerequisites <a href="#step-0-prerequisites" id="step-0-prerequisites"></a>

|                                  |                                                 |
| -------------------------------- | ----------------------------------------------- |
| **Resource**                     | Notes                                           |
| Collibra Edge Site               | DQ Connector is a capability of Edge            |
| Collibra Data Intelligence Cloud | 2021.07 Release (or newer)                      |
| Collibra Data Quality            | 2.15 (or newer)                                 |
| Collibra DQ Connector            | Synchronized Rules from Data Quality to Catalog |

{% hint style="success" %}
Let's proceed after gathering all prerequisites!
{% endhint %}

## Step 1: Download, Deploy and Start DQ Workflows <a href="#step-1-create-and-configure-edge-and-dq-connector" id="step-1-create-and-configure-edge-and-dq-connector"></a>

**1A. Download Package from Collibra Marketplace and Unzip Files**

\*\*1B. Deploy Workflows \*\*

![](<../.gitbook/assets/image (68).png>)

**1C. Adjust Workflow Settings (One-Time Setup)**

| Workflow Configuration Setting                                           | DQ Rule / DQ Sync Request | DQ Rule Modification             | DQ Data Remediation | DQ Issue Resolution | Manage DQ Subscriptions | Notify of DQ Metrics |
| ------------------------------------------------------------------------ | ------------------------- | -------------------------------- | ------------------- | ------------------- | ----------------------- | -------------------- |
| Applies To                                                               | Asset                     | Asset                            | Asset               | Asset               | Global                  | Global               |
| Applies To Asset Type                                                    | Column, Table             | Column, Table, Data Quality Rule | Column, Table       | Issue               |                         |                      |
| Other: Any Signed In User Can Start Workflow                             | Y                         | Y                                |                     |                     | Y                       | Y                    |
| Other: Perform Candidate User Check on Workflow Start                    | Y                         | Y                                | Y                   |                     | Y                       | Y                    |
| Other: This Workflow Can Only Run Once At Same Time on Specific Resource |                           |                                  |                     |                     | Y                       | Y                    |
| Other: Show In Global Create                                             |                           |                                  |                     |                     | Y                       | Y                    |
| Roles: Start Workflow                                                    |                           |                                  |                     |                     | Sysadmin                | Sysadmin             |
| Roles: Stop Workflow                                                     |                           |                                  |                     |                     | Sysadmin                | Sysadmin             |
| Roles: Reassign Tasks                                                    |                           |                                  |                     |                     | Sysadmin                | Sysadmin             |

![Example: DQ Rule Request](<../.gitbook/assets/image (69).png>)

![Example: Manage DQ Subscriptions](<../.gitbook/assets/image (70).png>)

## **Step 2: Create Data Quality Requests / Issues**

### **2A. Create Data Quality Issues**

| Workflow             | Main Requestor Persona                     | Description                                                                                                                                                                            | Steward Taking Action         |
| -------------------- | ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| DQ Data Remediation  | <p>Data Steward</p><p>Business Analyst</p> | Tracking / management for confirmed data issues which may require underlying data remediation                                                                                          | Data Lake Admin, ETL Engineer |
| DQ Rule Request      | Business Analyst                           | Proposing data quality rules in plain language e.g. "flag any German phone numbers in this dataset" or "identify customers with churn risk based on engagement time with our platform" | Data Steward                  |
| DQ Rule Modification | Business Analyst                           | Proposing adjustments to existing rules e.g. values, dimensions, passing thresholds                                                                                                    | Data Steward                  |
| DQ Sync Request      | Business Analyst                           | Request for synchronization of the DQ Connector to synchronize and/or onboarding a new dataset with pre-populated rules                                                                | Data Steward                  |

![Example: Data Quality Rule Request](<../.gitbook/assets/image (140).png>)

![Completed Rule Request Example](<../.gitbook/assets/image (104).png>)

![Example: Data Quality Rule Modification Request](<../.gitbook/assets/image (131).png>)

![Completed Data Quality Rule Modification Example](<../.gitbook/assets/image (130).png>)

![Example: DQ Synchronization Request with Rules Request optional checkbox](<../.gitbook/assets/image (150).png>)

## Step 3: Manage Data Quality Issues

### 3A. Setup Data Helpdesk Filter

**Data Helpdesk**

* Select Issues
* Navigate to 'Filters'
* Properties > Attributes > Relations > Issue \*\*categorized by \*\*Issue Category > Input 'Data Quality Issue' > Apply
* Save button > Save View as > '**Data Quality Issues**'
* Optional settings for View: Can pin, promote, make public, make default

### 3B. Manage Issues From Data Helpdesk View

![](<../.gitbook/assets/image (71).png>)

### 3C. Alternate: Manage Issues From Tasks

![](<../.gitbook/assets/image (72).png>)

## Step 4: Receive Notifications Of DQ Issues And Metrics

### 4A. Set Up DQ Metric Subscription

Who? Anyone can set up a DQ subscription, for yourself or for your teammates

![](<../.gitbook/assets/image (149).png>)

Alerts will be sent based on reviewing rules and metrics associated with **Tables** or **Columns** that violate the specified **Threshold**

![](<../.gitbook/assets/image (112).png>)

Assuming an e-mail is associated with the Subscriber within Collibra, the Subscriber will receive e-mail notifications by default at **12pm local server time**. This, along with other settings within the provided workflow, can be **adjusted** in **Eclipse**, Collibra's recommended workflow editor.

### 4B. Review DQ Metric Alerts

Ensure that the DQ alerts set for you are providing helpful details

![](<../.gitbook/assets/image (136).png>)

### 4C. Update Subscription Settings

![](<../.gitbook/assets/image (124).png>)

For every subscription set up for a Subscriber, the Manage DQ Subscriptions modal will cycle through for your review. You can update **Threshold**, add or delete **Notification Days**, add or delete **Tables** or **Columns**, rename the **Subscription title**, **Save the new settings**, or simply **Unsubscribe**.

![](<../.gitbook/assets/image (118).png>)

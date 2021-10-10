# DQ Workflows in Collibra DIC

## Benefits <a href="benefits" id="benefits"></a>

The DQ Workflows package listed on Collibra Marketplace allows you to 1) create and manage Data Quality Issues, 2) receive Notifications on Rule Metrics, and 3) request Rule Creation and Modification within **Collibra Data Intelligence Cloud**. Data stewards will be able to organize and prioritize all requests within DIC before they take any action within **Collibra Data Quality**. 

Once deployed, the workflows will facilitate quicker data issue remediation by involving business analysts and other personas who can now participate in your data quality workstreams.

_Please note: DQ Workflows are listed on Collibra Marketplace and are templates to get customers started. Collibra-provided Marketplace listings are not subject to the same SLA obligations (_[_https://marketplace.collibra.com/marketplace-terms/_](https://marketplace.collibra.com/marketplace-terms/)_)  In addition, they can only be leveraged within Collibra Data Intelligence Cloud. In the future, we will work towards releasing bi-directional workflows._

## Step 0: Prerequisites <a href="step-0-prerequisites" id="step-0-prerequisites"></a>

| **Resource**                     | Notes                                           |
| -------------------------------- | ----------------------------------------------- |
| Collibra Edge Site               | DQ Connector is a capability of Edge            |
| Collibra Data Intelligence Cloud | 2021.07 Release (or newer)                      |
| Collibra Data Quality            | 2.15 (or newer)                                 |
| DQ Connector                     | Synchronized Rules from Data Quality to Catalog |

{% hint style="success" %}
Let's proceed after gathering all prerequisites!
{% endhint %}

## Step 1: Download, Deploy and Start DQ Workflows <a href="step-1-create-and-configure-edge-and-dq-connector" id="step-1-create-and-configure-edge-and-dq-connector"></a>

**1A. Download Package from Collibra Marketplace and Unzip Files**

**1B. Deploy Workflows **

![](<../.gitbook/assets/image (68).png>)

**1C. Adjust Workflow Settings (One-Time Setup)**

| **Workflows**                                                     | Adjustments To Default Load Settings                                                                                                                                                                                                                                                                            |
| ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>DQ Rule Request<br>DQ Rule Modification<br>DQ Sync Request</p> | <p>Applies To: Edit: Global -> <strong>Asset</strong></p><p>Asset Type: Add Rules: <strong>Column, Table</strong></p><p>Other: Any signed in user can start workflow (<strong>Check</strong>)</p><p>Other: This workflow can only run once at the same time on specific resource (<strong>Uncheck</strong>)</p> |
| DQ Data Remediation                                               | <p>Applies To: Edit: Global -> <strong>Asset</strong></p><p>Asset Type: Add Rules: <strong>Column, Table</strong></p><p>Other: Any signed in user can start workflow (<strong>Check</strong>)</p>                                                                                                               |
| DQ Issue Resolution                                               | <p>Applies To: Edit: Global -> <strong>Asset</strong></p><p>Asset Type: Add Rules: <strong>Issue</strong></p>                                                                                                                                                                                                   |
| Manage DQ Subscriptions                                           | <p>Other: Any signed in user can start workflow (<strong>Check</strong>)</p><p>Other: Show in global create (<strong>Check</strong>)</p>                                                                                                                                                                        |
| Notify of DQ Metrics                                              | None                                                                                                                                                                                                                                                                                                            |

![Example: DQ Rule Request ](<../.gitbook/assets/image (69).png>)

![Example: Manage DQ Subscriptions ](<../.gitbook/assets/image (70).png>)

## **Step 2: Create Data Quality Requests / Issues**

### **2A. Create Data Quality Issues**

| Workflow             | Outcome |
| -------------------- | ------- |
| DQ Data Remediation  |         |
| DQ Rule Request      |         |
| DQ Rule Modification |         |
| DQ Sync Request      |         |

## Step 3: Manage Data Quality Issues

### 3A. Setup Data Helpdesk Filter

**Data Helpdesk**

* Select Issues
* Navigate to 'Filters'
* Properties > Attributes > Relations > Issue **categorized by **Issue Category > Input 'Data Quality Issue' > Apply
* Save button > Save View as > '**Data Quality Issues**'
* Optional settings for View: Can pin, promote, make public, make default

### 3B. Manage Issues From Data Helpdesk View

![](<../.gitbook/assets/image (71).png>)

### 3C. Alternate: Manage Issues From Tasks

![](<../.gitbook/assets/image (72).png>)

## Step 3: Receive Notifications Of DQ Issues And Metrics

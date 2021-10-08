# DQ Workflows in Collibra DIC

## Benefits <a id="benefits"></a>

The DQ Workflows package listed on Collibra Marketplace allows you to 1\) create and manage Data Quality Issues, 2\) receive Notifications on Rule Metrics, and 3\) request Rule Creation and Modification within **Collibra Data Intelligence Cloud**. Data stewards will be able to organize and prioritize all requests within DIC before they take any action within **Collibra Data Quality**. 

Once deployed, the workflows will facilitate quicker data issue remediation by involving business analysts and other personas who can now participate in your data quality workstreams.

_Please note: DQ Workflows are listed on Collibra Marketplace and are templates to get customers started. Collibra-provided Marketplace listings are not subject to the same SLA obligations \(_[_https://marketplace.collibra.com/marketplace-terms/_](https://marketplace.collibra.com/marketplace-terms/)_\)  In addition, they can only be leveraged within Collibra Data Intelligence Cloud. In the future, we will work towards releasing bi-directional workflows._

## Step 0: Prerequisites <a id="step-0-prerequisites"></a>

| **Resource** | Notes |
| :--- | :--- |
| Collibra Edge Site | DQ Connector is a capability of Edge |
| Collibra Data Intelligence Cloud | 2021.07 Release \(or newer\) |
| Collibra Data Quality | 2.15 \(or newer\) |
| DQ Connector | Synchronized Rules from Data Quality to Catalog |

{% hint style="success" %}
Let's proceed after gathering all prerequisites!
{% endhint %}

## Step 1: Download, Deploy and Start DQ Workflows <a id="step-1-create-and-configure-edge-and-dq-connector"></a>

**1A. Download Package from Collibra Marketplace and Unzip Files**

**1B. Deploy Workflows** 

![](../.gitbook/assets/image%20%2820%29.png)

**1C. Adjust Workflow Settings \(One-Time Setup\)**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Workflows</b>
      </th>
      <th style="text-align:left">Adjustments To Default Load Settings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">DQ Rule Request
        <br />DQ Rule Modification
        <br />DQ Sync Request</td>
      <td style="text-align:left">
        <p>Applies To: Edit: Global -&gt; <b>Asset</b>
        </p>
        <p>Asset Type: Add Rules: <b>Column, Table</b>
        </p>
        <p>Other: Any signed in user can start workflow (<b>Check</b>)</p>
        <p>Other: This workflow can only run once at the same time on specific resource
          (<b>Uncheck</b>)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DQ Data Remediation</td>
      <td style="text-align:left">
        <p>Applies To: Edit: Global -&gt; <b>Asset</b>
        </p>
        <p>Asset Type: Add Rules: <b>Column, Table</b>
        </p>
        <p>Other: Any signed in user can start workflow (<b>Check</b>)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DQ Issue Resolution</td>
      <td style="text-align:left">
        <p>Applies To: Edit: Global -&gt; <b>Asset</b>
        </p>
        <p>Asset Type: Add Rules: <b>Issue</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Manage DQ Subscriptions</td>
      <td style="text-align:left">
        <p>Other: Any signed in user can start workflow (<b>Check</b>)</p>
        <p>Other: Show in global create (<b>Check</b>)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Notify of DQ Metrics</td>
      <td style="text-align:left">None</td>
    </tr>
  </tbody>
</table>

![Example: DQ Rule Request ](../.gitbook/assets/image%20%2830%29.png)

![Example: Manage DQ Subscriptions ](../.gitbook/assets/image%20%2817%29.png)

## **Step 2: Create Data Quality Requests / Issues**

### **2A. Create Data Quality Issues**

| Workflow | Outcome |
| :--- | :--- |
| DQ Data Remediation |  |
| DQ Rule Request |  |
| DQ Rule Modification |  |
| DQ Sync Request |  |

## Step 3: Manage Data Quality Issues

### 3A. Setup Data Helpdesk Filter

**Data Helpdesk**

* Select Issues
* Navigate to 'Filters'
* Properties &gt; Attributes &gt; Relations &gt; Issue **categorized by** Issue Category &gt; Input 'Data Quality Issue' &gt; Apply
* Save button &gt; Save View as &gt; '**Data Quality Issues**'
* Optional settings for View: Can pin, promote, make public, make default

### 3B. Manage Issues From Data Helpdesk View

![](../.gitbook/assets/image%20%2822%29.png)

### 3C. Alternate: Manage Issues From Tasks

![](../.gitbook/assets/image%20%2832%29.png)

## Step 3: Receive Notifications Of DQ Issues And Metrics


# DQ Connector

## Benefits

The Native DQ Connector brings intelligence from **Collibra Data Quality** into **Collibra Data Intelligence Cloud**. Once this integration is established, you will be able to bring in your Data Quality user-defined rules, metrics, and dimensions into **Collibra Data Catalog**.

_Please note: Only data sources ingested by both Collibra Data Catalog and Collibra Data Quality will be able to synchronize Data Quality assets_

## Step 0: Prerequisites

| **Resource**                     | Notes                                               |
| -------------------------------- | --------------------------------------------------- |
| Collibra Edge Site               | DQ Connector is a capability of Edge                |
| Collibra Data Intelligence Cloud | 2021.07 Release (or newer)                          |
| Collibra Data Quality            | 2.15 (or newer)                                     |
| Database(s) and Driver(s)        | Proper Access and Credentials (Username / Password) |

{% hint style="success" %}
Let's proceed after gathering all prerequisites!
{% endhint %}

## Step 1: Create and Configure Edge and DQ Connector

**1A. Create Edge site and Add Name e.g. 'Collibra-DQ-Edge' and Description (One-Time)**

![Where: Collibra Data Intelligence Cloud Settings -\&gt; Edge -\&gt; Click ‘Create Edge site’](https://lh6.googleusercontent.com/H7aAEkqf4L0RK6xhTSG4yONGafGKhUvHiSz1SPh9c7kyEPfXmhkwWKtr3twcZt6SMo\_KBWj4JNStxURftlc3qeQ7VCyZXng3gUu6GHTCKjoIgMSYwy2tAcyRP\_KFUImGVrYN2tYC)

![](https://lh3.googleusercontent.com/Eyo8SV3nasLqqvXPw0zanZopx7sTV0G7SBcuYt63aI4YmZBXW9DgAHalQWfifNFwhTI5e9Qc3SpsfM3MWFHB6oVLBCeAHlkicRQ9FsBEEKnZ6KJZKuNyF7rmIOKVDch-unS4oAFJ)

{% hint style="info" %}
**Please see:** [**https://productresources.collibra.com/docs/cloud-edge/latest/Default.htm**](https://productresources.collibra.com/docs/cloud-edge/latest/Default.htm) **for more detailed information on Edge installation and configuration**
{% endhint %}

**1B. Establish Edge’s Connection To Each Data Source (One-Time For Each Source)**

Additional Steps in Collibra DG include:

* Provide Connection Name which exactly matches Connection / System Name in Collibra DQ
* Select Connection type e.g. Username / Password JDBC driver
* Input Username and Password to connect to your data source&#x20;
* Input fully qualified driver class name&#x20;
* Upload Driver jar (to reduce potential conflicts, use same driver jar from Collibra DQ)&#x20;
* Input Connection String Input credentials e.g. username / password or Kerberos config file&#x20;
* Reminder: All of the above information should be the same as in Collibra DQ

Additional Steps in Collibra DQ include:

* Verify Connection ‘Name’ in DGC matches Connection ‘Name’ in Collibra DQ
* Verify ‘Connection string’ in DGC matches ‘Connection URL’ in Collibra DQ
* Verify ‘Driver class name’ in DGC matches ‘Driver Name’ in Collibra DQ
* Verify ‘Driver jar’ in DGC matches Driver used in ‘Driver Location’ in Collibra DQ (may require SSH)

![Where: Settings > Edge > Select Edge site > JDBC Connections > Select ‘Create connection’](https://lh5.googleusercontent.com/-3FpYTn4vo4kWogSJNgPi4afMwty1a8pk-2\_m-bYYTAz195caF4jRbB0OF2bC0U1t559jNLOvXVAgRLt32EpWL5IEjpB8nqUZ0R1A98ODxKmC9GGCavw0Ad5iXTHss0nhCtcsK1W)

{% hint style="warning" %}
**Important: Connection / System name (in this example, ‘postgres-gcp’) must exactly match the Connection / System Name in Collibra DQ**
{% endhint %}

**1C. Establish Catalog JDBC Ingestion Capability On Edge (One-Time For Each Data Source)**

![Where: Settings -\&gt; Edge -\&gt; Capabilities -\&gt; Input Name -\&gt; 'Catalog JDBC Ingestion' ](https://lh3.googleusercontent.com/7To6AMTiyioNVZeZwK9pzi14Y7D1vCbAyRV4vj7iteI0wz30cGJI4jNaXO9gtLDSEwhltZnHwr48-NWSbFYtU9LJot7UBovm6-yyEoURnol-ksZ0F-Q81tRVOwYYKvnzesWKB19s)

**1D: Configure Destinations For DQ Assets (Rules, Metrics, Dimensions) Within DQ Connector (One-Time)**

Option A: Create New Destinations

* Create New Rulebook Domain (suggested domain type) for DQ Rules and DQ Metrics
  * Global Create -> Search for and select 'Rulebook' under 'Governance Asset Domain' -> Select desired 'Community' e.g. 'Data Governance Council' -> Input name of Rulebook domain e.g. 'CDQ Rules', 'CDQ Metrics'

{% hint style="info" %}
Record your domain resource ID e.g. 2xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (can be found in your URL) for Step 1G
{% endhint %}

* Create New Business Asset Domain (suggested domain type) for DQ Dimensions
  * Global Create -> Search for and select 'Business Asset Domain' -> Select desired 'Community' e.g. 'Data Governance Council' -> Input name of domain e.g. 'CDQ Dimensions'
  * Record your domain resource ID e.g. 2xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (can be found in your URL)

Option B: Use Existing Domains from existing Rulebook and Asset domains

{% hint style="info" %}
Record your domain resource ID e.g. 2xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (can be found in your URL) for Step 1G
{% endhint %}

![](https://lh3.googleusercontent.com/LOR\_nFMAjSrFUPNoOLqjEvDAxwBoeHsjYU\_c\_QsgH3QgRH-y8\_Uvtn2kfMesE68VcYDrpp1raPKOumsOAyoVek32I2x-e9OskR-JUDV8GxdmtFNOMK6iKTvcDejs56PXpmvh6pa1)

{% hint style="success" %}
You have now established destinations for where Collibra should ingest your User-Defined Rules, Metrics, and Dimensions
{% endhint %}

**1E. Assign Permissions for New Domains of DQ Assets (Rules, Metrics, Dimensions) (One-Time)**

Please assign your Edge user as a 'Technical Steward' in each of the domains specified in 1D such that  Edge can write create / update assets into each respective domain

![](https://lh3.googleusercontent.com/U5NnQT6ncu6XbL7YKWe8A0caumHxodHBCgU\_vJeJjWCyxYSzvGsRWWzH2HjjeVKYih4hvGXvDM7J1\_DB72EgdxoVLrRTNEQsg4enZotY7fEgjfxfI-cbz4vmFHxxzxEBQfUq\_ZpF)

{% hint style="success" %}
This step provides Edge with the proper permissions to create and update assets into the domains from the previous step
{% endhint %}

**1F. Allow DQ Assets To Attach To Tables and Column Assets (One-Time)**

Now we need to add a few relations and update global assignment characteristics

* **Table**: Settings -> Operating Model -> Relations -> Search in any column for 'Table' -> Global Assignment -> Characteristics -> Edit (larger of the two buttons) on right -> Add characteristic -> Search for and select 'governed by Governance Asset' -> Save

![](https://lh5.googleusercontent.com/RYKx\_CdwVsVauaJPmjP7yDlZzzTVCeLzcTQHix2wSOmgo8taapeg8lU87L5qatGIrbPKATLMEvN7skj7JHtqGJjMXGuJcVpWD5BToX1W92Q2edGs3ODi3CZ1C4WQX9MMW9bdmKFw)

* **Column**: Settings -> Operating Model -> Relations -> Search in any column for 'Column' -> Global Assignment -> Characteristics -> Edit (larger of the two buttons) on right -> Add characteristic -> Search for and select 'is governed by Data Quality Rule' -> Save

![](https://lh5.googleusercontent.com/JhUNVCCoHxkamUgeLsQ98tWPPvHeUNiGB6EjH\_wEugZ5OaenbQbTEL6bVv6W2EiyqtnivaDjCsoHagW0Q6U6s5GDpC37\_vnVND\_qhPGaZDw9GoUry6vrBqiSUwAABfi1npUO18\_E)

**1G. Establish DQ Connector (One-Time)**

DQ Connector is an Edge capability that will facilitate communication with your Collibra DQ instance

* Settings -> Edge -> Capabilities -> Add Capability -> Select 'DQ Connector' -> Input your Collibra DQ URL e.g. 'customerdq.collibra.com:port' input username and password

{% hint style="info" %}
Remember from previous step 1D, you will need to provide your resource / UUIDs for your specified domains for DQ Rules, Metrics, and Dimensions
{% endhint %}

![](https://lh4.googleusercontent.com/nRWd59wkPl\_yXKwCsgfvBuFMdiAwlW6nBoN1eV7c2YHN-Y2cHbC82TwGRiub297mQ0uBphUL4vewsBzFOKhesF5gaY6W3Beft2VC4ILmrJZuW8oiqEa45JrvHPFI1QiFtlC4kgs\_)

**Specify DQ Asset Destinations Within DQ Connector**

![Input your UUIDs from Step 1D for Rules, Metrics, Dimensions](https://lh6.googleusercontent.com/x-JOYKbeDBzsSnKI5czFiBkUuitcxQeLte9MAsTSJL3sfyw8\_3AwUog9HRyWdjUV9GpVdaUiM199dTf1NfNMGAfiANWmiW93VYAgZs\_PNnogG1KnKa1JRLxJSkEjLrp6J57iQVn-=s0)

{% hint style="success" %}
Excellent! We've now completed the initial one-time configuration!
{% endhint %}

## Step 2: Register Edge Connections to Collibra Catalog

**2A. Create System Asset Within Collibra Catalog To Connect To Edge**

![Global Create > 'System' > Select Domain > Enter Name e.g. 'postgres-gcp'](https://lh4.googleusercontent.com/e19f1vFffMGQDzgHD1m83C66pG9MwOeJwrd8-Jl42oC9ArjXaCGrwfu\_baSzdP4u1xelfB0YWHYA90tsT9g3NFHIE2ULhIdWnkZRUYi8f1sq8EIltYnm\_BhC-yVDSknI\_9ndGpB0)

{% hint style="warning" %}
**Important: Connection / System name (in this example, ‘postgres-gcp’) must exactly match the Connection / System Name in Collibra DQ**
{% endhint %}

**2B. Register Edge Data Source to Collibra Catalog**

![Catalog > Global 'Create' > Register Data Source with Edge](https://lh6.googleusercontent.com/NsIO-7QVn8gMLJi0YJmhC-gs-r26nPQWwQUY8-S2oQa-pWQAjMeJvo2ZvX5FYG3KqfrbuVE5U5aEeCj25kX19TuDL9MR4ves52EcMyadYgfbWIrC86rHinl7a\_ZUnv2gW9IPRlIZ)

## **Step 3: Start Ingesting Collibra Data Quality Into Catalog**

{% hint style="info" %}
**Prerequisite: Catalog will have ingested schemas on Edge**
{% endhint %}

![Catalog > Data Sources > Select Database e.g. 'postgres' > Configuration](https://lh6.googleusercontent.com/HgMjwe6cR3ne\_GpzqhHQNdB5tMWhIsfg-mU5iLUq7oBZnuomANBVhPGdMSH8kCHBwonZQVp2EhFMQ6H4eH\_P5t7lIGJrboU2y71Hy0HVvenK6uu8PeaxRCSQbEX1LbeKdSlBcdd7)

{% hint style="info" %}
**Prerequisite: Ensure targeted schemas have User-defined Rules, Metrics, and/or Dimensions within Collibra DQ that have been Executed**
{% endhint %}

**3A. Synchronize Data Quality for Selected Schemas**

![Catalog > Data Sources > Select Database > Configuration > Quality Extraction](https://lh4.googleusercontent.com/Xt8y\_PfQ3UZAWBdW6PTWTSX0ZU2830Z-MJykaugTuaWIFIyJR3Hdy0WmijTlFn47yhozmxVe-idXGk7u8wVlfCbk7qIAJMItx44pYVvDIDgjeL62DZ3i38ZrnBjTfwKhB9qa8Irs)

**3B. Verify Data Quality Results in Collibra Catalog**

![](https://lh4.googleusercontent.com/syFKZtlFsc0QAv2OwFx10oVNSfgUaA6fe004elBAWo8DXKXDKUdCpsuOyVK5zVNmhKwnYLLQi\_XdKV7B4BcTKLqtov4QCK2b\_MoSHDneKm0abhXv0BE33pQjtOfWb2IE4nJIpWNd)

{% hint style="success" %}
**Success! Example Output**
{% endhint %}

**Appendix: Synchronization For Single Table in Data Quality and Data Catalog**

![View in Collibra Data Quality](<../.gitbook/assets/image (3).png>)

![View in Collibra Catalog](../.gitbook/assets/image.png)

## FAQ

**Q: Known Limitations**

* Only 1 source tenant from Collibra DQ can be specified
* On-demand ingestion (vs. scheduled)
* Can only specify 1 domain destination for each of Rules, Metrics, and Dimensions
* Only JDBC sources supported (no file sources)

**Q: DQ Dashboard In DGC: I can verify the DQ Connector is synchronizing Data Quality Rules and Data Quality Metrics, but why don't Data Quality Dashboard Charts display?**

A: Ensure correct **Aggregation Paths** and **Global Assignments** (or create, if none exist) for **Table** and **Column** below

![Aggregation Path For Table (Data Quality Rules)](https://lh5.googleusercontent.com/74HV9oMYQkhBw-jrof1ubunkWPo8OZmgLrxHCM\_J0fFmwS0JR5HoZgCN6-TeGCxyArM65jjjPJSMuUXkaog0qFBnthfOlIDZfZCvjQ-bj7dM\_ALfcnFYENw\_8u4UnJwDnDGlort3=s0)

![Aggregation Path for Column (Data Quality Rules)](https://lh6.googleusercontent.com/Bo0xlZmY9-EbKc2nkbI8fOFX3IOdI2\_HFkFDt-mw99H10ovIU-nD6m1Jd1pnnfvcHceynzV07NzoarH\_AVbzFg90uyITf5PRM9bTWNHoPXGdVEgmJzR\_MkQrjLVgRhcnTPh3pIj7=s0)

![Global Assignments For Data Quality Rules](https://lh5.googleusercontent.com/9VHho9WDZhgDLAGYzZ-llIUWFJrLF6mis\_BpDG5HI-I45mVgi5yOF7p74sONmnLZ9e4pY4GaaCyEIl4yCTVInzbBBjgpmPOUV0NQykcdkUmmx6s-6\_DvoTpqs82jMO6AVBsM8\_E1=s0)

**Q: DQ Dashboard In DGC: Why won't my DQ Dimension charts display in my Dashboard?**

A: Please 1) add a new custom **Relation** 'Data Quality Metric classified by Data Quality Dimension',  2) **Global Assignment** for 'Data Quality Metric', 3) UUID of the new **Relation** into the **DQ Connector** setup in **Step 1G**, 4)&#x20;

![New Relation Type In Operating Model](https://lh5.googleusercontent.com/WqDQjGVtgHTGzDNwrb-yPZlhcAC11vAU2KxHox3QAZ4E1c-ThfbakEO9fjl2ZyqscPLB5a3FjBZvYQxxtYd89uv5YGEgCDTvIBUty9JoMsgTLl-I1dEtqo4vzIFKSas6rtXYpb5T=s0)

![New Global Assignment Characteristic](https://lh6.googleusercontent.com/9fxsT4RRkyFDh93CyK6ceRpLYTxboAk3XwpxRWtmp5om9ViZutcuvcOzaHFVh-R02n0mSJhhcYzhvptAOeFT3lWK0HKtI\_YLEaH1SUFgXN-5JQz532pdra-fsP2pD4w3XnDvNiEl=s0)

![Add 'classified by Data Quality Dimension'](https://lh4.googleusercontent.com/Suo299gJGe1Y2tsK6rE4m6kca0XO1Dp7WoHvKfrswRUxxobQBI\_AD0KfZswl5mcEtUVwm\_W70Ws0OJp2-as62s9NfvuqUzBwqsntCATSsCbREHefpFTJ0TsSOlRsnHME210goEIJ=s0)

![Copy Resource ID of New Relation Into DQ Connector Setup](https://lh4.googleusercontent.com/GNknIUuSsGe\_CiIyA\_eAymSeCvtQvQ7yHoqviqLcFWhF3MNQp5ynx\_r1a3eDg4\_Yw46gyegdJSlymUXxTZ91HOg5y\_xIWbVGSjeXRreA3rXyHofkwLaJzDBZ8ZpgfUcFx-pAqtUN=s0)

**Q: I've connected and configured data sources correctly, why aren't DQ Rules and DQ Metrics being synchronized?**

A: Please ensure Connection / System Names between Collibra Data Quality, Collibra, and Edge exactly match

A: Please ensure Edge user has admin permissions to write the assets into Catalog

A: Please ensure correct URL specified within the DQ Connector capability e.g. http://cdq.customer.com:9000/

**Q: Is DQ Connector unidirectional?**

A: Yes, from Collibra DQ to Collibra Catalog in Data Intelligence Cloud

**Q: How many DQ Connectors can I run simultaneously?**

A: Currently, one.

**Q: Does the DQ Connector work with On-Prem Collibra DGC?**

A: No, any work with on-prem Collibra DGC would be custom API development via Collibra Professional Services or a partner SI.

**Q: If I delete a rule from Collibra DQ that I have already synchronized into Collibra Catalog, will it be deleted from Catalog in the next synchronization?**

A: No, the DQ Connector only upserts into Catalog. If a rule is deleted from Collibra DQ, it will not be automatically deleted in Catalog.

**Q: Why are my scores different in Collibra DQ and Collibra Catalog?**

A: Currently, the DQ DQ Connector pulls in the most recent user-defined rules from Collibra DQ. Other components that affect score such as Behaviors, Outliers, Patterns, Dupes, Source are not yet included.

**Q: Getting errors when trying to delete both domain that Edge created for DB and the Connection?**

A: Please delete Edge created domain via API.

**Q: I've hit the synchronize button, how can I tell if my job is complete?**

A: Check the Activities circle (button on top right of menu) for the status of your DQ Synchronization.

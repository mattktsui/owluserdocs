---
description: Divide and conquer your data quality
---

# Multi-Tenancy

MultiTenancy allows a company the ability to instantiate different organizations within one entity.  For example say your organization is called Acme and inside of Acme there are two divisions AcmeTraders and AcmeInsurance and each organization is not allowed to see one another's owlcheck results.  You would simple segregate them into 2 different Tenants within the overarching Owl web application.

**Prerequisite(s)**

* DNS entry for owl web server IP = example below we call it hub (existing for single tenant setup)
* DNS entry for multiTenantSchemaHub = example below we call it owlhub.hub&#x20;

**Prerequisites For URL Based tenancy: tenant.host**

A DNS entry for each tenant

* DNS entry for every tenant you want to create = example below we call it tenant1.hub

Each record above points to the same IP address.

**Setup**

In order to setup multi-tenancy follow these steps

* If this is an upgrade please make sure to follow the steps outlined in the "[Upgrading to latest Version](broken-reference)"
* Make sure the web application has started up one time and you successfully logged into it with the default credentials.
* Then stop all the components using ./owlmanage.sh stop
* Modify the owl-env.sh file to include these to new parameters
  1. **export multiTenantSchemaHub=owlhub **(this is a new schema that will get created on owlweb start, note the name of the TenantSchemaHub can be changed to the desired name at setup time)
  2. **export MULTITENANTMODE=TRUE** (this enabled multi-tenancy to be used).
  3. **export URLBASEDMULTITENANTMODE=TRUE/FALSE**
     1. TRUE (default) means you are using the tenant name as a sub-domain (see prerequisites)&#x20;
     2. FALSE means you will let owl manage tenants via sessions/tokens
* If using agents as part of the operation of owl please be sure to modify the owl.properties file to include the following.
  1. spring.agent.datasource.url=jdbc:postgresql://cdh-edge-dan.us-east4-c.c.owl-hadoop-cdh.internal:5432/postgres**?currentSchema=owlhub **(matching the name of the schema set on step 3-1 above).
  2. jdbc:postgresql://cdh-edge-dan.us-east4-c.c.owl-hadoop-cdh.internal:5432/postgres**?currentSchema=owlhub **(matching the name of the schema set on step 3-1 above).
* Once the settings have been configured for multi-tenancy please start up the owlweb host first using ./owlmanage.sh start=owlweb.  Once the web is up and you can hit the page please start up the agents using ./owlmanage.sh start=owlagent.
* In order to use multi-tenancy in URLBASEDMULTITENANTMODE=TRUE you'll have to make sure we have DNS entries to the tenant endpoints, otherwise click the tenant management link from the login page.  Example:&#x20;
  1. If I have a DNS alias named hub.  I should be able to point me browser at hub:9002 (or your respective owlweb port) to get to the main Multi-Tenant login page as depicted below

![](<../../.gitbook/assets/image (75).png>)

* This is where DNS alias come into place.  Assuming we left the owlhub as the multiTenantSchemaHub name we hit the drop down and select owlhub and click the arrow it will place owlhub.hub into the url.  This means there also has to be a DNS Alias name for your selected multiTenantSchemaHub name.   NOTE: Username and password for tenant management is mtadmin / mtadmin123

![](<../../.gitbook/assets/image (76).png>)

* Now that you logged into the Tenant Management screen using the hub DNS alias we can create our first tenant.  In this example below I'm going to create a tenant named tenant1.  First click the "+ Add Tenant" button in the top right part of the screen.

![](<../../.gitbook/assets/image (77).png>)

Click Save.  Your tenant shows up in the list and now you can click the login button as shown below.

![](<../../.gitbook/assets/image (78).png>)

Clicking the Login button will redirect your browser to the tenant1.hub:9002 url (DNS entry needs to be in place for tenant1 as shown below).

![](<../../.gitbook/assets/image (79).png>)

Enter the admin username and password that you created for the tenant1 (refer to figure 3 about) and login to the tenant as the admin.

While logged in as a tenant admin the last step is to go to the Admin Console and click on "Sync Schema" this will generate the tables under the tenant called tenant1.

![](<../../.gitbook/assets/image (80).png>)

At this point you are ready to start administrating your tenant1 as you did with the owl web application in the past.

### Supplemental: Adding and Editing a Tenant

In many cases it may make sense to have isolated environments to check data quality. This need could be driven by a number of factors including data access rights, organization and business models, reporting needs, and/or other security requirements.

Regardless of the need, Owl will support dynamically creating tenants via our Owl Hub Management portal as part of the Owl Web Application. That's it, there is nothing else to install, simply enable Multi-Tenant mode in the application configuration properties and you are on your way.

Once enabled you will have a tenant selection screen prior to login where you can chose any of your configured tenants or access the Owl Hub (with the TENANT\_ADMIN role)

![](../../.gitbook/assets/screen-shot-2019-09-03-at-11.34.13-am.png)

After selecting the owlHub tenant, you will have the ability to manage each tenant, as well as create new tenants from the management console.

![](../../.gitbook/assets/screen-shot-2019-09-03-at-10.51.28-am.png)

All enabled tenants will be listed in the multi-tenant drop down menu. Access to tenants are handled by the administrator(s) within each tenant individually.

Access to agents are also handled by the administrator(s) within each tenant individually.

![](../../.gitbook/assets/screen-shot-2019-09-04-at-12.35.34-pm.png)

Each agent is visible and editable as an Admin from the UI.

![](<../../.gitbook/assets/owl-agent (1).png>)


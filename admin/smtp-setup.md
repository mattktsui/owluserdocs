# SMTP Setup

Simple Mail Transport Protocol or SMTP, is an internet standard for email transmission. Owl allows you to configure a single SMTP server in order to raise alerts to the attention of the dataset owner in case a specific condition is met. These alert conditions can be one of the following:

1. Owl Data Quality Score is below a specific threshold
2. Row Count is below a specific threshold
3. If a rule is triggered

In order to setup SMTP click on the gear icon -> Alerts as show in the screenshot below.

​![](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Setting%20Up%20SMTP/WebHome/1555068880284-638.png)SMTP Setup

When in the “Admin Manage Alerts” screen we can now setup the SMTP server by providing the following information:

1. Name of the SMTP server or IP Address.
2. Port used by the SMTP server
3. Username/account that has been configured on the SMTP server for use
4. Password in association with the username/account provided in step 3
5. From email or the originating email who will send the alert
6. Reply email or when responding back to the Alert the email whom you will respond to.

See screenshot below for example of configuration.![](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Setting%20Up%20SMTP/WebHome/1555069327842-964.png)Configuring SMTP

When completed click the “Add” button.

Once the information has been populated and added, the grey box above the form will get populated with the content supplied. If the data ever has to be changed clicking the ![1555069526616-123.png](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Setting%20Up%20SMTP/WebHome/1555069526616-123.png?width=35\&height=31) icon will repopulate the form in order to be modified and re added.

Now that configuration of the SMTP Email Server has been completed let’s create an alert and see that the alert triggers an email. In this example, we will use the dist_example dataset that we ran earlier from the demo.sh script.

![](<../.gitbook/assets/image (90).png>)

In the above screen shot we did the following:

1. Searched for the “dist_example” dataset
2. Provided an alert named “score_lt\_90”
3. Provided a condition that we know will be met “score < 90”
4. Provided who the recipient of this alert should be mailed to in this sample “user2@owl.net”
5. Custom Message = “score is below 90 for dist_exampe”

Clicking the “Save” button will move the contents of the form above to the List of Alerts for this particular dataset.

From the terminal on this install if you run the below command (which is just an extract out of the demo.sh file). We should see the alert get triggered

./owlcheck -ds dist_example -rd 2018-10-07 -d , -f /opt/owl/bin/demos/distribution_change.csv -fq "select \* from dataset where d_date ='2018-10-07'"

At the end of this command we should see the “Alert was triggered” as shown in the screenshot below.

![](<../.gitbook/assets/image (89).png>)

And the recipient [user2@owl.net](mailto:user2@owl.net) received the email.

![](<../.gitbook/assets/image (88).png>)

# Set up SMTP

Simple Mail Transport Protocol or SMTP, is an internet standard for email transmission. Collibra DQ allows you to configure a single SMTP server to send alerts to the attention of the dataset owner in case a specific condition is met, such as:

* Owl Data Quality Score is below a specific threshold.
* Row Count is below a specific threshold.
* If a rule is triggered.

### Steps

1. In the **Admin Console**, click **Alerts**.&#x20;
2. In the **Configuration** section, enter the required information:

| Option             | Description                                                                |
| ------------------ | -------------------------------------------------------------------------- |
| SMTP Host          | The name or the IP address of the SMTP server.                             |
| SMTP Port          | The port used by the SMTP server.                                          |
| SMTP Username      | The username or the account that is configured on the SMTP server for use. |
| SMTP Password      | The password of the SMTP server username or account.                       |
| (Default) To Email | The sender email address.                                                  |
| Reply Email        | The reply-to email address.                                                |

Save your changes.

![SMTP setup in Collibra DQ Admin Console](../../.gitbook/assets/smtp\_setup.gif)

See screenshot below for example of configuration.![](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Setting%20Up%20SMTP/WebHome/1555069327842-964.png)Configuring SMTP

When completed click the “Add” button.

Once the information has been populated and added, the grey box above the form will get populated with the content supplied. If the data ever has to be changed clicking the ![1555069526616-123.png](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Setting%20Up%20SMTP/WebHome/1555069526616-123.png?width=35\&height=31) icon will repopulate the form in order to be modified and re added.

Now that configuration of the SMTP Email Server has been completed let’s create an alert and see that the alert triggers an email. In this example, we will use the dist\_example dataset that we ran earlier from the demo.sh script.

![](<../../.gitbook/assets/image (90).png>)

In the above screen shot we did the following:

1. Searched for the “dist\_example” dataset
2. Provided an alert named “score\_lt\_90”
3. Provided a condition that we know will be met “score < 90”
4. Provided who the recipient of this alert should be mailed to in this sample “user2@owl.net”
5. Custom Message = “score is below 90 for dist\_exampe”

Clicking the “Save” button will move the contents of the form above to the List of Alerts for this particular dataset.

From the terminal on this install if you run the below command (which is just an extract out of the demo.sh file). We should see the alert get triggered

./owlcheck -ds dist\_example -rd 2018-10-07 -d , -f /opt/owl/bin/demos/distribution\_change.csv -fq "select \* from dataset where d\_date ='2018-10-07'"

At the end of this command we should see the “Alert was triggered” as shown in the screenshot below.

![](<../../.gitbook/assets/image (89).png>)

And the recipient [user2@owl.net](mailto:user2@owl.net) received the email.

![](<../../.gitbook/assets/image (88).png>)

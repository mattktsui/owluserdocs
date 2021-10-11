# Active Directory LDAP

Go to the Admin Console page (click the Owl -> click the Gear -> click Admin Console).

Click on “AD Setup” and you will see the screenshot below.

![](<../../.gitbook/assets/image (86).png>)

1. AD Enabled = flag to enabled AD (after binding please restart the owl-web application)
2. Page Size = 100 is recommended. The number of results in a single page (NOTE: For really large AD Environments it’s best to narrow down the Base Path and/or possibly using Group Search Path to narrow down to that group explicitly).
3. Host = Host: ldap://x.x.x.x or ldaps://x.x.x.x Port: is usually 389 for ldap or 636 for ldaps
4. Base Path is the domain specified in the example above owl.com (equals to DC=owl,DC=com).
5. Group Search Path = helps to narrow down list to an explicit group or parent group (example: CN=owladmins)
6. Bind user = \<user>@\<domain>
7. Bind Password = users domain password.
8. Click save and you should receive the message below on the top of the owl-web application.

![](https://lh4.googleusercontent.com/Z_btfJeipsC7WQrC2lC80Z9IwmomiBX8VFaNneAgdGOBPRfyArWao7f\_\_C9TEFVXDb0-DyxFpXc3BUrpmhJs20gelNfA8TI7-sVTkyD4aVlV7Q1WUR50dN7MvukyrcBoUysfYgvm)

When binding to AD you do not need a special AD username and password. The application just needs a user to bind with in order to run a read-only query on the groups. The AD credentials are not stored, owl uses this dynamically to understand what groups you want to map.

Now the binding is complete we can map an AD Group to an Owl ROLE.

![](<../../.gitbook/assets/image (85).png>)

1. Click on “ROLE MAPPING”
2. Select a ROLE in the drop down list - (Alternatively this is a time you can add a new Owl ROLE to map the AD Group(s) you want to include in that Owl ROLE).
3. Click Load Groups
4. Select Group in the left box (use the filter on top to filter base on what you provide in the text box).
5. click the name to move it left to right.
6. click “Save” and you’ll get a response back to Owl-web like the following.

![](https://lh5.googleusercontent.com/b6FG3k6y73mbVt9eXl8AG9CORfKRGwvcJhR5pRNtx5F4lkjeWc8ZB6uKSd6M0BpoNmYv6Iw8Aai78XNH4fq3bEe6eITdr5f9DFOy9eBDg5b58KWMf94OZoza8I8cwNPMA3uStoUQ)

Now that we’ve mapped an AD Group to an AD Role we can now log out and try to login as a domain user. (REMEMBER: you will have to restart the owl-web by running ./owlmanage.sh restart_owlweb when toggling AD Enabled).

When logging into the Owl Web application please make sure to append the domain to the end of the user name as depicted below.

![](<../../.gitbook/assets/image (84).png>)

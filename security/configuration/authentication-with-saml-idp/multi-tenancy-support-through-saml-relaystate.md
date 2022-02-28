# Multi-tenancy support through SAML RelayState

Starting with Collibra DQ version 2021.11, in a multi-tenant environment, you can help route SSO to the proper tenant with the SAML provided **RelayState** property.

When set, the property is sent to the IDP and then returned to the consumer service, such as /saml/SSO. The application checks that value to ensure the correct tenant is set up.

You can set the **RelayState** property in the in the **SAML Setup** section of the **Admin Console**.

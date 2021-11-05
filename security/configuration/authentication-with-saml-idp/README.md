# SAML Authentication

You can integrate Collibra DQ with an existing SAML solution and have your application act as a service provider. Once you set up the environment variables, you can access and configure SAML security settings as an administrator in the **SAML Setup** section of the **Admin Console**.

### Set the SAML authentication properties

Before configuring SAML authentication, you must add the following required properties to your configuration

{% tabs %}
{% tab title="Standalone installation" %}
1. Add the properties as environment variables to your **owl-env.sh** file located in **\<installation**_**\_**_**directory>/owl/config/**.
2. Prefix all properties with the `export` statement.
3. Restart the web app.
{% endtab %}

{% tab title="Cloud native installation" %}
1. Add the properties as environment variables to your **owl-web ConfigMap**.
2. Recycle the pod.
{% endtab %}
{% endtabs %}

#### Required properties

| Property         | Description                                                                                                                                                                                         |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SAML\_ENABLED    | <p>Whether Collibra DQ uses SAML.</p><p>If set to <code>false</code>, users sign in with a username and password.</p><p>If set to <code>true</code>, SAML handles the authentication request.</p>   |
| SAML\_ENTITY\_ID | <p>The name of the application for the identity provider, for example <em>Collibra DQ</em>.</p><p>It is an immutable unique identifier of the service provider for the identity provider (IDP).</p> |

#### Optional properties

You can further configure your SAML setup with the following optional properties.

| Property                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SAML\_ENTITY\_BASEURL    | <p>The base URL that is provided in the service provider metadata.</p><p>Set this property when you use DNS.</p>                                                                                                                                                                                                                                                                                                                                   |
| SAML\_LB\_EXISTS         | <p>Whether the application needs to configure a load balancer.</p><p>You generally need this setting only when the <strong>Load Balancer</strong> is set for <strong>SSL Termination</strong>.</p><p>The default value is <code>false</code>.</p><p>If set to <code>true</code>, you must also provide a value for <strong>SAML_LB_SERVER_NAME</strong>.</p>                                                                                       |
| SAML\_METADATA\_USE\_URL | <p>Whether Collibra DQ uses an URL or a file for the identity provider metadata.</p><p>The default value is <code>true</code>.</p><p>If set to <code>false</code>, the file must be accessible to the owl-web and the path provided in the <strong>Meta-Data URL</strong> field of the <strong>Meta Data Configurations</strong> section under <strong>Admin Console</strong> --> <strong>SAML Setup </strong>--> <strong>Connection</strong>.</p> |
| SAML\_ROLES\_PROP\_NAME  | <p>The attribute in which the identity provider stores the role of the user authenticating in the SAML response.</p><p>The default value is <code>memberOf</code>.</p>                                                                                                                                                                                                                                                                             |
| SAML\_GRANT\_ALL\_PUBLIC | <p>Whether any user authenticated by the identity provider is allowed to login the Collibra DQ application.</p><p>The default value is <code>false</code>.</p>                                                                                                                                                                                                                                                                                     |
| SAML\_USER\_NAME\_PROP   | The name of the attribute in the SAML response that contains the username of the user who is authenticating.                                                                                                                                                                                                                                                                                                                                       |
| SAML\_TENANT\_PROP\_NAME | <p>If using multi-tenant mode, the variable in which the identity provider stores the tenant name of the user authenticating in the SAML response.</p><p>The app will attempt to use the <code>RelayState</code> parameter to identify the tenant and then fall back on this property.</p>                                                                                                                                                         |
| SAML\_KEYSTORE\_FILE     | <p>The path to the keystore for SSL validation.</p><p>The store should contain the keypair of the identity provider for SSL verification.</p>                                                                                                                                                                                                                                                                                                      |
| SAML\_KEYSTORE\_PASS     | The password for the keystore provided in `SAML_KEYSTORE_FILE`.                                                                                                                                                                                                                                                                                                                                                                                    |
| SAML\_KEYSTORE\_ALIAS    | The alias of the keypair (private and public) in the keystore used for SSL verification.                                                                                                                                                                                                                                                                                                                                                           |

When **SAML\_METADATA\_USE\_URL** is set to `true` (default), the following additional properties are available.

| Property                            | Description                                                                                                                                                                             |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SAML\_METADATA\_TRUST\_CHECK        | <p>Whether to enable Collibra DQ to do trust verification of the identity provider.</p><p>The default value is <code>false</code>.</p>                                                  |
| SAML\_METADATA\_REQUIRE\_SIGNATURE  | <p>Whether Collibra DQ signs authentication requests to the identity provider.</p><p>The default value is <code>false</code>.</p>                                                       |
| SAML\_INCLUDE\_DISCOVERY\_EXTENSION | <p>Whether to enable Collibra DQ to indicate in the SAML metadata that it’s able to consume responses from an IDP Discovery Service.</p><p>The default value is <code>false</code>.</p> |

#### Optional Properties: Load Balancer

When **SAML\_LB\_EXISTS** is set to `true`, the following additional properties are available.

| Property                             | Description                                                                                                                                                                                                                |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SAML\_LB\_INCLUDE\_PORT\_IN\_REQUEST | <p>Whether to include the port number in the request.</p><p>The default value is <code>false</code>.</p>                                                                                                                   |
| SAML\_LB\_PORT                       | <p>The port number of the load balancer.</p><p>The default value is <code>443</code>.</p>                                                                                                                                  |
| SAML\_LB\_SCHEME                     | <p>The protocol of the load balancer.</p><p>The default value is <code>https</code>.</p>                                                                                                                                   |
| SAML\_LB\_SERVER\_NAME               | <p>The server or DNS name.</p><p>Usually, the same as <strong>SAML_ENTITY_BASEURL</strong> without specifying the protocol, for example without <em>https://</em>.</p><p>This property is required and has no default.</p> |
| SAML\_LB\_CONTEXT\_PATH              | Any path that may be defined on the load balancer.                                                                                                                                                                         |

{% code title="Example" %}
```
#enable SAML & show the SAML SSO option on the login page
SAML_ENABLED=true

#set SSL communication properties for SAML
SAML_KEYSTORE_FILE=/keystore.p12
SAML_KEYSTORE_PASS=****
SAML_KEYSTORE_ALIAS=****

#in multi-tenant mode set the name of the IDP variable to hold the tenat name
SAML_TENANT_PROP_NAME=tenant

#set the name of the IDP variable to hold the user roles in the response
SAML_ROLES_PROP_NAME=memberOf

#allow login if authenticated to the IDP
SAML_GRANT_ALL_PUBLIC=true

#set the EntityId of the application to be supplied to the IDP
SAML_ENTITY_ID=OwlOneLogin

#optinally set a property that contains the username in the response
SAML_USER_NAME_PROP=""

#optionally use a file for the IDP metadata vs a URL (default is true)
SAML_METADATA_USE_URL=false 

#optional security settings to 
SAML_METADATA_TRUST_CHECK=false
SAML_METADATA_REQUIRE_SIGNATURE=false
SAML_INCLUDE_DISCOVERY_EXTENSION=false
```
{% endcode %}

### Download service provider metadata for the IDP

Once you have enabled and configured SAML authentication, you can download the service provider metadata that is required by your identity provider from `https://<your_dq_environment_url>/saml/metadata`.

### Enable the SAML sign in option

When you are ready with your IDP settings, add the final configuration settings in the **Admin Console**:

1. Sign in as an existing administrator with a username and password to the tenant you want to configure.
2. In the **Admin Console**, click **SAML Setup**.
3. In the **Connection** tab, select the **SAML Enabled** check-box.
4. In the **Meta Data Configurations** section, click **+Add**.
5. Enter the required information.

| Option          | Description                                                                                                                                                           |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Meta-Data URL   | The URL of the identity provider metadata XML file or the location of the downloaded XML file, depending on how you configured the SAML\_METADATA\_USE\_URL property. |
| Meta-Data Label | The name for this specific configuration.                                                                                                                             |
| IDP URL         | The URL of the Collibra DQ application that is provisioned by the identity provider.                                                                                  |

Save your changes.

{% hint style="success" %}
Once you complete this setup, you can restart your application and sign in using the SAML SSO option.
{% endhint %}

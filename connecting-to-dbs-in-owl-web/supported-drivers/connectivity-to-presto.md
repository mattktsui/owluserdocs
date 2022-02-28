# Connectivity to Presto

### Example URL

```
jdbc:presto://xyz.presto.svc.cluster.local:8080/database
```

### Driver Name

```
com.facebook.presto.jdbc.PrestoDriver
```

### Connection Properties

These methods may be mixed; some parameters may be specified in the URL while others are specified using properties. However, the same parameter may not be specified using both methods.

### Parameter Reference <a href="#parameter-reference" id="parameter-reference"></a>

| Name                           | Description                                                                                                                                                                                                                                   |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `user`                         | Username to use for authentication and authorization.                                                                                                                                                                                         |
| `password`                     | Password to use for LDAP authentication.                                                                                                                                                                                                      |
| `socksProxy`                   | SOCKS proxy host and port. Example: `localhost:1080`                                                                                                                                                                                          |
| `httpProxy`                    | HTTP proxy host and port. Example: `localhost:8888`                                                                                                                                                                                           |
| `protocols`                    | Comma delineated list of HTTP protocols to use. Example: `protocols=http11`. Acceptable values: `http11,http10,http2`                                                                                                                         |
| `applicationNamePrefix`        | Prefix to append to any specified `ApplicationName` client info property, which is used to set the source name for the Presto query. If neither this property nor `ApplicationName` are set, the source for the query will be `presto-jdbc`.  |
| `accessToken`                  | Access token for token based authentication.                                                                                                                                                                                                  |
| `SSL`                          | Use HTTPS for connections                                                                                                                                                                                                                     |
| `SSLKeyStorePath`              | The location of the Java KeyStore file that contains the certificate and private key to use for authentication.                                                                                                                               |
| `SSLKeyStorePassword`          | The password for the KeyStore.                                                                                                                                                                                                                |
| `SSLTrustStorePath`            | The location of the Java TrustStore file that will be used to validate HTTPS server certificates.                                                                                                                                             |
| `SSLTrustStorePassword`        | The password for the TrustStore.                                                                                                                                                                                                              |
| `KerberosRemoteServiceName`    | Presto coordinator Kerberos service name. This parameter is required for Kerberos authentication.                                                                                                                                             |
| `KerberosPrincipal`            | The principal to use when authenticating to the Presto coordinator.                                                                                                                                                                           |
| `KerberosUseCanonicalHostname` | Use the canonical hostname of the Presto coordinator for the Kerberos service principal by first resolving the hostname to an IP address and then doing a reverse DNS lookup for that IP address. This is enabled by default.                 |
| `KerberosConfigPath`           | Kerberos configuration file.                                                                                                                                                                                                                  |
| `KerberosKeytabPath`           | Kerberos keytab file.                                                                                                                                                                                                                         |
| `KerberosCredentialCachePath`  | Kerberos credential cache.                                                                                                                                                                                                                    |
| `extraCredentials`             | Extra credentials for connecting to external services. The extraCredentials is a list of key-value pairs. Example: `foo:bar;abc:xyz` will create credentials `abc=xyz` and `foo=bar`                                                          |
| `customHeaders`                | Custom headers to inject through JDBC driver. The customHeaders is a list of key-value pairs. Example: `testHeaderKey:testHeaderValue` will inject the header `testHeaderKey` with value `testHeaderValue`. Values should be percent encoded. |

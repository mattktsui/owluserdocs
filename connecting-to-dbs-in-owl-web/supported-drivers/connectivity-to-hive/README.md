# Connectivity to Hive

### Example URL

```
jdbc:hive2://cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal:10000/default;AuthMech=1;KrbHostFQDN=cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal;KrbRealm=CW.COM;KrbServiceName=hive;SSL=1;SSLKeyStore=/opt/cloudera/security/pki/cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal-server.jks;AllowSelfSignedCerts=1;SSLKeyStorePwd=password;principal=hive/cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal@CW.COM
```

### Driver Name

```
com.simba.hive.jdbc41.HS2Driver
```

### Driver Properties

```
hive.resultset.use.unique.column.names=false
```

### What Does each option mean

**Base connection string** **=** jdbc:hive2://cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal:10000/default

**Authentication identifier** **=** AuthMech=1 (which states Kerberos)

**Kerberos Hive Server FQDN** **=** KrbHostFQDN=cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal

**Kerberos Realm used =** KrbRealm=CW.COM _(Not necessarily needed)_

**Kerberos Service name =** KrbServiceName=hive

**Enabling SSL =** SSL=1

**The SSL KeyStore to be used to =** SSLKeyStore=/opt/cloudera/security/pki/cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal-server.jks _(Could use SSLTrustStore also)_

**Allow for Self Signed certifications to be OK =** AllowSelfSignedCerts=1 _(our environment used self signed certs)_

**Password to the KeyStore =** SSLKeyStorePwd=password _(Not necessarily needed)_

**Kerberos Principal to use to Authenticate with =** principal=hive/cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal@CW.COM

### Example Connection

![](<../../../.gitbook/assets/image (41).png>)

### Within the Owl Web UI you have to specify the following (See ScreenShot below)

![HS2Driver Connection for Owl using HS2 SSL/TLS/Kerberos](http://18.204.201.140:8080/xwiki/bin/download/Internal%20Documentation/Enabling%20TLS%2FSSL%20for%20Hiveserver2/WebHome/Screen%20Shot%202019-06-12%20at%209.25.13%20AM.png)

**Name =** hivessl

**Connection URL =** jdbc:hive2://cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal:10000/default;AuthMech=1;KrbHostFQDN=cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal;KrbRealm=CW.COM;KrbServiceName=hive;SSL=1;SSLKeyStore=/opt/cloudera/security/pki/cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal-server.jks;AllowSelfSignedCerts=1;SSLKeyStorePwd=password;principal=hive/cdh-instance1.us-east1-b.c.owl-hadoop-cdh.internal@CW.COM

**Port =** 10000

**Driver Name =** com.cloudera.hive.jdbc4.HS2Driver

**Username =** [userspark@CW.COM](mailto:userspark@CW.COM)

**Password =** password

### FAQ

It is very common to require this connection property when not using the default schema. Remember to add this to the connection properties when defining the connection.

```
hive.resultset.use.unique.column.names=false
```

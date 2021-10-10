# Connectivity to Redshift

### Example URL

```
jdbc:redshift://redshift-cluster-name.kdkcis9g8.us-east-1.redshift.amazonaws.com:5439/dev
```

### Driver Name

```
com.amazon.redshift.jdbc.Driver
```

Amazon Redshift offers drivers for tools that are compatible with the JDBC 4.2 API. For information about the functionality supported by these drivers, see the [Amazon Redshift JDBC driver release notes](https://s3.amazonaws.com/redshift-downloads/drivers/jdbc/1.2.55.1083/Amazon+Redshift+JDBC+Release+Notes.pdf).

For detailed information about how to install the JDBC driver version 1.0, reference the JDBC driver libraries, and register the driver class, see [Amazon Redshift JDBC driver installation and configuration guide](https://s3.amazonaws.com/redshift-downloads/drivers/jdbc/1.2.55.1083/Amazon+Redshift+JDBC+Connector+Install+Guide.pdf).

For each computer where you use the Amazon Redshift JDBC driver, make sure that Java Runtime Environment (JRE) 8.0 is installed.

If you use the Amazon Redshift JDBC driver for database authentication, make sure that you have AWS SDK for Java 1.11.118 or later in your Java class path. If you don't have AWS SDK for Java installed, download the ZIP file with JDBC 4.2–compatible driver (without the AWS SDK) and driver dependent libraries for the AWS SDK:

*   [JDBC 4.2–compatible driver (without the AWS SDK) and driver dependent libraries for AWS SDK files version 1.2.55](https://s3.amazonaws.com/redshift-downloads/drivers/jdbc/1.2.55.1083/RedshiftJDBC42-1.2.55.1083.zip).

    The class name for this driver is `com.amazon.redshift.jdbc42.Driver`.

    This ZIP file contains the JDBC4.2–compatible driver (without the AWS SDK) and its dependent library files. Unzip the dependent jar files to the same location as the JDBC driver. Only the JDBC driver needs to be in the CLASSPATH because the driver manifest file contains all dependent library file names which are located in the same directory as the JDBC driver. For more information about how to install the JDBC driver, see [Amazon Redshift JDBC driver installation and configuration guide](https://s3.amazonaws.com/redshift-downloads/drivers/jdbc/1.2.55.1083/Amazon+Redshift+JDBC+Connector+Install+Guide.pdf).

    Use this Amazon Redshift JDBC driver with the AWS SDK that is required for IAM database authentication.
*   [JDBC 4.2–compatible driver (without the AWS SDK) version 1.2.55](https://s3.amazonaws.com/redshift-downloads/drivers/jdbc/1.2.55.1083/RedshiftJDBC42-no-awssdk-1.2.55.1083.jar).

    The class name for this driver is `com.amazon.redshift.jdbc42.Driver`.

    Be sure to use ANTLR version 4.8.1. The antlr4-runtime-4.8-1.jar is included in the ZIP download link above with the JDBC 4.2–compatible driver (without the AWS SDK) and driver dependent libraries for the AWS SDK.

For more information about previous driver versions, see [Use previous JDBC driver versions with the AWS SDK for Java](https://docs.aws.amazon.com/redshift/latest/mgmt/configure-jdbc-connection.html#jdbc-previous-versions-with-sdk).

Then download and review the [Amazon Redshift ODBC and JDBC driver license agreement](https://s3.amazonaws.com/redshift-downloads/drivers/Amazon+Redshift+ODBC+and+JDBC+Driver+License+Agreement.pdf).

If your tool requires a specific previous version of a driver, see [Use previous JDBC driver version 1.0 driver versions in certain cases](https://docs.aws.amazon.com/redshift/latest/mgmt/configure-jdbc-connection.html#jdbc-previous-versions).

### Getting the JDBC URL <a href="obtain-jdbc-url" id="obtain-jdbc-url"></a>

Before you can connect to your Amazon Redshift cluster from a SQL client tool, you need to know the JDBC URL of your cluster. The JDBC URL has the following format: `jdbc:redshift://endpoint`:`port`/`database`.Note

A JDBC URL specified with the former format of `jdbc:postgresql://endpoint`:`port`/`database` still works.

The fields of the format shown preceding have the following values.

| Field      | Value                                                                                                                                      |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `jdbc`     | The protocol for the connection.                                                                                                           |
| `redshift` | The subprotocol that specifies to use the Amazon Redshift driver to connect to the database.                                               |
| `endpoint` | The endpoint of the Amazon Redshift cluster.                                                                                               |
| `port`     | The port number that you specified when you launched the cluster. If you have a firewall, make sure that this port is open for you to use. |
| `database` | The database that you created for your cluster.                                                                                            |

The following is an example JDBC URL: `jdbc:redshift://examplecluster.abc123xyz789.us-west-2.redshift.amazonaws.com:5439/dev`

For information about how to get your JDBC connection, see [Finding your cluster connection string](https://docs.aws.amazon.com/redshift/latest/mgmt/configuring-connections.html#connecting-connection-string).

If the client computer fails to connect to the database, you can troubleshoot possible issues. For more information, see [Troubleshooting connection issues in Amazon Redshift](https://docs.aws.amazon.com/redshift/latest/mgmt/troubleshooting-connections.html).\


[https://docs.aws.amazon.com/redshift/latest/mgmt/configure-jdbc-connection.html](https://docs.aws.amazon.com/redshift/latest/mgmt/configure-jdbc-connection.html)

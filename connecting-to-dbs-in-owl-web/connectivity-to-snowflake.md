# Connectivity to Snowflake

### Example URL

### JDBC Driver Connection String

```text
jdbc:snowflake://accountname.us-east-2.aws.snowflakecomputing.com?db=cdq&warehouse=cdqw
```

### Driver Name

```text
net.snowflake.client.jdbc.SnowflakeDriver 
```

The previous driver class, `com.snowflake.client.jdbc.SnowflakeDriver`, is still supported but is deprecated \(i.e. it will be removed in a future release, TBD\). 

#### Connection Parameters

For documentation on individual connection parameters, see the [JDBC Driver Connection Parameter Reference](https://docs.snowflake.com/en/user-guide/jdbc-parameters.html).`<account_identifier>`

Specifies the account identifier for your Snowflake account. For details, see [Account Identifiers](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). For examples of the account identifier used in a JDBC connection string, see [Examples](https://docs.snowflake.com/en/user-guide/jdbc-configure.html#label-other-jdbc-connection-string-examples).`<connection_params>`

Specifies a series of [one or more parameters](https://docs.snowflake.com/en/user-guide/jdbc-parameters.html), in the form of `<param>=<value>`, with each parameter separated by the ampersand character \(`&`\), and no spaces anywhere in the connection string.

For documentation on individual connection parameters, see the [JDBC Driver Connection Parameter Reference](https://docs.snowflake.com/en/user-guide/jdbc-parameters.html).

#### Other Parameters

Any session parameter can be included in the connection string. For example:

> `CLIENT_SESSION_KEEP_ALIVE=<Boolean>`
>
> Specifies whether to keep the current session active after a period of inactivity, or to force the user to login again. If the value is `true`, Snowflake keeps the session active indefinitely, even if there is no activity from the user. If the value is `false`, the user must log in again after four hours of inactivity.
>
> Default is `false`.

For descriptions of all the session parameters, see [Parameters](https://docs.snowflake.com/en/sql-reference/parameters.html).

#### Examples

The following is an example of the connection string that uses an [account identifier](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html) that specifies the account `myaccount` in the organization `myorganization`.

> ```text
> jdbc:snowflake://myorganization-myaccount.snowflakecomputing.com/?user=peter&warehouse=mywh&db=mydb&schema=public
> ```

The following is an example of a connection string that uses the [account locator](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html#label-account-locator) `xy12345` as the account identifier:

> ```text
> jdbc:snowflake://xy12345.snowflakecomputing.com/?user=peter&warehouse=mywh&db=mydb&schema=public
> ```

Note that this example uses an account in the AWS US West \(Oregon\) region. If the account is in a different region or if the account uses a different cloud provider, you need to [specify additional segments after the account locator](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html#label-account-locator).

[https://docs.snowflake.com/en/user-guide/jdbc-configure.html](https://docs.snowflake.com/en/user-guide/jdbc-configure.html)


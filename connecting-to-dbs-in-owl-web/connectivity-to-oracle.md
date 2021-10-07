# Connectivity to Oracle

### Example URL

```text
jdbc:oracle:thin:@10.589.0.31:1521:DEV
```

### Driver Name

```text
oracle.jdbc.OracleDriver
```



**Connection Properties Recognized by Oracle JDBC Drivers**  


| **Name** | **Short Name** | **Type** | **Description** |
| :--- | :--- | :--- | :--- |
| user  | n/a  | String  | the user name for logging into the database  |
| password  | n/a  | String  | the password for logging into the database  |
| database  | server  | String  | the connect string for the database  |
| internal\_logon  | n/a  | String  | a role, such as `sysdba` or `sysoper`, that allows you to log on as `sys`  |
| defaultRowPrefetch  | prefetch  | String \(containing integer value\)  | the default number of rows to prefetch from the server \(default value is "10"\)  |
| remarksReporting  | remarks  | String \(containing boolean value\)  | "true" if getTables\(\) and getColumns\(\) should report TABLE\_REMARKS; equivalent to using setRemarksReporting\(\) \(default value is "false"\)  |
| defaultBatchValue  | batchvalue  | String \(containing integer value\)  | the default batch value that triggers an execution request \(default value is "10"\)  |
| includeSynonyms  | synonyms  | String \(containing boolean value\)  | "true" to include column information from predefined "synonym" SQL entities when you execute a `DataBaseMetaData getColumns()` call; equivalent to connection `setIncludeSynonyms()` call \(default value is "false"\)  |
| processEscapes  | n/a  | String \(containing boolean value\)  | "false" to disable escape processing for statements \(Statement or PreparedStatement\) created from this connection. Set this to "false" if you want to avoid many calls to `Statement.setEscapeProcessing(false);`. This is espcially usefull for PreparedStatement where a call to `setEscapeProcessing(false)` would have no effect. The default is "true".   |
| defaultNChar  | n/a  | String \(containing boolean value\)  | "false" is the default. If set to "true", the default behavior for handling character datatypes is changed so that NCHAR/NVARCHAR2 become the default. This means that setFormOfUse\(\) won't be needed anymore when using NCHAR/NVARCHAR2. This can also be set as a java property : `java -Doracle.jdbc.defaultNChar=true myApplication`   |
| useFetchSizeWithLongColumn  | n/a  | String \(containing boolean value\)  | "false" is the default. **THIS IS A THIN ONLY PROPERTY. IT SHOULD NOT BE USED WITH ANY OTHER DRIVERS.** If set to "true", the performance when retrieving data in a 'SELECT' will be improved but the default behavior for handling LONG columns will be changed to fetch multiple rows \(prefetch size\). It means that enough memory will be allocated to read this data. So if you want to use this property, make sure that the LONG columns you are retrieving are not too big or you may run out of memory. This property can also be set as a java property : `java -Doracle.jdbc.useFetchSizeWithLongColumn=true myApplication`   |
| SetFloatAndDoubleUseBinary  | n/a  | String \(containing boolean value\)  | "false" is the default. If set to "true", causes the java.sql.PreparedStatment setFloat and setDouble API's to use internal binary format as for BINARY\_FLOAT and BINARY\_DOUBLE parameters. See oracle.jdbc.OraclePreparedStatement setBinaryFloat and setBinaryDouble   |

[https://docs.oracle.com/cd/E11882\_01/appdev.112/e13995/oracle/jdbc/OracleDriver.html](https://docs.oracle.com/cd/E11882_01/appdev.112/e13995/oracle/jdbc/OracleDriver.html)


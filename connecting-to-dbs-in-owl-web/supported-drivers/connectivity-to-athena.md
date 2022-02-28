# Connectivity to Athena

Your host can connect to Athena with either an Athena public service endpoint or an Athena private endpoint. For more information on setting the endpoint, see [Command line options](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-options.html) and [Boto3 documentation](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/core/session.html).

### JDBC URL Example

jdbc:awsathena://AwsRegion=us-east-1;User=xxx;Password=xxx;S3OutputLocation=s3://data-bucket;**MetadataRetrievalMethod=Query**

* Athena uses port 443 to connect to the host.
* Athena's streaming API uses port 444 to stream the query results. When you use a JDBC/ODBC driver, Athena uses this port to stream the query results to the JDBC/ODBC driver installed on the client host. Therefore, unblock this port when you use a JDBC/ODBC driver to connect to Athena. If this port is blocked, your business intelligence tool might time out or fail to show query results when you run a query.
* Use the appropriate JDBC connection URLs in your business tool configuration according to your private DNS configuration for your endpoint.
  * Use the following connection string if you turned off the private DNS: jdbc:awsathena://vpce-.[athena.us-east-1.vpce.amazonaws.com:443](http://athena.us-east-1.vpce.amazonaws.com:443)
  * Use the following connection string if you turned on the private DNS: jdbc:awsathena://[athena.us-east-1.amazonaws.com:443](http://athena.us-east-1.amazonaws.com:443)
* Be sure that the[ security group](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-access.html#vpc-endpoints-security-groups) attached to your VPC endpoint allows traffic from the host where you installed the JDBC/ODBC driver.
* Be sure that port 444 isn't blocked. If you use an AWS PrivateLink endpoint to connect to Athena, then be sure that the security group attached to the AWS PrivateLink endpoint is open to inbound traffic on port 444. Athena uses port 444 to stream query results. If port 444 is blocked, then the results aren't streamed back to your client host. In such situations, you might receive an error message similar to "\[Simba]\[AthenaJDBC]\(100123) An error has occurred. Exception during column initialization". This can also cause the business intelligence tool to stop responding and not display the query results.

```
telnet athena.us-east-1.amazonaws.com 443
telnet glue.us-east-1.amazonaws.com 443
```

### Minimum Permissions

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "athena:StartQueryExecution",
                "s3:ListBucketMultipartUploads",
                "athena:GetQueryResultsStream",
                "glue:GetTables",
                "glue:GetPartitions",
                "athena:GetQueryResults",
                "glue:BatchGetPartition",
                "s3:ListBucket",
                "glue:GetDatabases",
                "athena:ListQueryExecutions",
                "s3:ListMultipartUploadParts",
                "glue:GetTable",
                "glue:GetDatabase",
                "athena:GetWorkGroup",
                "s3:PutObject",
                "s3:GetObject",
                "glue:GetPartition",
                "glue:GetCatalogImportStatus",
                "athena:StopQueryExecution",
                "athena:GetQueryExecution",
                "s3:GetBucketLocation",
                "athena:BatchGetQueryExecution",
                "athena:DeletePreparedStatement",
                "athena:CreatePreparedStatement"
            ],
            "Resource": [
                "arn:aws:athena:*:<AWSAccountID>:workgroup/primary",
                "arn:aws:s3:::<S3 bucket name>/*",
                "arn:aws:s3:::<S3 bucket name>",
                "arn:aws:glue:*:<AWSAccountID>:catalog",
                "arn:aws:glue:*:<AWSAccountID>:database/<database name>",
                "arn:aws:glue:*:<AWSAccountID>:table/<database name>/*"
            ]
        }
    ]
}
```

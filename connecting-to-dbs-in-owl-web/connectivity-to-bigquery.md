# Connectivity to BigQuery

### Steps for the BigQuery Connection

1. **Driver**: com.simba.googlebigquery.jdbc42.Driver
2. **Locate your service account owl-gcp.json** (your org auth key in JSON format)
3. **Create a JDBC connection** (for example only do not use this JDBC URL):\
   jdbc:bigquery://https://www.googleapis.com/bigquery/v2:443;ProjectId=;OAuthType=0;OAuthServiceAcctEmail=<1234567890>[-compute@developer.gserviceaccount.com;OAuthPvtKeyPath=/opt/ext/bq-gcp.json;Timeout=86400](mailto:-compute@developer.gserviceaccount.com;OAuthPvtKeyPath=/opt/ext/owl-gcp.json;Timeout=86400)
4. **Requires a path to a JSON file** that contains the service account for authorization. That same file is provided to the Spark session to make a direct to storage connection for maximum parallelism once Core fires up.”

The above and explained there are actually a number of others steps which must be performed to achieve success:

1. **Password for the BigQuery Connector form in Collibra DQ must be a base64 encoded string created from the json file (see step 3. above)** and input as password. For example:\
   `base64 your_json.json -w 0`\
   or\
   `cat your_json.json | base64 -w 0`
2. **Check that this JAR exists and is on the path of the Collibra DQ Web UI server** (eg. \<INSTALL_PATH>/owl/drivers/bigquery/core). Look at your driver directory location which contains this BigQuery JAR: spark-bigquery\_2.12-0.18.1.jar
3. **Make sure these JARs present in \<INSTALL_PATH>/owl/drivers/bigquery/:**\
   ****_animal-sniffer-annotations-1.19.jar_\
   _google-api-services-bigquery-v2-rev20201030-1.30.10.jar_\
   _grpc-google-cloud-bigquerystorage-v1beta1-0.106.4.jar_\
   _listenablefuture-9999.0-empty-to-avoid-conflict-with-guava.jar_\
   _annotations-4.1.1.4.jar_\
   _google-auth-library-credentials-0.22.0.jar_\
   _grpc-google-cloud-bigquerystorage-v1beta2-0.106.4.jar_\
   _opencensus-api-0.24.0.jar_\
   _api-common-1.10.1.jar_\
   _google-auth-library-oauth2-http-0.22.0.jar_\
   _grpc-grpclb-1.33.1.jar_\
   _opencensus-contrib-http-util-0.24.0.jar_\
   _auto-value-annotations-1.7.4.jar_\
   _GoogleBigQueryJDBC42.jar_\
   _grpc-netty-shaded-1.33.1.jar_\
   _perfmark-api-0.19.0.jar_\
   _avro-1.10.0.jar_\
   _google-cloud-bigquery-1.125.0.jar_\
   _grpc-protobuf-1.33.1.jar_\
   _protobuf-java-3.13.0.jar_\
   _checker-compat-qual-2.5.5.jar_\
   _google-cloud-bigquerystorage-1.6.4.jar_\
   _grpc-protobuf-lite-1.33.1.jar_\
   _protobuf-java-util-3.13.0.jar_\
   _commons-codec-1.11.jar_\
   _google-cloud-core-1.93.10.jar_\
   _grpc-stub-1.33.1.jar_\
   _proto-google-cloud-bigquerystorage-v1-1.6.4.jar_\
   _commons-compress-1.20.jar_\
   _google-cloud-core-http-1.93.10.jar_\
   _gson-2.8.6.jar_\
   _proto-google-cloud-bigquerystorage-v1alpha2-0.106.4.jar_\
   _commons-lang3-3.5.jar_\
   _google-http-client-1.38.0.jar_\
   _guava-23.0.jar_\
   _proto-google-cloud-bigquerystorage-v1beta1-0.106.4.jar_\
   _commons-logging-1.2.jar_\
   _google-http-client-apache-v2-1.38.0.jar_\
   _httpclient-4.5.13.jar_\
   _proto-google-cloud-bigquerystorage-v1beta2-0.106.4.jar_\
   _conscrypt-openjdk-uber-2.5.1.jar_\
   _google-http-client-appengine-1.38.0.jar_\
   _httpcore-4.4.13.jar_\
   _proto-google-common-protos-2.0.1.jar_\
   _core_\
   _google-http-client-jackson2-1.38.0.jar_\
   _j2objc-annotations-1.3.jar_\
   _proto-google-iam-v1-1.0.3.jar_\
   _error_prone_annotations-2.4.0.jar_\
   _google-oauth-client-1.31.1.jar_\
   _jackson-annotations-2.11.0.jar_\
   _grpc-alts-1.33.1.jar_\
   _jackson-core-2.11.3.jar_\
   _slf4j-api-1.7.30.jar_\
   _failureaccess-1.0.1.jar_\
   _grpc-api-1.33.1.jar_\
   _jackson-databind-2.11.0.jar_\
   _gax-1.60.0.jar_\
   _grpc-auth-1.33.1.jar_\
   _javax.annotation-api-1.3.2.jar_\
   _threetenbp-1.5.0.jar_\
   _gax-grpc-1.60.0.jar_\
   _grpc-context-1.33.1.jar_\
   _joda-time-2.10.1.jar_\
   _gax-httpjson-0.77.0.jar_\
   _grpc-core-1.33.1.jar_\
   _json-20200518.jar_\
   _google-api-client-1.31.1.jar_\
   _grpc-google-cloud-bigquerystorage-v1-1.6.4.jar_\
   _jsr305-3.0.2.jar_
4. You may get a CLASSPATH conflict regarding the JAR files.
5. Make sure the BigQuery connector Scala version matches your Spark Scala version.[![02%20PM](https://discourse-static.influitive.net/uploads/db\_033c9cc6\_3cea\_4623\_b4a8\_52ebc3f9e8a1/optimized/2X/d/dfca73373275afb5f063f192a3aa7105caa76bd8\_2\_286x500.png)](https://discourse-static.influitive.net/uploads/db\_033c9cc6\_3cea\_4623\_b4a8\_52ebc3f9e8a1/original/2X/d/dfca73373275afb5f063f192a3aa7105caa76bd8.png)

### Networking

Please account for these urls from a networking and firewall perspective. 

oauth2.googleapis.com\
www.googleapis.com\
bigquerystorage.googleapis.com\
bigquery.googleapis.com

### Permissions

Make sure the project and account have appropriate permissions.  These are common permissions to provide to the account. 

![](<../.gitbook/assets/image (69).png>)

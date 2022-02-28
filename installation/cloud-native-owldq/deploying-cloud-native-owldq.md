# Cloud native install

## Deploy Collibra DQ

Once you have created a namespace and added all of the required secrets, you can begin the deployment of Collibra DQ.

### Minimal install

Install Web, Agent, and metastore. Collibra DQ is inaccessible until you manually add an Ingress or another type of externally accessible service.

{% hint style="warning" %}
All of the following examples will pull containers directly from the Collibra DQ secured container registry. In most cases, InfoSec policies require that containers are sourced from a private container repository controlled by the local Cloud Ops team. Make sure to to add `--set global.image.repo=</url/of/private-repo>` so that you use only approved containers.
{% endhint %}

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=ClusterIP \
<deployment-name> \
/path/to/chart/owldq
```

{% hint style="info" %}
The metastore container must start first as the other containers use it to write data. On your initial deplyment, the other containers might start before the metastore and fail.&#x20;
{% endhint %}

### Externally accessible service

Perform the [minimal install](deploying-cloud-native-owldq.md#minimal-install) and add a preconfigured NodePort or LoadBalancer service to provide access to the Web.&#x20;

{% hint style="warning" %}
A LoadBalancer service type requires that the Kubernetes platform is integrated with a Software Defined Network solution. This will generally be true for the Kubernetes services offered by major cloud vendors. Private cloud platforms more commonly use Ingress controllers. Check with the infrastructure team before attempting to use LoadBalancer service type.&#x20;
{% endhint %}

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=<NodePort || LoadBalancer> \
<deployment-name> \
/path/to/chart/owldq
```

#### Externally accessible with SSL enabled

Perform the install with external service but with SSL enabled.

{% hint style="info" %}
Ensure you have already deployed a keystore containing a key to the target namespace with a secret name that matches the `global.web.tls.key.secretName` argument (_owldq-ssl-secret_ by default). Also, ensure that the secret's key name matches the `global.web.tls.key.store.name` argument (_dqkeystore.jks_ by default).&#x20;
{% endhint %}

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=<NodePort || LoadBalancer> \
--set global.web.tls.enabled=true \
--set global.web.tls.key.secretName=owldq-ssl-secret \
--set global.web.tls.key.alias=<key-alias> \
--set global.web.tls.key.type=<JKS || PKCS12> \
--set global.web.tls.key.pass=<keystore-pass> \
--set global.web.tls.key.store.name=keystore.jks \ 
<deployment-name> \
/path/to/chart/owldq
```

#### Externally accessible and History Server for GCS Log Storage

Perform the install with external service and Spark History Server enabled. In this example, the target log storage system is GCS.&#x20;

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=<NodePort || LoadBalancer> \
--set global.spark_history.enabled=true \
--set global.spark_history.logDirectory=gs://logs/spark-history/ \
--set global.spark_history.service.type=<NodePort || LoadBalancer> \
--set global.cloudStorage.gcs.enableGCS=true \
<deployment-name> \
/path/to/chart/owldq
```

#### Externally Accessible and History Server for S3 Log Storage

Perform the install with external service and Spark History Server enabled. In this example, the target log storage system is S3.&#x20;

{% hint style="info" %}
For Collibra DQ to be able to write Spark logs to S3, makes sure that an Instance Profile IAM Role with access to the log bucket is attached to all nodes serving the target namespace.
{% endhint %}

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=<NodePort || LoadBalancer> \
--set global.spark_history.enabled=true \
--set global.spark_history.logDirectory=s3a://logs/spark-history/ \
--set global.spark_history.service.type=<NodePort || LoadBalancer> \
--set global.cloudStorage.s3.enableS3=true \
<deployment-name> \
/path/to/chart/owldq
```

#### Externally accessible with external metastore

Perform the install with external service and an external metastore, for example AWS RDS, Google Cloud SQL, or just PostgresSQL on its own instance.&#x20;

{% hint style="warning" %}
Collibra DQ currently supports PostgreSQL 9.6 and newer.
{% endhint %}

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=<NodePort || LoadBalancer> \
--set global.metastore.enabled=false                                        
--set global.configMap.data.metastore_url=jdbc:postgresql://<host>:<port>/<database>
--set global.configMap.data.metastore_user=<user> \
--set global.configMap.data.metastore_pass=<password> \
<deployment-name> \
/path/to/chart/owldq
```

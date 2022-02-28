# Cloud native requirements

## Minimum requirements

You need a machine with the following files and packages to run the installation. You can run these from a laptop or separate VM and they do not need to be issued on the Kubernetes cluster itself.

### Prerequisites

* [Helm](https://helm.sh).
* [kubectl](https://kubernetes.io/docs/tasks/tools/).
* Cloud command line SDK, such as gcloud CLI, AWS CLI or similar.

### Files

* The helm chart.\*
* &#x20;JKS files with secrets created in kubectl:
  * _owldq-ssl-secret_
  * _owldq-pull-secret_\*
* A _spark-gcs-secret_ you create from your service account file or token.

{% hint style="info" %}
\*  Available upon request from Collibra.
{% endhint %}

### Application system requirements

| Component     | Processor | Memory | Storage    |
| ------------- | --------- | ------ | ---------- |
| Owl Web       | 1 core    | 2 GB   | 10 MB PVC  |
| Owl Agent     | 1 core    | 1 GB   | 100 MB PVC |
| Owl Metastore | 1 core    | 2 GB   | 10 GB PVC  |
| Spark\*       | 2 cores   | 2 GB   | -          |

{% hint style="info" %}
\*  This is the minimum quantity of resources required to run an a Spark job in Kubernetes. This amount of resources would only provide the ability to scan a few megabytes of data with no more than a single job running at a given time. Proper sizing of the compute space must take into account the largest dataset that may be scanned, as well as the desired concurrency.
{% endhint %}

## Network service considerations

Owl Web is the only required component that needs to be directly accessed from outside of Kubernetes. History Server is the only other component that can be accessed directly by users, however, it is optional.&#x20;

If the target Kubernetes platform supports a LoadBalancer service type, you can configure the Helm chart to directly deploy the externally accessible endpoint.&#x20;

{% hint style="info" %}
For testing purposes, you can also configure the Helm chart to deploy a NodePort service type.
{% endhint %}

For the Ingress service type, deploy OwlDQ without an externally accessible service and then attach the Ingress service separately. This applies when you use a third-party Ingress controller such as NGINX, Contour, and so on.

{% hint style="info" %}
The Helm chart is able to deploy an Ingress on GKE and EKS platforms, however, there is a wide variety of possible Ingress configurations that have not been tested.
{% endhint %}

## Obtaining credentials

Kubernetes stores credentials in the form of secrets. Secrets are base64 encoded files that you can mount into application containers and that application components can reference at runtime. You use _pull secrets_ to access secured container registries to obtain application containers.

### SSL certificates

To enable SSL for secure access to Owl Web, a keystore that contains a signed certificate, keychain, and private key is required. This keystore must be available in the target namespace before you deploy Collibra DQ.&#x20;

{% hint style="info" %}
By default, Collibra DQ looks for a secret called `owldq-ssl-secret` to find the keystore.
{% endhint %}

{% hint style="info" %}
Although it is possible to deploy with SSL disabled, is not recommended.&#x20;
{% endhint %}

### Cloud storage credentials

If you enable History Server, a distributed filesystem is required. Currently, Collibra DQ supports S3 and GCS for Spark history log storage.

{% hint style="info" %}
Azure Blob and HDFS on the near term roadmap.
{% endhint %}

| Target storage system | Credentials requirements                                                                                                                                                                                                                                                                                                                                              |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| S3                    | An IAM Role with access to the target bucket needs to be attached to the Kubernetes nodes of the namespace where OwlDQ is being deployed.                                                                                                                                                                                                                             |
| GCS                   | <p>You must create a secret from the JSON key file of a service account with access the the log bucket.<br>The secret must be available in the namespace before you deploy Collibra DQ. By default, Collibra DQ looks for a secret called <code>spark-gcs-secret</code>, if GCS is enabled for Spark history logs. You can change this via a helm chart argument.</p> |

### Container pull secret

Collibra DQ containers are stored in a secured repository in Google Container Registry. For Collibra DQ to successfully pull the containers when deployed, a pull secret with access to the container registry must be available in the target namespace.

{% hint style="info" %}
By default, Collibra DQ looks for a pull secret named `owldq-pull-secret`. You can change this via a helm chart argument.
{% endhint %}

### Spark service account

To anable Owl Agent and the Spark driver to create and destroy compute containers, you must have a service account with a role that allows get/list/create/delete operations on pods/services/secrets/configMaps in the target namespace. By default, OwlDQ attempts to create the required service account and the required RoleBinding to the default Edit role. Edit is a role that is generally available in a Kubernetes cluster. If the Edit role is not available, you can manually create it.

## Accessing the platform

To deploy anything to a Kubernetes cluster, the first step is to install the required client utilities and configure access:

* **kubectl**: The main method of communication with a Kubernetes cluster. All configuration or introspection tasks will be preformed using kubectl.
* **helm v3**: Used to deploy the OwlDQ helm chart without hand coding manifests.

After you install the utilities, the next step is to configure a kube-context that points to and authenticates to the target platform. On cloud platforms like GKE and EKS, this process is completely automated through their respective CLI utilities.

```
aws eks --region <region-code> update-kubeconfig --name <cluster_name>
```

```
gcloud container clusters get-credentials <cluster-name>
```

In private clouds, this process will vary from organization to organization, however, the platform infrastructure team should be able to provide the target kube-context entry.

## Preparing secrets

Once access to the target platform is confirmed, you can begin the preparation of the namespace. Typically the namespace that Collibra DQ is going to be deployed into is pre-allocated by the platform team.&#x20;

```
kubectl create namespace <namespace>
```

{% hint style="info" %}
There is a lot more that can go into namespace creation such as resource quota allocation, but that is generally a task for the platform team.
{% endhint %}

### Create an SSL keystore secret

```
kubectl create secret generic owldq-ssl-secret \
--from-file /path/to/keystore.jks \
--namespace <namespace>
```

{% hint style="warning" %}
The file name that you use in the `--from-file` argument should be _keystore.jks_. If the file name is anything else, you must include an additional argument specifying the keystore file name in the Helm command.
{% endhint %}

### Create a container pull secret

{% tabs %}
{% tab title="JSON key file credential" %}
```
kubectl create secret docker-registry owldq-pull-secret \
--docker-server=<owldq-registry-server> \
--docker-username=_json_key \
--docker-email=<service-account-email> \
--docker-password="$(cat /path/to/key.json)" \
--namespace <namespace>
```
{% endtab %}

{% tab title="Short lived access token" %}
```
kubectl create secret docker-registry owldq-pull-secret \
--docker-server=<owldq-registry-server> \
--docker-username=oauth3accesstoken \
--docker-email=<service-account-email> \
--docker-password="<access-token-text>" \
--namespace <namespace>
```

{% hint style="warning" %}
GCP Oauth tokens are usually only good for 1 hour. This type of credential is excellent if the goal is to pull containers into a private registry. It can be used as the pull secret to access containers directly, however, the secret would have to be recreated with a fresh token before restarting any of the Colbra DQ components.&#x20;
{% endhint %}
{% endtab %}
{% endtabs %}

### Create a GSC credential secret

```
kubectl create secret generic spark-gcs-secret \
--from-file /path/to/keystore.jks \
--namespace <namespace>
```

{% hint style="warning" %}
The file name that youuse in the `--from-file` argument should be _spark-gcs-secret_. If the file name is anything else, you must include an additional argument specifying the gcs secret name in the Helm command.
{% endhint %}

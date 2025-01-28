---
description: >-
  In this simple guide, we’ll go over the basic steps required to move beyond
  local deployment and get Digma up and running in a Kubernetes cluster that
  multiple people can connect to.
---

# Central (on-prem) Install

### Understanding the Deployment Architecture

Digma is deployed into the K8s cluster into its own namespace. Depending on your application deployment architecture you may want to deploy Digma with different parameters to enable the right connectivity.

<figure><img src="../.gitbook/assets/architecture dark (3).png" alt=""><figcaption></figcaption></figure>

Digma exposes the following services as a part of its Helm deployment:

* **collectorAPI** – Your application should be able to send observability data to the IP/DNS of this endpoint. You may need to configure your setup to allow this traffic. You may also choose to expose it as a public IP in your deployment (see below under Cloud Deployment)
* **analyticsApi** – This endpoint needs to be accessible to the IDE plugin. If you are deploying Digma into your internal network and use a VPN to access that IP you can choose not to expose this service as a public IP.
* **jaeger** – Digma bundles its own Jaeger service that aggregates sample traces for various insights, performance metrics, and exceptions. If you do not wish to expose this endpoint or prefer to configure your APM as the trace source, you can choose to disable this endpoint. Digma does offer enhancements over Jaeger such as a two-way mapping between the code and the trace.
* ui - This endpoint serves the Digma web application as well as provides templates and other UI elements for Digma email reports.

Prerequisites:

* Access to a [Kubernetes](https://kubernetes.io/) cluster
* [Helm](https://helm.sh/docs/intro/install/) installed locally
* Have a license key. You can use the one provided to you or [create a free Digma Account](https://digma.ai/sign-up) to receive one.

Installing Digma in your org is recommended using our Helm chart.

### **Step 1: Add the Digma Helm repo**

```bash
helm repo add digma https://digma-ai.github.io/helm-chart/
helm repo update
```

### **Step 2: Create a values file to configure Digma**

You can use a `values.yaml`file to configure many aspects of how Digma will function in your environment. In this section, we'll review the critical ones, but you can find a more exhaustive list on our GitHub repo [here](https://github.com/digma-ai/helm-chart/tree/main/charts/digma-ng).&#x20;

#### License

The license key is the only mandatory parameter for setting up Digma.

```yaml
digma:
  licenseKey: ""
```

#### Networking

The service(s) created by the deployment can be exposed within or outside the cluster using any of the following approaches:

* **ClusterIP \[Default]**: This exposes the service(s) on a cluster-internal IP address. This approach makes the corresponding service(s) reachable only from within the cluster. Set service.type=ClusterIP to choose this approach.
* **Ingres**s: This requires an Ingress controller to be installed in the Kubernetes cluster. Set ingress.enabled=true to expose the corresponding service(s) through Ingress.
* **NodePort**: This exposes the service(s) on each node's IP address at a static port (the NodePort). This approach makes the corresponding service(s) reachable from outside the cluster by requesting the static port using the node's IP address, such as NODE-IP:NODE-PORT. Set service.type=NodePort to choose this approach.
* **LoadBalancer**: This exposes the service(s) externally using a cloud provider's load balancer. Set service.type=LoadBalancer to choose this approach.

The following are examples of common networking configurations:

* Nginx controller with private networking
* [Public ALB controller on AWS](https://github.com/digma-ai/helm-chart/blob/main/examples/aws/aws-alb-ingress-values.yaml)
* [Using load balancers with no ingress](https://github.com/digma-ai/helm-chart/blob/main/examples/general/load_balancers_only.yaml)

#### Storage&#x20;

If you're running Digma on a public cloud, you may run into an issue with persistent volume claims affinity. Unless you are using multi-zone volumes, volumes are typically bound to a specific availability zone. The pod must be set with an affinity to that zone to ensure it can still mount the volume when it scales up/down.&#x20;

Handling this is usually done by setting the [node affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity) on the deployment/stateful set.  The following example values file demonstrates how to add affinity for all relevant Digma resources.

{% embed url="https://github.com/digma-ai/helm-chart/blob/main/examples/node_affinity/affinity-values.yaml" %}

#### Email Preferences

To activate Digma's email notifications feature you will need an email gateway API key and URL that will be used to send out the emails, these should be set in the values file as shown below. In addition, you can set other preferences regarding delivery times and recipients.&#x20;

The daily reports often include links to issues, which require the report HTML to reference the Digma `ui` service DNS/IP. If you have set up a specific ingress for that service, you'll need to also specify it in the settings file to ensure the links are functional.  Enter the DNS/IP used for the `ui` service as `uiExternalBaseUrl` below. The deployment will try to autodetect it if not directly specified.

```yaml
digma:
    report:
        enabled: true
        # The DNS/IP of the Digma UI service 
        # (Will attempt to automatically detect if not set)
        uiExternalBaseUrl: "digma.ui.acme.com"   
        # These settings are provided by Digma
        emailGateway:
            apiKey: "ENTER_API_KEY_PROVIDED_BY_DIGMA_FOR_YOU_ACCOUNT"
            emailGateway.url: "ENTER_EMAIL_URL_PROVIDED_BY_DIGMA_FOR_YOU_ACCOUNT"
        # Time of day in which daily report will be sent, HH:mm:ss (24-hour format) 
        scheduledTimeUtc: "09:00:00"
        # Comma-separated list of email recipients
        recipients.to: 	"teamleads@acme.com"
        # Comma-separated list of email recipients in CC
        # recipients.cc: ""
        # Comma-separated list of email recipients in BCC
        # recipients.bcc: ""

```

#### Image pull secrets

If you're using image pull secrets to avoid image repository throttling you can specify them globally using this value:

```
global:
    imagePullSecrets: []
```

### **Step 3: Deploy the Helm file**

{% code overflow="wrap" %}
```bash
 helm upgrade --install digma digma/digma-ng -f ./your-value.yaml -n digma
```
{% endcode %}

### **Step 4: Post-configuration step - setting URLs**

{% hint style="info" %}
#### If you are using an Ingress for your Digma services with a defined hostname you can skip this step as Digma will automatically use the Ingress host&#x20;
{% endhint %}

#### Set the Digma UI link used in Email notifications

The Digma email reports include a link to the issue that requires the Digma UI service URL. You can set it in the values file as follows:

```yaml
digma:
    report:
        enabled: true
        # The DNS/IP of the Digma UI service 
        # (Will attempt to automatically detect if not set)
        uiExternalBaseUrl: "digma.ui.acme.com"  
```

Set the _`uiExternalBaseUrl`_ parameter to the IP, DNS, or external IP of the _`ui`_ service, which should be accessible to the end user. &#x20;

#### Set the Digma Jaeger URL for displaying traces in the web UI

The web UI contains links to view traces in the Digma Jaeger instance. Set the `publicBseUrl`  value to the  IP, DNS, or external IP of th&#x65;_`jaeger`_ service, which should be accessible to the end user. &#x20;

```
jaeger:
  # -- jaeger external or public URL, automatically detected if not set
  # @section -- Jaeger parameters
  publicBaseUrl: "digma.jaeger.acme.com"// Some code
```



### **Step 5: Validating the deployment**

To check everything is working properly we can check the pod status and make sure they are all in the ‘Running’ state:

`kubectl get pods -n digma`

For example, this is the expected output:

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Step 4: Get the IP/DNS value for the Digma deployment**

Run the following command to get the address assigned to the **Collector**, **Plugin-API,** and **Jaeger** endpoints (if enabled). You’ll need these to complete the setup. Note that external load balancers for public IPs may take additional time to set up the address.

`kubectl get services --namespace digma`

Depending on your setup type get the public or internal IP for the following ser

vices:

* `otel-collector:` Receiver for OTEL observability
* `analytics-api:` Provides the plugin with data and issues&#x20;
* `jaeger-ui:` Digma's embedded Jaeger services for displaying traces

Capture these addresses as you’ll need them later to setup your IDE plugin.

**Step 5: Final validation**

You can try calling the following API to validate connectivity and ensure Digma is up and running. You’ll need to use the ANALYTICS-API address you’ve captured in the above step. If you've set an access token, you need to provide it as well as a header for the request, as seen in the example below:

{% code overflow="wrap" %}
```bash
curl -k -sS -w "%{http_code}" --location "https://<ANALYTICS-API]/about"

```
{% endcode %}

If you are using the optional  `digmaAnalytics.accesstoken` parameter, add the following argument: `-H 'Digma-Access-Token: Token <ACCESS_TOKEN>` to the `curl` command.

If you received a non-error response back you’re good to go for the next step!

### Connecting your IDE to the Org Digma deployment

Once Digma is up and running you can now set your IDE plugin to connect to it. To do that, open the plugin settings (Go to IntelliJ IDEA -> Settings/Preferences and search for ‘Digma’)

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

* Set the `Digma API URL` parameter using the `analytics-api` value you’ve captured previously (By default this should be prefixed as ‘https’ and use port 5051)
* Set the `Runtime observability backend URL` parameter using the `otel-collector` value you’ve captured previously
* Set the `Jaeger Query URL`(if this option was enabled) using the `jaeger-ui` address you’ve captured previously.

Click `Apply`/`OK` to enable the changes and check that the Digma UI is not indicating any connection errors.


# Instrumenting your application on Kubernetes

### Using Helm and Kustomize

If your application is running on Kubernetes you can easily instrument it using Digma without changing the original Helm chart/YAML files.  We recommend using [Kustomize](https://kustomize.io/) for ease of use.

1. Install [Kustimize](https://kubectl.docs.kubernetes.io/installation/kustomize/).&#x20;
2. Clone or download our [helper](https://github.com/digma-ai/digma-helm-helper) repo&#x20;
3. Run the `create_customization.sh` script. You'll need to pass it some parameters based on the application  and the Digma `collector-api` IP/DNS address (read more [here](../../installation/central-on-prem-install.md)). Once you run this command, the helper scripts will generate a patch that can be applied with your Helm file to instrument the application. &#x20;

{% code overflow="wrap" %}
```bash
[PATH_TO_HELPER_REPO_ROOT]/kustomize/create_kustomization.sh [DIGMA_COLLECTOR_URL] [SERVICE_NAME] [ENVIRONMENT_NAME] [LABEL_TARGET_SELECTOR]
```
{% endcode %}

* `PATH_TO_HELPER_REPO_ROOT`: The location where you cloned the helper repo to
* `DIGMA_COLLECTOR_URL`: The URL of the Digma collector endpoint and port. For example: `http://internal.collector.dns:5050`
* `ENVIRONMENT_NAME`: The Digma [Environment](../../digma-core-concepts/environments.md) that will be associated with this application deployment observability (e.g. `TEST`, `PERF_TESTS`, `STAGING`)
* `LABEL_TARGET_SELECTOR`: These are selectors used to select which application to apply the instrumentation [patch](https://kubectl.docs.kubernetes.io/references/kustomize/kustomization/patches/) to.&#x20;

4. Finally, run your helm file with an additional  `--post-renderer` argument

{% code overflow="wrap" %}
```bash
helm template [NAME] [PATH_TO_HELM_CHART] -n [NAMESPACE} --post-renderer [PATH_TO_HELPER_REPO_ROOT]/kustomize/kustomize_build.sh 
```
{% endcode %}

### Updating the Helm file manually

The key steps to updating the application deployment are:

1. Mounting the OTEL agent and Digma agent extension to a volume accessible to the app container
2. Setting environment variables so that the Java process will use the OTEL agent and extension

See below an example of accomplishing these two steps using an init container and some environment variables. You can see the added code between the comment lines.

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}-deployment
  labels:
    app: pet-clinic-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: pet-clinic-app
  template:
    metadata:
      labels:
        app: pet-clinic-app
    spec:
      containers:
      - name: pet-clinic
        image: springio/petclinic:latest
#--------------------------------------------- 
# add instrumentation logic
        env:
        - name: JAVA_TOOL_OPTIONS 
          value: -javaagent:/shared-vol/otel-agent.jar -Dotel.javaagent.extensions=/shared-vol/digma-ext.jar -Dotel.exporter.otlp.traces.endpoint=http://meloona-digma-collector-api.meloona.svc.cluster.local:5050 -Dotel.traces.exporter=otlp -Dotel.metrics.exporter=none -Dotel.logs.exporter=none -Dotel.exporter.otlp.protocol=grpc -Dotel.instrumentation.common.experimental.controller.telemetry.enabled=true -Dotel.instrumentation.common.experimental.view.telemetry.enabled=true -Dotel.instrumentation.experimental.span-suppression-strategy=none -Dotel.service.name=spring-petclinic
        - name: OTEL_RESOURCE_ATTRIBUTES
          value: digma.environment=PETCLINIC

        volumeMounts:
        - name: shared
          mountPath: /shared-vol

      initContainers:
      - name: java-agent-initializer
        image: digmaai/java-agent-initializer:latest
        volumeMounts:
        - name: shared
          mountPath: /shared-vol

      volumes:
      - name: shared
        emptyDir: {}
#--------------------------------------------- 
---

apiVersion: v1
kind: Service
metadata:
  name: petclinic
spec:
  selector:
    app: pet-clinic-app
  ports:
  - port: 8080
    protocol: TCP
```

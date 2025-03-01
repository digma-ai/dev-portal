# Instrumenting your code in CI/Staging or the terminal

{% hint style="info" %}
Connecting Digma to your CI environment requires [deploying Digma centrally ](../../../installation/central-on-prem-install.md)in your org.
{% endhint %}

The most straightforward way to instrument your application is simply to download the OTEL agent and Digma Extension files and then set some environment variables and system properties so that they can instrument the Java process.

### 1. Create a CI/Prod environment using the Digma UI:

Start by creating an environment using the Digma Observability panel. Give the environment a meaningful name and select the CI/Prod environment type.

<figure><img src="../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

### 2. Update your build file or deployment script

You can use the below or similar logic to download the OTEL agent and set the environment variables to instrument the application.

<pre class="language-bash" data-overflow="wrap" data-line-numbers data-full-width="false"><code class="lang-bash"><strong>digma_url=[DIGMA_COLLECTOR_URL]
</strong><strong>
</strong>curl --create-dirs -O -L --output-dir /tmp/otel https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v2.10.0/opentelemetry-javaagent.jar 

<strong>curl --create-dirs -O -L --output-dir /tmp/otel https://github.com/digma-ai/otel-java-instrumentation/releases/latest/download/digma-otel-agent-extension.jar 
</strong><strong>
</strong>curl --create-dirs -O -L --output-dir /tmp/otel https://github.com/digma-ai/digma-agent/releases/latest/download/digma-agent.jar

export JAVA_TOOL_OPTIONS="-javaagent:/tmp/otel/digma-agent.jar \
-javaagent:/tmp/otel/opentelemetry-javaagent.jar \
-Dotel.javaagent.extensions=/tmp/otel/digma-otel-agent-extension.jar \
-Dotel.exporter.otlp.traces.endpoint=$digma_url \
-Dotel.traces.exporter=otlp -Dotel.exporter.otlp.protocol=grpc \
-Dotel.metrics.exporter=none -Dotel.logs.exporter=none \
-Dotel.instrumentation.common.experimental.controller.telemetry.enabled=true \
-Dotel.instrumentation.common.experimental.view.telemetry.enabled=true \
-Dotel.instrumentation.experimental.span-suppression-strategy=none \
-Dotel.instrumentation.jdbc-datasource.enabled=true"

export OTEL_SERVICE_NAME=[SERVICE_NAME]
export OTEL_RESOURCE_ATTRIBUTES=digma.environment=[ENV_NAME],digma.environment.type=Public

java app.jar
</code></pre>

Substitute the following values:

* Replace `[`DIGMA\_COLLECTOR\_URL`]` with your Digma Collector-API address. If you're running Digma locally, this would be http://localhost:5050 by default
* Make sure to substitute `[SERVICE_NAME]` with your application name:
* Substitute the `[ENVIRONMENT_NAME]` value based on the environment identifier in Digma.  To retrieve the environment identifier see the instructions on the [environment page](https://docs.digma.ai/digma-developer-guide/digma-core-concepts/environments#retrieving-the-environment-id).&#x20;
* If you would like to use HTTP rather than GRPC as the collector protocol, simply change the following argument above:`-Dotel.exporter.otlp.protocol=http`&#x20;








# Instrumenting your code in CI/Staging or the terminal

The most straightforward way to instrument your application is simply to download the OTEL agent and Digma Extension files and then set some environment variables and system properties so that they can instrument the Java process.

You can use this simple script from the terminal:

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
```bash
curl --create-dirs -O -L --output-dir /tmp/otel https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v2.1.0/opentelemetry-javaagent.jar 

curl --create-dirs -O -L --output-dir /tmp/otel https://github.com/digma-ai/otel-java-instrumentation/releases/latest/download/digma-otel-agent-extension.jar 

export JAVA_TOOL_OPTIONS="-javaagent:/tmp/otel/opentelemetry-javaagent.jar -Dotel.exporter.otlp.endpoint=[DIGMA_URL] -Dotel.javaagent.extensions=/tmp/otel/digma-otel-agent-extension.jar -Dotel.metrics.exporter=none -Dotel.logs.exporter=none -Dotel.exporter.otlp.protocol=grpc" 

export OTEL_SERVICE_NAME=[SERVICE_NAME]
export OTEL_RESOURCE_ATTRIBUTES=digma.environment=[ENVIRONMENT_NAME]

java app.jar
```
{% endcode %}

Substitute the following values:

* Replace `[DIGMA_URL]` with your Digma Collector-API address. If you're running Digma locally this would be http://localhost:5050 by default
* Make sure to substitute `[SERVICE_NAME]` with your application name:
* Substitute the `[ENVIRONMENT_NAME]` value based on the environment context in Digma.  You can simply enter `LOCAL` as a default value or create an environment in the Digma UI to see which value to enter here.&#x20;

### Tracking code changes- Adding Commit hashes to your observability

When new, unexpected or regression issues are detected, it is helpful to be able to track them in you gi history. Adding the commit history to the traces will allow Digma to narrow down which code changes might be responsible to different problems.&#x20;

To add the commit identifier to your traces,  set the following Resource Attribute: `scm.commit.id` on the trace. The easiest way to do it is via an environment variable. If you've can access the commit has from your CI, you can add update row `8` above with the new attribute. Here is an example for implementing that in a Github Action:

{% code overflow="wrap" %}
```bash
git_hash=`git rev-parse --short HEAD`
export OTEL_RESOURCE_ATTRIBUTES=digma.environment=[ENVIRONMENT_NAME],scm.commit.id=${git_hash}
```
{% endcode %}

This information will be used when identifying issues. For example, here is the ticket information for a specific issue found by Digma:



<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



### &#x20;


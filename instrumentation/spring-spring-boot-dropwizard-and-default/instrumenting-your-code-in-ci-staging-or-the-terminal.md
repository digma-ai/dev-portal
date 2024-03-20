# Instrumenting your code in CI/Staging or the terminal

The most straightforward way to instrument your application is simply to download the OTEL agent and Digma Extension files and then set some environment variables and system properties so that they can instrument the Java process.

You can use this simple script from the terminal:

{% code overflow="wrap" fullWidth="true" %}
```bash
curl --create-dirs -O -L --output-dir ./otel https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v2.1.0/opentelemetry-javaagent.jar 

curl --create-dirs -O -L --output-dir ./otel https://github.com/digma-ai/otel-java-instrumentation/releases/latest/download/digma-otel-agent-extension.jar 

export JAVA_TOOL_OPTIONS="-javaagent:/otel/opentelemetry-javaagent.jar -Dotel.exporter.otlp.endpoint=[DIGMA_URL] -Dotel.javaagent.extensions=/otel/digma-otel-agent-extension.jar -Dotel.metrics.exporter=none -Dotel.logs.exporter=none -Dotel.exporter.otlp.protocol=grpc" 

export OTEL_SERVICE_NAME=[SERVICE_NAME]
 export OTEL_RESOURCE_ATTRIBUTES=digma.environment=[ENVIRONMENT_NAME]

java app.jar
```
{% endcode %}

Substitute the following values:

* Replace \[DIGMA\_URL] with your Digma Collector-API address. If you're running Digma locally this would be http://localhost:5050 by default
* Make sure to substitute \[`SERVICE_NAME]` with your application name:
* Substitute the \[ENVIRONMENT\_NAME] value based on the environment context in Digma.  You can simply enter `LOCAL` as a default value or create an environment in the Digma UI to see which value to enter here.&#x20;

###

###

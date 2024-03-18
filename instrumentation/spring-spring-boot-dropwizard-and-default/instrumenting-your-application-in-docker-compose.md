# Instrumenting your application in Docker Compose

This is just a neat trick that allows you to collect observability data from your application running via Docker Compose _without_ changing the original docker-compose.yml file. We accomplish this by using an override file that will add the OTEL agent and set the appropriate environment variables which we can use in dev/test.&#x20;

1. Download the latest OTEL agent&#x20;

{% code overflow="wrap" %}
```
curl --create-dirs -O -L --output-dir ./otel https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v2.1.0/opentelemetry-javaagent.jar

curl --create-dirs -O -L --output-dir ./otel https://github.com/digma-ai/otel-java-instrumentation/releases/latest/download/digma-otel-agent-extension.jar
```
{% endcode %}

2. Add a Docker Compose override file

Create a supplementary Docker Compose file that will include the agent files and provide the environment variables to export tracing data to Digma.

<pre class="language-yaml"><code class="lang-yaml">#docker-compose.override.otel.yml 
version: '3' 

services: 
    [your-service]: 
        volumes: 
            - "./otel/opentelemetry-javaagent.jar:/otel/opentelemetry-javaagent.jar" 
            - "./otel/digma-otel-agent-extension.jar:/otel/digma-otel-agent-extension.jar" 
        environment:
            - JAVA_TOOL_OPTIONS=-javaagent:/otel/opentelemetry-javaagent.jar -Dotel.javaagent.extensions=/otel/digma-otel-agent-extension.jar
<strong>            - OTEL_SERVICE_NAME=[your-service]
</strong>            - OTEL_EXPORTER_OTLP_ENDPOINT=http://host.docker.internal:5050
            - OTEL_METRICS_EXPORTER=none
            - OTEL_LOGS_EXPORTER=none
            - OTEL_EXPORTER_OTLP_PROTOCOL=grpc
            - DEPLOYMENT_ENV=DOCKER_LOCAL 
        extra_hosts:
            - "host.docker.internal:host-gateway"
</code></pre>



3. Run your original Docker Compose file along with the override file

```bash
docker compose -f docker-compose.yml -f docker-compose.override.otel.yml up -d
```

# Instrumenting your application in Docker Compose

This is just a neat trick that allows you to collect observability data from your application running via Docker Compose _without_ changing the original docker-compose.yml file. We accomplish this by using an override file that will add the OTEL agent and set the appropriate environment variables which we can use in dev/test.&#x20;

### Prerequisite: Create an environment in Digma

Follow [these](../../../digma-core-concepts/environments.md#how-to-create-environments) instructions to create a private or CI/prod environment depending on your use case and required visibility for the new environment.&#x20;

### 1. Download the latest OTEL and Digma agents

<details>

<summary>MacOS / Linux</summary>

<pre data-overflow="wrap"><code><strong>curl --create-dirs -O -L --output-dir ./otel https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v2.1.0/opentelemetry-javaagent.jar
</strong>
curl --create-dirs -O -L --output-dir ./otel https://github.com/digma-ai/otel-java-instrumentation/releases/latest/download/digma-otel-agent-extension.jar

curl --create-dirs -O -L --output-dir ./otel https://github.com/digma-ai/digma-agent/releases/latest/download/digma-agent.jar
</code></pre>

</details>

<details>

<summary>Windows (PowerShell)</summary>

```powershell
# Create the directory if it doesn't exist
New-Item -ItemType Directory -Force -Path .\otel

# Download the first file
Invoke-WebRequest -Uri "https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v2.1.0/opentelemetry-javaagent.jar" -OutFile .\otel\opentelemetry-javaagent.jar

# Download the second file
Invoke-WebRequest -Uri "https://github.com/digma-ai/otel-java-instrumentation/releases/latest/download/digma-otel-agent-extension.jar" -OutFile .\otel\digma-otel-agent-extension.jar

# Download the third file
Invoke-WebRequest -Uri "https://github.com/digma-ai/digma-agent/releases/latest/download/digma-agent.jar" -OutFile .\otel\digma-agent.jar
```

</details>

### 2. Add a Docker Compose override file

Create a supplementary Docker Compose file that will include the agent files and provide the environment variables to export tracing data to Digma.

<pre class="language-yaml"><code class="lang-yaml">#docker-compose.override.otel.yml 
version: '3' 

services: 
    [your-service]: 
        volumes: 
            - "./otel/opentelemetry-javaagent.jar:/otel/opentelemetry-javaagent.jar" 
            - "./otel/digma-agent.jar:/otel/digma-agent.jar" 
            - "./otel/digma-otel-agent-extension.jar:/otel/digma-otel-agent-extension.jar" 
        environment:
            - JAVA_TOOL_OPTIONS=-javaagent:/otel/digma-agent.jar -javaagent:/otel/opentelemetry-javaagent.jar -Dotel.javaagent.extensions=/otel/digma-otel-agent-extension.jar
<strong>            - OTEL_SERVICE_NAME=[your-service]
</strong>            - OTEL_EXPORTER_OTLP_ENDPOINT=http://host.docker.internal:5050
            - OTEL_METRICS_EXPORTER=none
            - OTEL_LOGS_EXPORTER=none
            - OTEL_EXPORTER_OTLP_PROTOCOL=grpc
            - OTEL_RESOURCE_ATTRIBUTES=digma.environment=[ENV_NAME],digma.environment.type=Public
            - OTEL_INSTRUMENTATION_COMMON_EXPERIMENTAL_CONTROLLER_TELEMETRY_ENABLED=true
            - OTEL_INSTRUMENTATION.EXPERIMENTAL_VIEW_TELEMETRY_ENABLED=true
            - OTEL_INSTRUMENTATION.EXPERIMENTAL_SPAN_SUPPRESSION_STRATEGY=none
            - OTEL_INSTRUMENTATION_JDBC_DATASOURCE_ENABLED=true
        extra_hosts:
            - "host.docker.internal:host-gateway"
</code></pre>

If you've created a private environment, use the following value for `OTEL_RESOURCE_ATTRIBUTES` instead of what is listed above:

`OTEL_RESOURCE_ATTRIBUTES=digna.environment=[ENV_NAME],digma.environment.type=Private,digma.user.id=[USER_ID]`          &#x20;

To retrieve the values for ENV\_NAME, USER\_ID, or ENV\_TYPE click on the `How to setup` option in the observability panel on the environment tab.

### 3. Run your original Docker Compose file along with the override file

```bash
docker compose -f docker-compose.yml -f docker-compose.override.otel.yml up -d
```

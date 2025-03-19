# Instrumenting your code for tracing

Digma's main input is your code's OpenTelemetry traces. Depending on your application programming language and frameworks/libraries, you may want to select a different strategy for collecting this data or 'instrumenting' your app code.&#x20;

If you're not using OpenTelemetry yet, the [OTEL getting started page](https://opentelemetry.io/docs/getting-started/dev/) is a great place to start. In many cases, you won't need to make any modifications to your code to get this data.

Digma also provides additional helpers, guides, and tools to streamline this process. Check out our documentation as an example.

### Sending tracing data to Digma

If you're already using an OpenTelemetry Collector, follow the instructions here:[sending-data-to-digma-using-the-otel-collector.md](sending-data-to-digma-using-the-otel-collector.md "mention"). If you're not yet using a collector and want an easier setup you can just use the following environment variable to control the OTLP tracing export and disable logging and metrics export to Digma as they are not supported:

```bash
export OTEL_METRICS_EXPORTER=none
export OTEL_LOGS_EXPORTER=none
export OTEL_EXPORTER_OTLP_TRACES_ENDPOINT=$DIGMA_COLLECTOR_URL
```

### Adding Digma Attributes&#x20;

Digma relies on specific OTEL resource attributes to classify the observability data based on the service, the [environment](../digma-core-concepts/environments.md), etc. The way to add these attributes might differ depending on how OTEL is activated. A standard convention is to use the following environment variables:

```bash
export OTEL_SERVICE_NAME=$YOUR_APP_SERVICE_NAME
```

You also need to tag the observability data based on the Digma [environments.md](../digma-core-concepts/environments.md "mention"). This is done automatically when your code is instrumented by the Digma IDE plugin for relevant languages.

```bash
export OTEL_RESOURCE_ATTRIBUTES=digma.environment={ENV_NAME},digma.environment.type={Public|Private}
```

###







&#x20;

# Sending Data to Digma using the OTEL Collector

If you’re already using OpenTelemetry (OTEL), integrating with Digma is seamless—Digma provides an OTEL receiver, so you only need to configure your system to export tracing data.

Not using OTEL yet? No worries! Setting up OTEL instrumentation is straightforward in most programming languages, often requiring little to no code changes. Plus, Digma offers enhanced observability support for certain languages, enabling deeper tracing even if traceability wasn’t originally part of your design.

### If you're using an OpenTelemetry Collector

1. Add an OTLP exporter and supply the Digma URL (ingress DNS or IP) for the `otel-collector` service. See the [central-on-prem-install.md](../installation/central-on-prem-install.md "mention") page for more details.&#x20;

```yaml
# collector-config.yaml

receivers:
# ...
exporters:

  #... other exporters
  
  otlp/digma:
    endpoint: ${DIGMA_COLLECTOR_URL}
    tls:
      insecure: true
```

2. Update your observability pipeline to include sending traces to the Digma receiver as well:

```yaml
# collector-config.yaml

receivers:
# ..  
exporters:
# ..  
service:
  pipelines:
    traces:
      receivers: [otlp]
      exporters: [OTHER_EXPORTERS,otlp/digma]
      processors: [batch]

```



### Not using a collector?

If you're not using a dedicated collector component to route your observability, simply follow the steps to instrument your code using OTEL and set the following environment variable to ,&#x20;



### &#x20;






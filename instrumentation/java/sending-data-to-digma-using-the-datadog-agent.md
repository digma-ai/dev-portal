# Sending Data to Digma Using the Datadog agent

### Set up Dual Shipping&#x20;

If you're using the Datadog Agent (dd-agent) and not an OTEL agent/collector, you can forward traces to Digma using Datadog's[ dual shipping](https://docs.datadoghq.com/agent/configuration/dual-shipping/?tab=helm) feature.

To use this feature,  modify the agent's configuration to include Digma's DataDog receiver:

```yaml
apm_config:
  additional_endpoints:
    "[REPLACE_WITH_DIGMAS_COLLECTOR_DATADOG_ENDPOINT]":
    - datadog_reciver
```

Alternatively, you can add the following env variable:

```
DD_APM_ADDITIONAL_ENDPOINTS={"[REPLACE_WITH_DIGMAS_COLLECTOR_DATADOG_ENDPOINT]": ["datadog_receiver"]}
```

### Add tags to specify the Digma environment

Digma will automatically copy data from the Datadog traces such as the git commit hash, if present. However, to ensure the data is classified correctly within Digma, you need to add two additional tags to your tracing data. This can be done using environment variables.&#x20;









Alternatively,&#x20;

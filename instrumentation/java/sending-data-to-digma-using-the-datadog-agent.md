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







Alternatively,&#x20;

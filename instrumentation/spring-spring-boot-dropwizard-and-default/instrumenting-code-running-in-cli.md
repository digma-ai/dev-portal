# Instrumenting code running in CLI

When running Java applications using a Rune Configuration in the IDE, Digma detects that the code is being executed and automatically adds the necessary variables to instrument the process and send data to Digma. However,  If you're running your code via a command line interface and outside the IDE, the Digma plugin is unaware that this is happening and cannot apply this configuration.

Thankfully, you can set everything up before you run your code by running a simple script.

### Running using Bash/Linux

To ensure data is sent to your Digma deployment (locally or centrally) when running your application from a Bash CLI, simply run the following script:

{% embed url="https://github.com/digma-ai/digma/blob/main/dev/cli/enable_java_observability.sh" %}

You can download and execute the script locally, or simply run:

{% code overflow="wrap" %}
```bash
curl -o enable_observability.sh https://raw.githubusercontent.com/digma-ai/digma/main/dev/cli/enable_java_observability.sh && chmod +x enable_observability.sh && ./enable_observability.sh --service_name $YOUR_SERVICE_NAME
```
{% endcode %}

Replace or set $YOUR\_SERVICE\_NAME to the name of your application service. For example: `ACME_ORDERS_SERVICE`

### Running using PowerShell/Windows

To set all of the necessary environment variables and download the agent files when running on Windows, you can use the following PS1 script from PowerShell terminal:

{% embed url="https://github.com/digma-ai/digma/blob/main/dev/cli/enable_java_observability.ps1" %}

### Sending data to central Digma instance or to a specific environment

If you're running Digma centrally or wish to send data to a shared environment, you need to set some additional flags when you run the script. You can find a full list of the different configuration options using the `--help` argument.

```
Usage: ./setup_otel.sh --service_name <SERVICE_NAME> [options]

Mandatory arguments:
  --service_name            The name of the your application service (Required)

Optional arguments:
  --digma_collector_url     URL for the Digma collector (default: https://localhost:5050)
  --env_name                The environment name (default: Local)
  --public_env              Set the environment type to Public (default: Private)
  --user_id                 User ID (required for Private environment in centralized deployments)
                            You can find your user_id value by selecting the 'How to setup'
                            option in the environment tab menu in the observability panel.
  --digma_deployment        Digma deployment type: can be 'Local' or 'Central' (default: 'Local')
  --help                    Show this help message
```




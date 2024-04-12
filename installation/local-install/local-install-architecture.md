# Local Install Architecture

<figure><img src="../../.gitbook/assets/image (30).png" alt="" width="375"><figcaption><p>Digma Local Install Architecture</p></figcaption></figure>

The Digma Engine is defined in a simple Docker Compose [file](https://github.com/digma-ai/digma/blob/main/docker/docker-compose.yml) that is available online and consists of four containers:

* `Digma Compound`- This container holds the Digma analytics engine for processing traces
* `Digma Persistence` - DBs and storage for processing the time series data and aggregating it
* `Jaeger` - An embedded Jaeger instance that also has additional features for linking spans with code
* `Digma DS` - All of the data science and ML logic for detecting anomalies, calculating correlations, etc

### Default Ports

The following are the default ports used by Digma:

* `5050` is used to collect observability data. This will use the OTEL standard so can accept traces from any OTLP exporter.
* `5051` is used as a backend API for the plugin. The plugin uses it to retrieve and render the insights and processed data
* `17686` is the default embedded Jaeger port. This is used to render the visualization for traces including code location data.

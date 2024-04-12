# What is a Continuous Feedback platform?

Digma's focus is analyzing observability. The basic premise is that there is a lot of useful information in logs traces and metrics - they just require a lot more processing to glean any insights you can actually use as a developer. You can think of Digma as a data pipeline. Its main concern is not storing a lot of raw data but aggregating and processing it continuously, looking for anomalies, changes, and useful analytics.&#x20;

Digma ingests observability based on the [OTEL standard](https://opentelemetry.io/) (which it can also automatically collect using the IDE), processes the data, and then exposes insights to the IDE plugin which can map and connect it with the code.

<figure><img src=".gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

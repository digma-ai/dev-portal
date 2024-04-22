# Covering more of your code with Observability

Beyond the automatic instrumentation of server and client libraries, you may wish to achieve a better understanding of your code and domain logic by collecting more tracing data.

### Using the @WithSpan or @Observe annotations to observe specific methods&#x20;

Digma makes it easy to add additional observability coverage to any location. Placing the cursor inside any method you can click on the Observability icon in the Insights side panel to quickly add an annotation that will include its data in the traces.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Note: If you're using the Micrometer Tracing observability strategy in Digma, clicking on `Add Observability` will add an @Observe annotation. Otherwise, the @WithSpan annotation will be used.

### Keeping track of specific values or parameters

Sometimes you may wish to include additional data in the trace, such as parameters, results, counters, or any other data that may later be useful when reviewing the trace.&#x20;

OpenTelemetry provides an easy way to accomplish that using Span attributes.  The following code illustrates how to add any value to the trace.

```java
Span span = Span.current();

// Add a tag to the span
span.setAttribute("my-tag", "my-value");
```

### Automatically instrument your code without changing it using the new Digma Extended Observability feature (beta)

Digma is unrolling a new feature to allow developers to automatically instrument all functions in a specific package without having to add annotations. We are still collecting feedback so your ideas and suggestions are welcome!&#x20;

To enable `Extended Observability` open the Digma plugin settings page and type in the name of your application package under the `Extended Observability (beta)` property.

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

To set the same values from the terminal line you should set the following environment variable:

`export DIGMA_AUTOINSTRUMENT_PACKAGES=my.package.com`


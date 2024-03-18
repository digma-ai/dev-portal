# Automatic Instrumentation in the IDE

The easiest way to get started with Digma is to use the Digma plugin to automatically instrument your application when you run it in the IDE.

To get started, make sure that that `Obervability` toggle is set to on. You can always use this control to turn auto-instrumentation on and off.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

By default, when you enable the observability toggle, Digma will download and add the OTEL Java Agent and dynamically add it to your runtime configuration when you launch your application in the IDE. In addition,  the Digma Agent extension is also downloaded and referenced to add additional instrumentation data.&#x20;

### How to tell if your code is automatically instrumented with the Java Agent

Running your application in the IDE you should expect to see the following messages in the console output:

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

If everything works well, after triggering several actions on your applications you should see the observability panel update to show the recent activity:

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

### How do I know if my Java stack is supported?

The Java OTEL Agent [supported libraries page](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/supported-libraries.md) maintains an exhaustive list of frameworks and libraries currently automatically instrumented by the Java OTEL agent. For any of these frameworks, without any code changes, Digma will automatically receive and process tracing data that includes endpoint information, database queries, consumer data, and more. &#x20;

### What if your Run Configuration is not automatically instrumented

With the observability toggle enabled, auto-instrumentation will automatically be added to the following run configurations:

1. Java applications configuration type
2. Spring applications using the Spring plugin
3. Specific common Maven / Gradle tasks for running application
4. Other plugins (Tomcat, others)

However, Digma will purposely not instrument \*every\* Run Configuration, as it can be harmful to add the agent instrumentation to utility or build tasks. If Digma is not automatically adding instrumentation to your custom Gradle or Maven task, you can add the `DIGMA_OBSERVABILITY=true` environment variable. This will ensure the Digma Plugin will instrument the run configuration configuration.

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

### How do I cover more of my code?

Automatic instrumentation will provide tracing data for server libraries, database drivers, HTTP clients, queueing libraries, and more. However, if you want to cover more of your code you can use observability annotations or try out Digma's `Extended Observability` feature, still in beta. More details here.

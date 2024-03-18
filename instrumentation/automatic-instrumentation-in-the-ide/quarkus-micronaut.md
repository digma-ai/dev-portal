# Quarkus, Micronaut

### Quarkus

If you're using Quarkus then the recommended way to enable tracing is not via the OTEL agent but rather using the [Quarkus OTEL Extension](https://quarkus.io/guides/opentelemetry#quarkus-extensions-using-opentelemetry). Fortunately, the Digma plugin helps automate all of that setup.

Once you've loaded a project that contains Quarkus modules, the Digma plugin will automatically pick up on that, and within a few seconds present you with an option to configure the dependencies for you.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Clicking the link will add the needed dependencies to your `pom.xml` or `build.gradle` files.

Once the dependencies have been added, you'll be able to use the Digma observability toggle to turn tracing on and off. Similar to other frameworks, the project Run Configuration will be modified in runtime to include the necessary system properties to send tracing data to the Digma Analytics Engine.



###




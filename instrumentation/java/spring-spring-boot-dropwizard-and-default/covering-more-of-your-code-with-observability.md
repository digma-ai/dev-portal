# Covering more of your code with Observability

Beyond the automatic instrumentation of server and client libraries, you may wish to achieve a better understanding of your code and domain logic by collecting more tracing data.

### Using the @WithSpan or @Observe annotations to observe specific methods&#x20;

Digma makes it easy to add additional observability coverage to any location. Placing the cursor inside any method you can click on the Observability icon in the Insights side panel to quickly add an annotation that will include its data in the traces.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

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

Digma is rolling out a new feature to allow developers to automatically instrument all functions in a specific package without having to add annotations. We are still collecting feedback so your ideas and suggestions are welcome!&#x20;

### In the IDE

To enable `Extended Observability` Open the Digma plugin settings page and type in the name of your application package under the `Extended Observability (beta)` property.

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

### In testing/production environments

The Digma Java agent is a preprocessor that is able to inject the OTEL span attributes for methods under specific packages. This allows adding traceability to code without making any code changes.

1. Download the agent

{% code overflow="wrap" %}
```bash
curl -O -L https://github.com/digma-ai/digma-agent/releases/latest/download/digma-agent.jar
```
{% endcode %}

2. To use the agent, include it in your JVM options . If you're using multiple agents, make sure this one is first in the list, as it is a preprocessor.

<pre class="language-bash"><code class="lang-bash"><strong>export JAVA_TOOL_OPTIONS=-javaagent:/path/to/digma-agent.jar
</strong></code></pre>

3. Specify which package you'd like to trace via a separate environment variable:

```bash
export DIGMA_AUTOINSTRUMENT_PACKAGES=my.package.com
```

4. If you're using the Datadog Java agent,  configure DD to also accept the OTEL standard instrumentation attributes:

```bash
export DD_TRACE_OTEL_ENABLED=true
```

### Gotchas with automatic instrumentation

* Avoid instrumenting low-level packages that would inflate your traces to an unmanageable degree. Try to be granular about the code of interest, You can start with specific classes and expand to packages
* Apply on dev environments before you roll out to production&#x20;

### Excluding specific packages

If you see the traces contain too much info or if you're seeing warning that Digma is trimming the traces and wish to include more spans or remove some of the noise, you can also include an exclude expression. You can apply that as a comma separate list in the plugin settings or via the environment variable: `DIGMA_AUTOINSTRUMENT_PACKAGES_EXCLUDE_NAMES`

#### Excluding  methods by name

You can specify the name of the method explicitly by the name, the name relative to the class, or the fully qualified name. For example:  for example: `myMethod`, `MyClass.myMethod` and `com.org.myapp.MyClass.myMethod` would all exclude the method.

#### Excluding  methods by wildcard

You can also use wildcard expressions to exclude all methods that start with, end with or contain a specific string. For example: `get*` , `*String` or `*Serialization*`  would match `getUsers` `toString` and `runSerializationProcess` respectively.

You can also exclude methods under a specific class using a wildcard using the `#` character.  So that `com.example.MyClass#getU*` would match all methods under the class `MyClass` that start with the given expression.

#### Excluding  classes

You can exclude an entire class by simply specifying the simple or the fully qualified name. For example, both of these would work:`MyClass` or `com.org.myapp.MyClass`

#### Excluding packages

Simply specify the package name to exclude and the package along with all of its hierarchy will be excluded. For example: `org.company.myapp.domain.data`

#### Example expression

{% code overflow="wrap" %}
```bash
export DIGMA_AUTOINSTRUMENT_PACKAGES_EXCLUDE_NAMES=org.company.myapp.domain.data,MyClass#get*,*toString
```
{% endcode %}










# Spring, Spring Boot and default

### 1. Automatic OTEL agent instrumentation (default)&#x20;

This is the default strategy in most scenarios, when you enable the observability toggle, Digma will download and add the OTEL Java agent to the runtime configuration when you launch your application in the IDE. In addition,  the Digma agent extension is also downloaded and referenced to add additional instrumentation data.&#x20;

With the observability toggle enabled, auto-instrumentation will automatically be added to the following run configurations:

1. Java applications configuration type
2. Spring applications using the Spring plugin
3. Specific common Maven / Gradle tasks for running application
4. Other plugins (Tomcat, others)

#### How to tell if your code is automatically instrumented with the Java Agent

Running your application in the IDE you should expect to see the following messages in the console output:

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

If everything works well, after triggering several actions on your applications you should see the observability panel update to show the recent activity:

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

#### What if your Run Configuration is not automatically instrumented

Digma purposely will not instrument \*everything\* as it can be harmful to add the agent instrumentation to utility or build tasks. If Digma is not automatically adding instrumentation to your custom Gradle or Maven task, you can add the `DIGMA_OBSERVABILITY=true` environment variable. This will ensure the Digma Plugin will instrument the run configuration configuration.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

### 2. Using the Observable API and Micrometer Tracing

Instead of using the OTEL agent, Digma can leverage Micrometer Tracing to collect information about your Spring application. You can select the Micrometer Tracing strategy from the Digma plugin settings page.  Open the IntelliJ settings screen and search for `Digma` to bring up the plugin options, then select `Micrometer` from the `Spring boot observability mode` dropdown.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Click on 'Apply' and close the settings page. After a few seconds, Digma will suggest configuring your project for Micrometer, if not yet configured. That basically means adding the required dependencies to your `build.gradle` or `pom.xml` file, depending on how the project is set up.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

You can now run your application from the IDE as usual. Instead of adding the OTEL agent to the process, the Digma observability toggle will now switch micrometer tracing on or off and set the required parameters so that traces are sent to the Digma Analysis Engine.&#x20;

Please note that Micrometer Tracing is supported as of Spring Boot 3.x and above.

# Using Micrometer Tracing (Spring Boot 3.x only)



Instead of using the OTEL agent, Digma can leverage Micrometer Tracing to collect information about your Spring application. You can select the Micrometer Tracing strategy from the Digma plugin settings page.  Open the IntelliJ settings screen and search for `Digma` to bring up the plugin options, then select `Micrometer` from the `Spring boot observability mode` dropdown.

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Click on 'Apply' and close the settings page. After a few seconds, Digma will suggest configuring your project for Micrometer, if not yet configured. That basically means adding the required dependencies to your `build.gradle` or `pom.xml` file, depending on how the project is set up.

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

You can now run your application from the IDE as usual. Instead of adding the OTEL agent to the process, the Digma observability toggle will now switch micrometer tracing on or off and set the required parameters so that traces are sent to the Digma Analysis Engine.&#x20;

Please note that Micrometer Tracing is supported as of Spring Boot 3.x and above.

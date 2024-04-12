# Instrumentation Troubleshooting

<details>

<summary>Not seeing any Data in Digma</summary>

There could be multiple reasons for this. There are several things to check in such a scenario:

* When running your process, do you see an additional message indicating the code is being instrumented? You should either see a `This process is enhanced by Digma` message or some message listing injected observability properties.
* If you're using a custom Gradle/Maven task, Digma might not be picking it up. Give Digma a hint by adding the following environment variable to your run config: `DIGMA_OBSERVABILITY=true`
* Perhaps there is a mismatch between the instrumentation strategy Digma has selected and the one your framework requires. You can override the Digma inferred strategy by adding the `INSTRUMENTATION_FLAVOR` environment variable to your runtime configuration. Valid values are: `Default`, `Quarkus,``Micronaut`, `SpringBootMicrometer`, `OpenLiberty`, `JavaServer`
* Make sure your code is generating observability. While most server frameworks (like Spring or Dropwizard) do, others do not. To make sure, add a @WithSpan(kind=Spankind.Server) annotation above your root function. Then check again if that is being picked up by Digma.
* Validate that Digma is indeed receiving the observability data. You can open up the logs for the `digma-compound` container. You should see log messages with numbers of environments and picked-up traces as seen below. You should look to see if some log messages are showing non-zero values : <img src="../.gitbook/assets/image (33).png" alt="" data-size="original">
* Try using a named environment. On some versions of Digma the environment is matched to the user based on the hostname, which can be problematic on some systems. Create a local environment via the Digma observability panel and set the runtime configuration to use it:

<img src="../.gitbook/assets/image (34).png" alt="" data-size="original">

</details>

Can't find the answers you are looking for? Try out [Slack](https://join.slack.com/t/continuous-feedback/shared\_invite/zt-1hk5rbjow-yXOIxyyYOLSXpCZ4RXstgA) channel.

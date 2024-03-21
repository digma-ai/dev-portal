# Test observability

### Why use observability with tests

Tests can be a great source of observability. The ability to study the application in a controlled experiment, changing only the code each time - is a huge opportunity to uncover issues and study how the system behaves.

In practical terms, this means that Digma creates a two-way mapping between the test of each asset - database query, endpoint, code location, or consumer.  From the test level, you can identify issues and study system analytics under the test environment.

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Interestingly, from the scope of each asset, you can see which tests are triggering it, as well as any related insights and traces.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

### Running tests in the IDE

When you run your integration or end-to-end tests in the IDE, Digma will automatically pick up on that to add observability to each test context. Assuming that the Observabily Toggle is turned on, Digma will wrap each test in a trace and begin to analyze which assets were called and how they performed.

### Connecting your CI tests with Digma

Follow the instructions for instrumenting your app in CI as documented [here](../instrumentation/spring-spring-boot-dropwizard-and-default/instrumenting-your-code-in-ci-staging-or-the-terminal.md).&#x20;

You should create unique [environments](../digma-core-concepts/environments.md) for different test types, to avoid data anomalies and maintain consistentcy in the analytics.&#x20;


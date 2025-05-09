# Table of contents

* [Welcome to the Digma Docs!](README.md)
* [What is a Continuous Feedback platform?](what-is-a-continuous-feedback-platform.md)
* [Digma Quickstart](digma-quickstart.md)

## Installation

* [Local Install](<README (1).md>)
  * [Local Install Architecture](installation/local-install/local-install-architecture.md)
  * [Installation Troubleshooting](installation/local-install/installation-troubleshooting.md)
* [Central (on-prem) Install](installation/central-on-prem-install.md)
  * [Resource Requirements](installation/central-on-prem-install/resource-requirements.md)

## INSTRUMENTATION

* [Instrumenting your code for tracing](instrumentation/instrumenting-your-code-for-tracing.md)
* [Java](instrumentation/java/README.md)
  * [Automatic Instrumentation in the IDE (IntelliJ)](instrumentation/java/automatic-instrumentation-in-the-ide.md)
  * [Spring, Spring Boot, Dropwizard](instrumentation/java/spring-spring-boot-dropwizard-and-default/README.md)
    * [Instrumenting your code in CI/Staging or the terminal](instrumentation/java/spring-spring-boot-dropwizard-and-default/instrumenting-your-code-in-ci-staging-or-the-terminal.md)
    * [Instrumenting your application in Docker Compose](instrumentation/java/spring-spring-boot-dropwizard-and-default/instrumenting-your-application-in-docker-compose.md)
    * [Instrumenting your application on Kubernetes](instrumentation/java/spring-spring-boot-dropwizard-and-default/instrumenting-your-application-on-kubernetes.md)
    * [Covering more of your code with Observability](instrumentation/java/spring-spring-boot-dropwizard-and-default/covering-more-of-your-code-with-observability.md)
    * [Using GitHub Actions (beta)](instrumentation/java/spring-spring-boot-dropwizard-and-default/using-github-actions-beta.md)
    * [Using Micrometer Tracing (Spring Boot 3.x only)](instrumentation/java/spring-spring-boot-dropwizard-and-default/using-micrometer-tracing-spring-boot-3.x-only.md)
    * [Instrumenting code running in CLI](instrumentation/java/spring-spring-boot-dropwizard-and-default/instrumenting-code-running-in-cli.md)
  * [Quarkus, Micronaut, OpenLiberty](instrumentation/java/quarkus-micronaut.md)
* [.NET](instrumentation/.net.md)
* [Correlating observability and source code commits](instrumentation/correlating-observability-and-source-code-commits.md)
* [Sending Data to Digma using the OTEL Collector](instrumentation/sending-data-to-digma-using-the-otel-collector.md)
* [Sending Data to Digma Using the Datadog agent](instrumentation/sending-data-to-digma-using-the-datadog-agent.md)

## Use Cases

* [Design and write code more efficiently by understanding the system flows](use-cases/understand-the-application-flows-better-for-faster-development.md)
* [Get early feedback on bottlenecks and code issues](use-cases/get-early-feedback-on-bottlenecks-and-code-issues.md)
* [Prioritize Technical Debt](use-cases/prioritize-technical-debt.md)

## Digma Core Concepts

* [Environments](digma-core-concepts/environments.md)
* [Assets](digma-core-concepts/assets.md)
* [Analytics vs. Issues](digma-core-concepts/analytics.md)

## Digma Features

* [Issues](insights-documentation/insights/README.md)
  * [Suspected N+1](insights-documentation/insights/suspected-n+1.md)
  * [Excessive API calls (chatty API)](insights-documentation/insights/excessive-api-calls-chatty-api.md)
  * [Bottleneck](insights-documentation/insights/bottleneck.md)
  * [Scaling Issue](insights-documentation/insights/scaling-issue.md)
  * [Session In View Query Detected](insights-documentation/insights/session-in-view-query-detected.md)
  * [Query Optimization Suggested](insights-documentation/insights/query-optimization-suggested.md)
  * [High number of queries](insights-documentation/insights/high-number-of-queries.md)
  * [Slow Endpoint](digma-features/issues/slow-endpoint.md)
* [Analytics](insights-documentation/analytics/README.md)
  * [Top Usage](digma-features/analytics/top-usage.md)
  * [Request Breakdown](insights-documentation/analytics/request-breakdown.md)
  * [Duration](insights-documentation/analytics/duration.md)
  * [Code Nexus](digma-features/analytics/code-nexus.md)
  * [Duration Breakdown](digma-features/analytics/duration-breakdown.md)
  * [Endpoint Low/High Usage](digma-features/analytics/endpoint-low-high-usage.md)
* [Performance Impact](digma-core-concepts/performance-impact.md)
* [Test observability](digma-features/test-observability.md)
* [Issue Criticality](digma-core-concepts/criticality.md)

## Sample Projects

* [Spring Boot](sample-projects/spring-boot.md)

## Troubleshooting

* [Reporting Plugin Issues](troubleshooting/reporting-plugin-issues.md)
* [Digma Overload Warning](troubleshooting/digma-overload-warning.md)

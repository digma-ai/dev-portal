---
description: >-
  Assets are different components identified by Digma in the tracing data. The
  represent the sum of unique elements in the application.
---

# Assets

Asset categories include HTTP Endpoints, code locations, consumers, database queries, and more. In most cases, an asset correlates to a [Span](https://opentelemetry.io/docs/concepts/signals/traces/#spans) that has been categorized and processed in a specific way.&#x20;

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Another reason for categorizing spans into assets is to be able to better compare them. There is no sense in comparing an endpoint to a database query, for example. In each category, it is possible to sort the assets based on duration, performance impact, errors, and other criteria.&#x20;

## Asset Naming

Assets are assigned unique names based on their role and attributes that are often different from the Span name. . this is a prerequisite for any meaningful data aggregation. &#x20;

For example, this is the name given to a SQL query Span in a trace:










---
description: >-
  Code usage analytics can be critical to understand how the code works and roll
  out changes faster and without issues.
---

# Design and write code more efficiently by understanding the system flows

### See runtime usages

Digma overlays observability over code, so developers are able to see the application flows triggering any code location, query, http call, or any other asset. This provides an automatic view of any runtime dependencies.

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

### Traces tied to the code

Each flow include a sample trace for that specific flow, which in turn is fully connected back to the code, so developers can transition from code to trace and vice versa while staying inside the IDE.&#x20;

<figure><img src="../.gitbook/assets/flow2 (1).gif" alt=""><figcaption></figcaption></figure>

Note: Areas of the code that are especially risky to change will have the [Code Nexus](../digma-features/analytics/code-nexus.md) insight.

### Browse all assets used by a specific endpoint

You can navigate the [assets](../digma-core-concepts/assets.md) tree or take an overview of an entire endpoint request to list all of the different unique assets that take part in its execution flow. Assets could be sorted by recency, performance impact, and other criteria. For each of the assets, you can navigate to the related code, see other flows it affects&#x20;

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

### Find dead code

Any code that is not triggered will have the `Never reached` code lens attached to it. This is a good way to detect dead code that might be a candidate for removal.

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>


# Issue Criticality

Over time, Digma may find numerous issues related to your code, however not all issues are equal in impact and priority. Trying to handle all issues at once may result in micro-optimization that will not yield meaningful and effective results.&#x20;

To help deal with that concern, Digma calculates a `criticality` score for each insight. The insight criticality is calculated differently for local vs. shared environments and is intended to provide a good indication of which insights are worth looking into.

Criticality score components:

1. Severity - The insight severity measures the insight relative to the problem it is describing. For example: The N+1 issue severity is determined by the number of repeated queries whereas the Scaling issue severity is determined by the performance degradation slope. You can find a description of how each issue's criticality is measured on each issue's dedicated [page](../insights-documentation/insights/).&#x20;
2. Usage (shared environments) - The other component for calculating criticality is measuring how the insight is manifesting. Specifically, how many requests and user flows it is affecting. This is only relevant in non-local non-dev environments.

Insights that have a very high criticality score will be further highlighted in the UI and contain the `may affect production` message.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Finally, when using the Issues tab you can choose to sort by issue criticality to home in on the most critical issues.

# Performance Impact

Performance impact is a unique Digma feature that is only measured in real-world-like scenarios such as end-to-end testing and staging environments.  Therefore, this feature is only activated once you install Digma in a [central environment.](../installation/central-on-prem-install.md)&#x20;

### What is a performance impact?

Digma measures the performance of each asset, but looking at that number does not necessarily provide useful information about what requires optimization. For example, you may encounter queries that are pretty slow but are hardly used at all, or HTTP calls that take up a substantial amount but are called asynchronously or are a part of such a long operation that their effect on the whole request is negligible.&#x20;

The performance impact analysis aims to answer this very question. Namely - "punch for the bucks" How much would I gain in optimizing this particular asset?

### Where can I see the performance impact of an asset?

You can see the performance impact of each asset in the Assets tab, and even sort each category of assets based on that value to find the most impactful candidates for optimization.

You can also access the Digma dashboards via the Insights Panel to see a scoreboard for the most impactful client assets:

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>


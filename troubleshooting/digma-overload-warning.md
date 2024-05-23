# Digma Overload Warning

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Overload when using Digma locally

Since Digma is running locally on your development machine, it is set up to avoid consuming too much CPU resources. Therefore, instead of scaling up to handle traces concurrently, when Digma reaches a certain throughput limit, it will begin throttling incoming observability data. In essence, this means that some of the incoming traces will be dropped and Digma will continue to process traces at the same speed as before.

If you've received the `Digma Overloaded` warning and you would like to scale up Digma to process the additional data - you can [install a Centralized Digma](../installation/central-on-prem-install.md) on a local Kubernetes cluster.

### Overload when using Digma centrally

When deploying Digma centrally, the Analytics Engine will scale based on the deployment configuration. Digma will monitor the size of its queues to detect if it is still unable to catch up with incoming data. In such a scenario, Digma must begin throttling or else risk running out of memory or accumulating too much lag. In such a scenario, you will receive a message that throttling is in place. One way to avoid this state is to deploy Digma using a larger deployment size.  See the [central install documentation](../installation/central-on-prem-install.md) for more details.




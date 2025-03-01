# Correlating observability and source code commits

### Adding Commit hashes to your observability

When new, unexpected, or regression issues are detected, it is helpful to be able to track them in you gi history. Adding the commit history to the traces will allow Digma to narrow down which code changes might be responsible for different problems.&#x20;

To add the commit identifier to your traces,  set the following Resource Attribute: `scm.commit.id` on the trace. The easiest way to do it is via an environment variable. If you can access the commit from your CI, you can add an update row `8` above with the new attribute. Here is an example for implementing that in a Github Action:

{% code overflow="wrap" %}
```bash
git_hash=`git rev-parse --short HEAD`
export OTEL_RESOURCE_ATTRIBUTES=ddigma.environment=[ENV_NAME],digma.environment.type=Public,scm.commit.id=${git_hash}
```
{% endcode %}

This information will be used when identifying issues. For example, here is the ticket information for a specific issue found by Digma:

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

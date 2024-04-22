---
description: Couch to Continuous Feedback in less than five minutes
---

# Digma Quickstart

### Step 1 - Install the Digma plugin

You can find the Digma Plugin in the IntelliJ Plugin Marketplace in your IDE by searching for `Digma` or visit the [plugin page ](https://plugins.jetbrains.com/plugin/19470-digma-continuous-feedback)to get it directly from there.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Installing the plugin will also kick off the Digma Local Engine installation. If you have Docker installed and running on your machine that should happen automatically! You can also run Digma yourself using a simple Docker Compose file. See [README (1).md](<README (1).md> "mention")for more info.

### Step 2 -  Just Run your Code&#x20;

Actually, that's it!  The Digma plugin will take care of adding the instrumentation to your code, you can control this behavior with a simple toggle:

<figure><img src=".gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

### Where to see the data?

Digma has three main areas in the IDE where it makes the observability analysis available.

#### The Observability Panel&#x20;

This panel will show the latest traces picked up by Digma and is a great place to check and see if everything is working end-to-end. As you are debugging, testing, or running your code, you should always see the observability panel updated with the latest feedback and analysis results.&#x20;

<figure><img src=".gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

#### The Insights Panel

This panel is dedicated to a more in-depth analysis of each code location, asset, db query endpoint, etc.  It interacts with the code in the IDE and can either take you to the relevant code locations or show the insights (issues and analytics) related to the currently selected code:

&#x20;

<figure><img src=".gitbook/assets/image (38).png" alt="" width="280"><figcaption></figcaption></figure>

#### Code lens on the code itself&#x20;

With the plugin installed, you'll be able to see new code lens overlayed on the code itself indicating runtime usage, dead code, and critical insights:

<figure><img src=".gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>



### Bonus Steps:

Digma will provide more insights as more data becomes available to it. There are multiple way to increase your observability coverage:

* [covering-more-of-your-code-with-observability.md](instrumentation/spring-spring-boot-dropwizard-and-default/covering-more-of-your-code-with-observability.md "mention")
* [instrumenting-your-code-in-ci-staging-or-the-terminal.md](instrumentation/spring-spring-boot-dropwizard-and-default/instrumenting-your-code-in-ci-staging-or-the-terminal.md "mention")

###

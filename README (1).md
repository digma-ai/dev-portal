---
description: >-
  Installing Digma locally is pretty straightforward, you can choose whether you
  want Digma to install its Analytics Engine for you or do it on your own.
---

# Local Install

## Prerequisites

1. [IntelliJ](https://www.jetbrains.com/idea/) Community or Ultimate Edition (2022.3 and up are supported, though latest is recommended)
2. An application running [Java](https://www.java.com/en/) or [Kotlin](https://kotlinlang.org/) code
3. Docker installed and running - Can be either [Docker Desktop](https://www.docker.com/products/docker-desktop/), [Podman](https://podman.io/), [Rancher Desktop](https://rancherdesktop.io/) or [Colima](https://www.google.com/search?q=colima\&rlz=1C5CHFA\_enUS977US977\&oq=Colima\&gs\_lcrp=EgZjaHJvbWUqBggAEEUYOzIGCAAQRRg7MgYIARBFGDsyBggCEEUYOzIHCAMQABiPAjIGCAQQRRg7MgYIBRBFGDwyBggGEEUYPDIGCAcQRRg80gEIMTUwM2owajSoAgCwAgE\&sourceid=chrome\&ie=UTF-8)

<details>

<summary>Note to Colima Users</summary>

Please make sure to set the memory size to at least 3GB as we've had complaints of issues with memory sizes smaller than that.

```bash
colima start --memory 3
```

</details>

## 1. Install the Digma plugin in the IDE marketplace

The Digma Plugin is available on the IntelliJ Marketplace.

<figure><img src=".gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

You can install the plugin from your IDE or open the plugin [page](https://plugins.jetbrains.com/plugin/19470-digma-continuous-feedback) in your browser.

## 2. Setup the Digma Analytics Engine

Digma runs locally on your machine. To process all of the captured traces, analyze them, detect issues, and provide analytics, Digma relies on Docker containers. When not ingesting any traces, these containers are completely idle.

After the plugin installs you'll get to choose the preferred way to install the Digma Engine. Several options are available:

<figure><img src=".gitbook/assets/image (5) (1) (1).png" alt="" width="240"><figcaption></figcaption></figure>

<details>

<summary>Auto install (Default)</summary>

This is the default option. After installation, the plugin will try to start the Digma Engine containers on your local Docker environment and will offer clear controls to allow you to `Stop` `Start` or `Remove` it. The benefit of using this approach is that Digma will be able to also update the Engine automatically when a new release becomes available.

![](<.gitbook/assets/image (4) (1) (1) (1).png>)

</details>

<details>

<summary>Install Digma via Docker Compose</summary>

You can simply install Digma yourself using the Docker Compose file.

Simply select the `Docker Compose` tab from the onboarding page and follow the instructions to download the Docker Compose file and run it locally.

![](<.gitbook/assets/image (6).png>)

Notice that you can use this method to deploy to other Docker platforms Both Rancher Desktop and Podman support the Docker Compose spec so you can use [Rancher Compose](https://rancher.com/docs/rancher/v1.6/en/cattle/rancher-compose/) or [Podman Compose](https://docs.podman.io/en/latest/markdown/podman-compose.1.html) respectively.

</details>

<details>

<summary>Install the Docker Extension</summary>

Digma also comes bundled as a Docker Extension. If you're using Docker Desktop you can deploy the Digma Engine straight from the Docker Extensions Marketplace. The benefit is that the Engine will run in its own system space and will not create any confusion with the rest of the containers you may be running for other use cases.

You can install the Digma Extension from the Docker Marketplace or by visiting the [extension page](https://hub.docker.com/extensions/digmaai/digma-docker-extension).

</details>

### 3. (Optional) If you have a product key please enter it in the configuration stage of the onboarding process along with your email

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### How do I know Digma is Running?

If you've run Digma via any of the first two options, you can check that the Analytics Engine containers are up and running. In the IDE you should see both the Observability side panel and the Insights side panel showing up with no errors and waiting to receive data.

<figure><img src=".gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

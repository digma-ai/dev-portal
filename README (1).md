---
description: >-
  Installing Digma locally is pretty straightforward, you can choose whether you
  want Digma to install its Analytics Engine for you or do it on your own.
---

# Local Install

## Prerequisites

1. IntelliJ Community or Ultimate Edition
2. Java or Kotlin code
3. Docker installed and running - Can be either Docker Desktop, Podman or Rancher Desktop&#x20;

## 1. Install the Digma plugin in the IDE marketplace

The Digma Plugin is available on the IntelliJ Marketplace.&#x20;

<figure><img src=".gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

You can install the plugin from your IDE or browse to the plugin [page](https://plugins.jetbrains.com/plugin/19470-digma-continuous-feedback). &#x20;

## 2.  Setup the Digma Analytics Engine

Digma runs locally on your machine. To process all of the captured traces, analyze them and detect issues and code insights, digma relies on Docker containers. When not ingesting any traces, this containers are completely idle.

After the plugin installs you'll get to choose the preffered way to install the Digma Engine.  Several options are available:

<figure><img src=".gitbook/assets/image (5).png" alt="" width="240"><figcaption></figcaption></figure>

The Digma Engine is defined in a simple Docker Compose [file](https://github.com/digma-ai/digma/blob/main/docker/docker-compose.yml) that is available online and consists of four containers:

* `Digma Compound`- This container holds the Digma backend service for processing traces
* `Digma Persistence` - DBs and storage for processing the time series data and aggregating it
* `Jaeger` - An embedded Jaeger instance that also has additional features for linking spans with code
* `Digma DS` - All of the data science and ML logic for detecting anomalies, calculating correlations, etc.

<details>

<summary>Auto install  (Default)</summary>

This is the default option. After installation, the plugin will try to start the Digme Engine containers on your local Docker environment and will offer clear controls to allow you to `Stop` `Start` or `Remove` it.  The benefit of using this approach is that Digma will be able to also update the Engine when a new release becomes available.:&#x20;

![](<.gitbook/assets/image (4).png>)

</details>

<details>

<summary>Install Digma via Docker Compose</summary>

You can simply install Digma yourself using the Docker Compose file.&#x20;

Simply select the `Docker Compose` tab from the onboarding page and follow the instructions to download the Docker Compose file and run it locally.

![](<.gitbook/assets/image (6).png>)

Notice that you can use this method to deploy to other Docker platforms Both Rancher Desktop and Podman support the Docker Compose spec so you can use [Rancher Compose](https://rancher.com/docs/rancher/v1.6/en/cattle/rancher-compose/) or  [Podman Compose ](https://docs.podman.io/en/latest/markdown/podman-compose.1.html)respectively. &#x20;

</details>

<details>

<summary>Install the Docker Extension</summary>

Digma also comes bundled as a Docker Extension. If you're using Docker Desktop you can deploy the Digma Engine this way as well. The benefit is that the Digma Containers will run in their own system space and will not create any confusion with the rest of the containers you're running for your application.

You can install the Digma Extension from the Docker Marketplace or by visiting the [extension page](https://hub.docker.com/extensions/digmaai/digma-docker-extension).&#x20;

</details>

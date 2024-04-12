# Installation Troubleshooting

<details>

<summary>Port conflicts</summary>

If your system is using one of the default ports required by Digma, you can easily change the port configuration by modifying the Digma Docker Compose file.

To change the default Digma API or Jaeger ports simply add the below:

```
  jaeger:
    image: jaegertracing/all-in-one:1.45.0
    expose:
      - "5317"
    ports:
      - "[NEW_JAEGER_PORT]:16686"
      
  digma-compound:
    image: digmatic/digma-compound:0.2.249
    ports:
      - "5050:5050"
      - "[NEW_API_PORT]:5051"
```

If you need to change the default collector port (:5050), the change also requires an additional step of setting an environment variable as follows:

```
  digma-compound:
    image: digmatic/digma-compound:0.2.249
    ports:
      - “[NEW_COLLECTOR_PORT:NEW_COLLECTOR_PORT”
      - “5051:5051"
    environment:
      - Collector.Endpoints__Default__Port=NEW_COLLECTOR_PORT    
```

Finally, update the new ports in the plugin settings page which you can access via the IntelliJ settings page:

<img src="../../.gitbook/assets/image (24) (1).png" alt="" data-size="original">





</details>

<details>

<summary>Digma unstable - containers failed to connect or constantly disconnecting</summary>

This is often related to memory limits related to the resources assigned to your Docker platform. When Digma is busy processing data, some of its components might use up more memory, peaking at a little over 2GB before going down again.

1. Try increasing the memory available to the Docker VM to at least 3GB
2. Check the docker logs for the restarting container to pick up on any issues
3. If you are using Docker Desktop make sure you update it to the latest release. Some older versions of Docker Desktop suffer from know problems that affect Digma.

</details>

Can't find the answers you are looking for? Try out [Slack](https://join.slack.com/t/continuous-feedback/shared\_invite/zt-1hk5rbjow-yXOIxyyYOLSXpCZ4RXstgA) channel.

---
description: >-
  Environments represent different deployment stages or scopes. Typical
  environments would include - local development, load testing, CI, staging, or
  production.
---

# Environments

### Why it's important to have more than one environment

Digma excels in analyzing observability data, detecting changes, and measuring baselines. Lumping together data from dev, test, load testing, and production would create a huge mess with many strange statistical artifacts. Each time you run a load test you'll notice huge performance degradations while running in debug mode would manifest bugs in code that hasn't yet been checked in.

To bring some order into this chaos, Digma uses environments as an abstraction to measure data from different deployment stages and use cases separately.

### How to create environments

Private environments are easy to create in your local deployment.


# Resource Requirements

The following resources should be allocated to the Kubernetes Cluster, based on the Digma sizing specification.

### Sizing Table

| Szie     | CPU | RAM (GB) |
| -------- | --- | -------- |
| `Small`  | 10  | 16       |
| `Medium` | 14  | 20       |
| `Large`  | 16  | 20       |



#### Sizing considerations:

It is recommended to avoid using Spot Instances or the T class of instances in AWS which are limited and throttled in CPU/IO

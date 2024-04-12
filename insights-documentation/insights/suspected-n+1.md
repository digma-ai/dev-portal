---
description: >-
  N+1 queries are usually a result of modeling issues created by ORMs. They
  manifest in an excessive number of queries that can carry a performance cost.
---

# Suspected N+1

<figure><img src="../../.gitbook/assets/Suspected N-Plus-1 - illustration.svg" alt=""><figcaption></figcaption></figure>

### Description

N+1 Select are numerous SELECT queries often caused by ORM models. They can be resolved by eager loading relationships or using JOIN expressions. These selects are often more costly in production where the database roundtrip time is longer.

### Thresholds

The default threshold is an N of af at least `5` select queries on a relationship.

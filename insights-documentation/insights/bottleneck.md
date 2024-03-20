---
description: >-
  This insight identifies assets that hold up requests by taking a large portion
  of their time. An asset will not be considered a bottleneck if it is a part of
  a non-blocking asynchronous execution.
---

# Bottleneck

<figure><img src="../../.gitbook/assets/Bottleneck - illustration.svg" alt=""><figcaption></figcaption></figure>

### Description

This area significantly slows down the entire request. You should consider making this code asynchronous or otherwise optimize it.

### Thresholds

At least 30% of request time and a minimum duration of 20ms.

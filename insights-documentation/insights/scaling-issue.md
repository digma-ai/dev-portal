---
description: >-
  The scaling issue insight analyzes how the code performs when running
  concurrently and automatically tries to RCA the cause of any performance
  issues.
---

# Scaling Issue

<figure><img src="../../.gitbook/assets/Scaling Issue Found - illustration.svg" alt=""><figcaption></figcaption></figure>

### Description

Scaling issues are performance problems that emerge when the code is run concurrently. Digma analyzes the correlation between concurrency and performance and can detect when the degradation becomes problematic. To see a detailed analysis click on the `Histogram button`

### Thresholds

Found bad scaling in analyzing the concurrency graph. Requires four levels of concurrency to be measured at four different time intervals (different seconds).

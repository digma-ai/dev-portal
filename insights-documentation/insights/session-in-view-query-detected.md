---
description: >-
  Open Session in View is a common anti-pattern in which the database session is
  left open during view rendering, possibly resulting in lazy database queries
  at the rendering phase.
---

# Session In View Query  Detected

<figure><img src="../../.gitbook/assets/Session in View Query Detected - illustration.svg" alt=""><figcaption></figcaption></figure>

### Description

Open Session in View is an anti-pattern in which the view rendering stage triggers DB calls because of lazy properties initialization. It is recommended to pass DTOs to the view and avoid hitting the DB.

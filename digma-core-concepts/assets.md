---
description: >-
  Assets are different components identified by Digma in the tracing data. The
  represent the sum of unique elements in the application.
---

# Assets

Asset categories include HTTP Endpoints, code locations, consumers, database queries, and more. In most cases, an asset correlates to a [Span](https://opentelemetry.io/docs/concepts/signals/traces/#spans) that has been categorized and processed in a specific way.&#x20;

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

Another reason for categorizing spans into assets is to be able to better compare them. There is no sense in comparing an endpoint to a database query, for example. In each category, it is possible to sort the assets based on duration, performance impact, errors, and other criteria.&#x20;

## Asset Naming and Uniqueness

Assets are assigned unique names based on their role and attributes that are often different from the default Span name.  This is a prerequisite to being able to group and aggregate data about them.  This is why there isn't really a one to one mapping between spans and assets. another way to think about it is that a span is instanced in each trace while a Digma asset is extracted for multiple traces

Consider the following OTEL naming strategies vs. the name Digma assigned after some pre-processing.

Here are some examples:

| Span Type   | OTEL Naming                                                                 | OTEL Example                                    | Digma Naming                                                                                | Digma Example                                                                                                               |
| ----------- | --------------------------------------------------------------------------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Database    | SELECT \<DBNAME> for example: `SELECT 37b32f66-7a82-45f3-9d47-dc1d89b49ec7` | `SELECT 37b32f66-7a82-45f3-9d47-dc1d89b49ec7`   | Analyzes query syntax and generates a hash based query skeleton (without the parameters) .  | `select v1_0.pet_id,v1_0.id,v1_0.visit_date,v1_0.description from visits v1_0 where v1_0.pet_id=? order by v1_0.visit_date` |
| HTTP Client | HTTP \<VERB>                                                                | `HTTP GET`                                      | Either HTTP \<VERB> \<Target Microservice Route> or HTTP \<VERB> \<Targer Domain>           | `HTTP GET /users_service/{userId}`                                                                                          |












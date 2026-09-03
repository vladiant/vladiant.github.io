---
layout: post
title: "Observability Notes"
date: 2026-09-03
tags: development design coding distributed
---

## Guidelines
* Metrics to know something is wrong.
* Logs to understand what went wrong.
* Traces to see where it went wrong.

## Notes
* Enable trace sampling 6. In production, collecting absolutely every trace doesn't make sense—it's too much data. Typically, sampling is based on a percentage (for example, 5-10% of random requests) or on an event (always store erroneous/long-running requests). OpenTelemetry allows you to set simple sampling using OTEL_TRACES_SAMPLER=traceidratio and OTEL_TRACES_SAMPLER_ARG=<rate> or implement more flexible tail-based sampling at the Collector level (where the decision to store is made after the trace has completed, taking into account its contents). The choice depends on the requirements, but enabling 100% sampling is not recommended—otherwise, you'll either run out of resources or end up storing mountains of similar data.

* Be careful with attributes and tags. Don't write unique values, such as user IDs, email addresses, and so on, into trace attributes. Otherwise, your storages (like ClickHouse) will bloat due to an endless number of unique labels. Keep attributes limited to what's actually needed for aggregates and filters: service name, request type, status, error code.

* Standardize the names of custom spans and labels. If you manually add spans or custom tags, think of clear names and a consistent format for them. For example, you could name all your business logic spans with the BusinessLogic prefix—then you can use a single filter to find all similar operations in the UI. The same goes for tags: instead of using a variety of tags like user, user_id, and userId, choose a single style (you can rely on the semantic conventions of OpenTelemetry). This will improve system maintainability.

* Move common tags to the middleware. It often happens that each controller adds the same tags (e.g., client IP, etc.). Instead of copy-pasting each controller, create a middleware that will assign the necessary tags to Activity.Current at the beginning of a request. Then all traces will be enriched with this information immediately, and you won't have to remember to do so when writing each new endpoint.

* Configure filtering for sensitive data. Logs and traces may contain personal data or secrets. In production, it is highly recommended to use filtering to prevent passwords, API keys, or user data from accidentally leaking into the monitoring system.

## Examples
* <https://github.com/makushevski/OtelDotnetExample>
* <https://github.com/jbogard/presentations/tree/master/OpenTelemetryBrownfield/Examples>
* <https://github.com/martinjt/modern-observability>


## References
* [Наблюдаемость .NET-сервисов с помощью OpenTelemetry. Практический пример](https://habr.com/ru/articles/984252/)
* [OpenTelemetry: Semantic Conventions](https://opentelemetry.io/docs/concepts/semantic-conventions/)
* [OpenTelemetry: Handling sensitive data](https://opentelemetry.io/docs/security/handling-sensitive-data/)
* [OpenTelemetry: Sampling](https://opentelemetry.io/docs/concepts/sampling/)
* [Observability - Metrics, Logs, and Traces](https://www.systemdesignbutsimple.com/p/observability-metrics-logs-and-traces)
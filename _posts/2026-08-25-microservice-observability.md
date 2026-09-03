---
layout: post
title: "Microservice Observability"
date: 2026-08-25
tags: development design coding distributed
---

## Concepts

### Trace
The full story of a single request. Made of many spans. Has a `trace_id` so all pieces stay linked.

### Span
One timed step in that story (e.g., DB query, HTTP call, function). Starts, ends, and carries metadata.

### Root Span
The first span (no parent). Usually the inbound HTTP request, queue message, or scheduled job trigger.

### Child Span
A smaller step inside a bigger one. Lets you break work into clear pieces.

### Context
The “current trace + active span” that rides along your async calls and network hops so new spans attach correctly.

### Sampler
The rule that decides: keep (record/export) this trace or drop it to save cost/noise.

### Exporter
The piece that ships finished spans to your backend (OneUptime, Jaeger, Tempo, etc.).

### Metrics
The heartbeat of your application. They tell you what is happening, when it happened, and how often it occurs.

## Spans

### Guidelines
* Is this the first span created when the request hit this service? → SERVER.
* Are we calling something else over the network? → CLIENT.
* Are we putting a message on a queue/stream? → PRODUCER.
* Are we handling a message pulled from a queue/stream? → CONSUMER.
* Otherwise → INTERNAL

### Common pitfalls:
* Marking everything INTERNAL (loses semantics).
* Using SERVER for background cron jobs (better: INTERNAL or a synthetic root INTERNAL span). If it's externally triggered (e.g., HTTP webhook) then SERVER is correct.
* Using CLIENT for DB calls when the instrumentation already sets the appropriate kind (double-wrapping spans).

### Span Naming Best Practices
* Server spans: `HTTP {METHOD} {ROUTE} => HTTP GET /checkout`
* DB spans: `db.query.table.operation`
* External API: `domain_group.resource.action`
* Background job: `job.queue.task`

## Events

### Use events for:
*  Milestones: validation.start, cache.miss, retry, circuit.breaker.open
* State transitions: order.status.changed
* Intermittent detail you may want to filter on later (but not enough to justify a new span)

### Avoid events for:
* Highly repetitive signals (loop iterations, per-row processing)
* Bulk debug dumping (use logs with trace/span IDs instead)
* Long-running operations (use a child span instead so you get duration)

### Best practices:
* Limit to a handful (e.g., < 15) per span or you risk noise.
* Prefer consistent event names (verb.noun or domain.action).
* Add minimal attributes (keep cardinality low: attempt, status, not user_id).

### Anti‑patterns:
* Turning every function call into an event.
* Emitting repeating per-element events in large batches.
* Using events to store big blobs (stick to small primitives / short strings).

### Events vs spans vs logs (quick guide)
* Duration of a sub-operation `Child span`
* Single point-in-time marker `Event`
* Rich, possibly verbose diagnostic output `Log (with trace + span IDs)`
* Structured milestone you may query/filter `Event (with attributes)`

## Common Anti-Patterns
* Span explosion (creating spans inside tight loops > thousands/second).
* High-cardinality span names (embedding IDs, timestamps).
* Logging everything as events (events should be selective).
* PII in attributes (violates privacy/compliance).
* Mixing domains in one span (split DB, cache, external API).
* Forgetting to end spans (leads to memory leaks / incomplete traces).

## Types of Metrics

### Counter
* Monotonically increasing values that only go up (or reset to zero).
* `Use cases` Request counts, error counts, bytes processed 
* `Example` http.requests.total, database.connections.created

### UpDownCounter
* Values that can increase or decrease.
* `Use cases` Active connections, queue sizes, memory usage
* `Example` http.active_requests, database.connections.active

### Histogram
* Records distribution of values by automatically creating buckets to track how values are distributed across different ranges.
* `Use cases`
   * Request latencies and response times
   * Response payload sizes
   * Processing times and queue wait times
   * Database query durations
   * File upload/download sizes
   * Memory allocation sizes
* `Example metrics` http.request.duration, database.query.duration, file.upload.size

### Gauge
* Represents a current value that can arbitrarily go up and down.
* `Use cases` CPU usage, memory usage, temperature readings
* `Example` system.cpu.utilization, heap.memory.used

## Metrics vs Other Signals

### Use Metrics When:
* Monitoring trends over time (error rates, latency percentiles)
* Creating dashboards and alerts for SLI/SLO monitoring
* Tracking business KPIs (revenue, user growth, conversion rates)
* Resource utilization monitoring (CPU, memory, disk)
* High-frequency data that needs efficient storage

### Use Traces When:
* Debugging specific requests or investigating issues
* Understanding request flow across microservices
* Performance profiling at the individual request level
* Root cause analysis for specific incidents

### Use Logs When:
* Capturing detailed context about specific events
* Debugging application logic and business flows
* Compliance and audit requirements
* Unstructured data that doesn't fit metric patterns

## Reference
* [OpenTelemetry Traces & Spans Explained](https://oneuptime.com/blog/post/2025-08-27-traces-and-spans-in-opentelemetry/view)
* [What are metrics in OpenTelemetry: A Complete Guide](https://oneuptime.com/blog/post/2025-08-26-what-are-metrics-in-opentelemetry/view)

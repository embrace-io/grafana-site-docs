---
date: "2024-07-22T23:43:16+01:00"
description: Mobile OpenTelemetry signals.
keywords:
  - Embrace
menuTitle: OpenTelemetry signals
title: Mobile OpenTelemetry signals
weight: 3
---

# Mobile OpenTelemetry signals

Embrace's Android and Apple SDKs are built to emit and export [OpenTelemetry](https://opentelemetry.io) [traces](https://opentelemetry.io/docs/concepts/signals/traces/) and [logs](https://opentelemetry.io/docs/concepts/signals/logs/). 

Each concept in these SDKs is directly mapped to an OTel signal. For example, [sessions](./../sessions/) are modeled and exported as Spans, while breadcrumbs, which are short messages to provide timely context during a session, are SpanEvents on that session Span.

This telemetry can all be [exported directly from the Embrace SDK](./exporting-signals/) with the rich context of the user session.

{{< admonition type="note" >}}
OpenTelemetry support in Embrace's React Native, Unity, and Flutter SDKs is forthcoming as the OTel community grows to support these mobile platforms.
{{< /admonition >}}

## Traces

Duration-based telemetry captured by the Embrace SDKs are modeled as traces, often with a root span full of child spans.

### Sessions

As noted above, user sessions are modeled as Spans. In the Embrace SDK, these are particular Spans that begin when the user session starts, and ends when the session ends.

Session Spans also hold a variety of automatically-added [Attributes](https://opentelemetry.io/docs/concepts/signals/traces/#attributes) to capture important user and device information like country, app version, and device model.

### Networking

Network requests are also modeled as Spans. Embrace's mobile SDKs automatically track the entire duration of request and response as Spans. The SDKs also add important, mutable metadata for those requests in the form of attributes like `http.response.status_code`, which might not be added until the Span itself has been started.

### Instrumented tracing

The Embrace Android and Apple SDKs provide interfaces for tracing the key user flows of your applications. This functionality sits atop the OTel specification, as the instrumentation itself also allows for Embrace-specific [Performance tracing](./../../insights/performance-tracing/) to measure those key flows.

{{< code >}}
```kotlin
val embrace = Embrace.getInstance()
val activityLoad = embrace.startSpan("load-activity")

// create and start a child span if activityLoad is created and started successfully
val imageLoad = activityLoad?.let { embrace.startSpan("load-image", this) }

val image = fetchImage()

// record important event at point in time
imageLoad?.addEvent("network-request-finished")

// record attribute particular to this span instance
imageLoad?.addAttribute("image-name", image.name)

```
```java
Embrace embrace = Embrace.getInstance();
EmbraceSpan activityLoad = embrace.startSpan("load-activity");
EmbraceSpan imageLoad = null;

// create and start a child span if activityLoad is created and started successfully
if (activityLoad != null) {
    imageLoad = embrace.startSpan("load-image", activityLoad);
}

FancyImage image = fetchImage();

if (imageLoad != null) {
    // record important event at point in time
    imageLoad.addEvent("network-request-finished");

    // record attribute particular to this span instance
    imageLoad.addAttribute("image-name", image.name);
}
```
```swift
let parentSpan = Embrace
                .client?
                .buildSpan(name: "process-batch")
                .markAsKeySpan()
                .startSpan()

// Create a child span by setting the parent span prior to start
let childSpan = Embrace
                .client?
                .buildSpan(name: "process-item")
                .setParent(parentSpan)
                .startSpan()

// Add span events to mark points in time
childSpan.addEvent(
    name: "image-render-complete", 
    attributes: [ "size" : .int(3) ],
    timestamp: Date.now
)

// Add attributes to spans to provide context
childSpan.setAttribute(key: "product.id", value: "ABC123")
```
{{< /code >}}

## Logs

In general, any timestamped record is modeled as an OpenTelemetry log. 

For the mobile use-case, however, an important consideration is whether that record needs the context of the user session or other higher-level constructs. If the record can only be meaningful within the duration of a session, it is better added as, for example a SpanEvent on the session Span.

Thus, only point-in-time records that can exist atomically are mapped to logs in the Embrace SDKs. These consist mainly of crashes and exceptions, along with manual instrumentation that allows developers to add logs where they see fit.
---
date: "2024-07-22T23:43:16+01:00"
description: Auto-Instrumentation.
keywords:
  - Embrace
menuTitle: Instrumentation
title: Mobile instrumentation
weight: 2
---

# Mobile instrumentation

{{< param "PRODUCT_NAME" >}}'s mobile SDKs provide a variety of automatic and manual instrumentation to track your user experience.

## Automatic instrumentation

When you add {{< param "PRODUCT_NAME" >}} to your app, it begins to capture important telemetry from the moment it is added. 

Automatic reporting for mobile features likes sessions, crashes, and ANRs lets you construct what happened while the user was in your app. Additionally, country, device make and model, app version, and OS version are all automatically captured for aggregation and root cause analysis.

Further, networking details and results are automatically captured, allowing you to relate your app's outcomes to the wider set of services that power it.

## Manual instrumentation

Along with the automatic instrumentation of the {{< param "PRODUCT_NAME" >}} mobile SDKs, there are many tools for assessing the experience and performance specifically in your app. Rich contextual features like [Performance Tracing](./../../insights/performance-tracing/) allow you to track the success and failure of important user flows in your app. Additionally, features such as [breadcrumbs](https://embrace.io/docs/best-practices/breadcrumbs/?_highlight=breadcrumbs) and [personas](https://embrace.io/docs/ios/open-source/metadata-personas) give insight into the specifics of user activities and outcomes.

Most instrumentation is standardized across the mobile SDKs. For example, Performance Tracing is a duration-based tooling that must be started and stopped, with various attributes and events that can be added. The interface for creating and starting spans is paradigmatic across SDKs:


{{< code >}}
```kotlin
val activityLoad = Embrace.getInstance().startSpan("load-activity")
```
```java
EmbraceSpan activityLoad = Embrace.getInstance().startSpan("load-activity");
```
```swift
let span = Embrace
            .client?
            .buildSpan(name: "load-activity")
            .startSpan()
```
```csharp
Embrace.Instance.StartSpan("load-activity", startTimeMillisPosix);
```
```javascript
import { startSpan } from '@embrace-io/react-native-spans';

const spanId = await startSpan("load-activity")
```
```dart
final span = await Embrace.instance.startSpan('load-activity');
```
{{< /code >}}
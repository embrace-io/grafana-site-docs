---
date: "2024-07-22T23:43:16+01:00"
description: Export OpenTelemetry signals.
keywords:
  - Embrace
menuTitle: Export OpenTelemetry signals
title: Export OpenTelemetry signals
weight: 3
---

# Exporting OpenTelemetry signals

Telemetry captured by the Embrace SDK can be sent directly from the mobile app to any configured OTel Collector.

Telemetry can be sent to any OpenTelemetry Collector directly from an app using the SpanExporter and LogRecordExporter. Once they are configured, any telemetry will be sent to these exporters as soon as it is recorded. More than one exporter can be configured for each signal, but be aware that there can be a performance impact when sending too many network requests.

Currently, traces and logs can be exported using the Embrace Android SDK and Embrace Apple SDK. These signals can be sent directly to Grafana using [OTLP](https://grafana.com/docs/grafana-cloud/send-data/otlp/send-data-otlp/).

## Android

When using the Embrace Android SDK, all exporters must be configured **before** the SDK is started. Exporters added after the SDK has already been started will not be used.

{{< code >}}
```kotlin
Embrace.getInstance().addSpanExporter(mySpanExporter)
Embrace.getInstance().addLogRecordExporter(myLogExporter)

//gRPC through an OTel Collector in a local docker image
val customDockerExporter = OtlpGrpcSpanExporter.builder()
    .setEndpoint("https://otel-collector.mydomain.com:4317")
    .build()

Embrace.getInstance().addSpanExporter(customDockerExporter)

//HTTPS to an OTEL Collector in Grafana Cloud
val grafanaCloudExporter = OtlpHttpSpanExporter.builder()
    .setEndpoint("https://myinstance.grafana.net/otlp/v1/traces")
    .addHeader("Authorization", "YourToken")
    .build()

Embrace.getInstance().addSpanExporter(grafanaCloudExporter)
```
```java
Embrace.getInstance().addSpanExporter(mySpanExporter);
Embrace.getInstance().addLogRecordExporter(myLogExporter);

 //gRPC through an OTel Collector in a local docker image
OtlpGrpcSpanExporter customDockerExporter = OtlpGrpcSpanExporter.builder()
    .setEndpoint("https://otel-collector.mydomain.com:4317")
    .build();

Embrace.getInstance().addSpanExporter(customDockerExporter);

 //HTTPS to an OTEL Collector in Grafana Cloud
OtlpHttpSpanExporter grafanaCloudExporter = OtlpHttpSpanExporter.builder()
    .setEndpoint("https://myinstance.grafana.net/otlp/v1/traces")
    .addHeader("Authorization", "YourToken")
    .build();

Embrace.getInstance().addSpanExporter(grafanaCloudExporter);
```
{{< /code >}}


## iOS

In the Embrace Apple SDK, exporters are configured at the same time that the SDK itself is configured. Any [Swift-language OTel exporter](https://github.com/open-telemetry/opentelemetry-swift/tree/main/Sources/Exporters) can be attached as an optional value when the SDK is set up. Multiple span exporters can be attached during configuration by using the otel-swift MultiSpanExporter.

```swift
// logging span exporter outputting to the Xcode console
var loggingSpanExporter = StdoutExporter()

// gRPC span exporter to an OTel Collector in a local docker image
var otelCollectorSpanExporter: OtlpTraceExporter {
    let config = ClientConnection.Configuration.default(
        target: ConnectionTarget.hostAndPort("localhost", 4317),
        eventLoopGroup: MultiThreadedEventLoopGroup(numberOfThreads: 1)
    )
        
    let client = ClientConnection(configuration: config)
    return OtlpTraceExporter(channel: client)
}

// HTTP span exporter to OTel Collector in Grafana Cloud
var grafanaOtelSpanExporter: OtlpHttpTraceExporter {
    let grafanaCloudTokenString = //String generated from your account
    let urlConfig = URLSessionConfiguration.default
    urlConfig.httpAdditionalHeaders = ["Authorization": "Basic \(grafanaCloudTokenString)"]
            
    return OtlpHttpTraceExporter(
        endpoint: URL(string: "https://otlp-gateway-prod-us-east-0.grafana.net/otlp/v1/traces")!,
        useSession: session
    )
}

// configure Embrace Apple SDK, with all three span exporters attached
try? Embrace
    .setup(
        options: Embrace.Options(
            appId: "AppID",
            export: OpenTelemetryExport(
                spanExporter: MultiSpanExporter(
                    spanExporters: [
                        loggingSpanExporter, 
                        otelCollectorSpanExporter,
                        grafanaOtelSpanExporter 
                        ]
                ),
                logExporter: nil
            )
        )
    )
    .start()
```
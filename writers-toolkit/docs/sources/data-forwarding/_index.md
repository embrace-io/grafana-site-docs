---
date: "2024-07-22T23:43:16+01:00"
description: Understand how to send your Embrace data to Grafana.
keywords:
  - Embrace
menuTitle: Data forwarding
title: Embrace data forwarding
weight: 4
---

# Embrace data forwarding

Embrace delivers context-rich mobile data to Grafana Cloud in the form of metrics and traces. Embrace's data seamlessly integrates with the LGTM stack in a number of ways, outlined below.

## Metrics

### Data Destinations

To forward your [Metrics](./../insights/dashboard-metrics/) to Grafana Cloud, Embrace offers a "push" method called [Data Destinations](./data-destinations/). In a set time interval, Embrace will forward such "standard metrics" as `crash total` and sessions total to Grafana. Additionally, Embrace users can create Custom Metrics according to their own criteria, and also forward these via Data Destinations.


### Metrics API

Embrace also offers a "pull" method for metrics in the form of our public [Metrics API](./metrics-api/). You can directly query Embrace's metrics from your backend using the [PromQL query language](https://prometheus.io/docs/prometheus/latest/querying/basics/).

## Traces

### Spans API

Similarly to the Metrics API, Embrace also offers a public [Spans API](./spans-api/) for trace querying. With the [TraceQL query language](https://grafana.com/blog/2023/02/07/get-to-know-traceql-a-powerful-new-query-language-for-distributed-tracing/), you can use the Grafana Tempo HTTP API to pull queries from Embrace into your Grafana project.


### End to end network requests

Network Span Forwarding is an end-to-end network tracing feature offered by Embrace and Grafana.
 
With this feature enabled in Embrace, you can trace the result of a networking request from the mobile device to your web service, with rich detail in both the Embrace dashboard and Grafana Cloud. The [w3c traceheader](https://www.w3.org/TR/trace-context-1/#traceparent-header) connects networking requests in your web service to activity in your mobile app.

## OpenTelemetry Export

The Embrace Android and Apple SDK allow for export of logs and traces from the mobile client. See [exporter documentation](./../mobile-signals/opentelemetry-signals/exporting-signals/) for more information.


## Questions and feedback

{{< param "PRODUCT_NAME" >}}'s mobile SDKs are open-sourced in the [{{< param "PRODUCT_NAME" >}} GitHub page]({{< param "GITHUB_ORG_URL" >}}).

If you have questions, you can ask them in the [Embrace Community Slack]({{< param "COMMUNITY_URL" >}}).

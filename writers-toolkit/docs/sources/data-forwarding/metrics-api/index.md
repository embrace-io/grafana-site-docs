---
date: "2024-07-22T23:43:16+01:00"
keywords:
description: Understand Embrace's Metrics APIs using PromQL.
  - Embrace
menuTitle: Metrics APIs
title: Metrics APIs
weight: 3
---

# Metrics APIs

Embrace provides APIs for querying metrics into Grafana, whether or not you have created Custom Metrics of your own in the Embrace dashboard.

The Embrace Metrics API allows you to query your Standard and Custom Metrics from Embrace using PromQL. In the Grafana dashboard, you can query the Metrics API using the URL `https://api.embrace.io/metrics`.

{{< admonition type="note" >}}
There is a Custom Metrics API, using the URL `https://api.embrace.io/custom-metrics`. You likely will not need this, as Custom Metrics created in the Embrace dash can be directly queried using the the Metrics API
{{< /admonition >}}


## Adding Metrics API as a Data Source

In your Grafana dashboard:

- Click the gear icon to go to the Configurations page.
- Click on "Add data source" and select Prometheus.
- Name your source "embrace-metrics-api" and set the following fields:
- URL: https://api.embrace.io/metrics
- Under Custom HTTP Headers, add a header with a name `Authorization` and use `Bearer <YOUR_API_TOKEN>` as your token string. For example, if your API token is `e2d75f07a40843f0b8a53d1e3201edba`, your token string should be `Bearer e2d75f07a40843f0b8a53d1e3201edba`.

Once you've added the Authorization, you should be able to make PromQL queries in Grafana according to your Standard Metric dimensions:
```
// Sample Standard Metric query
hourly_sessions_total{app_id="<app ID>"}
```

For more information about using the Metrics API in Grafana, see [Embrace documentation](https://embrace.io/docs/embrace-api/grafana_integrations/).

## Supported Custom Metrics

The following metrics are supported as Custom Metrics. Metrics with the suffix "_total" are gauges.

| Metric                                     | Description                                  | Filters                                                                                      | Group by granularity                                                    | Time granularity           |           
|--------------------------------------------|----------------------------------------------|----------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|----------------------------|
| anrs_total                                 | Number of anrs                               | method, sample_type                                                                          |                                                                         | five_minute, hourly, daily |
| crashes_total                              | Number of crashes                            | msg, tag_name, tag_value,                                                                    |                                                                         | five_minute, hourly, daily |
| flutter_exceptions_total                   | Number of flutter exceptions                 | group_id, is_handled, msg, state                                                             | group_id, msg                                                           | five_minute, hourly, daily |
| logs_total                                 | Number of moments                            | log_property_key, log_property_value, msg, type                                              | log_property_value                                                      | five_minute, hourly, daily |
| moments_total                              | Number of moments                            | duration_bucket, moment_property_key, moment_property_value, name                            | duration_bucket, moment_property_value                                  | five_minute, hourly, daily |
| network_requests_successful_duration_total | Sum of successful network requests durations | domain, method, path                                                                         | top_n_domain, top_n_path                                                | hourly, daily              |
| network_requests_successful_total          | Number of successful network requests        | domain, duration_bucket, method, path                                                        | top_n_domain, top_n_path                                                | hourly, daily              |
| network_requests_total                     | Number of network requests                   | domain, method, path, status_code                                                            | status_code, top_n_domian, top_n_path                                   | five_minute, hourly, daily |
| sessions_total                             | Number of sessions                           | has_anr, session_property_key, sessions_property_value                                       | session_property_value                                                  | five_minute, hourly, daily |
| sessions_duration_total                    | Sum of sessions durations                    | has_anr, session_property_key, sessions_property_value                                       | session_property_value                                                  | five_minute, hourly, daily |
| traces_total                               | Number of root traces                        | trace_attribute_key, trace_attribute_value, trace_duration_bucket, trace_name, trace_outcome | trace_attribute_value, trace_duration_bucket, trace_name, trace_outcome | five_minute, hourly, daily |
| traces_duration_total                      | Sum of root traces duration                  | trace_attribute_key, trace_attribute_value, trace_name, trace_outcome                        | trace_attribute_value, trace_name, trace_outcome                        | five_minute, hourly, daily |
| unity_exceptions_total                     | Number of unity exceptions                   | group_id, is_handled, msg, state                                                             | group_id, msg                                                           | five_minute, hourly, daily |


---
cascade:
  FULL_PRODUCT_NAME: Embrace Mobile
  PRODUCT_NAME: Embrace
  GITHUB_ORG_URL: https://github.com/embrace-io
  COMMUNITY_URL: https://community.embrace.io
  search_section: Embrace Mobile
  search_type: doc
hero:
  title: Embrace Mobile Observability
  level: 1
  image: ./assets/embrace_logo_square_black.svg
  width: 110
  height: 100
  description: >-
    Instrument mobile applications with Embrace to unite mobile and backend observability and measure real user impact.
cards:
  title_class: pt-0 lh-1
  items:
    - title: Get started
      href: ./get-started/
      description: Learn how to add Embrace to your mobile application.
    - title: Mobile signals
      href: ./mobile-signals/
      description: Use instrumentation to capture telemetry from your mobile application.
    - title: Dashboard insights
      href: ./insights/
      description: Learn about the performance and user insights Embrace's dashboard provides for mobile developers.
    - title: Data forwarding
      href: ./data-forwarding/
      description: Use Embrace's forwarding features and APIs to connect your mobile data to Grafana for end-to-end observability.
date: "2024-07-22T23:43:16+01:00"
description: |
  A guide to using Embrace for Mobile Observability
keywords:
  - Embrace
  - documentation
  - mobile
menuTitle: Embrace Mobile Observability
title: Embrace Mobile Observability
weight: 0
---

{{< docs/hero-simple key="hero" >}}

---

# {{< param "FULL_PRODUCT_NAME" >}} Observability

{{< param "PRODUCT_NAME" >}} integrates seamlessly with your LGTM stack to bring mobile and backend observability together into one picture. 

{{< param "PRODUCT_NAME" >}} is much more than mobile monitoring. {{< param "PRODUCT_NAME" >}}'s mobile signal capture, insights, and data forwarding allow you to build reliable, performant mobile ecosystems. {{< param "PRODUCT_NAME" >}}'s [mobile SDKs]({{< param "GITHUB_ORG_URL" >}}) capture all the important signals of mobile app, device, and user activity, allowing you to switch from reactive crash monitoring to proactive performance assessment and issue remediation. 

## Overview

{{< param "PRODUCT_NAME" >}}’s mobile SDKs and data services are designed to:
- [**Capture mobile application performance telemetry**](./mobile-signals/)
- [**Provide meaningful insights into user flows and network activity**](./insights/)
- [**Forward raw and aggregated telemetry to Grafana, using OpenTelemetry**](./data-forwarding/)

## Explore

{{< card-grid key="cards" type="simple" >}}

## Questions and feedback

{{< param "PRODUCT_NAME" >}}'s mobile SDKs are open-sourced in the [{{< param "PRODUCT_NAME" >}} GitHub page]({{< param "GITHUB_ORG_URL" >}}).

If you have questions, you can ask them in the [Embrace Community Slack]({{< param "COMMUNITY_URL" >}}).

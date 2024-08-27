---
date: "2024-07-22T23:43:16+01:00"
description: Set up Embrace SDK in your mobile app.
keywords:
  - Embrace
menuTitle: Add Embrace to mobile app
title: Add the Embrace SDK to your mobile app
weight: 3
---

# Add the {{< param "PRODUCT_NAME" >}} SDK to your mobile app

# Overview

Once you've configured your app in the {{< param "PRODUCT_NAME" >}} dash, you should add the relevant mobile platform's SDK to your application. There are different integration steps for each platform, as outlined below.

{{< param "PRODUCT_NAME" >}} will test the integration when the SDK is added. You'll know that your integration works when you begin to see [session data](./../../mobile-signals/sessions/) in the {{< param "PRODUCT_NAME" >}} dashboard:

<img src="./../../assets/embrace-dash-with-sessions.png" alt="Embrace dash with sessions" height="150px">

# Platform-specific instructions

{{< admonition type="note" >}}
Your App ID and API Token, created when you [configured your app](./../configure-app-in-embrace/), can be found in the settings page of your {{< param "PRODUCT_NAME" >}} dashboard.
{{< /admonition >}}

You can find instructions for:
- [native Android SDK](./android/)
- [native Apple SDK](./iOS/)
- [hybrid SDKs](./hybrid-sdk/)

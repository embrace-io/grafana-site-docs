---
date: "2024-07-22T23:43:16+01:00"
description: Configure a new app in your Embrace dashboard.
keywords:
  - Embrace
menuTitle: Configure your app
title: Configure your app
weight: 2
---

# Configure your app in the {{< param "PRODUCT_NAME" >}} dashboard

## Dashboard steps

Once you have [created an {{< param "PRODUCT_NAME" >}} account](./../create-account/), you can use the dashboard to configure mobile applications that you want to add {{< param "PRODUCT_NAME" >}}'s instrumentation to.

To configure a new app, you can tap the "Create Project" button at the top of your project list:

 <img src="./../../assets/embrace-dash-create-project.png" alt="Embrace dash create project" height="100px">

This will bring you to a screen with multiple fields to select:

1. Give your app a name that you will later find it with.
1. Select the platform that your app is built on. You can select native Android or iOS. For each "hybrid" platform - React Native, Unity, Flutter - you should select one native platform (Android or iOS) at this step, and should create a separate project for the other native platform if you will be developing on both.
1. Determine whether this app will be for production builds or development builds.

 <img src="./../../assets/embrace-create-app-page.png" alt="Embrace create app page" height="100px">

## Completed configuration

Configuring an app in the dashboard creates an **APP ID** for that app. The APP ID is a five-character key that will be used to connect the SDK to the {{< param "PRODUCT_NAME" >}} dashboard. Additionally, a longer **API TOKEN** string will be generated and used in some places. These values are always accessible from the Settings page in your dashboard.

Once you've configured your app in the dashboard, you will find platform-specific steps for [adding {{< param "PRODUCT_NAME" >}} to your mobile app](./../add-embrace-in-your-application/).
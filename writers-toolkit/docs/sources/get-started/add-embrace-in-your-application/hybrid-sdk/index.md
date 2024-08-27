---
date: "2024-07-22T23:43:16+01:00"
description: Set up Embrace Android SDK in your mobile app.
keywords:
  - Embrace
menuTitle: Hybrid SDKs
title: Add a hybrid Embrace SDK to your mobile app
weight: 3
---

# Add a hybrid {{< param "PRODUCT_NAME" >}} SDK to your mobile app

The {{< param "PRODUCT_NAME" >}} React Native, Unity, and Flutter SDKs are all built upon the native Android and iOS SDKs. This means when you add the hybrid SDK to your app, you will need to link to one native platform with an App ID and the other native platform with a different App ID.

Each hybrid SDK has specific setup steps for linking the Android and iOS dependencies. See the sections below for specifics. For more configuration information and options, you can view in-depth integration guides:
- [React Native](https://embrace.io/docs/react-native/integration/add-embrace-sdk/)
- [Unity](https://embrace.io/docs/unity/integration/)
- [Flutter](https://embrace.io/docs/flutter/integration/add-embrace-sdk/)

## React Native

### Add the JavaScript library

Use Yarn or NPM to install the NPM module.

```
yarn add @embrace-io/react-native
//or
npm install @embrace-io/react-native --save
```

### Adding the {{< param "PRODUCT_NAME" >}} React Native SDK

The {{< param "PRODUCT_NAME" >}} React Native SDK has a setup script that modifies the files in your project to add native dependencies. The setup scripts can be found in your `node_modules` folder at `node_modules/@embrace-io/dist/scripts/setup`

There is one setup script for each platform:
```
//Android
node node_modules/@embrace-io/react-native/lib/scripts/setup/installAndroid.js

//iOS
node node_modules/@embrace-io/react-native/lib/scripts/setup/installIos.js
```

## Unity

The easiest way to install {{< param "PRODUCT_NAME" >}} Unity SDK is to download the latest SDK:

- [Download Link for {{< param "PRODUCT_NAME" >}} Unity SDK](https://downloads.embrace.io/EmbraceSDK_1.26.1.unitypackage)

Once downloaded, import the Unity Package by selecting `Assets -> Import Package -> Custom Package`.

### Scoped Registries

Scoped Registries allow Unity to communicate the location of any custom package registry server to the Package Manager so that the user has access to several collections of packages at the same time. {{< param "PRODUCT_NAME" >}} uses Scoped Registries to allow our users to manage, download and install our SDK using the built-in Unity Package Manager.

### Configuring Unity for Native platforms

The {{< param "PRODUCT_NAME" >}} Unity SDK includes an editor script to assist with properly linking the SDK, and collecting and uploading debug information for symbolication. That component requires configuration prior to building. If your project ships on both Android and iOS, make sure to configure both platforms using the {{< param "PRODUCT_NAME" >}} editor window.

#### Configuring Unity for Android

{{< admonition type="note" >}}
To use the Embrace Unity SDK you must be using:
- At least version 6.5.1 of Gradle
- At least version 4.0.0 of the Android Gradle Plugin (classpath `com.android.tools.build:gradle`)
{{< /admonition >}}

Go to `Tools -> {{< param "PRODUCT_NAME" >}} -> Getting Started` and click on it to reveal the {{< param "PRODUCT_NAME" >}} editor window. Select the Android tab and fill in your unique App ID and API Token. 

On Android, Unity builds are handled by Gradle. To integrate {{< param "PRODUCT_NAME" >}}, we'll be adding some new dependencies to Unity's Gradle templates. Unity already provides ways to customize the Gradle configuration via templates accessible from the Player Settings menu.

#### Configuring Unity for iOS

Go to `Tools -> {{< param "PRODUCT_NAME" >}} -> Getting Started` and click on it to reveal the {{< param "PRODUCT_NAME" >}} editor window. Select the iOS tab and fill in the missing App ID and API Token.

When you build and run your project, the editor script will use those values to correctly setup the final IPA to work with {{< param "PRODUCT_NAME" >}}.

## Flutter

### Add the {{< param "PRODUCT_NAME" >}} Flutter SDK to the project

Add the {{< param "PRODUCT_NAME" >}} package to `pubspec.yaml` with the following command:
```
flutter pub add embrace
```

### Automated integration

You can use the `embrace-cli` Dart package to configure your Android and iOS projects to use the {{< param "PRODUCT_NAME" >}} Flutter SDK. Alternatively, you can perform the configuration manually.

To install the {{< param "PRODUCT_NAME" >}} CLI, run the following command from any directory:
```
dart pub global activate embrace_cli
```

### Using the {{< param "PRODUCT_NAME" >}} CLI

Run the following command to configure your project:

```
//Android
embrace_cli installAndroid YOUR_APP_ID YOUR_API_TOKEN

//iOS
embrace_cli installIos YOUR_APP_ID YOUR_API_TOKEN
```

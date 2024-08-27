---
date: "2024-07-22T23:43:16+01:00"
description: Add the Embrace Android SDK to your mobile app
keywords:
  - Embrace
menuTitle: Android
title: Add the Embrace Android SDK to your mobile app
weight: 1
---

# Add the {{< param "PRODUCT_NAME" >}} Android SDK to your mobile app

For native [Android apps](https://embrace.io/docs/android/integration/add-embrace-sdk/), you will need to:
- update `settings.gradle`
- update `gradle.properties`
- update `build.gradle`
- add a `embrace-config.json` in your `main` directory

1. Add the following to your `settings.gradle`:

{{< code >}}
```groovy
pluginManagement {
    repositories {
        mavenCentral()
    }

    plugins {
        id 'io.embrace.swazzler' version "${swazzler_version}" apply false
    }
}
```
```kotlin
pluginManagement {
    repositories {
        mavenCentral()
    }
    val swazzler_version: String by settings
    plugins {
        id("io.embrace.swazzler") version "${swazzler_version}" apply false
    }
}
```
{{< /code >}}

1. <!-- hack to get the numbers sequential  -->
1. Update your `gradle.properties` file to include the `swazzler_version:
```
swazzler_version=6.10.0
```

1. <!-- hack to get the numbers sequential  -->
1. <!-- hack to get the numbers sequential  -->
1. Add the following at the top of your `app/build.gradle`:

{{< code >}}
```groovy
plugins {
    id 'io.embrace.swazzler'
}
```
```kotlin
plugins {
    id("io.embrace.swazzler")
}
```
{{< /code >}}

1. <!-- hack to get the numbers sequential  -->
1. <!-- hack to get the numbers sequential  -->
1. <!-- hack to get the numbers sequential  -->
1. Add a config file `app/src/main/embrace-config.json` with the following contents:

```
{
  "app_id": "xxxxx",
  "api_token": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

Additional configuration options are available in {{< param "PRODUCT_NAME" >}}'s [Android documentation](https://embrace.io/docs/android/integration/add-embrace-sdk/)

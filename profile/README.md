<div align="center">

# ⚡ Rasgate

### Precision Push Notification Infrastructure & Native Mobile SDKs

[![Swift 5.9+](https://img.shields.io/badge/Swift-5.9+-FA7343.svg?style=for-the-badge&logo=swift&logoColor=white)](https://github.com/rasgate/ios)
[![Kotlin 1.9+](https://img.shields.io/badge/Kotlin-1.9+-7F52FF.svg?style=for-the-badge&logo=kotlin&logoColor=white)](https://github.com/rasgate/android)
[![Platform](https://img.shields.io/badge/Platforms-iOS%20%7C%20Android-0071E3.svg?style=for-the-badge)](https://rasgate.io)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-1D1D1F.svg?style=for-the-badge)](LICENSE)

<br/>

[Website](https://rasgate.io) • [Documentation](https://rasgate.io/docs) • [iOS SDK](https://github.com/rasgate/ios) • [Android SDK](https://github.com/rasgate/android)

<br/>

</div>

---

## 🚀 Overview

**Rasgate** provides high-performance push notification delivery and native mobile SDKs for Apple iOS and Android applications. 

- ⚡ **Fast-Path Delivery**: Sub-18ms delivery across Apple APNs and Google FCM.
- 📱 **Native Mobile SDKs**: Idiomatic Swift (SPM) and Kotlin (Maven) client libraries.
- 🛡️ **End-to-End Security**: Encrypted credential storage and HMAC request verification.
- 💰 **Predictable Pricing**: Flat-rate volume scaling with zero per-subscriber penalty fees.

---

## 📱 Mobile SDKs

### 🍏 [iOS SDK (`rasgate/ios`)](https://github.com/rasgate/ios)
Native Swift SDK with Swift Package Manager (SPM) support, automatic APNs token registration, and rich media notification extensions.

```swift
// Package.swift
dependencies: [
    .package(url: "https://github.com/rasgate/ios.git", from: "2.4.0")
]
```

```swift
// AppDelegate.swift
import Rasgate

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    Rasgate.initialize(appKey: "rg_app_your_key")
    return true
}

func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    Rasgate.shared.registerDeviceToken(deviceToken)
}
```

---

### 🤖 [Android SDK (`rasgate/android`)](https://github.com/rasgate/android)
Native Kotlin SDK with Maven Central distribution, Coroutines support, custom notification channels, and automatic FCM token synchronization.

```kotlin
// build.gradle.kts
dependencies {
    implementation("io.rasgate:sdk:2.4.0")
}
```

```kotlin
// MainApplication.kt
import io.rasgate.sdk.Rasgate
import io.rasgate.sdk.RasgateConfig

class MainApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        Rasgate.initialize(
            context = this,
            config = RasgateConfig(apiKey = "rg_app_your_key")
        )
    }
}
```

---

## 📄 License

Rasgate Mobile SDKs are open-source software licensed under the [Apache License 2.0](LICENSE).

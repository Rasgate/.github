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
- ⚙️ **Config-Driven Initialization**: Automated configuration loading via `Rasgate-Info.plist` (iOS) and `rasgate-services.json` / XML (Android).
- 🛡️ **End-to-End Security**: Encrypted credential storage and HMAC request verification.
- 💰 **Predictable Pricing**: Flat-rate volume scaling with zero per-subscriber penalty fees.

---

## 📱 Mobile SDKs

### 🍏 [iOS SDK (`rasgate/ios`)](https://github.com/rasgate/ios)
Native Swift SDK with Swift Package Manager (SPM) support, automatic `Rasgate-Info.plist` configuration loading, and APNs token registration.

#### 1. Add `Rasgate-Info.plist` to your Xcode project
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>API_KEY</key>
    <string>rg_app_your_publishable_key</string>
    <key>BASE_URL</key>
    <string>https://api.rasgate.io</string>
</dict>
</plist>
```

#### 2. Initialize in `AppDelegate.swift`
```swift
import Rasgate

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    // Automatically loads API_KEY and settings from Rasgate-Info.plist
    Rasgate.initialize()
    return true
}

func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    Rasgate.shared.registerDeviceToken(deviceToken)
}
```

---

### 🤖 [Android SDK (`rasgate/android`)](https://github.com/rasgate/android)
Native Kotlin SDK with Maven Central distribution, automated `rasgate-services.json` / XML discovery, and FCM token synchronization.

#### 1. Add `assets/rasgate-services.json` (or `res/values/strings.xml`)
```json
{
  "api_key": "rg_app_your_publishable_key",
  "base_url": "https://api.rasgate.io"
}
```
*Or in `res/values/strings.xml`:*
```xml
<resources>
    <string name="rasgate_api_key">rg_app_your_publishable_key</string>
</resources>
```

#### 2. Initialize in `MainApplication.kt`
```kotlin
import io.rasgate.sdk.Rasgate

class MainApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        // Automatically discovers rasgate-services.json or XML strings
        Rasgate.initialize(context = this)
    }
}
```

---

## 📄 License

Rasgate Mobile SDKs are open-source software licensed under the [Apache License 2.0](LICENSE).

<div align="center">

# ⚡ Rasgate — Precision Push Notification Infrastructure

### High-Throughput, Sub-18ms Push Gateway & Native Client SDKs for Apple, Android & Web

[![Swift 5.9+](https://img.shields.io/badge/Swift-5.9+-FA7343.svg?style=for-the-badge&logo=swift&logoColor=white)](https://github.com/rasgate/rasgate-ios-sdk)
[![Kotlin 1.9+](https://img.shields.io/badge/Kotlin-1.9+-7F52FF.svg?style=for-the-badge&logo=kotlin&logoColor=white)](https://github.com/rasgate/rasgate-android-sdk)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-3178C6.svg?style=for-the-badge&logo=typescript&logoColor=white)](https://rasgate.io/docs/web-api)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-14+-4169E1.svg?style=for-the-badge&logo=postgresql&logoColor=white)](https://postgresql.org)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-0071E3.svg?style=for-the-badge)](LICENSE)

<br/>

[🚀 Explore Free Sandbox](https://rasgate.io) • [📚 Developer Documentation](https://rasgate.io/docs) • [🍏 iOS SDK](https://github.com/rasgate/rasgate-ios-sdk) • [🤖 Android SDK](https://github.com/rasgate/rasgate-android-sdk) • [🌐 REST API](https://rasgate.io/docs/web-api)

<br/>

</div>

---

## 🌟 What is Rasgate?

**Rasgate** is an enterprise-grade push notification delivery engine built for high-throughput mobile applications and consumer SaaS platforms. Engineered with direct **multiplexed HTTP/2 connection pooling** to Apple APNs and Google FCM v1 gateway endpoints, Rasgate delivers push payloads globally in **sub-18ms** with **zero per-subscriber penalty fees**.

```
  ┌─────────────────┐       HMAC SHA-256        ┌─────────────────────────┐
  │   Your Server   │ ────────────────────────> │      Rasgate Cloud      │
  │   Application   │ <──────────────────────── │   Fast-Path Engine      │
  └─────────────────┘      Sub-18ms Dispatch    └────────────┬────────────┘
                                                             │
                  ┌──────────────────────────────────────────┼──────────────────────────────────────────┐
                  ▼                                          ▼                                          ▼
       ┌─────────────────────┐                    ┌─────────────────────┐                    ┌─────────────────────┐
       │   Apple APNs Pool   │                    │   Google FCM v1     │                    │    W3C Web Push     │
       │   (HTTP/2 Dual)     │                    │  (Async Coroutines) │                    │   (VAPID Keypair)   │
       └──────────┬──────────┘                    └──────────┬──────────┘                    └──────────┬──────────┘
                  ▼                                          ▼                                          ▼
       ┌─────────────────────┐                    ┌─────────────────────┐                    ┌─────────────────────┐
       │   iOS / iPadOS App  │                    │     Android App     │                    │  Desktop & PWA Web  │
       │ (Swift SPM SDK)     │                    │ (Kotlin Maven SDK)  │                    │ (Service Worker)    │
       └─────────────────────┘                    └─────────────────────┘                    └─────────────────────┘
```

---

## 📦 Open Source Client SDK Ecosystem

| Repository | Platform | Distribution Channel | Version | Status |
| :--- | :--- | :--- | :--- | :--- |
| [**`rasgate-ios-sdk`**](https://github.com/rasgate/rasgate-ios-sdk) | Apple iOS 14.0+, iPadOS, macOS | **Swift Package Manager (SPM)** & Universal XCFramework | `v2.4.0` | ![Build](https://img.shields.io/badge/Status-Active-brightgreen.svg?style=flat-square) |
| [**`rasgate-android-sdk`**](https://github.com/rasgate/rasgate-android-sdk) | Android 5.0+ (API 21+) | **Maven Central** (`io.rasgate:sdk`) & AAR Binary | `v2.4.0` | ![Build](https://img.shields.io/badge/Status-Active-brightgreen.svg?style=flat-square) |
| [**`rasgate-web-sdk`**](https://github.com/rasgate/rasgate-web-sdk) | Modern Browsers & PWAs | **NPM** (`@rasgate/web-push`) & CDN Script | `v2.4.0` | ![Build](https://img.shields.io/badge/Status-Active-brightgreen.svg?style=flat-square) |
| [**`rasgate-server-sdks`**](https://github.com/rasgate/rasgate-sdks) | Node.js, Python, Go, PHP | Packagist, PyPI, Go Modules | `v2.4.0` | ![Build](https://img.shields.io/badge/Status-Active-brightgreen.svg?style=flat-square) |

---

## ⚡ 1-Minute Quickstart

### 🍏 1. Apple iOS (`AppDelegate.swift`)
```swift
import UIKit
import Rasgate

@main
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Initialize Rasgate Engine
        Rasgate.initialize(appKey: "rg_app_your_publishable_key")
        return true
    }

    func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
        // Forward APNs Token
        Rasgate.shared.registerDeviceToken(deviceToken)
    }
}
```

### 🤖 2. Google Android (`MainApplication.kt`)
```kotlin
package com.yourcompany.app

import android.app.Application
import io.rasgate.sdk.Rasgate
import io.rasgate.sdk.RasgateConfig

class MainApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        Rasgate.initialize(
            context = this,
            config = RasgateConfig(apiKey = "rg_app_your_publishable_key")
        )
    }
}
```

### 🚀 3. Server-Side Programmatic Dispatch (cURL / REST API)
```bash
curl -X POST "https://api.rasgate.io/api/v1/notifications" \
  -H "Authorization: Bearer rg_live_sk_your_secret_key" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Flash Deal ⚡",
    "body": "Your saved item is 30% off for the next 2 hours.",
    "platforms": ["ios", "android", "web"],
    "action_url": "https://yourapp.com/deals/94812"
  }'
```

---

## 📊 Industry Benchmark Comparison

| Capability Standard | ⚡ Rasgate Engine | Legacy Multi-Channel Providers | Raw DIY Sockets |
| :--- | :--- | :--- | :--- |
| **P99 Dispatch Latency** | **< 18ms** (HTTP/2 Multiplexed) | 450ms – 3,200ms | Unbuffered / Spike Failures |
| **Per-Subscriber Overage Fees** | **Never (Volume-Only Pricing)** | Heavy Escalating Penalty Fees | High Server Maintenance Costs |
| **Native Swift SPM & Kotlin SDKs** | **100% Native Support** | Bloated Analytics Trackers | Manual JNI / Obj-C Bridges |
| **Cryptographic Key Vault** | **AES-256 Vault Encrypted** | Third-Party Stored | Unencrypted `.env` Files |
| **HMAC Replay Attack Defense** | **Built-in (< 300s Sliding Window)** | None / Custom Setup | Manual Implementation |

---

## 🛡️ Security & Zero-Trust Governance

- **AES-256 Encrypted Credential Vault**: `.p8` Apple private keys and Google service account `.json` secrets are encrypted at rest with AES-256-CBC.
- **Constant-Time Verification**: All API keys and HMAC signatures are validated using `hash_equals()` to prevent side-channel timing attacks.
- **Automated Replay Protection**: Timestamp validation discards any intercepted API requests older than 300 seconds.
- **Strict IDOR Tenant Isolation**: Every campaign, device token, and API key mutation is cryptographically bound to its parent company workspace.

---

## 🤝 Community & Support

- 📖 **Documentation**: [https://rasgate.io/docs](https://rasgate.io/docs)
- 💬 **Discord Community**: [https://discord.gg/rasgate](https://discord.gg/rasgate)
- 🐦 **Twitter / X**: [@rasgate_io](https://twitter.com/rasgate_io)
- 🚨 **Security Disclosures**: `security@rasgate.io`
- 🏢 **Enterprise Sales**: `sales@rasgate.io`

---

<div align="center">

<sub>Crafted with precision by the Rasgate Infrastructure Engineering Team. Distributed under the Apache License 2.0.</sub>

</div>

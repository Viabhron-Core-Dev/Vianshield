# Vianshield Blueprint

## 1. Project Overview & Mission
Vianshield is a lean, native Android security utility designed to run efficiently on resource-constrained devices (~3 GB RAM). The application architecture emphasizes zero background bloat, minimal memory overhead, zero third-party telemetry or ad SDKs, and clean separation between UI and the forthcoming firewall engine.

## 2. Technical Stack & Environment
- **Platform**: Android Native (Kotlin 2.2.10)
- **UI Framework**: Jetpack Compose (BOM 2024.09.00, Material 3)
- **Build System**: Android Gradle Plugin 9.1.1, Gradle 9.3.1 Wrapper
- **Application ID**: `app.vian.vianshield`
- **Namespace**: `com.example`
- **Target SDK**: 36 | **Min SDK**: 24 | **Java Version**: 21 (Temurin)
- **CI/CD Automation**: GitHub Actions (`.github/workflows/android-build.yml`)
- **Dependencies**: Minimal footprint (Jetpack Compose core/material3/lifecycle/activity only; Room, Moshi, Retrofit, Firebase, and telemetry completely excluded).

## 3. Development Phases
- **Phase 1: Native Shell & CI Pipeline (CURRENT)**
  - Establish stable Gradle 9.3.1 / AGP 9.1.1 build configuration.
  - Setup GitHub Actions automated debug APK workflow on `push` and `workflow_dispatch`.
  - Create minimal Jetpack Compose Home Screen with honest status disclosure ("Firewall engine not integrated yet").
  - Custom vector adaptive shield launcher icon.
  - Verification with local compilation and unit tests.
- **Phase 2: Engine Evaluation & Architecture Alignment (PENDING REVIEW)**
  - Architectural review of networking/packet-inspection options (e.g., VpnService vs Local Loopback proxy vs Tun2Socks).
  - Memory footprint estimation for ~3 GB RAM device profile.
  - Discussion and explicit green-light before any engine code is added.
- **Phase 3: Engine Integration & Firewall Service**
  - Implement zero-leak local VPN service.
  - Local rule engine and packet routing.
  - Strict battery and memory optimization.
- **Phase 4: Rule Management & Logging**
  - Domain blocklists, per-app network access toggles.
  - Zero-PII Log Keeper with master switch.

## 4. Running Ledger of Changes
- **2026-10-14 (Phase 1 Initial Creation)**:
  - Configured `applicationId = "app.vian.vianshield"` and app name "Vianshield".
  - Stripped out unused dependencies (Firebase, Room, Moshi, Retrofit, OkHttp) from `app/build.gradle.kts` to optimize APK size and build speed.
  - Generated Gradle wrapper (v9.3.1) with `gradlew` script for GitHub Actions execution.
  - Created `.github/workflows/android-build.yml` for automated CI debug APK builds and artifact generation.
  - Implemented `VianshieldHomeScreen` in `MainActivity.kt` with honest, clean status display.
  - Added custom adaptive shield vector icon in `ic_launcher_foreground.xml` and `ic_launcher_background.xml`.
  - Added `README.md` and `BLUEPRINT.md`.

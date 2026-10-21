# 🛡️ Saksham

**A privacy-first Android app for shelter matching, placement requests, and accessible transport coordination.**

Saksham helps people seeking safety find a suitable shelter, check live bed availability, request placement, receive verified confirmation, and arrange accessible transport, all without compromising their personal privacy.

> Version 1.0 (Hackathon MVP)

---

## 📖 Table of Contents

- [Problem Statement](#-problem-statement)
- [Key Features](#-key-features)
- [User Roles](#-user-roles)
- [Design Principles](#-design-principles)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Data Model](#-data-model)
- [Getting Started](#-getting-started)
- [Running Tests](#-running-tests)
- [Team](#-team)

---

## 🎯 Problem Statement

People in crisis often have to call multiple shelters, repeat their story, and share sensitive personal details just to find a safe place to stay. Shelters, in turn, have no easy way to share real-time bed availability, and survivors with children or mobility needs struggle to reach a shelter safely.

**Saksham** ("capable / empowered") brings shelters, survivors, transport providers, and administrators onto one coordinated platform, with privacy built in from the start.

---

## ✨ Key Features

### For people seeking safety
- 🏠 **Guided shelter search**: a simple 3-step flow capturing group size, children, wheelchair accessibility, and transport needs
- 📍 **Live shelter results**: available beds, travel time, verification badge, and facilities
- 📝 **Placement requests**: request a bed and track the status (Requested → Approved → Completed)
- 🚗 **Accessible transport**: request a pickup, track the vehicle, and see driver and vehicle details
- 🔐 **Verification PIN**: show a PIN at reception on arrival to confirm identity without sharing personal details
- 🆘 **Emergency help**: one-tap dialing for emergency helplines (112, 1091, 181)
- 🕶️ **Anonymous session**: a pseudonymous token identifies your request instead of your real identity or device ID

### For shelter staff
- 📊 Shelter dashboard to manage bed availability and review incoming placement requests
- ✅ Approve or reject requests and keep availability fresh in real time

### For transport providers
- 🚐 Transport dashboard to view and accept ride requests and update trip status

### For administrators
- 🔑 Separate admin login
- 🧾 Review and verify newly registered shelters (approve or reject with a reason)
- 📈 Dashboard overview of the platform

### General
- 🔔 Notifications, ⚙️ Settings, 👤 My Account, ❓ Help & Support, 🔒 Privacy Info, and ℹ️ About screens
- 📱 Responsive navigation (bottom navigation / side navigation)

---

## 👥 User Roles

| Role | Description |
|------|-------------|
| **Person Seeking Safety** | Searches shelters, sends placement and transport requests |
| **Shelter Staff** | Manages beds and handles placement requests |
| **Transport Provider** | Handles accessible transport requests |
| **Administrator** | Verifies and approves shelters |

---

## 🧭 Design Principles

- **One screen = one question = one main action**: low cognitive load for users in distress
- **Zero non-consensual biometric or telemetry tracking**
- **Real-time freshness** with trauma-informed shelter intake
- **Accessible transport dispatch** with verified arrival PINs

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| Language | Kotlin 2.2 |
| UI | Jetpack Compose + Material 3 |
| Architecture | MVVM (ViewModel + Repository + Room DAO) |
| Navigation | Navigation Compose |
| Local database | Room (SQLite) with KSP |
| Networking | Retrofit, OkHttp, Moshi |
| Async | Kotlin Coroutines & Flow |
| Firebase | Firebase BoM (AI, App Check) |
| Testing | JUnit, Robolectric, Roborazzi (screenshot tests), Espresso |
| Build | Gradle (Kotlin DSL) with version catalog |

**Android config:** `minSdk 24` · `targetSdk 36` · `compileSdk 36` · Java 11

---

## 📂 Project Structure

```
Saksham/
├── app/
│   └── src/
│       ├── main/java/com/example/
│       │   ├── MainActivity.kt
│       │   ├── data/
│       │   │   ├── local/          # Room database & DAO
│       │   │   ├── model/          # Entities (Shelter, TransportProvider, requests...)
│       │   │   └── repository/     # SakshamRepository
│       │   └── ui/
│       │       ├── SakshamApp.kt   # Navigation graph
│       │       ├── components/     # Reusable UI + bottom/side navigation
│       │       ├── theme/          # Colors, typography, theme
│       │       ├── viewmodel/      # SakshamViewModel
│       │       └── screens/
│       │           ├── auth/       # Login, Register
│       │           ├── survivor/   # Home, Find Shelter, Requests, Transport, Emergency
│       │           ├── staff/      # Shelter dashboard
│       │           ├── transport/  # Transport dashboard
│       │           ├── admin/      # Admin login, dashboard, shelter review
│       │           └── more/       # Settings, About, Privacy, Help, Account, Notifications
│       ├── test/                   # Unit & screenshot tests
│       └── androidTest/            # Instrumented tests
├── gradle/libs.versions.toml       # Dependency versions
├── build.gradle.kts
└── settings.gradle.kts
```

---

## 🗄️ Data Model

Stored locally with Room:

- **Shelter**: name, area, total/available beds, accepts children, wheelchair accessible, verification status, travel time, features
- **TransportProvider**: vehicle type, wheelchair accessibility, capacity, driver, plate, ETA
- **PlacementRequest**: anonymous session ID, shelter, group size, needs, status
- **TransportRequest**: pickup/destination, vehicle assignment, status, verification PIN
- **AvailabilityLog**: history of shelter availability updates

---

## 🚀 Getting Started

### Prerequisites
- [Android Studio](https://developer.android.com/studio) (latest stable, with Android Gradle Plugin 9.x support)
- JDK 11 or higher
- An Android emulator or physical device (Android 7.0 / API 24+)

### Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/Harshad0987123/Saksham.git
   cd Saksham
   ```

2. **Open in Android Studio**
   Select **File → Open** and choose the project folder. Let Gradle sync finish.

3. **(Optional) Configure environment variables**
   If you use Gemini / Firebase AI features, copy the example file and add your key:
   ```bash
   cp .env.example .env
   ```
   Then set `GEMINI_API_KEY` in `.env`. Never commit this file.

4. **Debug signing config**
   If the build complains about a missing debug keystore, remove or adjust the `signingConfig` line in `app/build.gradle.kts` as described in Android Studio's prompt.

5. **Run the app**
   Choose an emulator or device and press ▶️ **Run**.

---

## 🧪 Running Tests

```bash
# Unit tests
./gradlew test

# Instrumented tests (device/emulator required)
./gradlew connectedAndroidTest
```

---

## 👩‍💻 Team

This project was built as a team effort by:

| Name | GitHub |
|------|--------|
| **Shruti Shankwar** | — |
| **Harshad Chapte** | [@Harshad0987123](https://github.com/Harshad0987123) |
| **Tanvi Sawant** | — |

---

## 📄 License

This project was built as a hackathon MVP. Add a license of your choice (e.g. MIT) if you plan to open-source it.

---

<div align="center">

**Saksham**: safety, privacy, dignity. 💙

</div>

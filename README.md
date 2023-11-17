# Android BSS SDK

## Overview
The Android BSS SDK, provides convenient methods for handling authentication-related functionalities your Android application with Vision Plus.

## Installation
### Step 1. Add the JitPack repository to your build file
Add it in your build.gradle (root) at the end of repositories:
```groovy
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```

### Step 2. Add the dependency
Add it in your build.gradle (app):
```groovy
dependencies {
    implementation 'com.github.visionplus-development:android-auth-sdk:$latest_version'
}
```


## Prerequisite (*for the meantime*)
Before integrating the Android BSS SDK, ensure that the following dependencies are included in your project. If you're already using any of them, there's no need to add them again:
```kotlin
dependencies {
    implementation("androidx.activity:activity-compose:1.7.2")
    implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.6.2")
    implementation("androidx.compose.runtime:runtime-livedata:1.5.3")
    implementation("androidx.navigation:navigation-compose:2.7.4")
    implementation("com.google.android.gms:play-services-auth:20.7.0")
    implementation("com.facebook.android:facebook-android-sdk:15.1.0")

    val ktorVersion = "2.3.5"
    implementation("io.ktor:ktor-client-android:$ktorVersion")
    implementation("io.ktor:ktor-client-okhttp:$ktorVersion")
    implementation("io.ktor:ktor-client-logging:$ktorVersion")
    implementation("io.ktor:ktor-client-content-negotiation:$ktorVersion")
    implementation("io.ktor:ktor-serialization-kotlinx-json:$ktorVersion")
    implementation("org.jetbrains.kotlinx:kotlinx-serialization-json:1.6.0")
}
```


## Usage
### Configuration
Initialize the SDK **(*required*)** in your application class (.Application)
```kotlin
VPAuth.init(this)
```

Optionally, you can enable debug mode for additional information:
```kotlin
VPAuth.enableDebugMode()
```

Set language preferences:
```kotlin
VPAuth.updateLanguage("en")
```


### Login
Initiates the login process by opening the login page.
The user can perform the login action on the opened page. Upon completion, this method returns a token for success or an error message for failure.
```kotlin
val activityForResult = registerForActivityResult(ActivityResultContracts.StartActivityForResult()) { result ->
    when (result.resultCode) {
        Result.SUCCESS -> {
            // TODO: success action
            val token = result.data?.getStringExtra(ResultType.TOKEN)
        }

        Result.CANCELLED -> {
            // TODO: cancelled action if needed
        }

        Result.FAILED -> {
            // TODO: failed action if needed
        }
    }
}
VPAuth.login(this, activityForResult)
```


### Register
Initiates the registration process by opening the register page.
The user can perform the registration action on the opened page. Upon successful registration, the user is automatically logged in, and this method returns the login token.
```kotlin
val activityForResult = registerForActivityResult(ActivityResultContracts.StartActivityForResult()) { result ->
    when (result.resultCode) {
        Result.SUCCESS -> {
            // TODO: success action
            val token = result.data?.getStringExtra(ResultType.TOKEN)
        }

        Result.CANCELLED -> {
            // TODO: cancelled action if needed
        }

        Result.FAILED -> {
            // TODO: failed action if needed
        }
    }
}
VPAuth.register(this, activityForResult)
```

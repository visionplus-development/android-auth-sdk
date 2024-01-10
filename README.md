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


## Usage
### Configuration
Initialize the SDK **(*required*)** in your application class (.Application)
```kotlin
VPAuth.init(this,"mirada_prod")
```

Optionally, you can enable debug mode for additional information:
```kotlin
VPAuth.enableDebugMode()
```

Set language preferences:
```kotlin
VPAuth.updateLanguage("en")
```


### Analytics
Initialize analytics in your splash or main activity (call once).
```kotlin
setContent {
    VPAuth.initAnalytics()
}
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


### Verify by Email (deeplink)
Initiates the email verification process for a user account.
The verification process requires a session ID and user identity for authentication which are get from deeplink url.
Upon successful verification, the user is redirected to a success page then automatically open login page. In case of failure, the redirection is to a failed page.
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
VPAuth.verifyByEmail(this, $sessionID, $identity, activityForResult)
```

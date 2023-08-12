# Pocketbase Android

[![](https://jitpack.io/v/rohitsangwan01/pocketbase_android.svg)](https://jitpack.io/#rohitsangwan01/pocketbase_android)

Use pocketbase in your android device with this library 


## Add it in your root build.gradle at the end of repositories:

```gradlew
allprojects {
  repositories {
     ...
     maven { url 'https://jitpack.io' }
  }
}
 ```

## Add the dependency

```gradlew
dependencies {
    implementation 'com.github.rohitsangwan01:pocketbase_android:Tag'
}
```

## Usage

Use CoroutineScope to call pocketbase methods ( import kotlin coroutines libraries)

```kotlin
private val uiScope = CoroutineScope(Dispatchers.Main + Job())
```

To start pocketbase

```kotlin
// use dataPath where app have write access, for example temporary cache path `context.cacheDir.absolutePath` or filePath
uiScope.launch {
    withContext(Dispatchers.IO) {
        PocketbaseMobile.startPocketbase(dataPath, hostname, port, enableApiLogs)
    }
}
```

To stop pocketbase

```kotlin
uiScope.launch {
    withContext(Dispatchers.IO) {
        PocketbaseMobile.stopPocketbase()
    }
}
```

To listen pocketbase events, and also handle custom api requests

`pocketbaseMobile` have two custom routes as well ,`/api/nativeGet` and `/api/nativePost`, we can
get these routes in this callback and return response from kotlin

```kotlin
PocketbaseMobile.registerNativeBridgeCallback { command, data ->
    this.runOnUiThread {
        // Update ui from here
    }
    // return response back to pocketbase
    "response from native"
}
```

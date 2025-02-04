---
title: Android SDK Config
tag: [config, android]
ref: config-android
---

This document will introduce how to configure the Android SDK in the QWeather Develop Service.

> **Privacy Disclaimer:** QWeather Android SDK **DOES NOT require any special permissions such as phone, location, device unique identifiers, etc.** We does not and cannot collect private data from this SDK. 

## Download 

|Version|Update|MD5| 
|---|---|---|----------------------------------------------|
|{{ site.data.v.android.version }} [Download]({{ site.data.v.android.dllink }})|{{ site.data.v.android.date }} [Release note](https://blog.qweather.com/release/sdk/)|`{{ site.data.v.android.md5 }}`|

## OS requirement

Android 4.4+

## Create Project and Credential

Make sure you have created a Project and Credential, see [Project and KEY](/en/docs/configuration/project-and-key/) and [Authentication](/en/docs/authentication/).

## Project configuration

1. Unzip the file, put the jar in the folder into your project, and quote
2. Configure **Android Manifest** to add permissions

**Permission list**

| Permission   | Code                                    |
| ------------------------ | --------------------------------------- |
| Allow network connection | android.permission.INTERNET             |

**Reference Library**

```
compile'com.squareup.okhttp3:okhttp:3.12.12' (3.12.12+)
compile'com.google.code.gson:gson:2.6.2' (2.6.2+)
```

**Confusion**

Please add the following code to your obfuscated file **proguard-rules.pro**

Please note the version you quote

```java
// exclude okhttp
 -dontwarn com.squareup.**
 -dontwarn okio.**
 -keep public class org.codehaus.* {*;}
 -keep public class java.nio.* {*;}

// Exclude QWeather
 -dontwarn com.qweather.sdk.**
 -keep class com.qweather.sdk.** {*;}
```
 
## Data Access configuration

**Log function**

SDK no longer provides log function, error information can be provided by Throwable object in callback function OnError

**Initialization**

When using the SDK, you need to initialize the account in advance (you can execute it once globally)

```java
HeConfig.init("PublicId", "PrivateKey");
```

**Setup subscription**

Standard subscription is default, you can switch subscription by the following methods (execute it once globally)
 
```java
//Switch to Free subscription
HeConfig.switchToDevService();
//Switch to Standard subscription
HeConfig.switchToBizService();
```

**Data access example**

Call different methods according to your needs. The parameters in the interface callback method are the Classes returned by the interface

```java
/**
 * Real-time weather data
 * @param location location to be queried
 * @param lang (optional) set multi-language, the default is simplified Chinese
 * @param unit (optional) set unit, metric (m) or imperial (i), the default is metric unit
 * @param listener network access result callback
 */

QWeather.getWeatherNow(MainActivity.this, "101010300", Lang.ZH_HANS, Unit.METRIC, new QWeather.OnResultWeatherNowListener() {
    @Override
    public void onError(Throwable e) {
        Log.i(TAG, "getWeather onError: "+ e);
    }

    @Override
    public void onSuccess(WeatherNowBean weatherBean) {
        Log.i(TAG, "getWeather onSuccess: "+ new Gson().toJson(weatherBean));
        if (Code.OK.getCode().equalsIgnoreCase(weatherBean.getCode())) {
            WeatherNowBean.NowBaseBean now = weatherBean.getNow();
        } else {
            //Check the reason for the failure to return data here
            String status = weatherBean.getCode();
            Code code = Code.toEnum(status);
            Log.i(TAG, "failed code: "+ code);
        }
    }
});
```

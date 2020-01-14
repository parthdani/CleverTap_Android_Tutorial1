# CleverTap_Android_Tutorial_1
I shall be creating a multiple series of an example where I will help you to integrate with CleverTap SDK into your project. This project is the first example of that series. I will not take you through the flow of creating a new project in Android studio since the pre-requisite of this tutorial is that you already have your own project where you want to integrate CleverTap directly. Now please find the steps for integrating CleverTap with your project as follow

**Step 1: Adding the Dependency**
Add the following dependencies into your Gradle file. This will help you to get CleverTap SDK and Firebase Messaging SDK imported into your project.

```JAVA
dependencies {
    implementation 'com.clevertap.android:clevertap-android-sdk:+'
    implementation 'com.google.firebase:firebase-messaging:+'
    implementation 'com.google.android.gms:play-services-base:+'
    implementation 'com.android.support:support-v4:28.0.0'
}
// at the end of the build.gradle file
apply plugin: 'com.google.gms.google-services'
```
implementation 'com.clevertap.android:clevertap-android-sdk:+' : This will always import the latest version of CleverTap SDK into your project. Rest of the implementation are use for Push notification. If you already are using Firebase as a push notification then firebase-messaging, play-service-base and support-v4 are already there. so no need to add them again.

**Step 2: Adding CleverTap Details**
Every CleverTap Application is provided with Account ID and Token. You can find them under Settings > Accounts. For refrence, please find the screenshot as follow
![Screenshot](https://github.com/parthdani/CleverTap_Android_Tutorial1/blob/master/Screenshot%202020-01-14%20at%202.02.47%20PM.png)

Add this Account Id and Token in your AndroidManifest file under <application> tag. For refrence, please find the source code as follow

```JAVA
<meta-data
    android:name="CLEVERTAP_ACCOUNT_ID"
    android:value="Your CleverTap Account ID"/>
<meta-data
    android:name="CLEVERTAP_TOKEN"
    android:value="Your CleverTap Account Token"/>
 ```
 
 **Step 3: Disabling GDPR**
 By Default CleverTap SDK are GDPR compliance, If you wish to Opt-out from GDPR complainces then add the following code into AndroidManifest file under <application> tag

```JAVA
<meta-data
    android:name="CLEVERTAP_USE_GOOGLE_AD_ID"
    android:value="1"/> 
```

To read more on GDPR compliance, Please visit [here](https://clevertap.com/blog/in-preparation-of-gdpr-compliance/)

**Step 4: Add Required Permission**
For passing information such as events and user details to CleverTap, your applciation will require internet and for that you will need to take permission for Internet. For refrence, Add the following code in your Android Manifest.
```JAVA
<!-- Required to allow the app to send events and user profile information -->
<uses-permission android:name="android.permission.INTERNET"/>
<!-- Recommended so that CleverTap knows when to attempt a network call -->
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```
**Step 5: Enable Activity Life Cycle Callbacks**
For every Android Application has a lifecycle and lifecycle callbacks. Now to tracking events and attributes, SDK relies on this lifecycle callbacks. This also helps SDK to determine the best time to send back to CleverTap Servers without affecting apps performance. Now for CleverTap you can do this in three ways.

**Way 1:** If you don't have your application class file then define **com.clevertap.android.sdk.Application** in your application tag in Android Manifest. For refrence, you can do this as follow
```JAVA
<application
    android:label="@string/app_name"
    android:icon="@drawable/ic_launcher"
    android:name="com.clevertap.android.sdk.Application">
```
**Way 2:** If you already have the application class file define in your Android Manifest file then call **ActivityLifecycleCallback.register(this);** before **super.onCreate()** in your class. For refrence, it will look like as follow
```JAVA
import android.app.Application;
import com.clevertap.android.sdk.ActivityLifecycleCallback;
import com.clevertap.android.sdk.CleverTapAPI;

public class MyApplication extends Application {
    @Override
    public void onCreate() {
        CleverTapAPI.changeCredentials("Your account ID here", "Your account token here");
        ActivityLifecycleCallback.register(this); // Must be called before super.onCreate()
        super.onCreate();
    }
}
```


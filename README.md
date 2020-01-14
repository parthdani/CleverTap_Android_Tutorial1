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

Add this Account Id and Token in your AndroidManifest file. For refrence, please find the source code as follow

```JAVA
<meta-data
    android:name="CLEVERTAP_ACCOUNT_ID"
    android:value="Your CleverTap Account ID"/>
<meta-data
    android:name="CLEVERTAP_TOKEN"
    android:value="Your CleverTap Account Token"/>
    ```
    
    

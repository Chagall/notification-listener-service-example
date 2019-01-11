# Notification Listener Service Example

This example aims to teach you how to intercept notifications received by the Android System.

## What is a Notification
https://developer.android.com/guide/topics/ui/notifiers/notifications.html

As stated in the official Google Android Website, a notification is a message that can be displayed outside of the application normal User Interface

<b>It should look similar to this:</b> 

![alt text](https://i.stack.imgur.com/A0Y3K.jpg, "Notification")

## How to Intercept a Notification
In order to intercept a notification received by the android system we need to have a specific service running on the system's background. This service is called: <b>NotificationListenerService</b>. 

What the service basically does is: It registers itseft to the android system and after that starts to listen to the calls from the system when new notifications are posted or removed, or their ranking changed. 

When the <b>NotificationListenerService</b> identifies that a notification has been <b>posted</b>, <b>removed</b> or had its <b>ranking modified</b> it does what you told it to.

### Steps you need to follow to build a NotificationListenerService

<b>1.</b> Declare the Service in your AndroidManifest.xml file with the `BIND_NOTIFICATION_LISTENER_SERVICE` permission and include an intent filter with the `SERVICE_INTERFACE action`. 

Like this:

```xml
 <service android:name=".NotificationListener"
          android:label="@string/service_name"
          android:permission="android.permission.BIND_NOTIFICATION_LISTENER_SERVICE">
     <intent-filter>
         <action android:name="android.service.notification.NotificationListenerService" />
     </intent-filter>
 </service>
```
<b>2.</b> Extend the NotificationListenerService class and implement at least the following methods:

```java
  public class NotificationListenerExampleService extends NotificationListenerService {
  
    @Override
    public IBinder onBind(Intent intent) {
        return super.onBind(intent);
    }
  
    @Override
    public void onNotificationPosted(StatusBarNotification sbn){
      // Implement what you want here
    }

    @Override
    public void onNotificationRemoved(StatusBarNotification sbn){
      // Implement what you want here
    }
  }
```

##  How This Example Works
To illustrate the interception of notifications I've built a <b>NotificationListenerService</b> that does the following:

It changes the <b>ImageView</b> present on the screen whenever it receives a notification from the following apps: 

* Facebook
* Instagram
* Whatsapp

### Here are some images of the app. working, so you can see what it looks like
#### Tested using a ZenPhone2 (Android Version Lollipop 5.0)
![alt text](http://imgur.com/zkQ2S9P.jpg)
![alt text](http://imgur.com/gSOYgZm.jpg)
![alt text](http://imgur.com/asSZT0n.jpg)

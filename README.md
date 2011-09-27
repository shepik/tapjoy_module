# Tapjoy Module for Titanium

This module is a simple interface for connecting to [Tapjoy](http://tapjoy.com)

__NOTE: This was forked in order to get the "Secret" way of working with TapJoy
working on iPhone.  The android module has not been updated.__

# Build & Install

## iPhone

Simply run the ./build.py script in 'iphone/' then copy the com.tapjoy-iphone-*.zip file to your Titanium Library  ('/Library/Application Support/Titanium' or '~/Library/Application Support/Titanium')

## Android

Navigate into the 'android/' directory and run 'ant'. Then copy the com.tapjoy-android-*.zip file to your Titanium Library  ('/Library/Application Support/Titanium' or '~/Library/Application Support/Titanium')

# Usage

## iPhone

Add the following to app.js:

      var tapjoy = require('com.tapjoy');
      tapjoy.setSecret('SECRET');  // Secret only supported on iphone!!
      tapjoy.connect('API_KEY');

And later on, to mark an action performed:

      // Action complete... see TapJoy for your action id
      tapjoy.actionComplete('00000000-0000-0000-0000-000000000000');

## Android

Add the following to a custom AndroidManifest.xml. Place the following XML in the first '<activity>' block in the document.

NOTE: Secret version is not supported on Android in this version.

    <meta-data android:name="APP_ID" android:value="API_KEY"/> 
    <meta-data android:name="CLIENT_PACKAGE" android:value="com.my.app"/>

    <receiver android:name="com.tapjoy.TapjoyReferralTracker" android:exported="true">
            <intent-filter>
                    <action android:name="com.android.vending.INSTALL_REFERRER" />
            </intent-filter>
    </receiver>
    

Add the following to app.js:

      var tapjoy = require('com.tapjoy');
      tapjoy.connectCreate();
      Ti.App.addEventListener('close',function(e) {
        tapjoy.connectDestroy();
      });
    

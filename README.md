# Create-Deep-Links-and-Android-App-Links-to-Your-App-Content
This Tutorial will discuss how to create a deep link and prepare your app to implement the android app links feature. 

### This Tutorial discusses the following:
1. How Android System Deals with URLs ?
2. Create Deep Links
3. Test Your Deep Link
4. How to accomplish this using the App Links Assistant in Android Studio. 
5. Dive in the details of each line of code so you could have the whole picture of what is going on.
6. How to customize the Android App Links as per your needs.

### This is a part of Android App Links Series.

# How Android System Deals with URLs ?
As We mentioned earlier in a previous tutorial (Deep-Links-vs-Android-App-Links), Deep links make navigation easier within your app and from external app through the use of URLs. 

These URLs could be either: 
1. a URL link that you click on from anywhere in your mobile 
2. OR an imbedded URL called from another app (You can't see the URLs) like the Share Button in any app  

In either case, Android System will deals with them similarly. Let's see how Android System deals with a URLs:
1. First Step: Android System will open the user's preferred app that can handle the URI, if one is designated.
2. Second Step: if there is no preferred app and there is Only One App could handle this URL, Android System will open this app immediately.
3. Third Step: if there is no preferred app and there are more than One App could handle this URL, Android System will show a dialog containing all apps that could handle this URL.

# Create Deep Links ?
### Step One: Add Intent Filters from Incoming Intents
As We discussed in the previous tutorial (Allow-Other-Apps-to-Start-Your-Activity), If you want your app to be accessible by other apps, You have to allow this in your manifest file by declaring \<intent-filter>. You could use any Action, Category, and Data Type which satisfies your needs.

If you didn't read the **Allow-Other-Apps-to-Start-Your-Activity** tutorial yet, I recomment you to have a quick look on it now

https://github.com/KarimRedaHassan/Allow-Other-Apps-to-Start-Your-Activity/blob/master/README.md#allow-other-apps-to-open-a-certain-activity-in-your-app

#### NOTE: Android App Links is an Ownership-Verified Deep Link with some obligatory specifications
If you are intending to use Android App Links, there are some essential declarations to be made for your deep link in the \<intent-filter> as following:
1. Declare ACTION_VIEW, So your app could be accessible from Google Search.
2. Declare BROWSABLE category, So your app could be accessible from a web browser.
2. Declare DEFAULT category, So your app could be accessible Implicit Intents.
3. At Least Declare one <data> tag which must include the android:scheme.

Below is the minimum requirements in the \<intent-filter> which must be declared for a Deep Link. In Normal Scenarios, You at least specify the android:host or your app will respond for all URLs starts with http scheme

        <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="http" />
        </intent-filter>

### Step Two: Read From Incoming Intent 
Prepare your activity to receive the intent data as we discuss in the previous tutorial (Allow-Other-Apps-to-Start-Your-Activity),

Below is a code snippet from Android Documentation to handle an incomming intent. In normal cases, we don't write this code only, we have to do some checks and directions to the code.

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);

        Intent intent = getIntent();
        String action = intent.getAction();
        Uri data = intent.getData();
    }
    
If you didn't read the **Allow-Other-Apps-to-Start-Your-Activity** tutorial yet, I recomment you to have a quick look on it now

https://github.com/KarimRedaHassan/Allow-Other-Apps-to-Start-Your-Activity/blob/master/README.md#allow-other-apps-to-open-a-certain-activity-in-your-app


### Step Three: Test URL Deep Link

Use the following coommand to try if any activity could resolve the intent

        $ adb shell am start
        -W -a android.intent.action.VIEW
        -d <URI> <PACKAGE>
        
        
        /Volumes/HDD/Android/sdk/platform-tools/adb shell am start -W -a android.intent.action.VIEW -d https://www.smarkiz.com com.smarkiz.baseproject
  
You will see the following response

        Starting: Intent { act=android.intent.action.VIEW dat=https://www.smarkiz.com pkg=com.smarkiz.baseproject }
  
If the activity failed to resolve your Intent, You will receive the following:

        Error: Activity not started, unable to resolve Intent { act=android.intent.action.VIEW dat=https://www.smarkiz.com flg=0x10000000 pkg=com.smarkiz.baseproject }

If The activity could resolve your Intent, You will receive the following:

        Status: ok
        Activity: com.smarkiz.baseproject/.ui.settings.SettingsActivity
        ThisTime: 220
        TotalTime: 246
        WaitTime: 271
        Complete

For All Available adb commands, Please refer to this link

http://adbshell.com/commands

# What's Next ?


# Android App Links Series

Understand-The-URL
- https://github.com/KarimRedaHassan/Understand-The-URL

Deep-Links-vs-Android-App-Links
- https://github.com/KarimRedaHassan/Deep-Links-vs-Android-App-Links

Allow-Other-Apps-to-Start-Your-Activity
- https://github.com/KarimRedaHassan/Allow-Other-Apps-to-Start-Your-Activity

Create-Deep-Links-and-Android-App-Links-to-Your-App-Content
- https://github.com/KarimRedaHassan/Create-Deep-Links-and-Android-App-Links-to-Your-App-Content

# Additional Resources

http://adbshell.com/commands

https://developer.android.com/studio/write/app-link-indexing

https://developer.android.com/training/app-links/index.html

https://developer.android.com/training/app-links/deep-linking.html#adding-filters

https://developer.android.com/training/app-links/verify-site-associations.html

https://developer.android.com/training/basics/intents/filters.html

https://developer.android.com/guide/components/intents-filters.html

https://developers.google.com/digital-asset-links/tools/generator


# Also See

#### A Full List Of All My Tutorials

https://github.com/KarimRedaHassan?tab=repositories


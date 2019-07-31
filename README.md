# Create-Deep-Links-to-Your-App-Content
This Tutorial will discuss how to create a deep link and prepare your app to implement the android app links feature. 

### This Tutorial discusses the following:
1. How Android System Deals with URLs ?
2. How to accomplish this using the App Links Assistant in Android Studio. 
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
As We discussed in the previous tutorial (Allow-Other-Apps-to-Start-Your-Activity), If you want your app to be accessible by other apps, You have to allow this in your manifest file by declaring \<intent-filter> . But there are some essential declarations to be made in your \<intent-filter> as following:
1. Declare ACTION_VIEW, So your app could be accessible from Google Search.
2. Declare BROWSABLE category, So your app could be accessible from a web browser.
3. At Least Declare one <data> tag which must include the android:scheme.

Below is the minimum requirements in the \<intent-filter> which must be declared for a Deep Link. In Normal Scenarios, You at least specify the android:host or your app will respond for all URLs starts with http scheme

        <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="http" />
        </intent-filter>

#### Important Notes:

### Step Two: Read From Incoming Intent 
Prepare your activity to receive the intent data as we discuss in the previous tutorial (Allow-Other-Apps-to-Start-Your-Activity),

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);

        Intent intent = getIntent();
        String action = intent.getAction();
        Uri data = intent.getData();
    }
    
 ### Step Three: Test URL Deep Link
 
 
# What's Next ?

#### In Case You Miss Part One

Android-App-Links-via-App-Links-Assistant-Part-One

https://github.com/KarimRedaHassan/Android-App-Links-via-App-Links-Assistant-Part-One

# Additional Resources

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


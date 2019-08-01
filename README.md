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
 
usage: am [subcommand] [options]
usage: am start [-D] [-W] [-P <FILE>] [--start-profiler <FILE>]
               [--sampling INTERVAL] [-R COUNT] [-S] [--opengl-trace]
               [--user <USER_ID> | current] <INTENT>
       am startservice [--user <USER_ID> | current] <INTENT>
       am stopservice [--user <USER_ID> | current] <INTENT>
       am force-stop [--user <USER_ID> | all | current] <PACKAGE>
       am kill [--user <USER_ID> | all | current] <PACKAGE>
       am kill-all
       am broadcast [--user <USER_ID> | all | current] <INTENT>
       am instrument [-r] [-e <NAME> <VALUE>] [-p <FILE>] [-w]
               [--user <USER_ID> | current]
               [--no-window-animation] [--abi <ABI>] <COMPONENT>
       am profile start [--user <USER_ID> current] <PROCESS> <FILE>
       am profile stop [--user <USER_ID> current] [<PROCESS>]
       am dumpheap [--user <USER_ID> current] [-n] <PROCESS> <FILE>
       am set-debug-app [-w] [--persistent] <PACKAGE>
       am clear-debug-app
       am monitor [--gdb <port>]
       am hang [--allow-restart]
       am restart
       am idle-maintenance
       am screen-compat [on|off] <PACKAGE>
       am to-uri [INTENT]
       am to-intent-uri [INTENT]
       am to-app-uri [INTENT]
       am switch-user <USER_ID>
       am start-user <USER_ID>
       am stop-user <USER_ID>
       am stack start <DISPLAY_ID> <INTENT>
       am stack movetask <TASK_ID> <STACK_ID> [true|false]
       am stack resize <STACK_ID> <LEFT,TOP,RIGHT,BOTTOM>
       am stack list
       am stack info <STACK_ID>
       am lock-task <TASK_ID>
       am lock-task stop
       am get-config

am start: start an Activity.  Options are:
    -D: enable debugging
    -W: wait for launch to complete
    --start-profiler <FILE>: start profiler and send results to <FILE>
    --sampling INTERVAL: use sample profiling with INTERVAL microseconds
        between samples (use with --start-profiler)
    -P <FILE>: like above, but profiling stops when app goes idle
    -R: repeat the activity launch <COUNT> times.  Prior to each repeat,
        the top activity will be finished.
    -S: force stop the target app before starting the activity
    --opengl-trace: enable tracing of OpenGL functions
    --user <USER_ID> | current: Specify which user to run as; if not
        specified then run as the current user.

am startservice: start a Service.  Options are:
    --user <USER_ID> | current: Specify which user to run as; if not
        specified then run as the current user.

am stopservice: stop a Service.  Options are:
    --user <USER_ID> | current: Specify which user to run as; if not
        specified then run as the current user.

am force-stop: force stop everything associated with <PACKAGE>.
    --user <USER_ID> | all | current: Specify user to force stop;
        all users if not specified.

am kill: Kill all processes associated with <PACKAGE>.  Only kills.
  processes that are safe to kill -- that is, will not impact the user
  experience.
    --user <USER_ID> | all | current: Specify user whose processes to kill;
        all users if not specified.

am kill-all: Kill all background processes.

am broadcast: send a broadcast Intent.  Options are:
    --user <USER_ID> | all | current: Specify which user to send to; if not
        specified then send to all users.
    --receiver-permission <PERMISSION>: Require receiver to hold permission.

am instrument: start an Instrumentation.  Typically this target <COMPONENT>
  is the form <TEST_PACKAGE>/<RUNNER_CLASS>.  Options are:
    -r: print raw results (otherwise decode REPORT_KEY_STREAMRESULT).  Use with
        [-e perf true] to generate raw output for performance measurements.
    -e <NAME> <VALUE>: set argument <NAME> to <VALUE>.  For test runners a
        common form is [-e <testrunner_flag> <value>[,<value>...]].
    -p <FILE>: write profiling data to <FILE>
    -w: wait for instrumentation to finish before returning.  Required for
        test runners.
    --user <USER_ID> | current: Specify user instrumentation runs in;
        current user if not specified.
    --no-window-animation: turn off window animations while running.
    --abi <ABI>: Launch the instrumented process with the selected ABI.
        This assumes that the process supports the selected ABI.

am profile: start and stop profiler on a process.  The given <PROCESS> argument
  may be either a process name or pid.  Options are:
    --user <USER_ID> | current: When supplying a process name,
        specify user of process to profile; uses current user if not specified.

am dumpheap: dump the heap of a process.  The given <PROCESS> argument may
  be either a process name or pid.  Options are:
    -n: dump native heap instead of managed heap
    --user <USER_ID> | current: When supplying a process name,
        specify user of process to dump; uses current user if not specified.

am set-debug-app: set application <PACKAGE> to debug.  Options are:
    -w: wait for debugger when application starts
    --persistent: retain this value

am clear-debug-app: clear the previously set-debug-app.

am bug-report: request bug report generation; will launch UI
    when done to select where it should be delivered.

am monitor: start monitoring for crashes or ANRs.
    --gdb: start gdbserv on the given port at crash/ANR

am hang: hang the system.
    --allow-restart: allow watchdog to perform normal system restart

am restart: restart the user-space system.

am idle-maintenance: perform idle maintenance now.

am screen-compat: control screen compatibility mode of <PACKAGE>.

am to-uri: print the given Intent specification as a URI.

am to-intent-uri: print the given Intent specification as an intent: URI.

am to-app-uri: print the given Intent specification as an android-app: URI.

am switch-user: switch to put USER_ID in the foreground, starting
  execution of that user if it is currently stopped.

am start-user: start USER_ID in background if it is currently stopped,
  use switch-user if you want to start the user in foreground.

am stop-user: stop execution of USER_ID, not allowing it to run any
  code until a later explicit start or switch to it.

am stack start: start a new activity on <DISPLAY_ID> using <INTENT>.

am stack movetask: move <TASK_ID> from its current stack to the top (true) or   bottom (false) of <STACK_ID>.

am stack resize: change <STACK_ID> size and position to <LEFT,TOP,RIGHT,BOTTOM>.

am stack list: list all of the activity stacks and their sizes.

am stack info: display the information about activity stack <STACK_ID>.

am lock-task: bring <TASK_ID> to the front and don't allow other tasks to run

am get-config: retrieve the configuration and any recent configurations
  of the device

<INTENT> specifications include these flags and arguments:
    [-a <ACTION>] [-d <DATA_URI>] [-t <MIME_TYPE>]
    [-c <CATEGORY> [-c <CATEGORY>] ...]
    [-e|--es <EXTRA_KEY> <EXTRA_STRING_VALUE> ...]
    [--esn <EXTRA_KEY> ...]
    [--ez <EXTRA_KEY> <EXTRA_BOOLEAN_VALUE> ...]
    [--ei <EXTRA_KEY> <EXTRA_INT_VALUE> ...]
    [--el <EXTRA_KEY> <EXTRA_LONG_VALUE> ...]
    [--ef <EXTRA_KEY> <EXTRA_FLOAT_VALUE> ...]
    [--eu <EXTRA_KEY> <EXTRA_URI_VALUE> ...]
    [--ecn <EXTRA_KEY> <EXTRA_COMPONENT_NAME_VALUE>]
    [--eia <EXTRA_KEY> <EXTRA_INT_VALUE>[,<EXTRA_INT_VALUE...]]
    [--ela <EXTRA_KEY> <EXTRA_LONG_VALUE>[,<EXTRA_LONG_VALUE...]]
    [--efa <EXTRA_KEY> <EXTRA_FLOAT_VALUE>[,<EXTRA_FLOAT_VALUE...]]
    [--esa <EXTRA_KEY> <EXTRA_STRING_VALUE>[,<EXTRA_STRING_VALUE...]]
        (to embed a comma into a string escape it using "\,")
    [-n <COMPONENT>] [-p <PACKAGE>] [-f <FLAGS>]
    [--grant-read-uri-permission] [--grant-write-uri-permission]
    [--grant-persistable-uri-permission] [--grant-prefix-uri-permission]
    [--debug-log-resolution] [--exclude-stopped-packages]
    [--include-stopped-packages]
    [--activity-brought-to-front] [--activity-clear-top]
    [--activity-clear-when-task-reset] [--activity-exclude-from-recents]
    [--activity-launched-from-history] [--activity-multiple-task]
    [--activity-no-animation] [--activity-no-history]
    [--activity-no-user-action] [--activity-previous-is-top]
    [--activity-reorder-to-front] [--activity-reset-task-if-needed]
    [--activity-single-top] [--activity-clear-task]
    [--activity-task-on-home]
    [--receiver-registered-only] [--receiver-replace-pending]
    [--selector]
    [<URI> | <PACKAGE> | <COMPONENT>]



Use the following coommand to try if any activity could resolve the intent

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


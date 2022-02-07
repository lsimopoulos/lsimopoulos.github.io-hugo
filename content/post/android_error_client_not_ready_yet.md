+++
date = "2017-07-20T22:13:55+02:00"
archives = ["2017/07"]
categories = ["Android"]
tags = ["Android","Client not ready yet error", "Android Studio"]
title = "Android: Client not ready yet"
image = "banners/android.jpg"
+++

I started developing an android app on my surface but then I decided  to move the code to my stationary pc. I copied the whole source on a USB stick and pasted it on the other pc. 
I started the Android Studio and got an error dialog that it was warning me that the android sdk root path(that it was declared on the project) is not valid and I was propmpted to verify so the Android Studio points to the actual and correct path.
After that, I built the project successfully and then I ran the app in the emulator. 

I noticed first on the emulator that the app crashed on the deployment

![emulator crash error](/images/emulator_crash.jpg)

and I saw on the run tab on the Android Studio :

![Android studio](/images/error.JPG)

The message "Client not ready yet.." is not the most indicative. 

#What I tried and it did not work

1. Restarted the pc.

2. Deleted the app from emulator.

3. I did not add ``android:exported="true"`` on the MainActivity due to the fact that it had nested intent and it's exported by default. 

4. I Cleaned the project and rebuilt it. 

5. Went through AndroidManifest.xml but I did not find any error or "strange" setting that could explain this erroneous behaviour.

**Solution**

1. I presssed Ctrl + Alt + S to open the settings of the Android Studio.I navigated to  Build,Execution,Deployment>Instant Run I disabled the instant run.

![Android Studio Settings](/images/AndroidStudioSettings.JPG)

2. I ran the app and it was deployed successfully on the emulator and was running wihhout any problem.

3. I enabled the Instant Run  but i got again the same error.

4. Removed some comments from AndroidManifest.xml so I can trigger a full build.  [Instant Deploy](https://medium.com/google-developers/instant-run-how-does-it-work-294a1633367f) builds and deploy only the incremental changes.
It doesn’t reinstall the app, neither restart the app nor restart the Activity.

5. I clicked on the "Clean Project" and then on "Run app". It was working now even with the Instant Run enabled.

**Notes**

*I had the same error when I tried to deploy the app on my Samsung S8. 

*Android Studio Version : 2.3.3

## References
 This [link](https://medium.com/google-developers/instant-run-how-does-it-work-294a1633367f) is really useful. I learned a lot about Instant Run.
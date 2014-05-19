TPM 5/18/14

First off, I grabbed all these from GitHub and put the originals repos here, but I make a copy in my
workspace directory and did all the tweaks outlined below there.


Resources for Chromecast sample projects

http://googledevelopers.blogspot.com/2014/02/ready-to-cast-chromecast-now-open-to.html
https://developers.google.com/cast/
http://android-developers.blogspot.com/2014/02/google-play-services-42.html
https://github.com/googlecast/


For each github sample project I:

Forked
Cloned
Set upstream
Fetched upstream
Merged to upstream

Now, I'm not sure how I'm supposed to compile these samples...


These looked promising:

https://github.com/stigsfoot/cast-android-sample/blob/master/README_ECLIPSE.txt
https://github.com/stigsfoot/cast-android-sample/blob/master/INSTALL_CAST_ECLIPSE.txt (<-- best of all)
http://developer.android.com/tools/support-library/setup.html#libs-with-res


Started by copying and including the google-play-services_lib as a library in the workspace
Also added v7-appcompat and v7-mediarouter
Added all to the classpath
Added a dependency from mediarouter to appcompat


Had to manually change my project.properties for MediaRouter to:

# Project target.
target=android-18
android.library.reference.1=../../../../Dev/adt/sdk/extras/android/support/v7/appcompat
android.library.reference.2=../../../../Dev/adt/sdk/extras/android/support/v7/mediarouter
android.library.reference.3=../../google-play-services_lib
#android.library.reference.1=../../android-sdk-macosx/extras/android/support/v7/appcompat
#android.library.reference.2=../../android-sdk-macosx/extras/android/support/v7/mediarouter
#android.library.reference.3=../../android-sdk-macosx/extras/google/google_play_services/libproject/google-play-services_lib

Then right click project.properties and refresh in Eclipse

That resolved a lot of my issues.  I learned this from here:

	http://stackoverflow.com/questions/11550704/unknown-exception-in-parsesdkcontent

Then I noticed a circular reference with mediarouter pointing to appcompat pointing back to mediarouter, so
I deleted the line in the appcompat project.properties (and refreshed):

#android.library.reference.1=../mediarouter

This may have been causing my null pointer exception

Then I right clicked on all libraries and projects and under Android, for the Project Build Target selected
Google APIs 4.4.2 (API 19) for all, and that seemed to resolve most of my remaining issues.  Refreshes all
around, and a reload of the workspace left me with one error:

Then I had to remove bin/classes/.gitignore, then exit and reload the workspace.  This seemed to resolve all issues...

I have a few warnings now, but it looks like all is well.


Then I configured a AVD for 4_4_2_Google_Play_Cast and set it and ran it.

It seemed to run and deploy to the emulator!  Finally my first success with a sample app...


Now when running it, it seems some resources are missing and exceptions thrown...


I did skip some app registration steps....

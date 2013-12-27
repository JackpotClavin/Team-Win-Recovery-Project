**Team Win Recovery Project (TWRP)**

The goal of this branch is to rebase TWRP onto AOSP while maintaining as much of the original AOSP code as possible. This goal should allow us to apply updates to the AOSP code going forward with little to no extra work.  With this goal in mind, we will carefully consider any changes needed to the AOSP code before allowing them.  In most cases, instead of changing the AOSP code, we'll create our own functions instead.  The only changes that should be made to AOSP code should be those affecting startup of the recovery and some of the make files.

If there are changes that need to be merged from AOSP, we will pull the change directly from AOSP instead of creating a new patch in order to prevent merge conflicts with AOSP.

This branch is under final testing and will be used shortly for public builds, but has not officially been released.

You can find a compiling guide [here](http://forum.xda-developers.com/showthread.php?t=1943625 "Guide").

[More information about the project.](http://www.teamw.in/project/twrp2 "More Information")

If you have code changes to submit those should be pushed to our gerrit instance.  A guide can be found [here](http://teamw.in/twrp2-gerrit "Gerrit Guide").

12/27/2013: The RTC-Time-Hack branch is meant to give off the illusion that the phone can read the correct time from the RTC. Some devices like my LG G2 are epoch'd when they are initially turned on and locked in that time frame, so managing backups is difficult when the dates aren't familiar ("Was my stock backup on February 3rd, 1970 or was it January 19th, 1970????"). This patch merely changes the dates that are visible to the user (The time in the top-left-hand corner, and the timestamp of the backup) and everything else is left epoch'd, to prevent any strange behavior from services that might still be looking for modification dates that are from the 1970s, dude.

To access the menu, go to Settings->Set Time, and enter the date in "hr:min mm/dd/yyyy" format, and press enter; (like 10:01 12/27/2013). What this does is it writes an offset to the /sdcard/.twrps file, which will be loaded when the device boots, so your device will always be a constant billion seconds or so in front of the date your RTC says, so each time TWRP requests a timestamp that the end-user will see with their eyes, we will add the billion or so seconds to it, which will give the correct time as an illusion, Michael.

FYI: This menu is only available for 1080x1920 devices because that's what I needed this hack for, so follow the model of the ui.xml file I edited for your respective device's screen size in the gui/devices/XxY/res/ui.xml the corresponds to your device's screen size that is listed in the BoardConfig.mk (or BoardConfigCommon.mk) in your device's tree.

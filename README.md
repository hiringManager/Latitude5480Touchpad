# How To Use The Legacy Dell Configuration Instead of The Broken Windows Store App

## This is the best solution. It is the Windows 7 Driver. If you want to save some time, use it.

https://www.dell.com/support/home/en-us/drivers/driversdetails?driverid=94HPR&oscode=W764&productcode=latitude-15-5580-laptop

## Previous solution

* This allows you to configure your trackpad, and the pointing stick with some extra features that are fantastic, and you already have it installed! It's the legacy app that you loved before they completely broke it. Imagine that. #Dell
* This may work with non-Admin accounts, but I'm not sure until I get some feedback
* This will 99% work on all Dell Models that require 'Dell Touchpad Settings' or 'Dell Touchpad Assistant', but I only have a Latitude 5480/5488. And your drivers need to come with that legacy .exe obviously.

# tl;dr scroll to the bottom

## Literal screenshot from the Windows Store. Also there are two separate ones with the same description.
### *I almost didn't install it because it looked like malware. Wtf even is this Dell, you should be ashamed.
![image](https://user-images.githubusercontent.com/64992493/123536203-7d703c00-d6ee-11eb-9e2c-1496e0fa2359.png)

##### Not a typo in sight ~

### Alright so this is a work in progress, but I found a nice hacky solution if you want to:
* Modify your settings and have them save
* Do not have access to the windows store because it's an enterprise laptop that wants you to access the particularly malevolent Windows Store
* Disable the touchpad and not have it reset itself at boot.

If you're reading this, I'm sure you're aware that the forced-windows-store application doesn't work. This is because it resets at random, or you may not be able to install it due to the Windows Store being disabled by your admin. I don't use a non-admin account on Windows, so your mileage may vary. But you should be good.

#### While looking through the processes since alps.exe was wrecking my cpu, I noticed that the legacy software that used to actually work was actually *still there, and still works*. 

![image](https://user-images.githubusercontent.com/64992493/123537107-74ce3480-d6f3-11eb-9d4e-8e9454ee4e53.png)


After messing with it a while I noticed a few things. 

The Install directory for the default touchpad application is:
  C:\Windows\System32\DellTPad
After the automatic windows touchpad driver installation you should have these:

![image](https://user-images.githubusercontent.com/64992493/123536634-320b5d00-d6f1-11eb-9065-3ef50a043204.png)

Working out how to get this actually working right now, but I've had success by renaming one of the executables (So Windows won't automatically reinstall, since some of the files still exist).

BUT, interestingly enough you can use the legacy application, and all of the functions still work except:

* Point Stick / Nipple tap to click doesn't work (sucks anyway imo - feels like imma break my keyboard by how much force it takes).
* Tray Icon needs to be symlinked to the window store app maybe? idk I'm not fixing that.

Also the additional function of:
  *make the pointing stick more responsive / change polling rate(?) with the 'touchtracker thingy*

Theory right now is that one of these can be blacklisted, or have service disabled for people who want to make 

This shows me that the ApntEx.exe sends the pointing stick messages to Apoint.exe, and can in-fact be configured with DellTPad.exe.


### To do
* Replicate this on a fresh install
* Screenshot Setting for touchpad response / pointstick response
*   Does the windows setting affect this?
*   How does HID Filter play into all of this?
*   Is there a non-admin solution to this? 
*   Maybe that's why the fucking windows store packages doesn't work. .pkg files don't have write access to certain sys directories, so that could be why it's so unreliable

### Status:

* Tray Icon doesn't work. 
*   You may be able to change the name and symlink it to %PROGRAMDATA%\DellWhatever\WhateverTheNameIs.exe
*   Those cheap bastards LITERALLY are using the legacy tray icon just to open the garbage store app lmao. That's probably some /Dell/Shit/ though, not ALPS.
*   *FIXED* After install 'Nov 26 2019 Driver, latency when going from touchpad to nipple / vice-versa. *Probably due to the polling thingy*

# How To Disable Touchpad 

* Uninstall the Windows Store App if you have it (either of them)
* Install Nov 26 2019 Driver from Dell website (5480, but this whole guide works for a ton of models)
* Change directory to C:\Windows\System32\DellTPad\
* Configure in DellTpad.exe as Admin*
*   Disable touchpad, nipple speed is determined by the touchpad speed, and the stick can be configured under 'touchpad settings'
*   (I believe they are hard-coded to be the same speed. Can't remember if the linux driver differs)
* run ApClose.exe
* run Apoint.exe
* Point stick may not be functioning properly (slow as molasses). just reboot.
* Settings should now be persistent with how you just configured them, and you won't have to mess with them again.

### If you run into issues ---
* I did two things that may or may not have allowed this to work. -- I'll check next time my drivers kill themselves.
* First allowed my user account to have r/w permissions for DellTPad.exe (see other files for screencaps)
* Second, I ran DellTPad as admin, but currently my changes don't require elevated-privlages. 
* This also fixed the issue with the middle-scroll button scrolling awfully. Like snapping around and being unmanagable. 
(Think this was due to 'TouchCheck being modified to 'maximum'. My theory is that this is actually 'polling rate' and why 'precision touchpads' are generally marketing bs. (Especially since this laptop /has/ precision zoom when booted into Chrome-OS, so that means the hardware is capable of it but as you know, the drivers just suck.)

# How to Use the Dell Configuration Utility That Works Perfectly, But They Removed For Some Reason.
* Follow same steps as "How to Disable Touchpad" but don't disable touchpad. 

### Precision Drivers Are a Myth 
By the way, since you don't have precision drivers but want that delicious precision zoom on Microsoft Edge Chromium / Chrome, check out the extension 'Mouse Pinch-To-Zoom' in the Chrome store. I generally don't trust chrome extenstions, but I went through the code and didn't see anything shady (think it's just a hook to the WindowsAction, and like 3 tiny .js.) It only has 500 users so use at your own risk unless you also want to audit it. So I installed it and disabled 'auto-updating' for the extension out of paranoia. Works for mouse too, so that's dope. #PrecisionTouchpadMyth #ButIHavePrecisionZoomInLinuxWtf

### Please Tell me if you run into any problems. I've attached my notes while trying to figure this out with screenshots and stuff, and your answer is probably there. If not, post an Issue.

##### If this helped you out, then I would really appreciate you subscribing to 'PewDiePie' on Youtube.

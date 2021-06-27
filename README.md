# How to bypass the horrible jank that is Alps Pointing Drivers

## Literal screenshot from the Windows Store. Also there are two separate ones with the same description.
## *I almost didn't install it because it looked like malware.*
![image](https://user-images.githubusercontent.com/64992493/123536203-7d703c00-d6ee-11eb-9e2c-1496e0fa2359.png)

### Alright so this is a work in progress, but I found a nice hacky solution if you want to:
* Modify your settings and have them save
* Do not have access to the windows store because it's an enterprise laptop that wants you to access the particularly malevolent Windows Store
* Disable the touchpad and not have it reset itself at boot.

If you're reading this, I'm sure you're aware that the forced-windows-store application doesn't work. This is because it resets at random, or you may not be able to install it due to the Windows Store being disabled by your admin. I don't use a non-admin account on Windows, so your mileage may vary. At the very least you should be able to have your admin kill the service or rename / move the exe that is annoying.

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
* Settings saving currently
* Tray Icon surviving reboot?

Also the additional function of:
  *make the pointing stick more responsive / change polling rate(?) with the 'touchtracker thingy*

Theory right now is that one of these can be blacklisted, or have service disabled for people who want to make s

This shows me that the ApntEx.exe sends the pointing stick messages to Apoint.exe, and can in-fact be configured with DellTPad.exe.


## To do
* Replicate this on a fresh install
* Screenshot Setting for touchpad response / pointstick response
*   Does the windows setting affect this?
*   How does HID Filter play into all of this?
*   Is there a non-admin solution to this? (Required to blacklist whatever EXE is the bastard)
*   Maybe that's why the fucking windows store packages doesn't work. .pkg files don't have write access to certain sys directories, so that could be why it's so unreliable

## Status:

* Tray Icon doesn't work. 
*   You may be able to change the name and symlink it to %PROGRAMDATA%\DellWhatever\WhateverTheNameIs.exe
*   Those cheap bastards LITERALLY are using the legacy tray icon just to open the garbage store app lmao. That's probably some /Dell/Shit/ though, not ALPS.
*   After install 'Nov 26 2019 Driver, latency when going from touchpad to nipple / vice-versa. *Probably due to the clicklock thingy*

## How To:
      Install Nov 26 2019 Driver from 

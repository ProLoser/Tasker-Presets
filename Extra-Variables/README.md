# Extra Variables
The profiles included here maintain a set of variables that might otherwise exist as system variables or States in Tasker. These variables can be used to conditionally execute individual actions within a task, in IF actions to conditionally execute a group of actions, or in Variable Value contexts to simulate States not built in to Tasker.

### Source
http://tasker.wikidot.com/extendedvariables?branch_used=true

### Variables
* `%myDISPLAY` - the current state of the didplay: on, off or unlocked
* `%myPHONE` - the current state of the phone: idle, ringing or offhook
* `%myPOWER` - the current state of power: ac, usb, wireless or none
* `%myTRUSTEDWIFI` - whether the devices is connected to a trusted Wifi network: true or false
* `%myUIMODE` - the current UI mode: car, desk or normal
* `%myUSER` - the current state of the user: present or absent

### More Information
Some of these variables duplicate (or appear to) built in variables in Tasker. So why are they here? Let's take a look:

`%myDISPLAY` is similar to the %SCREEN variable in Tasker, but it adds unlocked as a possible value, allowing us to differentiate between on and unlocked. These values are set based on the corresponding Tasker Events, and can be used as a Context (using Variable Value), or for flow control within Tasks.

`%myPHONE` reflects the current state of the phone based on the corresponding Tasker Events. This allows the current state of the phone to be used as a Context (using Variable Value), or for flow control within Tasks.

`%myPOWER` reflects the current state of power, corresponding to the corresponding Tasker States, and can be used for flow control within Tasks.

`%myTRUSTEDWIFI` has possible values of true and false. If you're connected to a trusted Wifi network, your device is assumed to be in a safe environment, and if found, will be returned to you without any unauthorized use. I use this in conjunction with the %myDISPLAY=unlocked state to disable my pin lock. If I'm connected to one of these networks and my device is unlocked, I don't want to have to unlock it each time I want to use it. Once disconnected from these networks for more than one minute, the pin lock is re-enabled.

`%myUIMODE` is a more flexible version of Tasker's built-in %UIMODE variable, which depends on OEM hardware dock detection. If you're using an OEM dock, you have no need for %myUIMODE, however, %myUIMODE will maintain the same value as %UIMODE in this case. If you're not using an OEM dock, or your dock is not detectable for some reason, %myUIMODE will give you a pseudo dock mode. %myUIMODE is set to car if the device is powered and held in a portrait orientation momentarily. %myUIMODE is set to desk if the device is powered and held on it's left side momentarily. %myUIMODE will be set to normal once power is removed from the device. This means that once the device is in either car or desk mode, it will remain that way until power is removed, regardless of any changes to the orientation of the device. Once in desk mode, you can lay the device on a table face up and it will remain in desk mode. Once in car mode, it will remain in car mode regardless of how any bumps in the road might confuse the orientation sensor; you can even rotate the device to a landscape orientation and it will stay in car mode. If you don't have an OEM dock, you can disable the myUIMODE=UIMODE profile with no side effects.

`%myUSER` is an attempt to identify whether the user is actively using the device. There is nothing like this built into Tasker. I use it primarily to conditionally execute Vibrate and Play Ringtone actions in Tasker, based on whether the user is actually interacting with the device at the time.

### Initializing things
This project includes an initialization profile that runs only once after you import the project. It sets up initial values for all variables that might not otherwise be set immediately by virtue of the contexts used in the profiles.

### Things you'll want to check/change
The profiles included in this project are used on my phone, and consequently some of the details are particular to me or my environment. As such, you'll want to look at the following profiles to change the details to suite your needs:

`%myTRUSTEDWIFI` - check/change the SSIDs listed in the Wifi Connected context for this profile.

### Why post this project?
I posted this project as a first step in posting my revamped Notification Reminder project, which makes use of several of the variables maintained by this project. Plus, I am hoping to help others who need similar states in Tasker.

### Revisions:
* `06 Apr 2013` - Corrected issue where quickly turning on the display and unlocking sometimes resulted in %myDISPLAY being set to on instead of unlocked (two tasks queued with equal priority and sometimes executed in the unintended order)

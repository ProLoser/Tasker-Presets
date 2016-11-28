# Extra Variables
The profiles included here maintain a set of variables that might otherwise exist as system variables or States in Tasker. These variables can be used to conditionally execute individual actions within a task, in IF actions to conditionally execute a group of actions, or in Variable Value contexts to simulate States not built in to Tasker.

### Source
http://tasker.wikidot.com/extendedvariables?branch_used=true

### Variables
* `%EX_PHONE` - the current state of the phone: idle, ringing or offhook
* `%EX_POWER` - the current state of power: ac, usb, wireless or none
* `%EX_UIMODE` - the current UI mode: car, desk or normal
* `%EX_USER` - the current state of the user: present or absent

### More Information
Some of these variables duplicate (or appear to) built in variables in Tasker. So why are they here? Let's take a look:

`%EX_PHONE` reflects the current state of the phone based on the corresponding Tasker Events. This allows the current state of the phone to be used as a Context (using Variable Value), or for flow control within Tasks.

`%EX_POWER` reflects the current state of power, corresponding to the corresponding Tasker States, and can be used for flow control within Tasks.

`%EX_UIMODE` is a more flexible version of Tasker's built-in `%UIMODE` variable, which depends on OEM hardware dock detection. If you're using an OEM dock, you have no need for %EX_UIMODE, however, `%EX_UIMODE` will maintain the same value as `%UIMODE` in this case. If you're not using an OEM dock, or your dock is not detectable for some reason, `%EX_UIMODE` will give you a pseudo dock mode. `%EX_UIMODE` is set to car if the device is powered and held in a portrait orientation momentarily. `%EX_UIMODE` is set to desk if the device is powered and held on it's left side momentarily. `%EX_UIMODE` will be set to normal once power is removed from the device. This means that once the device is in either car or desk mode, it will remain that way until power is removed, regardless of any changes to the orientation of the device. Once in desk mode, you can lay the device on a table face up and it will remain in desk mode. Once in car mode, it will remain in car mode regardless of how any bumps in the road might confuse the orientation sensor; you can even rotate the device to a landscape orientation and it will stay in car mode. If you don't have an OEM dock, you can disable the `%EX_UIMODE=UIMODE` profile with no side effects.

`%EX_USER` is an attempt to identify whether the user is actively using the device. There is nothing like this built into Tasker. I use it primarily to conditionally execute Vibrate and Play Ringtone actions in Tasker, based on whether the user is actually interacting with the device at the time.

### Initializing things
This project includes an initialization profile that runs only once after you import the project. It sets up initial values for all variables that might not otherwise be set immediately by virtue of the contexts used in the profiles.

### Why post this project?
I posted this project as a first step in posting my revamped Notification Reminder project, which makes use of several of the variables maintained by this project. Plus, I am hoping to help others who need similar states in Tasker.

### Revisions:
* `27 Nov 2016` - Removed EX_DISPLAY and EX_TRUSTEDWIFI since they were unreliable and added a task `Is Device Locked?`.
* `06 Apr 2013` - Corrected issue where quickly turning on the display and unlocking sometimes resulted in `%EX_DISPLAY` being set to on instead of unlocked (two tasks queued with equal priority and sometimes executed in the unintended order)

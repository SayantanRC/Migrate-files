# Troubleshooting
## Telegram group for reporting issues:
You can provide feedback and report issues in our Telegram group: https://t.me/migrateApp

## Migrate Helper apk
In some cases, you might not get the prompt to continue restore. Please download the apk, install it manually and open it to continue restoring.  
[Helper apk](https://github.com/SayantanRC/Migrate-files/blob/master/helper.apk?raw=true)

## [TWRP error] Can't install helper. Flashing zip fails.
Helper usually fails to install from TWRP when the system directory is full. You may want to use a different ROM or use a smaller GApps package. This will be avoided from Migrate v3.0 and above.  

If nothing helps, try this:  
Inside each of your backup.zip file, there will be a file named as `verify.sh`. Replace that with this file. You may use:  
1. Any zip explorer and directly replace the file.  
OR  
2. Extract the zip file, replace the verify.sh script, zip it again.  

You should be able to flash the file now without any problem.  
YOU WILL NEED TO INSTALL THE HELPER APK SEPARATELY i.e manually. You can get the apk either from [the section "Migrate Helper apk"](https://github.com/SayantanRC/Migrate-files/blob/master/troubleshooting.md#migrate-helper-apk) or under the "system" directory inside the backup.zip file which you flashed from TWRP.  

## [TWRP error] Error 7 or any other
This currently prevalent in system-as-root devices like `violet` (Redmi Note 7 pro), `lavender` (Redmi Note 7). Currently system-as-root device users are advised to not use this app. A suitable solution will be made available soon.  

For any other cases, you can send a log file to the [Telegram group](https://t.me/migrateApp).  
To resolve this please see the section ____________________

To send the log file of TWRP, boot into TWRP -> Flash Migrate zip -> (You will get an error) <b>DO NOT REBOOT</b> -> Go to TWRP main menu -> Advanced -> File manager.
Navigate to `/tmp`. Copy the `recovery.log` file to under `/sdcard`.

Alternatively from adb (in TWRP itself, <b>DO NOT REBOOT</b>), enter this command without the `<space>` words:
```
cp <space> /tmp/recovery.log <space> /sdcard/
```
Now, reboot to system and upload the `recovery.log` file, from Internal storage, in our [Telegram group](https://t.me/migrateApp).

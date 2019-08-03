# Troubleshooting
## Telegram group for reporting issues:
You can provide feedback and report issues in our Telegram group: https://t.me/migrateApp

## Restore after setting up ROM
In some cases, you might observe some problems if you flash migrate backup zips before setting up your ROM, Google account in Gapps etc. Although the process of flashing ROM <b>AND</b> flashing all migrate zips in one go in TWRP, without rebooting may seem convenient and in most cases have no problems, sometimes, dependent on ROM and device, you might face some problems while restoring.  

In such cases, try this:  
1. Clean flash ROM  
2. Don't flash any migrate zip  
3. Boot up and complete ROM, Gapps etc setup  
4. Boot back to TWRP recovery  
5. Flash migrate zips  
6. Try to restore  

## Migrate Helper apk
In some cases, you might not get the prompt to continue restore. Please download the apk, install it manually and open it to continue restoring.  
[Helper apk](https://github.com/SayantanRC/Migrate-files/blob/master/helper.apk?raw=true)

## [TWRP error] Can't install helper. Flashing zip fails.
Helper usually fails to install from TWRP when the system directory is full. You may want to use a different ROM or use a smaller GApps package. This will be avoided from Migrate v3.0 and above.  

If nothing helps, try this:  
Inside each of your backup.zip file, there will be a file named as `verify.sh`. Replace that with this file:
[Right click on this link -> Save link as](https://raw.githubusercontent.com/SayantanRC/Migrate-files/master/verify.sh)  

You may use:  
1. Any zip explorer and directly replace the file.  
OR  
2. Extract the zip file, replace the `verify.sh` script, zip it again.  

You should be able to flash the file now without any problem.  
YOU WILL NEED TO INSTALL THE HELPER APK SEPARATELY i.e manually. You can get the apk either from [the section "Migrate Helper apk"](https://github.com/SayantanRC/Migrate-files/blob/master/troubleshooting.md#migrate-helper-apk) or under the "system" directory inside the backup.zip file which you flashed from TWRP.  

## [TWRP error] Error 7 or any other
This currently prevalent in system-as-root devices like `violet` (Redmi Note 7 pro), `lavender` (Redmi Note 7). Currently system-as-root device users are advised to not use this app. A suitable solution will be made available soon.  

For any other cases, you can send a log file to the [Telegram group](https://t.me/migrateApp).  
To resolve this please see [the section "TWRP alternate flasher (failsafe method)"](https://github.com/SayantanRC/Migrate-files/blob/master/troubleshooting.md#twrp-alternate-flasher-failsafe-method) below.

To send the log file of TWRP, boot into TWRP -> Flash Migrate zip -> (You will get an error) <b>DO NOT REBOOT</b> -> Go to TWRP main menu -> Advanced -> File manager.
Navigate to `/tmp`. Copy the `recovery.log` file to under `/sdcard`.

Alternatively from adb (in TWRP itself, <b>DO NOT REBOOT to system</b>), enter this command without the `<space>` words:
```
cp <space> /tmp/recovery.log <space> /sdcard/
```
Now, reboot to system and upload the `recovery.log` file, from Internal storage, in our [Telegram group](https://t.me/migrateApp).

## TWRP alternate flasher (failsafe method)
This is a failsafe method, in case you are having any problem flashing a migrate zip in TWRP <b>(Redmi Note 7 series and other system as root devices are not yet supported)</b>. Please note that you cannot use this on multiple migrate backup zips on the same time. You would need to repeat the process for each zip file. Please follow the instructions <b>EXACTLY</b> as provided below.  

1. Make a folder just inside internal storage named "backup". The folder must be completely empty.  
2. Extract a single migrate backup zip file inside the created "backup" folder. The contents of the zip must directly be inside the "backup" folder.  
> Say the zip file has a name "BackupXYZ.zip", your extracted contents must <b>NOT</b> look like: <i>Internal storage -> backup -> BackupXYZ -> {zip file contents}</i>  
> It should look like: <i>Internal storage -> backup -> {zip file contents}</i>  
3. Download this file: [twrp_extract.zip](https://github.com/SayantanRC/Migrate-files/blob/master/twrp_extract.zip?raw=true). Put this file preferably under `Download` folder in the internal storage of your Android device.  
4. Open TWRP, click "Install" button, navigate to the above downloaded file (Internal storage -> Download -> twrp_extract.zip) and flash it.  
4. Reboot. You should now get a prompt to continue restore via the helper app. If not, check [the section "Migrate Helper apk"](https://github.com/SayantanRC/Migrate-files/blob/master/troubleshooting.md#migrate-helper-apk)  

If you want to flash another migrate zip file, clean the "backup" folder created in step 1. Extract another zip file as in step 2, go to TWRP and flash the already downloaded "twrp_extract.zip" file again.

## Segmentation fault
The error "Segmentation fault" is related to kernel. This is mostly observed in KangarooX kernel for `whyred` (Redmi Note 5). People encountering this are requested to change the kernel and retry backup.

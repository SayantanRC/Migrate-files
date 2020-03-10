# Troubleshooting

Most of the TWRP related issues should be resolved by going to [the section "TWRP alternate flasher (failsafe method)"](https://github.com/SayantanRC/Migrate-files/blob/master/troubleshooting.md#twrp-alternate-flasher-failsafe-method) below. 

However, you should also check the other sections before trying that. Also look into [the section "Important points when making the migrate backup"](https://github.com/SayantanRC/Migrate-files/blob/master/troubleshooting.md#important-points-when-making-the-migrate-backup) at the bottom.

## Telegram group for reporting issues:
You can provide feedback and report issues in our Telegram group: https://t.me/migrateApp

## Segmentation fault
The error "Segmentation fault" is related to kernel. This is mostly observed in KangarooX kernel for `whyred` (Redmi Note 5). People encountering this are requested to change the kernel and retry backup.

## Zero app backup
In some cases, the app is not backing up any apk or data. In that case, please click hamburger menu (green circle in top left corner in the first screen of the app) -> Preferences -> Uncheck `Use new method to calculate size` option.  
The issue will probably be fixed in v3.0.

## Restore after setting up ROM

1)) A detailed description of how to restore can be found on the migrate application.
Run the application
You will see a "how to restore" button. click on it

This is the recommended method of restoring. Try it first.

2)) In some cases, you might observe some problems if you flash migrate backup zips before setting up your ROM, Google account in Gapps etc. Although the process of flashing ROM <b>AND</b> flashing all migrate zips in one go in TWRP, without rebooting may seem convenient and in most cases have no problems, sometimes, dependent on ROM and device, you might face some problems while restoring.  

In such cases try the following:

A))
1. Clean flash ROM 
(wipe cache , dalvik cache , data and the flash the ROM)
2. *** DON'T FLASH ANY MIGRATE ZIP FILES YET***
3. Flash OpenGapps 
(optional - no need to if your ROM already has Gapps, or if you don't want them)
4. Flash magisk 
5. Boot into the ROM and complete setup.
6. Reboot into twrp
7. FLASH THE MIGRATE ZIP FILES
8. Boot into the ROM and restore

If this doesn't work then try

B))
1. Clean flash ROM 
(wipe cache , dalvik cache , data and the flash the ROM)
2. *** DON'T FLASH *MAGISK* OR ANY MIGRATE ZIP FILES YET***
3. Flash OpenGapps 
(optional - no need to if your ROM already has Gapps, or if you don't want them)
4. Boot into the ROM and complete setup.
5. Reboot into twrp
6. FLASH MAGISK
7. FLASH THE MIGRATE ZIP FILES
8. Boot into the ROM and restore

## Migrate Helper apk
In some cases, you might not get the prompt to continue restore , in which case you have to run the migratehelper application manually.

The helper application is found on your internal storage in:
/sdcard/Android/data/balti.migratehelper/helper/MigrateHelper.apk

Or you download the apk, install it manually and open it to continue restoring.

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

## [TWRP error] Error 7 or any other error
There a number of things you can try when you get error 7

1. Change your recovery from TWRP to Orangefox and try again. 
Orangefox recovery has been shawn to handle error 7 better than TWRP.

2. Make sure you delete cache before you make the backup. 
It has been shown that the chances of getting any error are reduced tremendously if you clean cache before you backup.
Refer to [the section "Important points when making the migrate backup"](https://github.com/SayantanRC/Migrate-files/blob/master/troubleshooting.md#important-points-when-making-the-migrate-backup)

3. If the above two methods fail then you have to consider the following:

Error 7 is currently prevalent in system-as-root devices like `violet` (Redmi Note 7 pro), `lavender` (Redmi Note 7). Currently system-as-root device users are advised to not use this app. A suitable solution will be made available soon.  

4. For any other cases, you can send a log file to the [Telegram group](https://t.me/migrateApp).  
To resolve this please see [the section "TWRP alternate flasher (failsafe method)"](https://github.com/SayantanRC/Migrate-files/blob/master/troubleshooting.md#twrp-alternate-flasher-failsafe-method) below.

To send the log file of TWRP, boot into TWRP -> Flash Migrate zip -> (You will get an error) <b>DO NOT REBOOT</b> -> Go to TWRP main menu -> Advanced -> File manager.
Navigate to `/tmp`. Copy the `recovery.log` file to under `/sdcard`.

Alternatively from adb (in TWRP itself, <b>DO NOT REBOOT to system</b>), enter this command without the `<space>` words:
```
cp <space> /tmp/recovery.log <space> /sdcard/
```
Now, reboot to system and upload the `recovery.log` file, from Internal storage, in our [Telegram group](https://t.me/migrateApp).

## If the method above doesn't work for error 7, try this [worked for me]
Extract all the files from zip file, find prep.sh file, open it and edit a few codes :
remove ">> /proc/self/fd/${OUTFD}"
replace "awk" with "/tmp/busybox awk" [make sure to replace all 4 "awk" instances]
now repack the files into a zip and flash it.

If you have multiple zips, follow the procedure for each zip one by one [but you can flash them all together]

## TWRP alternate flasher (failsafe method)
<b>IMPORTANT: System apps are not restored by this process.</b>  

This is a failsafe method, in case you are having any problem flashing a migrate zip in TWRP <b>(Redmi Note 7 series and other system as root devices are not yet supported)</b>. Please note that you cannot use this on multiple migrate backup zips on the same time. You would need to repeat the process for each zip file. Please follow the instructions <b>EXACTLY</b> as provided below.  

1. Make a folder just inside internal storage named "backup". /sdcard/backup. The folder must be completely empty.  
2. Extract a single migrate backup zip file inside the created "backup" folder. The contents of the zip must directly be inside the "backup" folder.  
> For those technically minded this is what is happening:
> Say the zip file has a name "BackupXYZ.zip", your extracted contents must <b>NOT</b> look like: <i>Internal storage -> backup -> BackupXYZ -> {zip file contents}</i>  
> It should look like: <i>Internal storage -> backup -> {zip file contents}</i>  
3. Download this file: [twrp_extract.zip](https://github.com/SayantanRC/Migrate-files/blob/master/twrp_extract.zip?raw=true). For nearly all phones the default download folder/directory is the `Download` folder in the internal storage of your Android device. /sdcard/Download .
You can you leave it and use it from here (recommend). It does not matter where you put the file as long as you remember where it is.
4. Boot into TWRP recovery (Or Orangefox recovery if that is what you have installed), click "Install" button, navigate to the above downloaded file (Internal storage -> Download -> twrp_extract.zip) and flash it.  
4. Reboot into the system (phone). You should now get a prompt to continue restore via the helper app. If not, check [the section "Migrate Helper apk"](https://github.com/SayantanRC/Migrate-files/blob/master/troubleshooting.md#migrate-helper-apk)  

If you want to flash another migrate zip file, clean the "backup" folder created in step 1 of all it's contents. Extract the other/new zip file into this folder as in step 2, boot into TWRP and flash the already downloaded "twrp_extract.zip" file again.

## Important points when making the migrate backup
1. Users may want to delete cache. This reduces errors in making the zip.
You can use an application that deletes cache...
and you can individually delete cache in the applications that keep a lot of cache (e.g Facebook , chrome)

2. check to see if you can open your zip files immediately after you make them.
This will avoid corrupted zip files

3. Generally migrate zip files above 4GB can cause restore problems 

A full system backup will make multiple zip files less than 4 GB each

Partial system breakups can make a single zip file which is more than 4GB in size.

So it is generally better to make a full system backup ,and during restore you can make partial restores.

4. If you are experiencing crashes after restore... then don't restore data + permissions for those applications that are crashing


# Troubleshooting
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
YOU WILL NEED TO INSTALL THE HELPER APK SEPARATELY i.e manually. You can get the apk either from [here](https://github.com/SayantanRC/Migrate-files/blob/master/helper.apk?raw=true) or under the "system" directory inside the backup.zip file which you flashed from TWRP.  

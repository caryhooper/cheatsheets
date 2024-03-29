# Android Hacking
======
#### Unpack APK (unzip)
unzip app.apk -d /path/to/directory
#### External Storage
Files created on external storage such as SD cards are globally readable and writable.  Don't store sensitive information here!  In addition, you should not store executable or class files because it should be treated as untrusted.

## Apktool
------
#### Unpack APK (apktool)
apktool d app.apk
#### Get package name (reference) from APK
grep "package" ./application/AndroidManifest.xml
#### Convert smali to dex
fullpath=$(pwd); for file in $(find . -name "*.smali"); do smali a $fullpath/$file;  done

## ADB
------
#### List Devices
adb devices
#### Install App
adb install /path/to/apk
#### Upload File
adb push /from /to
#### Download File
adb pull /from /to
#### Uninstall Package (while specifying session)
adb -s 192.168.0.1:5555 uninstall com.app.local
#### List Packages
adb shell 'pm list package'
#### List Running Processes
adb shell 'ps | grep com'
#### Add a Device
adb connect 192.168.0.28:5555
#### Drop Shell on System
adb shell
#### Drop Shell on an emulated system
adb -s 192.168.0.165:5555 shell
#### View Android Logs
adb logcat
####




#### Install Burp Certificate in Browser

#### Trusted Cert Location
/system/etc/security/cacerts
#### Downloads Folder Location
/storage/emulated/0/Download
#### Temporary Folder Location
/data/local/tmp
#### Loot Directories (secrets may be stored here)
/assets, /res/raw
#### Push Burp Certificate to System Store
adb -s 192.168.0.165:5555 push .\9a5ba575.0 /system/etc/security/cacerts
#### Remount RO Disk
adb remount
#### Check for package update functionality
application/vnd.android.package-archive
#### GenyMotion
Downloaded 'for personal use'.  Created an account and chose existing VirtualBox installation.  Clicked the "plus" to add a new device and selected Samsung 10 (2048 MB of memory).  Booted up

## Tools
------
#### Jadx (Convert APK to Java)
jadx -d /path/to/output app.apk
#### Dex2Jar (Convert APK to Jar)
d2j-dex2jar.sh /path/to/app.apk
#### JD-GUI
Java Decompiler for .JAR files
#### Apktool (convert source to smali)
apktool d file.apk
#### MARA Framework (Static Analysis)
./mara.sh -s '/path/to/app.apk'
#### QARK (Static Vulnerability Analysis Tool)
Decompiles/Scans for security issues
#### MobSF (Mobil Security Framework)
Automated analysis of Android/iOS/Windows for static and dynamic analysis.

## Common API Calls
------
#### Execute Commands
Runtime.exec()
#### Execute Commands
ProcessBuilder()
#### Execute Commands
system()

## Reversing 
------
#### List Symbols from (shared) object files
nm -Ca foo.o
#### List functions dynamically (only meaningful for dynamic objects such as SO)
nm -D foo.so
#### List Information about Object
objdump -f foo.so
#### List (dis)assembly of executable sections
objdump -d foo.so
#### Generate Assembly
objdump --section=.text -s -d main.o
#### View GOT
objdump -d -j .got /path/to/bin
#### Uncrackable
adb -s 192.168.0.165:5555 reboot; adb -s 192.168.0.165:5555 install .\UnCrackable-Level1.apk

## Frida
------
#### Definition
Frida is a dynamic binary instrumentation tool.  
#### List processes
frida-ps -U -D 192.168.0.165:5555
#### Function tracing (traces read and recv functions within Twitter app)
frida-trace -i "recv*" -i "read*" *twitter*
#### Search for Root Detection Method
strings to search: /su,superuser.apk,supersu,busybox
#### Use Frida to attach to process/inject code
frida -D 192.168.0.165:5555 -l .\fridademo-pinBypass.txt infosecadventures.fridademo  
#### Change arguements of Java Function
(within JS) var ret_value = this.function(2,5); return ret_value;
#### frida-trace (trace calls to a library)
frida-trace -D <device> -p <pid> -i "libfoo.so!"
#### frida-trace (trace calls to a library)
frida-trace -D <device> -p <pid> -i "Java_*""
#### Attach to Frida process and enumerate exports
+ frida -r process.exe
+ Module.enumerateExports("foobar.dll")


## Objection
------
#### Repack APK with frida-gadget DLL
objection patchapk -s test_app.apk
#### Interact with gadget
frida -U gadget
#### Reference
https://11x256.github.io/Frida-hooking-android-part-1/
#### Search for secrets in memory (objection)
memory search secretPass --string

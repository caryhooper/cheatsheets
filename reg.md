# Windows Registry
======

## HKLM (HKEY_LOCAL_MACHINE)
------
#### Usage
Maintained in memory and used to map all other sub-keys.
#### HKLM\SAM
References Security Accounts Manager (SAM) database.  This contains built-in accounts for the local system.
#### HKLM\SYSTEM
Contains info about system setup, data for RNG, and list of mounted devices containing the filesystem.
#### HKLM\SYSTEM\Control Sets
contain alternative configurations (current + backup).
#### Each Control Set Contains:
+ all plug-and-play devices
+  services, installed system drivers, all programs running as services (including auto-start)
+  hardware drivers and programs running as services
+  Hardware profiles used to modify the default profile.

#### HKLM\SOFTWARE
software and windows settings.  Modified by applications and system installers.
#### HKLM\SOFTWARE\Wow6432Node
Used by 32-bit apps on 64-bit Windows.  Presented as HKLM\SOFTWARE to 32bit apps
#### HKLM\BCD
Boot Configuration Data is stored in a data file formatted to make the Windows Registry hive (eventually mounted as HKLM\BCD00000)
#### HKLM\COMPONENTS
used by Windows update services and linked to WINSYS folder.

## HKCC (HKEY_CURRENT_CONFIG)
------
#### Usage
Contains information gathered at runtime.  Information is regenerated at boot and not stored on the disk.  HKCC is a handle to HKLM\System\CurrentControlSet\Hardware Profiles\Current.

## HKCR (HKEY_CLASSES_ROOT)
------
#### Usage
Contains information about registered applications, file associations, and OLE Object Class IDs.  Compilation of HKCU\Software\Classes and HKLM\Software\Classes.

## HKU (HKEY_USERS)
------
#### Usage
Contains subkeys corresponding to the HKEY_CURRENT_USERS (HKCU) keys for each user profile actively loaded.  User hives typically only loaded for currently logged-on users.

## HKCU (HKEY_CURRENT_USERS)
------
#### Usage
Stores settings for each logged-in user.  Link to the sub-key of HKU for the logged-in user.  On Windows NT systems, user settings are stored in NTUSER.DAT and USRCLASS.DAT inside the user's subfolder.

## HKPD (HKEY_PERFORMANCE_DATA)
------
#### Usage
translates runtime info to performance data.  Info provided by NT kernel or device drivers.  Not stored in a hive and not visible in regedit, but is visible through registry functions in the Windows API.

## HKDD (HKEY_DYN_DATA)
------
#### Usage
Only on Windows 95/98/ME.  Contains information about hardware devices, PnP, and network performance statistics.  Not stored on HD.  Gathered/configured at startup and stored in memory.
#### Windows Auto-Login
reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"
#### AutoRuns
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run 
#### AutoRuns
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Runonce 
#### AutoRuns
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run 
#### AutoRuns
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Runonce 
#### Service startup order
reg query hklm\system\currentcontrolset\control\servicegrouporder 
#### Service Info
reg query HKLM\SYSTEM\CurrentControlSet\Services\hMailServer	
#### Dump Windows SAM file
reg save hklm\sam c:\sam 
#### Dump Windows SYSTEM file
reg save hklm\system c:\system
#### Persistence
reg add HKLM\SOFTWARE\Classes\exefile\shell\open /v command /t REG_SZ /d '%SystemRoot%\svchost.com "%1" %*'
#### Previously Connected WiFi access points
HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles 
#### Connected USB Devices
HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR
#### Typed URLs (from iexplore or Edge)
HKCU\SOFTWARE\Microsoft\Internet Explorer\TypedURLs
#### Recently-Opened Documents
HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
#### Shim Cache (recently executed .EXEs run in compatibility mode)
HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\AppCompatCache\AppCompatCache
#### Most Actively Used .EXE List
HKCU\Software\Microsoft\Windows \CurrentVersion\Explorer\UserAssist (Note: Bins are ROT13)
#### "Shell Bags" (Folders that have been opened up in explorer at least once)
HKCU\Software\Microsoft\Windows\Shell\BagMRU
#### Environment Variables
reg query "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager\Environment"
#### KnownDLLs (DLLs known to be included in the System)
HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\KnownDLLs
#### Safe DLL Search (searches current directory last)
HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\SafeDllSearchMode
#### CWDIllegalInDllSearch (??)
HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\CWDIllegalInDllSearch
#### Active Setup (Autoruns which run before Run/Runonce)
HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components\
#### Load custom DLL when LSA restarts
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa\ (Security Packages -- REG_MULTI_SZ -- mimilib)
#### Protocol Handlers
HKEY_LOCAL_MACHINE\SOFTWARE\Classes\PROTOCOLS\Handler\
#### COM Class Unique Identifiers/Information (CLSID)
-HKEY_LOCAL_MACHINE\SOFTWARE\Classes\CLSID\{CLSID}
#### Disable Windows Defender
reg add  "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\Real-Time Protection" /v DisableRealtimeMonitoring /t REG_DWORD /d 1
